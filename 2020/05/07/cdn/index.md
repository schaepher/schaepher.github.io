# CDN


整体结构：  

```
     +---------+
     |         +----------+
     | Source  |          |
     |         +<------+  |
     +--+--+---+       |  |
 Back   ^  |           |  |
 To     |  |           |  |
 The    |  |           |  |
 Source |  v           |  |
     +--+--+---+       |  |
     |         |       |  |
     | Static  |       |  |
     | Relay   |       |  |
     | Cluster |       |  |
     |         |       |  |
     +--+--+---+       |  |
   ...  ^  |           |  |
   One  |  |           |  |
   Or   |  |           |  |
   More |  v           |  v
     +--+--+---+    +--+--+---+
     |         |    |         |
     | Static  |    | Dynamic |
     | Relay   |    | Relay   |
     | Cluster |    | Cluster |
     |         |    |         |
     +--+--+---+    +--+--+---+
        ^  |           ^  |
        |  |           |  |
        |  v           |  v
     +--+--+-----------+--+---+
     |                        |
     |      Edge Cluster      |
     |                        |
     +--+--+-----------+--+---+
        ^  |           ^  |
Request |  |   Request |  |
Static  |  |   Dynamic |  |
Source  |  v   Source  |  v
     +--+--+-----------+--+---+
     |                        |
     |       User Agent       |
     |                        |
     +------------------------+
```

类似于 CPU 的多级缓存。把 Edge Cluster 当成一级缓存，把 Source 当成内存。寄存器呢？ User Agent 自身的缓存（如浏览器缓存）在这个架构上相当于寄存器。

Static Relay Cluster 的磁盘容量比 Edge Cluster 大。就像 CPU 的 L2 缓存比 L1 缓存大。  

Dynamic Relay Cluster 用于 User Agent 和 Source 运营商不一致时，在机器内做转换，提高速度和减少运营商转换的费用。该 Cluster 里的每台机器都有两个或者多个运营商的 IP。

源服务器是 CDN 客户自己搭建的，也可能是客户使用 CDN 服务商的云服务器（主要用于静态资源存储）。

预热（主动缓存）：在资源提供给用户使用之前，先自己请求一次资源，让这些数据预先加载到 Edge Cluster 。

集群架构：  

```
                     xxxx.com(VIP)
                               +
         +---------------------+
         v
  +------+---------------------------------------+
  |                        Layer 4 Load Balance  |
  |     VIP                                      |
  |  +--------+ +------------------> +--------+  |
  |  |        |                      |        |  |
  |  |  LVS   | Heartbeat/Keepalived |  LVS   |  |
  |  | Master |                      | Backup |  |
  |  |        | <------------------+ |        |  |
  |  +--------+                      +--------+  |
  |                                              |
  +----+------------+-------------+-----------+--+
       |            |             |           |
       |            |             |           |
       |            |             |           |
       v            v             v           v
+------+------------+-------------+-----------+-----+
|                             Layer 7 Load Balance  |
|                                                   |
|                                                   |
|  +---------+   +---------+          +---------+   |
|  |         |   |         |          |         |   |
|  | HAProxy |   | HAProxy |  ......  | HAProxy |   |
|  |         |   |         |          |         |   |
|  +---------+   +---------+          +---------+   |
|                                                   |
+------+------------+-------------+-----------+-----+
       |            |             |           |
       |            |             |           |
       |            |             |           |
       v            v             v           v
+------+------------+-------------+-----------+-----+
|                                                   |
|                                                   |
|  +---------+   +---------+          +---------+   |
|  |         |   |         |          |         |   |
|  | Real    |   | Real    |          | Real    |   |
|  | Server  |   | Server  |  ......  | Server  |   |
|  |         |   |         |          |         |   |
|  +---------+   +---------+          +---------+   |
|                                                   |
+---------------------------------------------------+
```

LVS 可以使用 ospfd 让每一台 LVS 服务器都提供服务，充分利用资源。此时 LVS 的机器数量上限仅受三层交换机设备的影响。

## 用户访问过程  

可以通过 dig 查看相关信息。  

```
[root@hostname]# dig example.com

; <<>> DiG 9.11.4-P2-RedHat-9.11.4-16.P2.el7_8.2 <<>> example.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41101
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;example.com.			IN	A

;; ANSWER SECTION:
example.com.		599	IN	CNAME	example.com.xxcdn.com.
example.com.xxcdn.com.	59	IN	A	xxx.xx.xxx.xxx
example.com.xxcdn.com.	59	IN	A	xxx.xx.xxx.xx

;; Query time: 203 msec
;; SERVER: xxx.xxx.xxx.xxx#53(xxx.xxx.xxx.xxx)
;; WHEN: Fri May 08 14:04:47 UTC 2020
;; MSG SIZE  rcvd: 101
```

使用 CDN 的域名会将其主域名在 dns 上配置 CNAME，指向 CDN 厂商的域名，该域名称为一级域名。  

一级域名会指向 CDN 厂商的 DNS 服务器。DNS 服务器会根据用户购买的服务（套餐），将该域名 CNAME 到另一个域名（二级域名，Map）。即根据套餐配置一个对应的域名。  

> 这样在客户变更套餐时，可以创建另一个域名，分配好资源，然后 DNS 服务器对一级域名的解析切换到到这个新域名。  

获取二级域名后，会根据情况找到发起请求的用户所在的资源区域（因为有些 DNS 服务器不支持获取请求地的信息），称为 view。每个 view 都会配置多个用于提供服务的机器集群（覆盖）。  

> 资源区域所包括的集群未必是同一个地理区域的集群。  
> 例如福建的资源区域可能包含浙江地区的集群。一般会选择地理区域近的集群。

每个集群都有一个虚 IP，用于高可用以及屏蔽集群的架构信息。   

例如上面解析到的 xxx.xx.xxx.xxx 和 xxx.xx.xxx.xx 都是虚 IP，代表着两个集群。

由于二级域名会根据情况选取不同资源区域的集群提供服务，因此在不同地区 dig 出来的结果不一致。

每个 view 拥有多个 DNS Host Cluster（DHC），每个二级域名会唯一对应一个资源区域里的 DHC。二级域名会使用一个 DHC 里的部分集群。

不同客户的二级域名可能指向同一个集群。机器资源的利用率。

## 服务角度  

应用服务是相同服务特性的跨节点的多个集群的集合。这些集群的机器拥有相近或相同的硬件配置。  

应用服务组是由边缘集群、静态中转集群、动态中转集群的应用服务组成的集合。  

应用服务和应用服务组是多对多的关系。  

应用服务的粒度太小，配置麻烦；应用服务组的粒度太大，配置失误的影响很大。所以在两者之间加了一个 DHC 的逻辑概念。  

DHC 一般按区域划分，如华南地区某个应用服务组底下的集群划分为一个 DHC。虽然该应用服务在华北地区也可能有集群。

一个 DHC 有多个列表，每个列表代表不同区块。例如南非、中国大陆...   

同一个列表里面通常表示一个区块的运营商在各个更小粒度地区的集群。例如 DHC 某个列表包含了中国大陆的某些省份的集群。通常一个省份对应一个集群。

## 参考  

> L1，L2，L3 Cache究竟在哪里？   
> [https://zhuanlan.zhihu.com/p/31422201](https://zhuanlan.zhihu.com/p/31422201)  

