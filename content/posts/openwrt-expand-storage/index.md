---
title: OpenWRT 扩展容量
date: 2019-10-19 17:36:00
updated: 2019-10-19 17:36:00
categories:
 - OpenWRT
tags:
 - OpenWRT
 - 扩容
---

# 场景一：自身存储小，通过 U 盘扩展（U 盘挂载到根目录）

仅适用于有 USB 插口的路由器。

注：如果提示软件无法安装，一般是因为没有执行 `opkg update`

<!-- more -->

## 支持 U 盘

1. 安装
	```
	opkg install kmod-usb-core \
				kmod-usb-uhci \
				kmod-usb-storage \
				kmod-usb2 \
				kmod-usb-ohci \
				block-mount \
				mount-utils \
				fdisk
	```

	如果 U 盘或移动硬盘是 FAT32 的，就再装个 `kmod-fs-vfat`；如果是 NTFS 的，就装 `ntfs-3g`。

1. 挂载  
   1. 执行 `mkdir /mnt/usb` 创建挂载目录
   2. 插入 U 盘
   3. 执行 `fdisk -l | grep "^/"` 会看到与 U 盘容量差不多的分区。这里假设为 `/dev/sda4`
   4. 执行 `mount /dev/sda4 /mnt/usb`

这样进入 `/mnt/usb` 就能看到 U 盘的文件了

## 扩容

> 需要已经按照上面的【支持 U 盘】安装了相应软件。

路由器的存储非常小，装几个软件就没了。例如 小米路由器mini 只有 16MB 的 Flash。  

那么其实我们只要把根目录挂载到 U 盘上，那么就能把软件装在 U 盘上了。能存多少东西就取决于 U 盘的容量。此外还可以添加 Swap，扩充内存。用来运行需要比较大内存的程序。

步骤大致有：  

1. fdisk 对 U 盘分区
2. 复制当前根目录的所有文件到 U 盘的根目录分区
3. 设置让系统把 U 盘的分区挂载到根目录，并重启（重启后生效）
4. 让 /var 不再指向临时文件系统

### 1. fdisk 对 U 盘分区

我总共分了三个分区：  
1. 普通分区，插到 Windows 也能用的。分区类型为 FAT32。这个分区也可以不要。
2. 根目录分区。分区类型为 ext4。除了 1 和 3，剩余容量放这个分区。以下假设为 `/dev/sda1`。
3. Swap 分区。分区类型为 Swap。以下假设为 `/dev/sda2`。  
   具体容量看你想要多少内存。一两个 GB 就可以了。

我没有使用 fdisk 分区，而是在 Windows 上用 DiskGenius 分区的。所以用 fdisk 分区的方式见：  
[https://www.cnblogs.com/wangkangluo1/archive/2012/06/08/2541161.html](https://www.cnblogs.com/wangkangluo1/archive/2012/06/08/2541161.html)

分区后 U 盘插入路由器，用 `block info` 查看结果。  
> 如果已经有安装 blkid，也可以执行 `blkid` 查看结果。

以下假设 /dev/sda1 为 U 盘上要作为根目录的分区

```sh
opkg install kmod-fs-ext4 e2fsprogs  
mkfs.ext4 /dev/sda1
```

命令的含义：  
1. `kmod-fs-ext4` 是对 ext4 文件系统的支持。`e2fsprogs` 包含了 mkfs 命令，用于格式化分区。
2. 将 /dev/sda1 格式化为 ext4

### 2. 复制当前根目录的所有文件到 U 盘的根目录分区

以下假设 /dev/sda1 为 U 盘上要作为根目录的分区

```sh
mkdir /mnt/udisk
mount /dev/sda1 /mnt/udisk
mkdir /tmp/root
mount --bind / /tmp/root
tar -C /tmp/root -cvf - . | tar -C /mnt/udisk -xvf -
sync
umount /tmp/root
```

命令的含义：  

1. 创建下面 U 盘分区要挂载的目录
2. 将 U 盘中要作为根目录分区挂载到 /mnt/udisk
3. 创建一个临时目录，用于拷贝根目录文件
4. 将当前根目录以 bind 的方式挂载到临时目录，此时临时目录里可以看到和根目录一样的文件
5. 将临时目录的内容打包并解压到 /mnt/disk，tar 用于保留文件的属性信息
6. 将所有缓存写入 ROM
7. 取消挂载

### 3. 设置让系统把 U 盘的分区挂载到根目录，并重启（重启后生效）

1. 让系统自己检测分区情况  
    `block detect > /etc/config/fstab`

1. 编辑 `/etc/config/fstab`，编辑后的内容大致如下
   ```
    config global
        option auto_swap '1'
        option auto_mount '1'
        option delay_root '5'
        option check_fs '0'
        option anon_swap '1'
        option anon_mount '1'

    config mount
        option target '/'
        option uuid '0000-0000'
        option enabled '1'
   ```
   第一部分的 global 不需要修改。  
   第二个部分的 mount 中，target 改为 /，即挂载到根目录；uuid 为 U 盘分区的标识符。  
   如果不确定哪个 UUID 是对应刚才的分区，可以执行 `block info` 查看。

1. 执行 `reboot` 重启

> 重启后执行 `df -h` 就能看到 `/` 对应的容量扩大了

### 4. 让 /var 不再指向临时文件系统

执行：`ls -l /` 查看 /var 是否指向临时文件系统。如果看到：`var -> tmp` ，就表示重启路由后，你对 /var 里文件的修改会丢失。比如应用的日志。

执行以下命令：

```sh
rm /var
mkdir /var
cp -r /tmp/* /var/
reboot
```

依次是：
1. 删除当前的软连接
2. 创建文件夹
3. 将 /tmp 里的文件复制到 /var 里面
4. 重启

> 注：如果 /var 指向 tmp，可能会导致 supervisor 无法正确启动。因为涉及到 `/var/run/` 文件夹。

## 扩充内存

上面扩容的时候，有分了一个 Swap 分区。现在我们把它挂载到系统的 Swap。  

假设设置为 Swap 的分区为 /dev/sda2，执行以下命令：

```sh
mkswap /dev/sda2
swapon /dev/sda2
```

命令的含义：  

1. 将 /dev/sda2 设置为 Swap
2. 启用这个 Swap

此时用 `free` 命令查看就可以看到 Swap 已经加载了。  

接下来让路由器启动的时候自动加载这个 Swap。

编辑 `/etc/config/fstab`。

在下面多添加：  

```
config swap
    option enabled '1'
    option device '/dev/sda2'
```

> 注：swap 无法通过 UUID 挂载，它只有 PARTUUID。只能通过盘号挂载

执行 `reboot` 重启路由器。重启后执行 `free` 就能看到效果了。

## 参考链接

[https://segmentfault.com/a/1190000000380233](https://segmentfault.com/a/1190000000380233)


# 场景二：自身容量大，但 OpenWRT 只用了一小部分

这里以 Raspberry Pi 4B 为例：

镜像下载地址：

https://openwrt.org/toh/hwdata/raspberry_pi_foundation/raspberry_pi_foundation_raspberry_pi_4_b

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