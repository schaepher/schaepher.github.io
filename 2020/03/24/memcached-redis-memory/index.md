# Memcached Redis 字符串存储容量上限


在 Memcached 和 Redis 的比较中，总会提到它们存储字符串的区别。

Memcached 默认上限是 1MB （最大上限是 1GB），而 Redis 是 512MB 。

但是这样就够了吗？我们很自然的会对此提出一些问题。

# 这个“字符串存储容量上限”的限制配置在哪？

看看源码吧。

`memcached/memcached.c`：

```c
static void settings_init(void) {
    // ... 省略代码
    settings.item_size_max = 1024 * 1024; /* The famous 1MB upper limit. 著名的 1MB 上限 */
    settings.slab_page_size = 1024 * 1024; /* chunks are split from 1MB pages. 数据块由 1MB 的页分割得到 */
    // ... 省略代码
}
```

当然，这是默认的 1MB。启动时可以通过参数修改这个最大上限。这个最大上限能调整到什么程度呢？

<!-- more -->

`memcached/memcached.h`：

```c
/** Maximum length of a key. */
#define KEY_MAX_LENGTH 250

// ... 省略代码

/*
 * Valid range of the maximum size of an item, in bytes.
 */
#define ITEM_SIZE_MAX_LOWER_LIMIT 1024
#define ITEM_SIZE_MAX_UPPER_LIMIT 1024 * 1024 * 1024
```

顺便可以看到，上限还能往下调，调到 1KB。 Key 的最大长度为 250 Byte。

`redis/src/t_string.c`：

```c
static int checkStringLength(client *c, long long size) {
    if (size > 512*1024*1024) {
        addReplyError(c,"string exceeds maximum allowed size (512MB)");
        return C_ERR;
    }
    return C_OK;
}
```

# 这个配置是由什么引起的？

## Memcached

Memcached 在紧挨 item_size_max 后面还有个重要的配置 —— slab_page_size ，它决定了每次向系统申请多少内存，将这一块内存称之为页（page）。  

在申请一页的内存后， Memcached 会将其切割成大小相等的数据块 （chunk）。

但是数据块并不是最小的单位， chunk 还会做等量切割，形成一系列的 item 。这也是上限的 item_size_max 前缀 item 的指向。

```c
all = x * page
page = n * chunk  
chunk = m * item
```

page 的大小限制了数据的上限，如果想要存储超过该上限的值，则必须在客户端切割字符串。

## Redis

Redis 是直接把大小限制放在存入字符串之前，直接用大小判断。与内存无直接联系。

## 内存是如何申请的？

## Memcached

do_slabs_newslab

## Redis

Redis 由于是直接使用 TCMalloc 和 Jemalloc ，所以其实是要了解这两者。

## TCMalloc


## Jemalloc

```
                                                                          divided into     region_size = 2 pages

                                                                          +--> page_0      +
                                                                          |                +--> region_0
                                                   divided into           +--> page_1      +
                                                                          |
                                                   +--> run_0 +---------> +--> ...          ...
                                                   |                      |
                                                   +--> run_1 <--+        +--> page_n-1    +
                                                   |             |        |                +--> region_y
                                 +--> chunk_0 +--> +--> run_2    |        +--> page_n      +
                                 |                 |             |
                                 |                 +--> run_3 <---------------------------------+
                                 |                 |             |                              |
                                 |                 +--> run_4    |                              |
                                 |                 |             |                              |
                                 |                 +--> run_5 <---------------------------------------+
           +--> chunks      +--> +--> ...          |             |                              |     |
           |                     |                 +--> ...      |                              |     |
           |                     |                 |             |                              |     |
           |                     |                 +--> run_n    |                              |     |
           |                     |                               |                              |     |
           |                     |                               |                              |     |
           |                     |                               |                              |     |
           |                     +--> chunk_x                    |                              |     |
           |                                       point to      |                              |     |
           |                                                     |                              |     |
           |                                       +---> run_1 +-+    +                         |     |
           |                                       |                  |                         |     |
           |                     +--> bin_0   +--> +---> ...          +--> region_size_3_runs   |     |
           |                     |                 |                  |                         |     |
           |                     |                 +---> run_p        +                         |     |
arena +--> +--> bins        +--> +--> ...                                                       |     |
           |                     |                                                              |     |
           |                     |                                                              |     |
           |                     +--> bin_z                                                     |     |
           |                                                                                    |     |
           |                     point to                                                       |     |
           |                                                                                    |     |
           |                     +--> run_3   +-------------------------------------------------+     |
           |                     |                                                                    |
           +--> avail_clean +--> +--> ...                                                             |
           |                     |                                                                    |
           |                     +--> run_t                                                           |
           |                                                                                          |
           |                     point to                                                             |
           |                                                                                          |
           |                     +--> run_5   +-------------------------------------------------------+
           |                     |
           +--> avail_dirty +--> +--> ...
                                 |
                                 +--> run_j
```


- arena  ：最高层次的内存管理单元，具有多个。每个 arena 管理多个内存单元 chunk ， arena 的其他信息是对 chunk 内部信息的汇总。
- chunk  ：内存单元。chunk 的空间被切割成多个大小相等的 run 。 
- run    ：每个 run 由一个或多个连续的页（page）组成。每个 run 的空间被切割成多个大小相等的 region 。这些 region 以页为单位。
- region ：用户申请到的内存。划分为三类：
    + 小（Small）：单个 region 小于 page。
    + 大（Large）：单个 region 大于 page 但小于 chunk 。
    + 巨大（Huge）：单个 region 大于 chunk ，不归 arena 管。
- bin    ：每个 bin 管理 arena 内所有 region 相同的 run 。

未完待续...

# 参考文档

Structures in jemalloc： https://medium.com/iskakaushik/eli5-jemalloc-e9bd412abd70

jemalloc 源码分析： https://youjiali1995.github.io/allocator/jemalloc/

ptmalloc,tcmalloc和jemalloc内存分配策略研究： https://cloud.tencent.com/developer/article/1173720

图解 TCMalloc： https://zhuanlan.zhihu.com/p/29216091

Memcache-内存模型-源码分析： https://www.jianshu.com/p/a824ae00d9bb

https://medium.com/iskakaushik/eli5-jemalloc-e9bd412abd70



