# 【PHP 源码】PHP 函数调用


## 想法

我以前对于 C 语言的印象是有很强的确定性，而 PHP 在执行的时候会被翻译为 C 语言执行，所以一直很好奇 PHP 怎么调用底层函数。

换句话说就是已知函数名字的情况下如何调用 C 语言中对应名字的函数？

<!-- more -->

解决这个问题前，首先根据过往的经验做出假设，然后再去验证。

之前在写《用 C 语言实现面向对象》的时候，就意识到使用 void 指针实现很多功能，包括指向任意的函数。接着在写《PHP 数组底层实现》的时候，了解了 HashTable 的实现，即在 C 语言层面通过字符串 key 找到任意类型值。  

现在把两者结合起来，是否就能解决以上问题了？比如说把函数名作为 HashTable 的 key，函数指针作为 HashTable 的 value，这样就可以通过函数名获取函数指针来调用函数了。

接下来通过查看 PHP 的源码来看这个假设与真实情况有多少差距。

总体分为三个步骤：

1. 从 PHP 层进入 C 语言层
2. 找到字符串函数名与函数的关系
3. 函数的调用

注：这篇博客的源码对应的版本是 PHP 7.4.4 。  

> [https://github.com/php/php-src/tree/php-7.4.4](https://github.com/php/php-src/tree/php-7.4.4)

## 从 PHP 层进入 C 语言层

首先要找到 C 语言层调用函数的地方。怎么找？

经常使用 PHP 的同学看到前面的问题描述很容易联想到 PHP 中的一个传入函数名及其参数就可以调用函数的函数 `call_user_func()` 。可以从这里入手。

怎么找到 `call_user_func()` 在 PHP 源码中的位置？这就要根据 PHP 源码的规律来找了。

> 当然也可以直接全代码搜索，只是比较慢。

PHP 源码里面在定义一个 PHP 函数的时候会用 `PHP_FUNCTION(函数名)` ，所以只要找到 `PHP_FUNCTION(call_user_func)` 就可以了。

另外 `call_user_func()` 不像 `array_column()` 这种函数有特定前缀 `array_` ，所以属于比较基础的函数，而 PHP 的基础函数会放在两个地方：  

- 内置函数，放在 `Zend/zend_buildin_functions.c`；
- 标准库函数，放在 `ext/standard/` 。  
    举个例子： `ext/standard/array.c` 里有 `array_column()` 之类的函数。

在这两个地方搜索就能找到 `PHP_FUNCTION(call_user_func)` ，如下：  

`ext/standard/basic_functions.c`  

```c
PHP_FUNCTION(call_user_func)
{
    // ...
    if (zend_call_function(&fci, &fci_cache) == SUCCESS && Z_TYPE(retval) != IS_UNDEF) {
        // ...
    }
}
```

现在我们已经从 PHP 层面进入到 C 语言层面，接下去就是在 C 语言代码里面探索了。

## 找到字符串函数名与函数的关系

从上文展示位于 `ext/standard/basic_functions.c` 的 `call_user_func()` 函数定义可以找到关键点 `zend_call_function()` ，现在要找到这个函数。

这种以 `zend_` 开头的函数都在 `Zend/` 文件夹底下，所以我们要换个目录了。  

在 `Zend/` 文件夹里面随便搜索 `zend_call_function` ，从搜索结果里面随便挑一个跳转，然后通过 IDE 的功能（ctrl + 鼠标左键）跳转到它定义的地方就可以了。  

> 如果 IDE 能直接跳转就不用在 `Zend/` 文件夹搜索了，这里是因为 VS Code 没法直接跳转。  

注：以下代码中的 `// ...` 都表示我省略了一部分代码，但我会尽量保持代码结构。

> 第一遍看代码的时候不需要掌握所有细节，只需要了解整体概念或者前后关系，否则会陷入细节无法自拔。

`Zend/zend_execute_API.c`  

```c
int zend_call_function(zend_fcall_info *fci, zend_fcall_info_cache *fci_cache) /* {{{ */
{
    // ...
    if (!fci_cache || !fci_cache->function_handler) {
        // ...
        if (!zend_is_callable_ex(&fci->function_name, fci->object, IS_CALLABLE_CHECK_SILENT, NULL, fci_cache, &error)) {
            // ...
        }
        // ...
    }

    func = fci_cache->function_handler;
    // ...
    call = zend_vm_stack_push_call_frame(call_info,
        func, fci->param_count, object_or_called_scope);
    // ...
    if (func->type == ZEND_USER_FUNCTION) {
        // ...
    } else if (func->type == ZEND_INTERNAL_FUNCTION) {
        // ...
            func->internal_function.handler(call, fci->retval);
        // ...
    } else {
        // ...
    }
    // ...
    return SUCCESS;
}
/* }}} */
```

这里的关键点在于和函数名以及函数调用相关的词。关键词有：

- function name
- call
- return value

上面的代码片段中，我把几个有可能的点抽出来了。从这几个点出发，往前追溯参数来源或者查看后面使用它的地方就行了。  

> 如果被这个函数里面大量的 `EG(...)` 吸引而想知道其内部结构的话，就离结果非常近了。如果没有被其吸引，那也没关系，继续看。

优先深入看哪个呢？根据以前看数组源码的经验， “查找” 这个行为更容易获得信息，于是先看 `zend_is_callable_check_func()` 。

`Zend/zend_API.c`

```c
static zend_always_inline int zend_is_callable_check_func(int check_flags, zval *callable, zend_fcall_info_cache *fcc, int strict_class, char **error) /* {{{ */
{
    // ...
    if (!ce_org) {
        // ...
        /* Check if function with given name exists.
         * This may be a compound name that includes namespace name */
        if (UNEXPECTED(Z_STRVAL_P(callable)[0] == '\\')) {
            // ...
            func = zend_fetch_function(lmname);
            // ...
        }
        // ...    
    }
    // ...
}
```

`zend_fetch_function()` 与我们想要的答案有很强的相关性，看它怎么实现的。

`Zend/zend_execute.c`

```c
ZEND_API zend_function * ZEND_FASTCALL zend_fetch_function(zend_string *name)
{
    zval *zv = zend_hash_find(EG(function_table), name);
    // ...
}
```

来了来了！在这里就可以看到函数的确存在于 HashTable 里面。而这个 HashTable 通过 EG 获取。

`Zend/zend_globals_macros.h`

```c
# define EG(v) (executor_globals.v)
```

再跳转一次。

`Zend/zend_compile.c`

```c
ZEND_API zend_executor_globals executor_globals;
```

`zend_executor_globals` 是一个结构体。  

PHP 的源码中，结构体的真实定义会以下划线开头。

于是找 `_zend_executor_globals` 。

`Zend/zend_globals.h`

```c
struct _zend_executor_globals {
    // ...
    HashTable *function_table;    /* function symbol table */
    HashTable *class_table;        /* class table */
    HashTable *zend_constants;    /* constants table */
    // ...
}
```

到这里就找到存储函数的地方了。验证了函数名作为 key，函数指针作为 value 的可行性。

不过 PHP 并没有把函数指针直接作为 value，而是包装到了 zval 里面，以实现更多功能。从下面这一句就可以看出。

```c
zval *zv = zend_hash_find(EG(function_table), name);
```

看看 zval 里面有什么。

`Zend/zend_types.h`

```c
typedef struct _zval_struct     zval;

struct _zval_struct {
    zend_value        value;            /* value */
    // ...
};
```

继续：

`Zend/zend_types.h`

```c
typedef union _zend_value {
    zend_long         lval;                /* long value */
    double            dval;                /* double value */
    zend_refcounted  *counted;
    zend_string      *str;
    zend_array       *arr;
    zend_object      *obj;
    zend_resource    *res;
    zend_reference   *ref;
    zend_ast_ref     *ast;
    zval             *zv;
    void             *ptr;
    zend_class_entry *ce;
    zend_function    *func;
    struct {
        uint32_t w1;
        uint32_t w2;
    } ww;
} zend_value;
```

> 注：这个结构体很重要，我保留了全貌。

看到 `zend_function` 这个结构体，搜索 `_zend_function` 。

```c
union _zend_function {
    // ...
    zend_internal_function internal_function;
};
```

在 zend_value 联合体中可以看到 `zend_internal_function` 这个内部函数专用结构体，调用内部函数时用到它。搜索 `_zend_internal_function`。

`Zend/zend_compile.h`

```c
/* zend_internal_function_handler */
typedef void (ZEND_FASTCALL *zif_handler)(INTERNAL_FUNCTION_PARAMETERS);

typedef struct _zend_internal_function {
    /* Common elements */
    zend_uchar type;
    zend_uchar arg_flags[3]; /* bitset of arg_info.pass_by_reference */
    uint32_t fn_flags;
    zend_string* function_name;
    zend_class_entry *scope;
    zend_function *prototype;
    uint32_t num_args;
    uint32_t required_num_args;
    zend_internal_arg_info *arg_info;
    /* END of common elements */

    zif_handler handler;
    struct _zend_module_entry *module;
    void *reserved[ZEND_MAX_RESERVED_RESOURCES];
} zend_internal_function;
```

结构体 `_zend_internal_function` 里面的 handler 成员是 `zif_handler` 类型。  从前面的定义可以知道 `zif_handler` 是一个函数指针类型，这就是用来存函数指针的地方。

## 函数的调用

现在知道函数指针是存放在 handler 里面了，接着就是找到使用它的地方。

此时再回过头看 `zend_call_function` 这个函数。

`Zend/zend_execute_API.c`  

```c
int zend_call_function(zend_fcall_info *fci, zend_fcall_info_cache *fci_cache) /* {{{ */
{
    // ...
    if (func->type == ZEND_USER_FUNCTION) {
        // ...
    } else if (func->type == ZEND_INTERNAL_FUNCTION) {
        // ...
            func->internal_function.handler(call, fci->retval);
        // ...
    }
    // ...
}
/* }}} */
```

可以看到调用函数的地方：

```c
func->internal_function.handler(call, fci->retval);
```

handler 的参数固定是两个。这里要结合之前的 `PHP_FUNCTION(call_user_func)` 来看。

为了将 `PHP_FUNCTION(call_user_func)` 展开，以下连续列出三个定义：

`main/php.h`

```c
#define PHP_FUNCTION            ZEND_FUNCTION
```

`Zend/zend_API.h`

```c
#define ZEND_FN(name) zif_##name
#define ZEND_MN(name) zim_##name
#define ZEND_NAMED_FUNCTION(name)        void ZEND_FASTCALL name(INTERNAL_FUNCTION_PARAMETERS)
#define ZEND_FUNCTION(name)                ZEND_NAMED_FUNCTION(ZEND_FN(name))
```

`Zend/zend.h`

```c
#define INTERNAL_FUNCTION_PARAMETERS zend_execute_data *execute_data, zval *return_value
```

根据这三个地方的代码展开 `PHP_FUNCTION(call_user_func)` 可以得到：  

```c
void ZEND_FASTCALL call_user_func(zend_execute_data *execute_data, zval *return_value)
```

再看一次 `func->internal_function.handler(call, fci->retval);` 。联系起来了！

## 函数调用真正的入口

上文以 `PHP_FUNCTION(call_user_func)` 作为入口只是其中一种思路。实际上 PHP 在调用函数的时候不是通过 `call_user_func` ，不然 `call_user_func` 本身又是如何被调用的呢？

PHP 执行的时候，会在 PHP 虚拟机里面去调用函数。PHP 虚拟机首先会读取 PHP 文件，然后解析为 OPCode （操作码）执行。这里就要借助调试器的力量了。  

这里跳过 OPCode 的生成，因为与本次要探索的内容关系不是很大。

开启调试。然后不断往下走，可以找到一个比较接近答案的地方。

`Zend/zend_vm_execute.h`

```c
ZEND_API void zend_execute(zend_op_array *op_array, zval *return_value)
{
    zend_execute_data *execute_data;
    // ...
    i_init_code_execute_data(execute_data, op_array, return_value);
    zend_execute_ex(execute_data);
    zend_vm_stack_free_call_frame(execute_data);
}
```

先看 `zend_execute_ex` ：

`Zend/zend_vm_execute.h`

```c
// ...
# define OPLINE EX(opline)
// ...
# define ZEND_OPCODE_HANDLER_ARGS_PASSTHRU execute_data
// ...

ZEND_API void execute_ex(zend_execute_data *ex)
{
    DCL_OPLINE
    // ...
    zend_execute_data *execute_data = ex;
    // ...
    LOAD_OPLINE();
    ZEND_VM_LOOP_INTERRUPT_CHECK();
    // ...
    while (1) {
        // ...
        int ret;
        // ...
        if (UNEXPECTED((ret = ((opcode_handler_t)OPLINE->handler)(ZEND_OPCODE_HANDLER_ARGS_PASSTHRU)) != 0)) {
            // ...
            if (EXPECTED(ret > 0)) {
                execute_data = EG(current_execute_data);
                ZEND_VM_LOOP_INTERRUPT_CHECK();
            } else {
                // ...
                return;
            }
            // ...
        }
    }
    zend_error_noreturn(E_CORE_ERROR, "Arrived at end of main loop which shouldn't happen");
}
```

又看到了 handler，这里难道就是真正执行函数的地方？

先找到 OPLINE 的真身，根据：

`Zend/zend_compile.h`

```c
#define EX(element)             ((execute_data)->element)
```

对 OPLINE 展开后，得到 `execute_data->opline` 。

再根据 `execute_ex()` 前面的定义对整行展开得到：  

```c
if (UNEXPECTED((ret = ((opcode_handler_t)(execute_data->opline)->handler)(execute_data)) != 0))
```

现在出现四个新问题：

- opline 的 handler 存在哪个结构体？
- opline 的 handler 指向哪些函数？
- opline 的 handler 在哪里被赋值？
- 调用 opline 的 handler 就真的开始执行函数了吗？

### opline 的 handler 存在哪个结构体？

要解决这个问题，得先找到 opline 是哪来的。

回到 `Zend/zend_vm_execute.h` 的 `zend_execute()` ：

`Zend/zend_vm_execute.h`

```c
ZEND_API void zend_execute(zend_op_array *op_array, zval *return_value)
{
    zend_execute_data *execute_data;
    // ...
    i_init_code_execute_data(execute_data, op_array, return_value);
    zend_execute_ex(execute_data);
    zend_vm_stack_free_call_frame(execute_data);
}
```

 在 `zend_execute_ex()` 前面有个 `i_init_code_execute_data()` ：

`Zend/zend_execute.c`

```c
static zend_always_inline void i_init_code_execute_data(zend_execute_data *execute_data, zend_op_array *op_array, zval *return_value) /* {{{ */
{
    // ...
    EX(opline) = op_array->opcodes;
    // ...
}
```

opline 来自于 zend_op_array 的 opcodes ，搜索 `_zend_op_array` 。

`Zend/zend_compile.h`

```c
struct _zend_op_array {
    // ...
    zend_op *opcodes;
    // ...
};
```

opcodes 是 zend_op 这种结构体，搜索 `_zend_op` 。

`Zend/zend_compile.h`

```c
struct _zend_op {
    const void *handler;
    znode_op op1;
    znode_op op2;
    znode_op result;
    uint32_t extended_value;
    uint32_t lineno;
    zend_uchar opcode;
    zend_uchar op1_type;
    zend_uchar op2_type;
    zend_uchar result_type;
};
```

到这里就找到了 handler 存储的位置。

> 注：在 `Zend/zend_vm_opcodes.h` 可以找到 OPCode 对应的整数，在 `Zend/zend_vm_opcodes.c` 可以找到这些整数和字符串的对应。

### opline 的 handler 指向哪些函数？

由于 handler 是函数指针，可以指向任意函数，所以无法直接定位。于是通过调试执行下面这一句来找一些线索：  

`Zend/zend_vm_execute.h`

```c
ZEND_API void execute_ex(zend_execute_data *ex)
{
    // ...
    while (1) {
        // ...
        if (UNEXPECTED((ret = ((opcode_handler_t)OPLINE->handler)(ZEND_OPCODE_HANDLER_ARGS_PASSTHRU)) != 0)) {
            // ...
        }
    }
    // ...
}
```

在这一句的位置使用 “jump into”，会跳转到一个函数。这个函数就是 handler 指向的函数了。  

由于每次跳到的函数都可能不一样，所以选其中一个来查。  

`Zend/zend_vm_execute.h`

```c
static ZEND_VM_HOT ZEND_OPCODE_HANDLER_RET ZEND_FASTCALL ZEND_INIT_FCALL_SPEC_CONST_HANDLER(ZEND_OPCODE_HANDLER_ARGS)
{
    // ...
}
```

搜索函数名 `ZEND_INIT_FCALL_SPEC_CONST_HANDLER`。

`Zend/zend_vm_execute.h`

```c
void zend_vm_init(void)
{
    static const void * const labels[] = {
        // ...
        ZEND_INIT_FCALL_SPEC_CONST_HANDLER,
        // ...
    };
    static const uint32_t specs[] = {
        // ...
    };
    // ...
    zend_opcode_handlers = labels;
    zend_handlers_count = sizeof(labels) / sizeof(void*);
    zend_spec_handlers = specs;
    // ...
}
```

handler 可以指向 labels 里面包含的所有函数。

### opline 的 handler 在哪里被赋值？

上一节列出的 `zend_vm_init()` 把所有函数都放到了 labels 数组里面，并赋值给了 zend_opcode_handlers ，找找用到它的地方。

`Zend/zend_vm_execute.h`

```c
static const void* ZEND_FASTCALL zend_vm_get_opcode_handler_ex(uint32_t spec, const zend_op* op)
{
    // ...
    return zend_opcode_handlers[(spec & SPEC_START_MASK) + offset];
}
```

如果搜索调用 `zend_vm_get_opcode_handler_ex` 的代码，那么就很容易找到给 handler 赋值的地方了。

`Zend/zend_vm_execute.h`

```c
ZEND_API void ZEND_FASTCALL zend_vm_set_opcode_handler(zend_op* op)
{
    // ...
    op->handler = zend_vm_get_opcode_handler_ex(zend_spec_handlers[opcode], op);
}
```

### 调用 opline 的 handler 就真的开始执行函数了吗？

把上面举的例子 handler 指向的函数 `ZEND_INIT_FCALL_SPEC_CONST_HANDLER` 再拿出来。  

为了更加明显，此处不省略代码。

`Zend/zend_vm_execute.h`

```c
static ZEND_VM_HOT ZEND_OPCODE_HANDLER_RET ZEND_FASTCALL ZEND_INIT_FCALL_SPEC_CONST_HANDLER(ZEND_OPCODE_HANDLER_ARGS)
{
    USE_OPLINE
    zval *fname;
    zval *func;
    zend_function *fbc;
    zend_execute_data *call;

    fbc = CACHED_PTR(opline->result.num);
    if (UNEXPECTED(fbc == NULL)) {
        fname = (zval*)RT_CONSTANT(opline, opline->op2);
        func = zend_hash_find_ex(EG(function_table), Z_STR_P(fname), 1);
        if (UNEXPECTED(func == NULL)) {
            ZEND_VM_TAIL_CALL(zend_undefined_function_helper_SPEC(ZEND_OPCODE_HANDLER_ARGS_PASSTHRU));
        }
        fbc = Z_FUNC_P(func);
        if (EXPECTED(fbc->type == ZEND_USER_FUNCTION) && UNEXPECTED(!RUN_TIME_CACHE(&fbc->op_array))) {
            init_func_run_time_cache(&fbc->op_array);
        }
        CACHE_PTR(opline->result.num, fbc);
    }

    call = _zend_vm_stack_push_call_frame_ex(
        opline->op1.num, ZEND_CALL_NESTED_FUNCTION,
        fbc, opline->extended_value, NULL);
    call->prev_execute_data = EX(call);
    EX(call) = call;

    ZEND_VM_NEXT_OPCODE();
}
```

从中看不到执行的地方。找到的 func 也只是被放入 fcb，然后 push 到虚拟机调用栈里面。

> 注：这里另一个值得注意的地方是 `ZEND_VM_NEXT_OPCODE();` 。因为最开始的 `execute_ex` 函数（下一节列出了代码）里面只是一个死循环，且没有修改 OPLINE 的指向，而是在这些 handler 函数里面修改。

那真正调用函数的地方在哪呢？

### 真正调用函数的地方

回到最开始的 `execute_ex()` 。

`Zend/zend_vm_execute.h`

```c
ZEND_API void execute_ex(zend_execute_data *ex)
{
    DCL_OPLINE
    // ...
    zend_execute_data *execute_data = ex;
    // ...
    LOAD_OPLINE();
    ZEND_VM_LOOP_INTERRUPT_CHECK();
    // ...
    while (1) {
        // ...
        int ret;
        // ...
        if (UNEXPECTED((ret = ((opcode_handler_t)OPLINE->handler)(ZEND_OPCODE_HANDLER_ARGS_PASSTHRU)) != 0)) {
            // ...
            if (EXPECTED(ret > 0)) {
                execute_data = EG(current_execute_data);
                ZEND_VM_LOOP_INTERRUPT_CHECK();
            } else {
                // ...
                return;
            }
            // ...
        }
    }
    zend_error_noreturn(E_CORE_ERROR, "Arrived at end of main loop which shouldn't happen");
}
```

通过调试可以知道，如果是一些简单的操作， handler 就会直接处理。比如加减法。但是像函数调用这种，就不会在 handler 这里处理。

那么只能看下面的代码。

只有当 ret 大于 0 的时候会有额外的操作。通过调试可以看到有以下几个大于 0 的情况。

`Zend/zend_vm_execute.h`

```c
# define ZEND_VM_ENTER_EX()        return  1
# define ZEND_VM_ENTER()           return  1
# define ZEND_VM_LEAVE()           return  2
```

这个信息没有多大影响。

那么接下来就得看 `ZEND_VM_LOOP_INTERRUPT_CHECK();` 了。

`Zend/zend_execute.c`

```c
#define ZEND_VM_LOOP_INTERRUPT_CHECK() do { \
        if (UNEXPECTED(EG(vm_interrupt))) { \
            ZEND_VM_LOOP_INTERRUPT(); \
        } \
    } while (0)
```

继续：

`Zend/zend_vm_execute.h`
```c
#define ZEND_VM_LOOP_INTERRUPT() zend_interrupt_helper_SPEC(ZEND_OPCODE_HANDLER_ARGS_PASSTHRU);
```

继续：

`Zend/zend_vm_execute.h`

```c
static zend_never_inline ZEND_OPCODE_HANDLER_RET ZEND_FASTCALL zend_interrupt_helper_SPEC(ZEND_OPCODE_HANDLER_ARGS)
{
    EG(vm_interrupt) = 0;
    if (EG(timed_out)) {
        zend_timeout(0);
    } else if (zend_interrupt_function) {
        SAVE_OPLINE();
        zend_interrupt_function(execute_data);
        ZEND_VM_ENTER();
    }
    ZEND_VM_CONTINUE();
}
```

搜索 `zend_interrupt_function` 发现它是一个函数指针。那么转成搜索 `zend_interrupt_function =` ，看看哪个函数的指针传给了它。

这时搜索到了两条线。一条是 `ext/pcntl/pcntl.c`，另一条是 `win32/signal.c`。

这里选 `win32/signal.c`：

`win32/signal.c`

```c
PHP_WINUTIL_API void php_win32_signal_ctrl_handler_init(void)
{/*{{{*/
    // ...
    zend_interrupt_function = php_win32_signal_ctrl_interrupt_function;
    // ...
}/*}}}*/
```

接着找函数 `php_win32_signal_ctrl_interrupt_function` 。

`win32/signal.c`

```c
static void php_win32_signal_ctrl_interrupt_function(zend_execute_data *execute_data)
{/*{{{*/
    if (IS_UNDEF != Z_TYPE(ctrl_handler)) {
        zval retval, params[1];

        ZVAL_LONG(&params[0], ctrl_evt);

        /* If the function returns, */
        call_user_function(NULL, NULL, &ctrl_handler, &retval, 1, params);
        zval_ptr_dtor(&retval);
    }

    if (orig_interrupt_function) {
        orig_interrupt_function(execute_data);
    }
}/*}}}*/
```

感觉很接近了。

`call_user_function` 传了两个 NULL，为了避免理解上有偏差，把它的定义列出来。

`Zend/zend_API.h`

```c
#define call_user_function(function_table, object, function_name, retval_ptr, param_count, params) \
    _call_user_function_ex(object, function_name, retval_ptr, param_count, params, 1)
```

继续：

`Zend/zend_execute_API.c`

```c
int _call_user_function_ex(zval *object, zval *function_name, zval *retval_ptr, uint32_t param_count, zval params[], int no_separation) /* {{{ */
{
    zend_fcall_info fci;

    fci.size = sizeof(fci);
    fci.object = object ? Z_OBJ_P(object) : NULL;
    ZVAL_COPY_VALUE(&fci.function_name, function_name);
    fci.retval = retval_ptr;
    fci.param_count = param_count;
    fci.params = params;
    fci.no_separation = (zend_bool) no_separation;

    return zend_call_function(&fci, NULL);
}
```

绕了一圈还是绕回来了。又一次见到 `zend_call_function` 。上文已经分析过这个函数了，不再重复。

## 小结

本文通过假设 PHP 函数调用方式和查询源码验证，得到了 PHP 底层将 C 语言函数存储到 HashTable 然后通过函数名字找到函数指针来调用这一结论。同时也了解了 PHP 函数执行的大致流程。

虽然了解了也没什么用的样子，但好奇心得到了满足 233

