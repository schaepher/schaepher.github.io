---
title: 【数据结构】从源码看 PHP 7 数组的实现
date: 2020-03-15 16:59:00
updated: 2020-03-18 02:05:00
tags: 
- Map 
- Hash 
- PHP
---

> 本文所用源码为 PHP 7.4.4 的版本。

## PHP 7 数组概述

> PHP 中的数组实际上是一个有序映射。映射是一种把 values 关联到 keys 的类型。此类型在很多方面做了优化，因此可以把它当成真正的数组，或列表（向量），散列表（是映射的一种实现），字典，集合，栈，队列以及更多可能性。由于数组元素的值也可以是另一个数组，树形结构和多维数组也是允许的。 —— PHP 官方文档中文版

这里主要关注两个点：

- key 可以是整数，也可以是字符串。Float、Bool、Null 类型的 key 会被转换为整数或者字符串存储，其他类型的会报错。  
  value 可以是任意类型。  
- 遍历数组时，数组元素按照其 key 添加的顺序依次取出。

PHP 7 的数组分为 packed array 和 hash array 两种类型，在满足一定条件时可以互转。

- hash array 的 key 可以是整数也可以是字符串，在 hash 冲突时使用链表（冲突链）来解决冲突问题。
- packed array 的所有 key 是自然数，且依次添加的元素的 key 逐渐增大（不要求连续）。它的耗时和内存占用都比 hash 数组低。

以下仅介绍 hash array 相关的内容。

<!-- more -->

## 主要数据类型

下图是数组主要的数据类型：

```
                    Hash 区               arData                 Data 区

                                            +
                                            | 指 针 指 向 Data 区 的 开 始
                                            v

+----------+----------+----------+----------+----------+----------+----------+----------+
|          |          |          |          |          |          |          |          |
|nTableMask|nTableMask|  ......  |    -1    |    0     |    1     |  ......  |nTableSize|
|          |    +1    |          |          |          |          |          |    +1    |
+---------------------------------------------------------------------------------------+
|          |          |          |          |          |          |          |          |
| uint32_t | uint32_t |  ......  | uint32_t |  Bucket  |  Bucket  |  ......  |  Bucket  |
|          |          |          |          |          |          |          |          |
+----------+----------+----------+----------+----------+----------+----------+----------+
```

从整体看，这是一个数组。但入口是 arData 而不是处于最左侧的一个元素。arData 把数组分为两部分：  
- 左边是 Hash 区，其值为 uint32_t 类型，是冲突链的第一个元素在 Data 区的下标；  
- 右边是 Data 区，其值为 Bucket 类型，用于存储数据及其相关信息。 

由于 arData 主要指向 Data 区，因此其默认类型被配置为 Bucket 指针。

在申请内存时，会把 Hash 区所需的内存大小加上 Data 区所需的内存大小，然后一起申请。  

### Bucket 长什么样？

`zend_types.h`：

```c
/* 数组的基本元素 */
typedef struct _Bucket {
    zval              val;              /* 值 */
    zend_ulong        h;                /* hash 值（或者整数索引） */
    zend_string      *key;              /* 字符串 key（如果存储时用整数索引，则该值为 NULL） */
} Bucket;
```

Bucket 把 key 和 value 放在一起了。  

在冲突链中，Bucket 是一个节点。那么此时心里会有一个疑问：怎么获取冲突链的下一个节点？

### 冲突链

说到链表，会很自然地想到链表元素的结构体里包含着指向下一个元素的指针 `next` 。例如单向链表：

```c
typedef struct listNode {
    struct listNode *next;
    void *value;
} listNode;
```

但 Bucket 却不包含这个指针。

会不会在 Bucket 上一层，也就是数组的结构体定义中有一个专门存放冲突链的地方？

`zend_types.h`：

```c
typedef struct _zend_array HashTable;
struct _zend_array {
    zend_refcounted_h gc;
    union {
        struct {
            ZEND_ENDIAN_LOHI_4(
                zend_uchar    flags,
                zend_uchar    _unused,
                zend_uchar    nIteratorsCount,
                zend_uchar    _unused2)
        } v;
        uint32_t flags;
    } u;
    uint32_t    nTableMask;       // 用于把 hash 值转化为 [nTableMask, -1] 区间内的负数。根据 nTableSize 生成。
    Bucket     *arData;           // 指向 Data 区的指针。
    uint32_t    nNumUsed;         // Data 区最后一个有效 Bucket 的下标 + 1。
    uint32_t    nNumOfElements;   // 存在多少个有效 Bucket。删除数组元素时，会使其减一。
    uint32_t    nTableSize;       // 总共有多少空间。
    uint32_t    nInternalPointer;
    zend_long   nNextFreeElement;
    dtor_func_t pDestructor;
};
```

想错了，换个角度想想.jpg

那往 Bucket 下一层看看：

`zend_types.h`：

```c
typedef struct _zval_struct     zval;
struct _zval_struct {
    zend_value        value;    // 通用值结构。存储基础类型（double）或指针（数组、对象等等）
    union {
        struct {
            // 省略其他定义
        } v;
        uint32_t type_info;        // 值的类型，例如 IS_ARRAY 、IS_UNDEF
    } u1;
    union {
        uint32_t     next;         // 指向 hash 冲突链的下一个元素    <--- 就是这里
        // 省略其他定义
    } u2;                       // u2 表示第二个 union
};
```

惊！链表元素的 next 居然藏在 PHP 的通用数据类型 `zval` 里面。

想不到吧？.jpg

> 补充一点：  
> PHP HashMap 的冲突链始终是一个链表，不会像 JAVA 的 HashMap 那样在达成一定条件时转成红黑树。这会带来一定的问题。后面再详细说明。

## 怎么看 HashTable ？

再看一遍结构体。

`zend_types.h`：

```c
typedef struct _zend_array HashTable;
struct _zend_array {
    zend_refcounted_h gc;
    union {
        struct {
            ZEND_ENDIAN_LOHI_4(
                zend_uchar    flags,
                zend_uchar    _unused,
                zend_uchar    nIteratorsCount,
                zend_uchar    _unused2)
        } v;
        uint32_t flags;
    } u;
    uint32_t    nTableMask;       // 根据 nTableSize 生成的负数。用于把 hash 值转化为 [nTableMask, -1] 区间内的负整数，防止越界。
    Bucket     *arData;           // 指向 Data 区的指针。
    uint32_t    nNumUsed;         // Data 区最后一个有效 Bucket 的下标 + 1。
    uint32_t    nNumOfElements;   // 存在多少个有效 Bucket。删除数组元素时，会使其减一。
    uint32_t    nTableSize;       // 总共有多少空间。
    uint32_t    nInternalPointer; // 内部指针。受到 reset() 、 end() 、 next() 等的影响。
    zend_long   nNextFreeElement;
    dtor_func_t pDestructor;
};
```

有效 Bucket 指的是 Bucket val 的类型不为 IS_UNDEF 。也就是不为未定义的（undefined）值。无效 Bucket 反之。

nNumUsed 、nNumOfElements 、 nTableSize 的区别：

```
nNumUsed        = 4
nNumOfElements  = 3
nTableSize      = 8

+----------+----------+-----------+----------+-----------+-----------+-----------+
|          |          |           |          |           |           |           |
|    0     |    1     |     2     |    3     |     4     |  ......   |     7     |
|          |          |           |          |           |           |           |
+--------------------------------------------------------------------------------+
|          |          |           |          |           |           |           |
|  Bucket  |  Bucket  | Undefined |  Bucket  | Undefined | Undefined | Undefined |
|          |          |   Bucket  |          |   Bucket  |  Buckets  |   Bucket  |
+----------+----------+-----------+----------+-----------+-----------+-----------+
```

## 数组的主要操作

PHP 数组主要用到的基本操作有：查找、添加、更新、删除

PHP 内部操作有：rehash 、扩容

其中查找是较为简单的，添加、更新、删除都包含了查找的动作，因此先看查找。

### 查找

由于 key 有整数和字符串这两种类型，因此查找的实现也分为两种。这里以整数 key 为例。

> 读源码时要注意 HT_HASH_* 和 HT_DATA_* 开头的函数，分别代表着在 Hash 区和 Data 区的操作。

`zend_hash.c`

```c
static zend_always_inline Bucket *zend_hash_index_find_bucket(const HashTable *ht, zend_ulong h)
{
    uint32_t nIndex;
    uint32_t idx;
    Bucket *p, *arData;

    arData = ht->arData;
    nIndex = h | ht->nTableMask;                // 避免 Hash 区越界
    idx = HT_HASH_EX(arData, nIndex);           // 在 Hash 区取 nIndex 位置的值，结果是 Data 区某个 Bucket 的下标
    while (idx != HT_INVALID_IDX) {
        ZEND_ASSERT(idx < HT_IDX_TO_HASH(ht->nTableSize));  // 确保 Data 区没有越界
        p = HT_HASH_TO_BUCKET_EX(arData, idx);  // 用 Data 区下标获取 Bucket，即冲突链的第一个 Bucket
        if (p->h == h && !p->key) {             // 整数 key 存到 h，因此比对 h。p->key 为 NULL 表示 Bucket 的 key 为整数 key
            return p;
        }
        idx = Z_NEXT(p->val);                   // 没有找到的话，从当前的 Bucket 获取冲突链的下一个 Bucket
    }
    return NULL;                                // 链表遍历完也没找到，那就是不存在
}
```

举个例子：

```c
 nTableSize = 8

 nTableMask = -(nTableSize + nTableSize)

            = (-16)            = (11111111111111111111111111110000)
                   10                                              2

 h          = (100000000)      = (00000101111101011110000100000000)
                         10                                        2

 nIndex     = (h | nTableMask) = (11111111111111111111111111110000)  = (-16)
                                                                   2     +  10
                                                                         |
     +-------------------------------------------------------------------+
     |
     |                  Hash          arData          Data
     |
     |                                   +
     |                                   |              +----------------------------+
     v                                   v              v                            |
                                                                                     |
+---------+---------+----------+---------+---------+---------+----------+---------+  |
|         |         |          |         |         |         |          |         |  |
|   -16   |   -15   |  ......  |   -1    |    0    |    1    |  ......  |    7    |  |
|         |         |          |         |         |         |          |         |  |
+---------------------------------------------------------------------------------+  |
|         |         |          |         |         |         |          |         |  |
|    1    |    6    |  ......  |    5    | Bucket0 | Bucket1 |  ......  | Bucket7 |  |
|         |         |          |         |         |         |          |         |  |
+---------+---------+----------+---------+---------+---------+----------+---------+  |
                                                                                     |
     +                                                 +                     ^       |
     |                                                 |        next         |       |
     |                                                 +---------------------+       |
     |                                                                               |
     +-------------------------------------------------------------------------------+
```


至于为什么 `nTableMask = -(nTableSize + nTableSize)` ，见下文的【负载因子】。

nTableMask 使得无论多大的 uint32_t ，在按位或以及转成有符号整数后，都会变成负整数，并且其值会在 [nTableMask, -1] 这个区间。

介绍完整数 key 的查找，顺便对比一下字符串 key 的查找，不同之处如下：

- 字符串 key 会存到 `p->key` 里面，而这个字符串的 hash 存到 `p->h` 里面。
- 在比较 key 的时候，整数 key 是比较两个整数是否相等，而字符串 key 会先比较 hash 是否相等，然后比较两个字符串是否相等。

## 添加

依然取整数 key 为例。这里不关注更新元素的部分和 packed array 的部分。

`zend_hash.c`:

```c
static zend_always_inline zval *_zend_hash_index_add_or_update_i(HashTable *ht, zend_ulong h, zval *pData, uint32_t flag)
{
    // ... 省略代码
    idx = ht->nNumUsed++;                       // 使用空间 + 1
    nIndex = h | ht->nTableMask;                // 取 hash 值对应的 Hash 区的下标
    p = ht->arData + idx;                       // 获取指向新元素的指针
    Z_NEXT(p->val) = HT_HASH(ht, nIndex);       // 新 Bucket 指向 Hash 区下标所指的冲突链第一个 Bucket
    HT_HASH(ht, nIndex) = HT_IDX_TO_HASH(idx);  // Hash 区下标指向新 Bucket
    if ((zend_long)h >= (zend_long)ht->nNextFreeElement) {
        ht->nNextFreeElement = h < ZEND_LONG_MAX ? h + 1 : ZEND_LONG_MAX;
    }
add:
    ht->nNumOfElements++;                       // 元素个数 + 1
    p->h = h;                                   // 整数 key 的下标就是 hash
    p->key = NULL;                              // 整数 key 时，必须把 p->key 设置为 NULL
    ZVAL_COPY_VALUE(&p->val, pData);            // 把要添加的值复制到新 Bucket 里面

    return &p->val;
}
```

小二，上图！

```c
 nNumUsed       = 1

 nNumOfElements = 1

 nTableSize     = 8

 nTableMask     = (-16)            = (11111111111111111111111111110000)
                       10                                              2

 h              = (100000000)      = (00000101111101011110000100000000)
                             10                                        2

 nIndex         = (h + nTableMask) = (11111111111111111111111111110000)  = (-16)
                                                                       2        10
                                                                             +
                                                                             |
     +-----------------------------------------------------------------------+
     |
     |                 Hash          arData          Data
     |
     |                                  +
     |                                  |    +-------------------------------------+
     v                                  v    v                                     |
                                                                                   |
+---------+---------+---------+---------+---------+---------+---------+---------+  |
|         |         |         |         |         |         |         |         |  |
|   -16   |   -15   | ......  |   -1    |    0    |    1    |  ...... |    7    |  |
|         |         |         |         |         |         |         |         |  |
+-------------------------------------------------------------------------------+  |
|         |         |         |         |         |Undefined|Undefined|Undefined|  |
|    0    |   -1    | ......  |   -1    | Bucket0 | Bucket1 | Buckets | Bucket7 |  |
|         |         |         |         |         |         |         |         |  |
+---------+---------+---------+---------+---------+---------+---------+---------+  |
                                                                                   |
     +                                                                             |
     +-----------------------------------------------------------------------------+

                                                        ^
                                                        +

                                                   可 用 的 Bucket

 nNumUsed       = 2

 nNumOfElements = 2

                       Hash          arData          Data

                                        +
                                        |              +---------------------------+
                                        v              v                           |
                                                                                   |
+---------+---------+---------+---------+---------+---------+---------+---------+  |
|         |         |         |         |         |         |         |         |  |
|   -16   |   -15   | ......  |   -1    |    0    |    1    | ......  |    7    |  |
|         |         |         |         |         |         |         |         |  |
+-------------------------------------------------------------------------------+  |
|         |         |         |         |         |         |Undefined|undefined|  |
|    1    |   -1    | ......  |   -1    | Bucket0 | Bucket1 | Buckets | Bucket7 |  |
|         |         |         |         |         |         |         |         |  |
+---------+---------+---------+---------+---------+---------+---------+---------+  |
                                                                                   |
     +                                       ^   next   +                          |
     |                                       +----------+                          |
     |                                                                             |
     +-----------------------------------------------------------------------------+
```

文字表述为：

1. 获取数组 arData 最后一个元素之后的合法位置（这个位置的内存在之前已经申请好了）。把这里的 Bucket 称为 BucketA。
2. 把 BucketA 的下标放入 BucketA 的 h 中，把要添加的元素值放入 BucketA 的 val 。
3. 把 Hash 区 `(h | nTableMask)` 位置指向的 Data 下标存储的 Bucket 称为 BucketB。
4. 把 BucketA 的 val 的 next 指向 BucketB 。
5. 更新Hash 区 `(h | nTableMask)` 位置的值为 BucketA 的下标。

> Hash 区 -1 表示 `HT_INVALID_IDX`

## 更新

在上面的添加部分，可以看到函数的定义是：  

```c
static zend_always_inline zval *_zend_hash_index_add_or_update_i(HashTable *ht, zend_ulong h, zval *pData, uint32_t flag)
```

它把添加和更新放在一起处理了。

实际上在添加的时候，会先使用：   

`zend_hash_index_find_bucket(const HashTable *ht, zend_ulong h)`   

来看 h 这个 key 是否存在。如果存在就执行更新，如果不在就执行添加。

更新的操作就是把 pData 复制到找到的 Bucket 里面，替换掉原先的值。

## 删除

删除分为三种情况：

1. 目标 key 不存在
2. 目标 key 存在，其指向的 Bucket 处于冲突链的第一个位置
3. 目标 key 存在，其指向的 Bucket 不处于冲突链的第一个位置

目标 key 不存在，直接返回就可以了。

目标 key 存在时，包括两个主要的操作：

- 处理冲突链指针
- 释放内存

处理冲突链的指针时，分为两种情况：

- 在第一个位置：直接让 Hash 区的值指向冲突链第二个位置的 Bucket 在 Data 区的下标；
- 不在第一个位置：同链表删除中间元素的操作。

释放内存时：

- 如果 key 是字符串，则尝试释放 key 的空间；
- 把 Bucket 的 val 复制到另一个变量 data，把 Bucket 的 val 的类型设置为 undefined；
- 尝试释放 data 所占的空间。

做删除动作的入口是： 

`zend_hash_del_bucket(HashTable *ht, Bucket *p)`  

做核心操作的是：  

`_zend_hash_del_el_ex(HashTable *ht, uint32_t idx, Bucket *p, Bucket *prev)`

看一看源码：

`zend_hash.c`:

```c
static zend_always_inline void _zend_hash_del_el_ex(HashTable *ht, uint32_t idx, Bucket *p, Bucket *prev)
{
    if (!(HT_FLAGS(ht) & HASH_FLAG_PACKED)) {
        if (prev) {                                                 // 处于冲突链的中间
            Z_NEXT(prev->val) = Z_NEXT(p->val);
        } else {                                                    // 处于冲突链的第一个
            HT_HASH(ht, p->h | ht->nTableMask) = Z_NEXT(p->val);    // 让 Hash 区的值指向下一个 Bucket 的 Data 区下标
        }
    }

    idx = HT_HASH_TO_IDX(idx);
    ht->nNumOfElements--;    // 数组元素计数器减一。此时 nNumUsed 保持不变。

    // 如果数组内部指针指向要删除的这个 Bucket ，则让其指向数组下一个有效 Bucket 。
    if (ht->nInternalPointer == idx || UNEXPECTED(HT_HAS_ITERATORS(ht))) {
        uint32_t new_idx;

        new_idx = idx;
        while (1) {
            new_idx++;
            if (new_idx >= ht->nNumUsed) {
                break;
            } else if (Z_TYPE(ht->arData[new_idx].val) != IS_UNDEF) {
                break;
            }
        }
        if (ht->nInternalPointer == idx) {
            ht->nInternalPointer = new_idx;
        }
        zend_hash_iterators_update(ht, idx, new_idx);
    }

    // 如果要删除的元素是数组的最后一个元素，则尝试从后往前多回收几个无效 Bucket
    if (ht->nNumUsed - 1 == idx) {
        do {
            ht->nNumUsed--;
        } while (ht->nNumUsed > 0 && (UNEXPECTED(Z_TYPE(ht->arData[ht->nNumUsed-1].val) == IS_UNDEF)));
        ht->nInternalPointer = MIN(ht->nInternalPointer, ht->nNumUsed);
    }

    // key 为字符串时，释放字符串内存
    if (p->key) {
        zend_string_release(p->key);
    }

    if (ht->pDestructor) {      // 如果配置了析构函数，则调用析构函数
        zval tmp;
        ZVAL_COPY_VALUE(&tmp, &p->val);
        ZVAL_UNDEF(&p->val);
        ht->pDestructor(&tmp);
    } else {
        ZVAL_UNDEF(&p->val);    // 没有析构函数，则直接将 zval 的 u1.type_info 配置为 undefind。不用释放空间，因为以后元素可以重用这个空间
    }
}
```

## PHP 数组可拥有的最大容量

`zend_types.h`

```c
#if SIZEOF_SIZE_T == 4
# define HT_MAX_SIZE 0x04000000 /* small enough to avoid overflow checks */
/* 省略代码 */
#elif SIZEOF_SIZE_T == 8
# define HT_MAX_SIZE 0x80000000
/* 省略代码 */
#else
# error "Unknown SIZEOF_SIZE_T"
#endif
```

根据 `sizeof(size_t)` 的执行结果判断应该设置为 67108864 还是 2147483648 。

> 0x04000000 转为二进制是： 00000100000000000000000000000000  
> 0x80000000 转为二进制是： 10000000000000000000000000000000

当 nNumUsed 大于等于 nTableSize 时，会触发 Resize 操作，以此获取更多可使用的 Bucket 。

## Resize 策略

Resize 的定义是：  

`zend_hash.c`：

`static void ZEND_FASTCALL zend_hash_do_resize(HashTable *ht)`

Resize 有两种策略：

- rehash
- 双倍扩容 + rehash

之所以有不用双倍扩容的选择，是因为 PHP 在删除元素时，只是将对应 Data 区的 Bucket 的值设置为 undefined，并没有移动后面的元素。

选择的条件主要涉及 HashTable 的三个成员：  

```c
struct _zend_array {
    // ...省略
    uint32_t    nNumUsed;         // Data 区最后一个有效 Bucket 的下标 + 1。
    uint32_t    nNumOfElements;   // 存在多少个有效 Bucket。删除数组元素时，会使其减一。
    uint32_t    nTableSize;       // 总共有多少空间。
    // ...省略
}
```

#### 什么情况下只需要 rehash ？

源码是：

`ht->nNumUsed > ht->nNumOfElements + (ht->nNumOfElements >> 5)`  

这里做一个转换，方便理解：  

`ht->nNumUsed - ht->nNumOfElements > (ht->nNumOfElements >> 5)`  

也就是被设置为 undefined 的 Bucket 数量大于当前元素个数除以 32 向下取整的值。

例如：

- 当 nNumUsed 为 2048 ， nNumOfElements 为 2000 的时候，得到 `2048 - 2000 < 62` ，因此执行扩容。
- 当 nNumUsed 为 2048 ， nNumOfElements 为 1900 的时候，得到 `2048 - 1900 > 59` ，因此执行 rehash。

rehash 做以下操作：  

1. 清空 Hash 区；
2. 取两个指针，一个指向当前扫描的位置（叫做 p），一个指向迁移后的位置（叫做 q），遍历直到 p 到达 nNumUsed ；  
   p 在碰到无效 Bucket 时，会继续往前走一步，不做其他事。  
   p 在碰到有效 Bucket 时，会把 Bucket 的值复制到 q 指向的 Bucket 的值，并且 p 和 q 一起往前走一步。  
   这种做法的效率会比每次移动有效 Bucket 都把后面的数据一起往前移动来得高。
3. 重新创建冲突链；
4. 更新内部指针，使其指向更新位置后的 Bucket；
5. 更新 nNumUsed，使其等于 nNumOfElements 。

#### 什么情况下双倍扩容 + rehash ？

满足只 rehash 的条件就只做 rehash，如果不满足条件并且 nTableSize 小于数组可拥有的最大容量（`HT_MAX_SIZE`），则双倍扩容。

由于 `HT_MAX_SIZE` 是 `0x04000000` 或者 `0x80000000`，并且 nTableSize 始终是 2 的次方，所以最后一次双倍扩容后的容量刚好是 `HT_MAX_SIZE` 。

> 0x04000000 转为二进制是： 00000100000000000000000000000000  
> 0x80000000 转为二进制是： 10000000000000000000000000000000 

双倍扩容时，做以下操作：  

1. nTableSize 变为原先的两倍；
2. 重新申请一次 Hash 区和 Data 区的内存，然后把原先 Data 区的数据以内存拷贝的方式复制到新的 Data 区；
3. 重新计算 nTableMask；
4. 释放掉原先 Data 区的内存；
5. 做 rehash 。主要是为了重建 Hash 区。


## 负载因子（Load Factor）

负载因子会影响 hash 碰撞的概率从而影响到耗时，也会影响 Hash 区的大小来影响内存消耗。  

在 PHP 中，用 nTableMask 和 nTableSize 的关系来体现：

`负载因子 = |nTableMask / nTableSize|`

- 负载因子为 1 的时候（PHP 5），`nTableMask == - (nTableSize)` 。  
- 负载因子为 0.5 的时候（PHP 7）， `nTableMask == - (nTableSize + nTableSize)` 。

> 上一次修改负载因子的提交是：  
> [https://github.com/php/php-src/commit/34ed8e53fea63903f85326ea1d5bd91ece86b7ae](https://github.com/php/php-src/commit/34ed8e53fea63903f85326ea1d5bd91ece86b7ae)

为什么负载因子会影响时间消耗和内存消耗？ 

负载因子越大， nTableMask 绝对值就越小（nTableMask 本身受到 nTableSize 的影响），从而导致 Hash 区变小。

Hash 区一旦变小，更容易产生碰撞。也就使得冲突链更长，执行的操作会在冲突链的时间消耗变得更长。

负载因子越小，Hash 区变大，使得内存消耗更多，但冲突链变短，操作耗时变小。

|负载因子|时间消耗|内存消耗|
|:--|:--|:--|
|大|小|大|
|小|大|小|

所以要根据对内存和时间的要求来做调整。  

PHP 的负载因子从 1 （PHP5） 降到 0.5 （PHP7），使得速度变快了，但同时内存消耗变大。

针对内存消耗，PHP 还做了个改进，增加了 packed array。

## packed array

packed array 的所有 key 是自然数，且依次添加的元素的 key 逐渐增大（不要求连续）。  

packed array 查询时可以直接根据下标计算目标元素的位置（相当于 c 语言的数组），因此它不需要 Hash 区来加速。  

不过由于在某些条件下， packed array 会转成 hash array ，所以它仍然保留 nTableMask 。只是 nTableMask 固定为最小值，当前为 -2 。

Hash 区只有两个位置，其值都是 HT_INVALID_IDX ，也就是 -1 。