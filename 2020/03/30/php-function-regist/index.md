# 【PHP 源码】PHP 函数注册



# 函数的注册

调用顺序为：  

```
- main
-- php_cli_startup
--- php_module_startup
---- zend_startup
----- zend_startup_builtin_function
------ zend_register_module_ex(*module)
------- zend_register_functions(module->functions)
```

<!-- more -->

`sapi/cli/php_cli.c`

```c
int main(int argc, char *argv[])
{
    // ...

    sapi_module_struct *sapi_module = &cli_sapi_module;
    
    // ...
    
    /* startup after we get the above ini override se we get things right */
    if (sapi_module->startup(sapi_module) == FAILURE) {
        // ...
    }
    
    // ...
            exit_status = do_cli(argc, argv);
    // ...
}
```

`main/SAPI.h`

```c
typedef struct _sapi_module_struct sapi_module_struct;

struct _sapi_module_struct {
    char *name;
    char *pretty_name;

    int (*startup)(struct _sapi_module_struct *sapi_module);
    // ...
}
```

`sapi/cli/php_cli.c`

```c
static sapi_module_struct cli_sapi_module = {
    "cli",                            /* name */
    "Command Line Interface",        /* pretty name */

    php_cli_startup,                /* startup */

    // ...

    const zend_function_entry *additional_functions;

    // ...
}
```

`sapi/cli/php_cli.c`

```c
static int php_cli_startup(sapi_module_struct *sapi_module)
{
    if (php_module_startup(sapi_module, NULL, 0)==FAILURE) {
        return FAILURE;
    }
    return SUCCESS;
}
```

`main/main.c`

```c
int php_module_startup(sapi_module_struct *sf, zend_module_entry *additional_modules, uint32_t num_additional_modules)
{
    // ...

    zend_startup(&zuf);

    // ...
}
```

`Zend/zend.c`

```c
int zend_startup(zend_utility_functions *utility_functions) /* {{{ */
{
    // ...

    zend_startup_builtin_functions();

    // ...
}
```

`Zend/zend_builtin_functions.c`

```c
int zend_startup_builtin_functions(void) /* {{{ */
{
    zend_builtin_module.module_number = 0;
    zend_builtin_module.type = MODULE_PERSISTENT;
    return (EG(current_module) = zend_register_module_ex(&zend_builtin_module)) == NULL ? FAILURE : SUCCESS;
}
```

`Zend/zend_builtin_functions.c`

```c
zend_module_entry zend_builtin_module = { /* {{{ */
    STANDARD_MODULE_HEADER,
    "Core",
    builtin_functions,
    ZEND_MINIT(core),
    NULL,
    NULL,
    NULL,
    NULL,
    ZEND_VERSION,
    STANDARD_MODULE_PROPERTIES
};
```

`Zend/zend_builtin_functions.c`

```c
static const zend_function_entry builtin_functions[] = { /* {{{ */
    ZEND_FE(zend_version,        arginfo_zend__void)
    ZEND_FE(func_num_args,        arginfo_zend__void)
    ZEND_FE(func_get_arg,        arginfo_func_get_arg)
    ZEND_FE(func_get_args,        arginfo_zend__void)
    ZEND_FE(strlen,            arginfo_strlen)
    // ...
    ZEND_FE(function_exists,    arginfo_function_exists)
    // ...

}
```

`Zend/zend_API.c`

```c
ZEND_API zend_module_entry* zend_register_module_ex(zend_module_entry *module)
{
    // ...
    if (module->functions && zend_register_functions(NULL, module->functions, NULL, module->type)==FAILURE) {
        // ...
    }
    // ...
}
```

`Zend/zend_API.c`

```c
/* registers all functions in *library_functions in the function hash */
ZEND_API int zend_register_functions(zend_class_entry *scope, const zend_function_entry *functions, HashTable *function_table, int type)
{
    // ...
    if (!target_function_table) {
        target_function_table = CG(function_table);
    }
    // ...
    while (ptr->fname) {
        // ...
        memcpy(reg_function, &function, sizeof(zend_internal_function));
        if (zend_hash_add_ptr(target_function_table, lowercase_name, reg_function) == NULL) {
            // ...
        }
        // ...
    }
}
```

基本函数的注册到这里就基本结束了。

但是像 `array_column()` 这种函数不属于内置函数，它属于 standard 扩展的函数。那么它在哪里被注册呢？

`main/main.c`

```c
int php_module_startup(sapi_module_struct *sf, zend_module_entry *additional_modules, uint32_t num_additional_modules)
{
    // ...

    /* startup extensions statically compiled in */
    if (php_register_internal_extensions_func() == FAILURE) {
        php_printf("Unable to start builtin modules\n");
        return FAILURE;
    }

    // ...
}
```


看到这里就基本结束了。其他细节有兴趣可以继续研究。



结构体：

`Zend/zend_modules.h`

```c
typedef struct _zend_module_entry zend_module_entry;
struct _zend_module_entry {
    // ...
    const struct _zend_function_entry *functions;
    // ...
}
```

`ext/standard/basic_functions.c`

```c
zend_module_entry basic_functions_module = {
    // ...
    "standard",                    /* extension name */
    basic_functions,            /* function list */
    // ...
};
```

`ext/standard/basic_functions.h`

```c
extern zend_module_entry basic_functions_module;
```

## 后记

最开始写这篇文章的时候，是靠分析和 VS Code 的查找功能来理清楚调用顺序的。结果在 `php_module_startup` 这一层里面找的时候，没注意 `zend_startup` 就跳过这一行找下面了。导致绕了个弯。最后决定编译 PHP 源码，用调试的方式看源码，就像当初学习 Laravel 那样。这样看起源码来容易多了，而且以后看源码也能减少很多负担。

在开启调试后，回头又补充了前面关于函数调用的解释。最开始使用 `array_key_exist()` 来查看调用栈，没想到 PHP 并没有调用 `ext/standard/array.c` 里面 `array_key_exist` 的代码，而是直接使用 `Zend/zend_execute.c` 里的 `zend_array_key_exists_fast`，让我多花了一些时间。

