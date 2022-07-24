---
title: 高可用的实现（Keepalived + 虚 IP）
date: 2020-05-07 08:19:00
updated: 2020-05-07 09:08:00
tags: 
- Keepalived
- VIPA
- 高可用
---

为了避免服务单点，也为了负载均衡，我们会加一层 Nginx 层。这个 Nginx 层要有多于一台机器，不然它自身也成为一个单点。

最初加 Nginx 层会变成这样：  

```
                   schaepher.com
                       +
                       |
               +-------+
               |
               v
           +---+---+          +-------+
           |       |          |       |
           | Nginx |          | Nginx |
           |       |          |       |
           +--+----+          +---+---+
              |                   |
    +---------+---+-------------+-+-----------+
    |             |             |             |
    v             v             v             v
+---+----+    +---+----+    +---+----+    +---+----+
|        |    |        |    |        |    |        |
| Real   |    | Real   |    | Real   |    | Real   |
| Server |    | Server |    | Server |    | Server |
|        |    |        |    |        |    |        |
+--------+    +--------+    +--------+    +--------+
```

<!-- more -->

如果有一台 Real Server 发生故障，则 Nginx 就不会转发到故障的机器，保证服务正常进行。  

但是如果主 Nginx 故障了呢？

## 故障切换的五种方式

- 客户端自己配置多个 Nginx IP，故障时自己切换。  
    
    优点：  
    + 后端不需要做调整  

    缺点：  
    + 客户端要自己维护 IP 列表。  
    + 客户端要实现一套应对故障的逻辑。  
    + 不能用于用户和服务之间，只能用于服务与服务之间。  

- 单一服务的情况下，把另一台 Nginx 服务器的 IP 发给用户，让用户访问这个 IP。  

    优点：  
    + 简单

    缺点：  
    + 只有内部系统用户才可能接受这种做法。面向外部用户的时候，外部用户不会接受。  

- 运维人员手动修改 DNS 解析，将域名解析到另一台 Nginx 服务器。或者程序定期检测，发现有问题就自动发起修改 DNS 解析的请求。  

    解决了什么问题？  
    + 用户需要手动修改 hosts 或者需要切换 URL 的问题。

    没有解决什么问题？  
    + 在 DNS 解析生效之前，服务完全不可用。  
    + 客户端会缓存 DNS 解析，也要等客户端缓存过期。

- 将域名解析到所有 Nginx 服务器。程序定期做检测，当发现有问题的时候发起请求，让 DNS 将故障的 IP 移除掉。   
    > DNSPod 自带这个功能  

    解决了什么问题？  
    + 在 DNS 解析生效之前，服务完全不可用的问题。 

    没有解决什么问题？    
    + 仍然有部分用户无法访问服务。  

- 使用虚 IP（Virtual IP Address，以下称为 VIPA）。域名固定解析到这个 IP，当 VIPA 所在服务器故障时，让 VIPA 自动漂移到另一台服务器。  
    
    解决了什么问题？  
    + 不需要修改 DNS 解析，秒级别的生效延迟。  
    + 用户无感知。
    
    带来了什么问题？  
    + 多了一个故障点，即使得 VIPA 自动漂移的那个程序，如 Keepalived。  
    + 需要额外申请一个 IP 作为 VIPA 。  
    + 涉及存储的时候，由于切换速度很快，可能会导致数据不一致。  

## VIP 是什么

全称为 VIPA（Virtual IP Address），虚拟 IP 地址。

通常一个 IP 只能绑定在某台机器的一个网卡上。一旦这台机器故障，根据 IP 找到这台机器的请求就会得不到响应。

```
正常
     schaepher.com
     192.168.1.101
           +
           |
           |
           |
           v

    +---------------+        +---------------+
    |               |        |               |
    | 192.168.1.101 |        | 192.168.1.102 |
    |               |        |               |
    +---------------+        +---------------+

故障
     schaepher.com
     192.168.1.101
           +
           +
             +-+ 不通
           |
           v
          故障
    +---------------+        +---------------+
    |               |        |               |
    | 192.168.1.101 |        | 192.168.1.102 |
    |               |        |               |
    +---------------+        +---------------+
```

而 VIPA 虽然最终也会配置在一台机器上，但一旦这台机器故障，备用机器就会把这个 IP 抢过去配置到网卡上（VIPA 漂移到备机）。这样可以在 IP 不变的情况下，让请求转移到正常的机器，减少服务故障时间。

```
正常
     schaepher.com
     192.168.1.100(VIPA)
           +
           |
           |
           |
           v

    +---------------+        +---------------+
    | 192.168.1.100 |        |               |
    | 192.168.1.101 |        | 192.168.1.102 |
    |               |        |               |
    +---------------+        +---------------+

故障
     schaepher.com
     192.168.1.100(VIPA)
           +
           |
           +-------------------------+
                                     |
                                     v
          故障
    +---------------+        +---------------+
    |               |        | 192.168.1.100 |
    | 192.168.1.101 |        | 192.168.1.102 |
    |               |        |               |
    +---------------+        +---------------+
```

而 Keepalive 则是实现 VIPA 漂移的一种工具。  

> 另一种是比较复杂的 Heartbeat。

## Keepalived

Keepalived 实现 VIPA 漂移的基础是 VRRP 协议。

VRRP 最早用于路由器，将多台路由器设备虚拟成一台路由器。每台设备都有一个角色。角色有两种 Master 和 Backup。Master 会持有虚 IP。每台设备都有一个权重，权重最高的正常设备会被选举为 Master。  

现在 Keepalived 实现了 VRRP 协议，使得可以将其用在其他设备上。

将 Keepalived 安装在一组设备上，它们之间会互相通信来检测状态。如果发现 Master 超过一定时间没有反应，则重新选举 Master。  

Master 可能直接故障没有反应，也可能只是服务出现问题。如果是后一种情况，需要主动关闭 Keepalived 进程。

以下展示配置文件。

|IP|所属|角色|
|:--|:--|:--|
|192.168.1.100|Master||
|192.168.1.101|主机 A|Master|
|192.168.1.102|主机 B|Backup|

#### 192.168.1.101 - 主机 A - Master

`/etc/keepalived/keepalived.conf`

```
! Configuration File for keepalived

global_defs {
    script_user root
    router_id LVS_DEVEL
    vrrp_skip_check_adv_addr
    vrrp_strict     # 严格模式使得无法使用 unicast_peer 配置，好处是无需指定其他机器的 IP
    vrrp_garp_interval 0
    vrrp_gna_interval 0
}

vrrp_script chk_http_port {
    script "/etc/keepalived/chk_nginx.sh"   # 检测当前机器的服务是否故障，如果故障则关闭 keepalived
    interval 2
    weight -5
    fall 2
    rise 1
}

vrrp_instance VI_1 {
    state MASTER    # 主备配置不一致
    interface eth0
    virtual_router_id 51
    priority 100
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass aaaaaaa   # 主备该配置必须一样
    }
    virtual_ipaddress {
        192.168.1.100
    }
    track_script {
        chk_http_port   # 在 vrrp_script 定义的名字
    }
    notify_master "/etc/keepalived/notify.sh 192.168.1.100 master"  # 当这台机器成为 Master 时发送通知
    notify_backup "/etc/keepalived/notify.sh 192.168.1.100 backup"
    notify_fault  "/etc/keepalived/notify.sh 192.168.1.100 fault"
}
```

#### 192.168.1.102 - 主机 B - Backup

只需改两个配置的值

`/etc/keepalived/keepalived.conf`

```
! Configuration File for keepalived

global_defs {
    script_user root
    router_id LVS_DEVEL
    vrrp_skip_check_adv_addr
    vrrp_strict
    vrrp_garp_interval 0
    vrrp_gna_interval 0
}

vrrp_script chk_http_port {
    script "/etc/keepalived/chk_nginx.sh"
    interval 2
    weight -5
    fall 2
    rise 1
}

vrrp_instance VI_1 {
    state BACKUP    # 主备配置不一致
    interface eth0
    virtual_router_id 51
    priority 90     # 备机权重比主机低
    advert_int 1
    nopreempt       # 防止争抢 VIPA，只有 state 设置为 BACKUP 才能使用该选项
    authentication {
        auth_type PASS
        auth_pass aaaaaaa
    }
    virtual_ipaddress {
        192.168.1.100
    }
    track_script {
        chk_http_port
    }
    notify_master "/etc/keepalived/notify.sh 192.168.1.100 master"  # 当这台机器成为 Master 时发送通知
    notify_backup "/etc/keepalived/notify.sh 192.168.1.100 backup"
    notify_fault  "/etc/keepalived/notify.sh 192.168.1.100 fault"
}
```

#### /etc/keepalived/chk_nginx.sh

```bash
#!/bin/bash
if [[ -z "$(ps aux | grep "nginx: master process" | grep -v grep)" ]]; then
    systemctl restart nginx # 尝试重启 nginx  
    sleep 5  

    if [[ -z "$(ps aux | grep "nginx: master process" | grep -v grep)" ]]; then
        # 启动失败则关闭 keepalived，触发 VIPA 漂移
        systemctl stop keepalived
    fi
fi
```

#### /etc/keepalived/notify.sh

```bash
#!/bin/bash

# contact=xxx.schaepher.com

notify() {
    vip=$1
    role=$2
    mailSubject="$(hostname) to be ${role}: ${vip} floating"
    mailBody="$(date '+%F %H:%M:%S'): vrrp transition, $(hostname changed to be ${role})"
    # echo ${mailBody} | mail -s "${mailSubject}" "${contact}"
    echo ${mailSubject} >> /var/log/keepalived.mail
    echo ${mailBody} >> /var/log/keepalived.mail
    echo "" >> /var/log/keepalived.mail
}

notify $1 $2
```

## 扩展

- 提高利用率
    由于一个 VIPA 只能配置在一台机器上，如果共有两台机器，则浪费了 50% 的资源。  
    如果要提高资源的利用率，可以再申请一个 VIPA。把备机配置为 Master，把主机配置为 Backup。

- VIPA 争抢  
    由于 nopreempt 只能配置在 BACKUP 上，如果 state 为 MASTER 的机器故障并恢复，则会把 VIPA 抢过去。  
    整个过程是：  
    1. 主机 A 故障
    2. VIPA 漂移到主机 B
    3. 主机 A 恢复
    4. VIPA 漂移到主机 A  

    这样就会导致第四步多漂移了一次。而漂移可能会对服务有很短暂的影响。如果希望主机 A 恢复后，仍然让主机 B 持有 VIPA，则要在主机的 Keepalived 启动之前修改配置中的 state，改为 BACKUP。

- 避免丢包  
    在 VIPA 漂移到备机之间，短暂的时间内数据包仍然会发送到主机。如果主机能够连上，则可以使用防火墙将数据包转发到备机。然后停止 Keepalived 。  

    ```
    iptables -F
    iptables -t nat -I PREROUTING -i eth0 -j DNAT --to-destination 192.168.1.102
    iptables -t nat -I POSTROUTING -o eth0 -j MASQUERADE
    ```

- 数据库的问题  
    数据库如果使用双主，在 VIPA 切换的时候，数据可能未同步完成，可能会造成自增 ID 冲突。  
    可以配置 Keepalived 等一段时间后再发送 ARP 请求，以此等待同步完成。  
    配置项是：`vrrp_garp_master_delay 10` 表示延迟 10 秒返送。

## 参考  

- [https://www.linuxprobe.com/keepalived-nginx.html](https://www.linuxprobe.com/keepalived-nginx.html)

