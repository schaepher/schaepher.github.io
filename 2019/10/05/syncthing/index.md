# Syncthing 通过网络同步文件



## 简介

Syncthing 是一款同步功能简洁但提供 P2P 功能的基于网络的多端（IOS除外）文件同步的开源软件。

<!-- more -->

## 要点

1. 基于网络同步。不是用来将本机的某个硬盘同步到另一个硬盘内。这种需求请使用 FreeFileSync 这种软件。
2. 自带支持两台无公网 IP 的设备进行同步。不需要自己申请公网机器，使用社区贡献的中继服务器即可。当然，也可以自己申请公网机器来做中继服务器。
3. 有 WEB UI 。自带 Basic Auth 认证方式，根据需要开启。
4. 有文件版本管理功能。
5. 自动同步。
6. 可以添加多个文件夹到同步列表，并控制对哪个设备共享该文件夹。
7. 可设置文件夹为仅发送、仅接收、发送和接收（默认）。
8. 没有列出文件对比的功能。

## 两台要同步的设备如何发现对方？

每个启用了 Syncthing 的设备都会得到一个 ID。Syncthing 在启动后会向默认的发现服务器（Syncthing Discovery Server）发送自己的信息。  

当添加远程设备时，把另一个设备的 ID 复制进去。此时 Syncthing 会向默认的发现服务器请求这个 ID 的设备信息。这样就可以连上了。

## 两台设备如何传输数据？

如果两台设备的其中一台拥有公网 IP，那么 Syncthing 会使用逆向链接的 P2P 通信方式传输数据。

如果两台设备都没有公网 IP，那么 Syncthing 会寻找一台 **社区贡献的** 拥有公网 IP 的中继服务器（Syncthing Relay Server），使用中继的 P2P 通信方式让两台设备通过中继服务器传输数据。  

中继服务器列表：  
[https://relays.syncthing.net/](https://relays.syncthing.net/)

## 发现服务器和中继服务器的问题

使用默认的发现服务器的问题是隐私。因为使用时会把设备和 ID 信息发送给发现服务器，这样这一台发现服务器的拥有者就可以得知这些信息。  

使用社区贡献的中继服务器的问题除了隐私外，还有速度的问题。

## 自己搭建发现服务器和中继服务器

参考这篇博客：  
[https://segmentfault.com/a/1190000017273107](https://segmentfault.com/a/1190000017273107)

## P2P 通信方式

1. 中继（Relaying）  
   两台机器都没有公网 IP 时，使用该方式通过公网的中继服务器传输数据。传输速度受中继服务器的传输速度影响。
2. 逆向链接（Connection reversal）  
   其中一台机器拥有公网 IP 时，内网机器发起连接到公网机器。传输速度受两台连接的机器的带宽影响。
3. UDP 打洞（UDP hole punching）  
   两台机器都没有公网 IP 时，使用该方式通过公网的服务器建立连接。传输速度受两台连接的机器的带宽影响。  
   要求两台内网机器都处于锥形 NAT 下。如果是对称 NAT，则无法建立连接。

## 能否让 Syncthing 使用 UDP 打洞方式连接

试试 FRP ？

## 参考链接

> P2P通信原理与实现(C++)：  
> [https://www.cnblogs.com/pannengzhi/p/4800526.html](https://www.cnblogs.com/pannengzhi/p/4800526.html)

> CONE NAT 和 Symmetric NAT：  
> [https://www.cnblogs.com/dyufei/p/7466924.html](https://www.cnblogs.com/dyufei/p/7466924.html)

> Syncthing - 文件同步工具:  
> [https://zhuanlan.zhihu.com/p/69267020](https://zhuanlan.zhihu.com/p/69267020)
