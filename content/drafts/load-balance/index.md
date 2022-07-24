---
title: load-balance
date: 2019-08-26 16:07:47
updated: 2019-08-26 16:07:47
tags:
---

## 简介

- Keepalived 实现 VIP 漂移到正常的机器
- Nginx 用 stream 模块实现 TCP 层（四层）的负载均衡

Keepalived是一款高可用软件，它的功能主要包括两方面：
1）通过IP漂移，实现服务的高可用：服务器集群共享一个虚拟IP，同一时间只有一个服务器占有虚拟IP并对外提供服务，若该服务器不可用，则虚拟IP漂移至另一台服务器并对外提供服务；
2）对LVS应用服务层的应用服务器集群进行状态监控：若应用服务器不可用，则keepalived将其从集群中摘除，若应用服务器恢复，则keepalived将其重新加入集群中。

## 链接

https://blog.51cto.com/zephiruswt/1235852

https://www.jianshu.com/p/b6bc24a1201f

https://cloud.tencent.com/developer/article/1027563

https://www.cnblogs.com/kevingrace/p/8290452.html

https://www.chainnews.com/articles/868724777800.htm

https://zhuanlan.zhihu.com/p/34246665

https://www.cnblogs.com/liwei0526vip/p/6370103.html

https://my.oschina.net/leeypp1/blog/294807
