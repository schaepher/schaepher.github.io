---
title: 用 TTL 救活变砖的小米路由3
date: 2019-10-07 01:00:00
updated: 2019-10-07 03:00:00
categories:
 - Router
 - OpenWRT
tags:
 - Router
 - OpenWRT
 - XiaoMi Router R3
 - TTL
---

## 背景

之前往 小米路由3 刷入小米路由 MINI 的 OpenWRT 包，结果发现无法安装软件。于是就想刷回来，但是 MTD 信息已经被清空，无法通过 mtd write 来重新写入其他固件。  

也无法通过官方的方法（U盘放入官方固件 miwifi.bin）来恢复。因为系统压根就不理这个文件，毕竟 bootloader 不一样。

这时候跟变砖已经没什么两样了。

一开始折腾到绝望，然后买了台二手小米 MINI，勉强先用着。直到今天才又开始继续折腾。幸运的是刷回来了，否则今晚会睡不着。

<!-- more -->

## 准备

### 硬件  

- 一台被刷坏的 小米路由3 和电源
- 一个带有 小米路由3 固件二进制文件的 U 盘
- 一个 USB 转 TTL 转换器  
  我用的是 CH340G RS232升USB转TTL模块转串口，12 块钱。
- 公对母杜邦线 3 条（10 条 6 块钱）  
  买转换器的时候顺便买几条。实在没有就用导线代替。
- 十字螺丝刀
- 网线一条

### 软件

- PuTTY 或者 XShell，用于读写串口
- Windows 自带的 tftp

### 路由器系统相关文件

- uboot_md5-b7a74e9668289dd68f1c637cd99dcc5c.bin  
  Bootloader
- miwifi_r3_firmware_e9f31_2.27.120.bin  
  官方固件

## 大概要做啥

1. 把 小米路由3 的电路板拆出来
2. 将 USB 转 TTL 转换器的 TTL 端连接到电路板上的 TTL 接口，USB 端连 Windows
3. 小米路由3 通过网线连接到 Windows 上
4. Windows 上通过软件与路由器 TTL 交互
5. 路由器接入电源，进入命令行模式，做一些配置
6. 路由器重启，进入【通过 TFTP 写入 Flash】模式
7. 通过 TFTP 将 uboot 和 miwifi 这两个二进制文件写入路由器
8. 重启路由器
9. 如果提示 Press reset button to enter USB recovery，则按照官方刷机教程刷机

## 把 小米路由3 的电路板拆出来

后盖商品信息条的中间部分有一颗螺丝，把它转出来。然后就可以撬开外壳了。  

把天线连接到电路板的那个地方拔起来。这样就可以把整块板取出来。

## TTL 转换器连接

1. 连接路由电路板  
   在电路板靠电源的一边，有四个小孔。分别是 3.3V、RX、GND、TX。  
   转换器有五个口，分别是 5V、3.3V、TXD、RXD、GND。  
   以下是连线关系，左边连接到右边（公的部分直接插到电路板的孔里就可以用，不需要焊接）：  
   
   |转换器|电路板|
   |:--|:--|
   |TXD|RX|
   |RXD|TX|
   |GND|GND|
   
   其他不需要连接

2. 把转换器的 USB 端连接到 WIndows 上  
   通过 Windows 的【设备管理器】得到刚刚插入的串口号：COMn。这里的 n 是一个数字，在不同电脑上可能不同。

## 小米路由3 通过网线连接到 Windows 上

用于传输数据

1. 路由端连 LAN 口
2. Windows 连接后，要在网络配置里面，做以下配置：  
   - IP 获取模式： DHCP 改为手动  
   - IP： 192.168.1.3
   - 子网掩码：255.255.255.0 或者子网前缀长度：24
   - 网关：192.168.1.1（路由器的地址）
3. Windows 如果有启动 WiFi，则关掉

## Windows 上通过软件与路由器 TTL 交互

用于发送指令

这里以 PuTTY 为例：  

|配置项|配置|
|Connection type|Serial|
|Serial line|COMn（记得根据实际情况把 n 替换为某个数字）|
|Speed|115200|

配置完后点【Open】，打开交互界面，继续下面的操作

## 路由器接入电源，进入命令行模式

要先在上一步 Open 之后才接入电源，这样才不会让路由器直接加载系统。  

接入电源后，能从交互界面上看到一些信息，直到展示下面这些：  

```
Please choose the operation: 
   1: Load system code to SDRAM via TFTP. 
   2: Load system code then write to Flash via TFTP. 
   3: Boot system code via Flash (default).
   4: Entr boot command line interface.
   7: Load Boot Loader code then write to Flash via Serial. 
   9: Load Boot Loader code then write to Flash via TFTP. 
```

先选择 4，进入命令行界面。配置启动选项等待和开启写入。

执行以下命令：

```
setenv boot_wait on
setenv uart_en 1
saveenv
```

这些命令相当于在官方或者潘多拉固件里执行：  

```
nvram set boot_wait=on
nvram set uart_en=1
nvram commit
```

或者相当于 OpenWrt 里执行：  

```
fw_setenv boot_wait on
fw_setenv uart_en 1
```

## Windows 开启 TFTP

打开 Windows 命令行界面（CMD 或者 PowerShell），执行 tftp。如果提示无法执行，则表示没有开启该功能。  

按以下步骤开启：  

1. WIN+R 打开 Run，输入 appwiz.cpl，并打开
2. 点击左侧的【启用或关闭 Windows 功能】
3. 找到 【TFTP Client】，前面打勾
4. 确定

## 路由器重启，进入【通过 TFTP 写入 Flash】模式

### 写 BootLoader

拔掉电源，再插入。这次选择 9。

- 选 Y
- 填入 192.168.1.1（默认就是）
- 填入 192.168.1.3（我们在上面设置的 Windows IP）
- 文件名填入 `uboot.bin`  
  > 我们下面假设 `uboot_md5-b7a74e9668289dd68f1c637cd99dcc5c.bin` 存放在 `E:\uboot.bin`

此时会进入等待状态。

在 Windows 上打开命令行界面，执行：  

```
tftp -i 192.168.1.1 PUT E:\uboot.bin
```

执行过程中可能会出现 N 次失败，比如 `Retry count exceeded;` 或者 `Timeout`，不断重试直到成功就行了。  

如果看到 `Writing image to`，就表示很快要成功了。

### 写 Firmware

同理，拔电源重启，这次选 2。

其余和上面差不多，就是把 uboot 换成 `miwifi_r3_firmware_e9f31_2.27.120.bin`。

## 重启路由器

写入成功后，会自动重启路由器。看着交互界面读取的信息就有一股成功的气息。  

路由器会做一些初始化，需要等待一段时间。这段时间灯会常亮黄色灯。  

路由器会多次自动重启。

1. 如果看到 `Booting up finished`，那么就是成功了。通过 `192.168.31.1` 就可以看到界面。
2. 如果一直提示 `Press reset button to enter USB recovery`，则把 miwifi 那个文件重命名为 `miwifi.bin` 放到 U 盘根目录，然后插入 USB 口。  
   按住 Reset 按键不放，然后拔电源重启。当黄灯慢闪烁后，放开 Reset 键。等待安装完成。从交互界面可以看到安装的进度。  
   安装完经过初始化，就能够运行啦！

## 参考文档

非常感谢这些文档的作者~没有这些文档，我是不可能在短时间内救活我的路由器的。

主要参考文档：  
https://blog.csdn.net/flyhorstar/article/details/95729059  

提供了非常关键的 mi3_uboot：  
https://aisoa.cn/post-2213.html

OpenWRT：  
https://openwrt.org/toh/xiaomi/mir3

LEDE 全球首发，支持小米路由3（Xiaomi Mi Router R3）:  
https://www.right.com.cn/forum/thread-261964-1-1.html

小米路由器3潘多拉固件刷机教程：  
https://blog.csdn.net/u011054333/article/details/88564078


## 资源  

小米路由器历史固件集合：https://www.right.com.cn/FORUM/thread-706545-1-1.html

-------

没想到这篇居然写了两个小时 > <