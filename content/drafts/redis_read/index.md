---
title: 阅读 Redis 源码
date: 2019-05-27 12:33:00
updated: 2019-05-27 12:33:00
categories:
 - Redis
tag:
 - Source Code
---

# 服务端

首先找到服务端主入口，在 `server.c` 文件的 `int main(int argc, char **argv)`。 

首先定义了时间变量 tv，类型是结构体 timeval，来源于 `#include <sys/time.h>`。

`#ifdef` 是编译用的，如果满足条件就编译；否则不编译。

设置本地化参数。

设置 zmalloc （申请内存的工具，代替 malloc） 内存溢出的错误处理函数。

srand() 用来设置 rand() 产生随机数时的随机数种子

gettimeofday 给 tv 变量设置当前时间。

用 hashseed 设置 Dic Set 的 Seed

检查服务器启动参数是否开启了哨兵模式，并设置服务器的哨兵模式。

## 初始化服务器配置

设置时间到 server 结构体，缓存起来。

|变量|配置常量|配置|默认值|作用|
|:--|:--|:--|:--|:--|
|runid|无||||
|configfile|无||NULL|配置文件路径|
|executable|无||NULL|可执行文件路径|
|timezone|无|||设置时区。如果是 LINUX，则使用 time.h 的 timezone。否则使用 gettimeofday 获取时区。|
|hz|无|||设置 `serverCron()` 调用频率，单位 hz（hertz）。默认十次/秒。|
|dynamic_hz|CONFIG_DEFAULT_DYNAMIC_HZ|||客户端设置 hz 变量。|
|arch_bits|无|||CPU 位数|
|port|CONFIG_DEFAULT_SERVER_PORT|||设置端口|
|tcp_backlog|CONFIG_DEFAULT_TCP_BACKLOG||||
|bindaddr_count|无||0|绑定地址个数|
|unix_socket|无||NULL||
|unix_socketperm|CONFIG_DEFAULT_UNIX_SOCKET_PERM||0|权限|
|ipfd_count|无|||ip 文件描述符数量|
|sofd|无||-1|socket 文件描述符|
|protected_mode|CONFIG_DEFAULT_PROTECTED_MODE||1|根据配置设置保护模式，不接收外部连接|
|gopher_enabled|CONFIG_DEFAULT_GOPHER_ENABLED||0|不知道是啥|
|dbnum|CONFIG_DEFAULT_DBNUM||16|设置数据库个数，用于存储 key-value|
|verbosity|CONFIG_DEFAULT_VERBOSITY||LL_NOTICE|设置日志是否记录更多内容|
|maxidletime|CONFIG_DEFAULT_CLIENT_TIMEOUT||0|客户端最大空闲时间（超时时间）|
|tcpkeepalive|CONFIG_DEFAULT_TCP_KEEPALIVE||300|TCP 连接保活时间|
|active_expire_enabled|无||1||
|active_defrag_enabled|CONFIG_DEFAULT_ACTIVE_DEFRAG||0||
|active_defrag_ignore_bytes|CONFIG_DEFAULT_DEFRAG_IGNORE_BYTES||100<<20||
|active_defrag_threshold_lower|CONFIG_DEFAULT_DEFRAG_THRESHOLD_LOWER||10||
|active_defrag_threshold_upper|CONFIG_DEFAULT_DEFRAG_THRESHOLD_UPPER||100||
|active_defrag_cycle_min|CONFIG_DEFAULT_DEFRAG_CYCLE_MIN||5||
|active_defrag_cycle_max|CONFIG_DEFAULT_DEFRAG_CYCLE_MAX||75||
|active_defrag_max_scan_fields|CONFIG_DEFAULT_DEFRAG_MAX_SCAN_FIELDS||1000||
|proto_max_bulk_len|CONFIG_DEFAULT_PROTO_MAX_BULK_LEN||21211\*1024\*1024|协议桶最大长度|
|client_max_querybuf_len|PROTO_MAX_QUERYBUF_LEN||1024*1024*1024|客户端最大查询缓冲区长度|
|saveparams|无||NULL|为RDB保存点数组|
|loading|无||0|是否正在从磁盘加载数据|
|logfile|CONFIG_DEFAULT_LOGFILE||""|日志文件路径|
|syslog_enabled|CONFIG_DEFAULT_SYSLOG_ENABLED||0|使用系统日志|
|syslog_ident|CONFIG_DEFAULT_SYSLOG_IDENT||"redis"||
|syslog_facility|LOG_LOCAL0||16<<3||
|daemonize|CONFIG_DEFAULT_DAEMONIZE||0|是否放后台运行 Redis|
|supervised|无||0||
|supervised_mode|SUPERVISED_NONE||0||

AOF(Append Only File)，持久化方案之一。将每一个数据操作记录到文件中。体积过大时会对其进行重写。
> 官方文档： [https://redis.io/topics/persistence](https://redis.io/topics/persistence)

|变量|配置常量|配置|默认值|作用|
|:--|:--|:--|:--|:--|
|aof_state|AOF_(ON\|OFF\|WAIT_REWRITE)||0(AOF_OFF)|是否开启 AOF|
|aof_fsync|CONFIG_DEFAULT_AOF_FSYNC||2(AOF_FSYNC_EVERYSEC) 或者 0(AOF_FSYNC_NO) 或者 1(AOF_FSYNC_ALWAYS)||
|aof_no_fsync_on_rewrite|CONFIG_DEFAULT_AOF_NO_FSYNC_ON_REWRITE||||
|aof_rewrite_perc|AOF_REWRITE_PERC||||
|aof_rewrite_min_size|AOF_REWRITE_MIN_SIZE||||
|aof_rewrite_base_size|无||||
|aof_rewrite_scheduled|无||||
|aof_last_fsync|无||||
|aof_rewrite_time_last|无||||
|aof_rewrite_time_start|无||||
|aof_lastbgrewrite_status|||||
|aof_delayed_fsync|无||||
|aof_fd|无||||
|aof_selected_db|无||||
|aof_flush_postponed_start|无||||
|aof_rewrite_incremental_fsync|CONFIG_DEFAULT_AOF_REWRITE_INCREMENTAL_FSYNC||||
|aof_load_truncated|CONFIG_DEFAULT_AOF_LOAD_TRUNCATED||||
|aof_use_rdb_preamble|CONFIG_DEFAULT_AOF_USE_RDB_PREAMBLE||||
|aof_filename|CONFIG_DEFAULT_AOF_FILENAME||||
||||||
||||||
||||||

RDB(Redis Database)，持久化方案之一。将 Redis 在内存中的数据建立一份快照（Snapshot），存储到文件中。
> 官方文档： [https://redis.io/topics/persistence](https://redis.io/topics/persistence)

|变量|配置常量|配置|默认值|作用|
|:--|:--|:--|:--|:--|
|rdb_save_incremental_fsync|CONFIG_DEFAULT_RDB_SAVE_INCREMENTAL_FSYNC||1|增量存储数据。不是一次性把所有数据准备好再写入文件，而是每生成 32MB 数据，就写一次文件。|
|rdb_filename|CONFIG_DEFAULT_RDB_FILENAME||"dump.rdb"|RDB 保存的文件名|
|rdb_compression|CONFIG_DEFAULT_RDB_COMPRESSION||1|是否对数据启用压缩|
|rdb_checksum|CONFIG_DEFAULT_RDB_CHECKSUM||1|是否开启校验和|
||||||

