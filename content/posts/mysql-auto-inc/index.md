---
title: MySQL 自增主键
date: 2020-04-28 21:16:00
updated: 2020-04-28 22:45:00
tags:
- MySQL
- 索引
- 主键
---

原文：
> MySQL 自增主键  
> [https://schaepher.github.io/2020/04/28/mysql-auto-inc/](https://schaepher.github.io/2020/04/28/mysql-auto-inc/)

以下仅考虑 InnoDB 存储引擎。

自增主键有两个性质需要考虑：  

- 单调性  
    每次插入一条数据，其 ID 都是比上一条插入的数据的 ID 大，就算上一条数据被删除。
- 连续性  
    插入成功时，其数据的 ID 和前一次插入成功时数据的 ID 相邻。

<!-- more -->

## 自增主键的单调性

为何会有单调性的问题？

这主要跟自增主键最大值的获取方式，以及存放位置有关系。

如果最大值是通过计算获取的，并且在某些情况下需要重新获取时，会因为最新的数据被删除而减小。

### 自增主键最大值怎么取的？存放到哪里？

MySQL 5.7 及之前的版本，自增主键最大值会在启动（重启）后从数据库中取出放到内存：  

```sql
SELECT MAX(ai_col) FROM table_name FOR UPDATE; 
```

这样获取是通过计算的，并且由于存放在内存而容易丢失。

如果删除最新一条数据（假设 ID 为 10），因故障或者其他必要重启后再插入一条数据时会使用之前的 ID （即 ID 为 10）。

问题在于如果有其他表依赖了该 ID，则其他表的数据关联到的数据就符合要求了。除非设置了外键。

比如我要向最大一个 ID 的账号充了 100 万。但是在充值之前，该账号被删除，然后服务器故障重启，重启后有人新注册了一个账号。结果我的 100 万充到了他的新账号上。注册新账号的人以为是新手福利，笑嘻嘻。

### 如何解决单调性的问题？

从 MySQL 8.0 开始，自增主键最大值会在每次修改后写入到 redo log，并且在每个检查点写入引擎私有的系统表。  

- 如果是正常重启，则读取系统表里的值。
- 如果是故障重启，则先读取系统表里的值放到内存。接着扫描 redo log 里存储的值。如果扫描到的值大于内存的值，则将该值覆盖到内存。

但由于数据库可能在 redo log 刷入磁盘前就故障了，所以可能会用到之前申请的 ID。  

注：如果 redo log 都没刷入，就更不用说将数据插入数据表了。  

> InnoDB AUTO_INCREMENT Counter Initialization  
> [https://dev.mysql.com/doc/refman/8.0/en/innodb-auto-increment-handling.html#innodb-auto-increment-initialization](https://dev.mysql.com/doc/refman/8.0/en/innodb-auto-increment-handling.html#innodb-auto-increment-initialization)

## 自增主键插入时的连续性

> 这里不考虑由于删除导致的连续性问题

为何会有连续性问题？

这主要是跟插入事务回滚有关系。

对于两个插入事务，事务 A 先执行插入语句，之后事务 B 执行插入语句。在这之后，事务 A 回滚，导致 A 执行插入语句时占用的 ID 被抛弃。

之所以事务 A 没提交的情况下，事务 B 就能执行插入语句，跟 InnoDB 的自增长锁（AUTO-INC Locking）相关。该锁是一种特殊的表锁（table-level lock），但会在插入语句执行后立即释放，不会等到事务结束。

### 如何解决连续性问题？

使用最高隔离级别 SERIALIZABLE （串行）。

由于性能上的考虑，通常不这样做。

## 多事务批量插入的连续性

事务 A 和事务 B 都在执行 **不确定数量** 的批量插入（INSERT ... SELECT）：

- 保证事务 A 的数据的 ID 连续： innodb_autoinc_lock_mode = 0 （AUTO-INC Locking）  
    必须等待语句执行结束才释放锁。
- 保证事务 A 的数据的 ID 连续： innodb_autoinc_lock_mode = 1 （AUTO-INC Locking）  
    和上面的区别在于，当执行 **确定数量** 的批量插入时，使用轻量级互斥量（mutex）而不是特殊表锁（AUTO-INC Locking），从而提前向内存的计数器申请相应数量的 ID。之后立即释放，不用等语句执行结束。  
    会因为回滚而使得全局 ID 不连续。
- 不保证事务 A 的数据的 ID 连续： innodb_autoinc_lock_mode = 2 （mutex）

三种插入定义：  

- 简单插入  
    能够提前知道插入的行数
- 批量插入  
    不能提前知道插入的行数
- 混合插入  
    批量插入中的一部分的 ID 是指定的（非 0 且非 NULL），另一部分未指定，使用数据库生成的自增 ID。

## 其他

如果主动指定 ID 为 0 或者 NULL 插入，则会使用数据库生成的自增 ID。

## 参考文档

> 为什么 MySQL 的自增主键不单调也不连续  
> [https://database.51cto.com/art/202004/614923.htm](https://database.51cto.com/art/202004/614923.htm)  
> 《MySQL技术内幕——InnoDB存储引擎》 第 6 章：锁  