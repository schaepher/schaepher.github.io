---
title: lvs-ospf
date: 2020-02-06 11:18:40
updated: 2020-02-06 11:18:40
tags:
---

## VIP + Keepalived + LVS

LVS 使用 VIP + Keepalived 形成一主多备（通常是一主一备）的四层负载均衡（位于 OSI 第四层的传输层）。

VIP（Virtual IP，虚 IP)，用户访问域名时解析到的 IP 地址。用于屏蔽服务的架构。

Keepalived 装在所有 LVS 机器上。

在一主一备的 LVS 架构中，VIP 会设置到主的机器上。当主挂掉，备的 Keepalived 检测到该信息，让 VIP 漂移到备上面。  

问题是流量如何从主转移到备。在 LVS 前面还会有一台路由器，这台路由器接收到报文，并且根据 IP 获取到目标 LVS 的 MAC 地址，然后转发出去。

那么这就涉及到 ARP 了。当主还没挂掉的时候，路由器的 ARP 缓存中有 VIP 和主的 MAC 地址（虚拟的 MAC，不是实际上的 MAC）映射关系。  

> 顺便注：这个映射关系有 10-20 分钟的过期时间，但实际上用不到。

当 Keepalived 检测到主挂掉后，让备发一个携带备的虚拟 MAC 和 VIP 映射关系的 ARP 报文，路由器根据这个更新 ARP 缓存。

## VIP + OSPF + Keepalived + LVS

当 LVS 为一主一备的时候，备机处于空闲状态，资源利用率只有 50%。OSPF 则是将这 50% 利用起来。

需要在路由器上配置 VIP 可以转发到不同的 LVS 服务器上。
