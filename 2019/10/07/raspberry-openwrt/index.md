# 树莓派4 安装 OpenWRT 作为路由器



## 下载与安装

https://openwrt.org/toh/hwdata/raspberry_pi_foundation/raspberry_pi_foundation_raspberry_pi_4_b

当前只有 snapshot 版本。找到【Firmware OpenWrt snapshot Install URL】，后面是下载地址。下载下来解压得到 .img 文件。

使用 Win32DiskManager 将 img 文件刷入到 SD 卡。

<!-- more -->

## 配置

将设备接入电脑，电脑使用 Xshell 或者其他工具连接 192.168.1.1，用户名为 root，无密码。

执行以下命令：                                                                                                                                                                                                                

```
uci set network.lan.proto=dhcp
uci delete network.lan.ipaddr
service network restart
```

将设备接入以前的路由器。进入路由器界面，找到路由器分配给 Raspberry 的 IP。然后用 Xshell 连接。此时可以下载软件，以及做其他配置。

## Snapshot 版本

需要自己安装界面管理 LuCI。

```
opkg update
opkg install luci
```

## https 支持

```
opkg update
opkg install libustream-openssl20150806
```

## 安装 USB 转千兆网卡驱动

购买 USB 转千兆网卡。例如绿联20255，其芯片为 AX88179，安装命令为：
```
opkg update
opkg install kmod-usb-net-asix-ax88179
```

## 配置拨号连接

将设备连接到家庭网络的入口，电脑连接 Raspberry，进入 http://openwrt.lan/cgi-bin/luci 。

进入 [Network | Interfaces] ，[Add new interface] 添加接口：

|选项|填写||
|:--|:--|:--|
|Protocol|PPPoE||
|username|宽带账号||
|password|宽带密码||
|firewall-zone|WAN||

然后编辑原先的 DHCP 的接口：

|选项|填写||
|:--|:--|:--|
|Protocol|Static address||
|address|192.168.100.1||
|netmask|255.255.255.0||
|firewall-zone|LAN||
|Bridge interfaces|打勾||
|Interface|eth1 和 wlan0||

点 [Save & Apply] 保存并应用。

## 扩容

以下内容引用自：

https://schaepher.github.io/2019/10/19/openwrt-expand-storage/#more

1. 先把 OpenWRT 装好，网络配置为 DHCP
   
2. 把存储卡剩余容量格式化为 ext4  
   给多少容量无所谓，这一步是为了存备份文件
   
3. 进入到路由，执行命令把系统文件备份到刚刚创建的 ext4 分区(假设为 /dev/sda3)

    ```
    mkdir /mnt/udisk
    mount /dev/sda3 /mnt/udisk
    mkdir /tmp/root
    mount --bind / /tmp/root
    tar -C /tmp/root -cvf /mnt/udisk/backup.tar .
    ```

4. 如果有 Ubuntu 系统桌面版，直接进去 Ubuntu 系统使用下面的操作。  
   没有的话，刷一个到 U 盘，然后用 U 盘启动。

5. 使用 Ubuntu 自带的 disk 软件，将原先装系统文件的那个分区格式化为 ext4  
   注意：一定要使用格式化，不能直接删除该分区。因为该分区前面的空白分区需要保留。如果直接删除，会被合并起来。

6. 将上一步格式化为 ext4 分区的容量调大到想要的大小，例如 4GB

7. 把 backup.tar 解压到这个分区里面

8. 在这前面还有一个分区，叫 boot 分区。进去里面编辑 cmdline.txt  
   把 `rootfstype=squashfs,ext4` 改为 `rootfstype=ext4,squashfs` ，并保存

9. 把卡插到 Raspberry 启动

## 安装 DDNS

如果家里网络是有外网 IP 的，且申请了域名，那么可以给域名设置 DDNS。

```
opkg update
opkg install ddns-scripts luci-app-ddns
```

配置：

namecheap 会提供一个 [Dynamic DNS Password]，这个用作密码。

http://electropit.com/index.php/2015/10/16/openwrt-ddns-setup-for-namecheap/

## 其他软件

```
opkg update
opkg install lrzsz vim curl
```

## 注意点

WiFi 无法发送信号，只能用于接收信号。  

WiFi 可接收 2.4G 和 5G 信号，5G 信号仅能接收 100 信道以下的。
