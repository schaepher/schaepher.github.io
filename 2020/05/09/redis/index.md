# Redis


熟悉 Redis 要包含以下知识点：  

- Redis 数据类型及使用场景
- 单线程模型
- 两种持久化方式
- 与 Memcached 的区别
- I/O 多路复用
- Redis 主从同步
- Redis 集群（Sentinel）
- 性能 QPS

<!-- more -->

高级一点的是：  

- Redis 各种数据类型的底层实现
- Redis 实现分布式锁的两种方式（RedLock/多独立集群）

## 数据类型

- 字符串
- 列表
- 哈希表
- 集合（无序）
- 有序集合  
- Bitmaps（不常用）
- HyperLogLogs（不常用）

#### 场景

- 字符串  
    与 Memcached 用法相似，缓存的基本功能
- 列表  
    消息队列  
    异步操作  
- 哈希表  
    存储对象属性  
- 集合  
    获取唯一值的场景，例如访问页面的所有 IP
- 有序集合  
    排序的场景。获取前 10 个访问量最高的页面；延迟队列

## Redis 和 Memcached 的区别是什么？

Redis： [https://github.com/antirez/redis](https://github.com/antirez/redis)  

Memcached： [https://github.com/memcached/memcached](https://github.com/memcached/memcached)

|功能|Redis|Memcached|
|:--|:--|:--|
|数据结构|字符串(string)、列表(list)、哈希(hash)、集合(set)、有序集合(zset)|只有字符串|
|持久化|支持|不支持|
|字符串键最大上限|512MB|250B|
|字符串值默认上限|512MB|1MB|
|内存管理器|Jemalloc（默认）、TCMalloc|SLAB Allocator|
|主从同步|支持|不支持|
|集群 key 所在服务器|服务端计算|客户端计算|
|线程|单线程（CPU非瓶颈）|多线程（多核/加锁）|
|单机 QPS|5~6万|几十万|

## Redis 的底层数据结构

我们可以很容易了解到以下信息：  

|类型|底层数据结构|
|:--|:--|
|字符串|SDS|
|列表|双向链表|
|哈希表|哈希表|
|集合|哈希表|
|有序集合|跳跃表（Skip Table）|

那么问题来了，这只是数据类型的底层数据结构。往上一层看，Redis 如何根据我们给出的 key 找到这些数据类型对应的对象？

例如：  

```bash
> redis-cli put key value
> redis-cli lpush list item
```

Redis 是如何存储这些 key 和 value 的对应关系，以及 list 和 item 的对应关系？

如果由我们自己设计，肯定会选择哈希表。而 Redis 也确实是这么实现的。

`server.h`

```c
typedef struct redisDb {
    dict *dict;                 /* The keyspace for this DB */
    dict *expires;              /* Timeout of keys with a timeout set */
    dict *blocking_keys;        /* Keys with clients waiting for data (BLPOP)*/
    dict *ready_keys;           /* Blocked keys that received a PUSH */
    dict *watched_keys;         /* WATCHED keys for MULTI/EXEC CAS */
    int id;                     /* Database ID */
    long long avg_ttl;          /* Average TTL, just for stats */
    unsigned long expires_cursor; /* Cursor of the active expire cycle. */
    list *defrag_later;         /* List of key names to attempt to defrag one by one, gradually. */
} redisDb;
```

这也是为什么对同一个 key 设置不同类型的数据的时候， Redis 会报错：  

```
(error) WRONGTYPE Operation against a key holding the wrong kind of value
```

#### 集合  

如果要列举一个集合实现方式的列表，可以直接到 JAVA 去找。  

- HashSet： 使用 Hash Table 的 key 存储元素
- LinkedHashSet： HashSet + LinkedList
- TreeSet： 红黑树

Redis 采用 HashSet 的方式实现集合， Hash Table 的 value 固定为 null。

#### 有序集合  

使用跳跃表（skip tables）实现。比红黑树实现简单。Redis 的跳跃表的时间复杂度为 O(log(N)) 。

说到跳跃表，要先说指数单链表。其每 2 的次方位置都添加一个 Level 节点。

跳跃表与指数单链表的不同之处在于 Level 节点数量与指数单链表一致，但位置随机。


