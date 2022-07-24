---
title: 内存分配器
date: 2020-03-23 23:46:00
updated: 2020-03-24 02:44:00
tags: 
- Memcache 
- Redis 
- PHP 
- GO 
- 内存 
- 内存分配
---

## 传统的内存分配和现代的内存分配

传统的内存分配是在需要内存的时候使用 `malloc()` 函数直接向操作系统申请内存，在释放内存的时候用 `free()` 把内存还给操作系统。

> malloc = memory allocate 

直接使用这两个函数来管理内存的问题在于，每次申请内存都是一个很耗时的操作，而且频繁申请和释放内存会导致内存有很多碎片（外部碎片）。

> 外部碎片：分散在内存中的小块内存，其总和可以满足某个进程的申请要求，但由于内存碎片不连续，进程无法一次性申请这些内存。

例如：

```c
+-----+-----+-----+-----+-----+-----+-----+-----+-----+
|  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |
+-----------------------------------------------------+
| |-------| | |-------| | |-------------| |           |
| |-------| | |-------| | |-------------| |           |
+-----------+-----------+-----------------+-----+-----+

+-----+-----+-----+-----+-----+-----+-----+-----+-----+
|  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |
+-----------------+-----------------------------------+
| |-------| |           | |-------------| |           |
| |-------| |           | |-------------| |           |
+-----------+-----------+-----------------+-----+-----+
```

<!-- more -->

1. 申请 2 块单位为 2 的内存和 1 块单位为 3 的内存；
2. 释放掉中间一块单位为 2 的内存；
3. 此时如果要申请一块长度为 3 的内存，无法申请到。

为了解决这些问题，现代的内存分配器会一次性向操作系统申请一块（或者一堆）大内存。大内存可按照特定单位切割成一块块大小相等的内存块，不同类型的单位切割成的内存块大小不同。当进程内部需要内存的时候，找到一块与所需内存大小非常接近但又比所需内存大的内存块，并直接使用。

例如：  

```c
内存以 3 为单位做切割。

+-----+-----+-----+-----+-----+-----+-----+-----+-----+
|  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |
+-----------+-----------------+-----------------------+
| |--------|      | |-------|       | |-------------| |
| |--------|      | |-------|       | |-------------| |
+-----------------+-----------------+-----------------+

+-----+-----+-----+-----+-----+-----+-----+-----+-----+
|  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |
+-----------+-----------+-----+-----------------------+
| |--------|      |                 | |-------------| |
| |--------|      |                 | |-------------| |
+-----------------+-----------------+-----------------+
```

1. 申请 2 块单位为 2 的内存和 1 块单位为 3 的内存；
2. 释放掉中间一块单位为 2 的内存；
3. 此时如果要申请一块长度为 3 的内存，可以直接申请中间那块。

这比向系统直接申请的方式快得多，并且减少了外部碎片。但因为内存块往往比所需内存大一点，多出来的部分就成了内部碎片。这个问题相比外部碎片好一些，内部碎片可以通过设置以不同单位为块的内存来缓解。

## 现代内存分配器

现代内存分配器例如 Linux 的 SLUB Allocator （前身是 SLAB Allocator），此外还有比较常见的： jemalloc 、 TCMalloc 和 ptmalloc 。

> TCMalloc = Thread-Caching Malloc   
> ptmalloc = pthreads Malloc

以下举一些例子。

### PHP

PHP 的内存分配器参考 jemalloc 和 TCMalloc 的实现。

`Zend/zend_alloc.c`：

```c
/*
 * zend_alloc is designed to be a modern CPU cache friendly memory manager
 * for PHP. Most ideas are taken from jemalloc and tcmalloc implementations.
 * ....
 */
```

### Golang

Golang 的内存分配器是基于 TCMalloc 实现的。

`runtime/malloc.go`：

```go
// Memory allocator.
//
// This was originally based on tcmalloc, but has diverged quite a bit.
```

### Redis

Redis 把 jemalloc 和 TCMalloc 作为可选项，可以在编译的时候选择用哪种分配器。  

`src/zmalloc.h`：

```c
#if defined(USE_TCMALLOC)
// 省略
#include <google/tcmalloc.h>
// 省略
#endif

#elif defined(USE_JEMALLOC)
// 省略
#include <jemalloc/jemalloc.h>
// 省略
#endif
```

在 redis 源码中，自带了 jemalloc 源码 `deps/jemalloc`。

### Memcache

使用的是 SLAB Allocator 的机制。

```c
/*
 * Slabs memory allocation, based on powers-of-N.
 * ....
 */
```

## 扩展阅读

内存优化总结:ptmalloc、tcmalloc和jemalloc： http://www.cnhalo.net/2016/06/13/memory-optimize/  

图解Go内存分配器： https://tonybai.com/2020/02/20/a-visual-guide-to-golang-memory-allocator-from-ground-up/

Memcache-内存模型-源码分析： https://www.jianshu.com/p/a824ae00d9bb

Linux slab 分配器剖析： https://www.ibm.com/developerworks/cn/linux/l-linux-slab-allocator/index.html

图解 TCMalloc： https://zhuanlan.zhihu.com/p/29216091

（七）PHP内存管理详解： https://blog.csdn.net/IT_10/article/details/94768679
