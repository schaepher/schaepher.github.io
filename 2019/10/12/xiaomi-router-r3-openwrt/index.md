# 小米路由3 刷 OpenWRT



步骤：  
- 开启 SSH
- 用 XShell 登录
- 挂载 U 盘
- 备份 MTD
- 刷 Breed （Bootloader）
- 不使用 Breed 刷 OpenWRT

<!-- more -->

## 开启 SSH 登录

进入官网：  
> [https://d.miwifi.com/rom/ssh](https://d.miwifi.com/rom/ssh)

登录并绑定路由器。此时可以得到 **账号和密码**。  

点击【下载工具包】。

之后按官方的说法操作：

> 请将下载的工具包bin文件复制到U盘（FAT/FAT32格式）的根目录下，保证文件名为miwifi_ssh.bin；  
> 断开小米路由器的电源，将U盘插入USB接口；  
> 按住reset按钮之后重新接入电源，指示灯变为黄色闪烁状态即可松开reset键；  
> 等待3-5秒后安装完成之后，小米路由器会自动重启，之后您就可以尽情折腾啦 ：）  

## 用 XShell 登录

路由器默认的地址为 192.168.31.1。如果曾经修改过，按照修改后的值登录。

端口是 22，账号密码用上面步骤获取到的输入。

## 挂载 U 盘

1. 查看 U 盘可能的位置：`ls /dev/sd*`
   得到：`/dev/sda   /dev/sda1`

2. 取数字最高的挂载到 /mnt 文件夹：`mount /dev/sda1 /mnt`

## 备份 MTD

备份后就算刷坏也能还原。

`for name in $(grep -v 'dev' /proc/mtd | awk -F ':' '{print $1}'); do dd if=/dev/$name of=/mnt/$name.bin; done`

> 如果用这种方式都不能还原，可以用 TTL 救回来

## 刷 Breed

需要改硬件，我就暂时不尝试了。

有两个版本：  

1. 按套路的版本：  
   [http://bbs.mydigit.cn/read.php?tid=2325027](http://bbs.mydigit.cn/read.php?tid=2325027)
2. 不按套路的版本（不需要专业工具）：  
   [http://tieba.baidu.com/p/6078302343](http://tieba.baidu.com/p/6078302343)  

Breed 的刷入命令是：  
`mtd -r write /mnt/breed-mt7620-xiaomi-mini.bin Bootloader`  

其中 `/mnt/breed-mt7620-xiaomi-mini.bin` 这个是文件位置。这里假设把 U 盘挂载到 /mnt 上。

如果刷了 Breed，那后面直接用 Breed 刷就行了。见另一篇在 2019-07-25 写的小米路由 mini 刷 OpenWRT 教程。

要刷入的 bin 在以下地址中找到以 `xiaomi_miwifi-r3-squashfs-breed-factory.bin` 结尾的文件：  
[https://dl.x-wrt.com:4443/rom/](https://dl.x-wrt.com:4443/rom/)

## 不使用 Breed 刷 OpenWRT

由于 OpenWRT 不想支持小米路由3，因此要刷 ptpt52 大神基于 OpenWRT 改的 X-Wrt。  

> 在 Github 上说不支持：  
> [https://github.com/openwrt/openwrt/pull/597#issuecomment-407720718](https://github.com/openwrt/openwrt/pull/597#issuecomment-407720718)

> X-Wrt 官网：  
> https://x-wrt.com  
> 点【固件下载】进入下载界面

要下载的文件有两个：  
- 以 `xiaomi_miwifi-r3-squashfs-kernel1.bin` 结尾的文件
- 以 `xiaomi_miwifi-r3-squashfs-rootfs0.bin` 结尾的文件

回到 XShell，执行以下命令（bin 文件的名称根据下载的文件名而定，这里只是举个例子）：
  
```bash
nvram set flag_last_success=1
nvram set boot_wait=on
nvram set uart_en=1
nvram commit

mtd write xxxxx-kernel1.bin kernel1
mtd write xxxxx-rootfs0.bin rootfs0

# 如果你刷了 Breed，要再执行以下命令（记得去掉前面的 #）：
# mtd write xxxxx-kernel1.bin kernel0

reboot
```

前面 4 条命令开启了串口，非常重要。小米默认锁死串口。如果不开启，万一刷机失败或者出现意外，再也救不回来了。


