# docker-swarm


## Docker 网络

查看当前主机 Docker Daemon 已创建的网络： `docker network ls`。

Docker 网络驱动（driver）主要由五种： bridge （默认）、 host 、 overlay 、 macvlan 、 none 。

1. bridge    
   桥接网络。加入同一个 bridge 的容器可以互相通信。用于同一个 Docker Daemon 内容器通信。

2. host  
   使用主机的网络。对使用 host 网络的容器不做网络隔离，把容器暴露在公网中。

3. overlay  
   跨主机通信使用的网络。连接多个 Docker Daemon ，多用于 Docker Swarm 集群。  
   Swarm 会默认创建一个 ingress 的 overlay。

4. macvlan  
   MAC 级别网络。会给容器分配 MAC 地址，使其在网络中看起来像是一个独立的物理设备。

5. none  
   隔绝网络。当使用自定义网络驱动时，使用 none。

> Network - Docker Document:  
> [https://docs.docker.com/network/](https://docs.docker.com/network/)  
> 浅聊几种主流 Docker 网络的实现原理 - InfoQ:  
> [https://www.infoq.cn/article/9vfPPfZPrXLM4ssLlxSR](https://www.infoq.cn/article/9vfPPfZPrXLM4ssLlxSR)
> MPLS L3 VPN - Zhihu:  
> [https://zhuanlan.zhihu.com/p/27539826](https://zhuanlan.zhihu.com/p/27539826)

需要注意的问题：  
使用 bridge 和 overlay 网络时，需要注意分配的网段。  
例如在内网中，如果使用了 192.168.1.0/24 这个网段，就不能让这两个 driver 使用这个网段。否则会出现容器请求了某个 IP，但被 Docker 内部网络拦截而导致无法请求到外部机器的问题。

## 集群基础

#### 节点

|节点类型|说明||
|:--|:--|:--|
|Worker|工作节点。只用于提供服务||
|Leader|主控节点。用于管理其他节点||
|Manager|管理节点。一个 Leader 节点必须是一个 Manager 节点。Leader 节点由所有 Manager 选举产生。管理节点也可以作为 Worker||

#### Leader 节点选举

当 Leader 节点故障时，Manager 节点会举行一次投票，在存活的 Manager 节点中选举出一个新的 Leader。

（票数）过半原则：Leader 选举时，投票数要超过 Manager 总数（包括故障的 Manager）的一半才能成功。  

如果没有过半的节点参与投票，那么集群会变为不可用。

因此如果总共有 3 个 Manager 节点，挂掉一个节点没事。挂掉两个节点时，集群变为不可用。

正是因为这个过半原则，我们通常使用奇数个 Manager 节点。如果用偶数个节点会是什么情况呢？  

假设有 4 个 Manager 节点，挂掉一个节点没事。挂掉两各节点时，剩余的两个节点无论怎么投票，都不会超过总 Manager 数量的一半。集群也会变得不可用。

> [https://juejin.im/post/5cb6d5a0e51d456e51614a88](https://juejin.im/post/5cb6d5a0e51d456e51614a88)

## 



https://zhoujinl.github.io/2018/10/19/docker-swarm-manager-ha/

https://severalnines.com/database-blog/introduction-docker-swarm-mode-and-multi-host-networking


构建请求变更域名解析的镜像，设置为只在 manager 开启。

Portainer Agent 在部署后，应通过 Portainer 应用连接 Agent 地址。

docker login -u username -p password https://registry.schaepher.com

docker build --tag=itask_test . && docker tag itask_test registry.schaepher.com/task/itask_test && docker push registry.schaepher.com/task/itask_test

supervisord priority 默认 999 ，越低越早启动
http://supervisord.org/configuration.html


集群同步数据及主备切换：  
https://zhuanlan.zhihu.com/p/46675331

MySQL 主备切换：

https://www.cnblogs.com/gomysql/p/3663146.html

https://www.jianshu.com/p/41b700ebf1c1
