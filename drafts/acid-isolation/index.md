# 事务隔离级别


原文：  
> 事务隔离级别  
> [https://schaepher.github.io/2020/04/24/acid-isolation/](https://schaepher.github.io/2020/04/24/acid-isolation/)

事务隔离级别有四种。它们的区别在于一个修改数据的事务在提交前和提交后，另一个进行中的事务读取到的数据是修改前还是修改后的数据。

- READ-UNCOMMITED = 读-未提交  
- READ-COMMITED = 读-已提交
- REPEATABLE-READ = 可重复-读 （InnoDB）
- SERIALIZABLE = 串行

<!-- more -->

以下假设事务B都处于进行中。

事务A进行中：

|隔离级别|事务B|问题|
|:--|:--|:--|
|READ-UNCOMMITED|修改后|脏读（事务回滚）|
|READ-COMMITED|修改前||
|REPEATABLE-READ|修改前||
|SERIALIZABLE|阻塞|并发能力低|

事务A提交后：

|隔离级别|事务B|问题|
|:--|:--|:--|
|READ-UNCOMMITED|修改后||
|READ-COMMITED|修改后|不可重复读（update/delete）|
|REPEATABLE-READ|修改前（快照数据 undo段）|幻读（insert）可通过 Next-Key Lock 解决|
|SERIALIZABLE|修改后||

## 锁

修改数据会加 X 锁。  

查询数据需要使用以下方式：  

- `SELECT ... FOR UPDATE` 加 X 锁
- `SELECT ... LOCK IN SHARE MODE` 加 S 锁

锁会在事务结束后释放。

由于每条语句都是单独一个事务，且数据库使用 Auto Commit，结果是在执行语句后会自动提交事务。

所以如果不主动开启事务或者关闭 Auto Commit，就算执行时加了锁，在 SELECT 事务结束后会立即释放。无法达到目的。

关闭自动提交：

```mysql
SET AUTOCOMMIT=0;
```

开启事务（两者等效）：  

```mysql
BEGIN;
```

```mysql
START TRANSACTION;
```

两种开启事务的方式都使用 `COMMIT;` 来提交事务。

