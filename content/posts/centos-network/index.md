---
title: CentOS7 NetworkManager 管理网络
date: 2019-10-07 14:23:09
updated: 2019-10-07 14:23:09
categories:
 - Installation And Configuration
tags:
 - Linux
 - CentOS
---


## 工具

`yum install -y NetworkManager-wifi`

### 查看网卡状态  

`nmcli dev status`

结果示例：  

```
DEVICE         TYPE      STATE         CONNECTION         
eth0           ethernet  connected     Wired connection 1 
wlan0          wifi      disconnected  --                 
p2p-dev-wlan0  wifi-p2p  disconnected  --                 
lo             loopback  unmanaged     --
```

如果是 unavailable，则重启系统。

### 查看 WiFi 列表

`nmcli dev wifi`

结果示例：

```
IN-USE  SSID               MODE   CHAN  RATE        SIGNAL  BARS  SECURITY  
        CMCC-5xJW          Infra  6     130 Mbit/s  100     ▂▄▆█  WPA1 WPA2 
        CMCC-CsJc          Infra  13    130 Mbit/s  55      ▂▄__  WPA1 WPA2
        TP-LINK_3F82       Infra  11    405 Mbit/s  29      ▂___  WPA1 WPA2
```

### 连接 WiFi

`nmcli dev wifi con "SSID" password "密码"`

注：  
如果之前有通过其他方式连接或者创建配置文件到 `/etc/sysconfig/network-scripts/` 里面，则要先删除。  
否则会提示：`Secrets were required, but not provided`

### 启动已经连接过的 WiFi

`nmcli con up "SSID"`

### 设置开机自动连接 WiFi

`nmcli con mod "SSID" connection.autoconnect yes`

### 如果发现无法通过 WiFi 连接 SSH

重启路由器

## 参考链接  

https://www.cnblogs.com/asker009/p/10212045.html