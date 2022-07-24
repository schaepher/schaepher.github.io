# Mariadb 配置



## 主从

> 官方文档  
> [https://mariadb.com/kb/en/library/setting-up-replication/](https://mariadb.com/kb/en/library/setting-up-replication/)

<!-- more -->

主从配置其实很简单。有以下几个步骤：

|步骤|Primary|Replica|
|---|---|---|
|1|开启 bin-log，设置服务器 ID，重启 Mariadb||
|2||设置服务器 ID，重启 Mariadb|
|3|创建 Replica 连接 Primary 所需的用户名密码，并授予 replication 权限||
|4|把内存脏页刷到磁盘并加上读锁，防止其他事务修改数据||
|5|查看 bin-log 文件名和 bin 位置，并记录||
|6||Replica 找 Primary 同步所有表及数据|
|7|释放读锁||
|8||创建到 Primary 的连接，并附上刚才记录的 bin-log 文件名和 bin 位置|
|9||启动 replication 服务|

启动后查看服务状态，如果报错，则停掉 replication 服务，并解决问题。然后重置 replication 链接，并从 4 开始。
