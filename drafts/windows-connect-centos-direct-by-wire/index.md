# Windows 主机通过网线直连 CentOS 主机


1. 用网线将两者连接
2. 到 【控制面板\网络和 Internet\网络和共享中心\更改适配器配置】 选择可连外网的网卡（以下称外网网卡），进入属性，切换到共享页面。  
   注意！是连接外网的网卡，通常是连接 WiFi 的那张，因为有线连接已经被占用去连接 CentOS 了。  
   点开【允许其他网络....】，然后选择连接台式机的那个网卡（以下称内网网卡）
   保存
3. 此时内网网卡会自动设置一个 IP ，我们假设它是 192.168.137.1 。
4. 打开 windows 的路由转发。打开注册表，HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters ，把 IPEnableRouter 设置为 1
5. 进入 centos 的 /etc/sysconfig/network-scripts/ ，修改网卡配置。

TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no

BOOTPROTO=static
IPADDR=192.168.137.2
NETMASK=255.255.255.0
BROADCAST=192.168.137.255
GATEWAY=192.168.137.1

DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp2s0
UUID=418b805a-b022-4bca-8629-4a7ffac3c2a7
DEVICE=enp2s0
ONBOOT=yes
ZONE=public
PREFIX=24
DNS1=192.168.50.89
DNS2=192.168.50.87

解释：
BOOTPROTO 选 static
IPADDR 只要是 192.168.137.0 网段的就行
GATEWAY 设置为 192.168.137.1
DNS 设置和 外网网卡的 DNS 设置一致



参考文档：
https://www.cnblogs.com/Bonker/p/4849295.html
https://blog.csdn.net/cbuy888/article/details/81362601
