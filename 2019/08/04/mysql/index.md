# MySQL 笔记


### 字符串转整形排序

法一：CAST  

```
SELECT val FROM test ORDER BY CAST(val AS unsigned);
```

MySQL 5.6 不支持直接 cast 到 integer，所以使用 signed 或者 unsinged。

法二：加减法

```
SELECT val FROM test ORDER BY 0 + val;
```

```
SELECT val FROM test ORDER BY 0 - val;
```

```
SELECT val FROM test ORDER BY -val;
```
同 0 - val

```
SELECT val FROM test ORDER BY --val;
```
同 0 + val

# 临时表

临时表使用 MEMORY 引擎。用 Hash 作为主键索引方式。行长度为定长。

group by 的后面作为临时表的 key。文档说的 100% dynamic hash 的 100% 指的是所有行都是一条记录没有链表么？还是相同的 key 会放到同一个桶里面？


