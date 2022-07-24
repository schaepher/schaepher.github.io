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


