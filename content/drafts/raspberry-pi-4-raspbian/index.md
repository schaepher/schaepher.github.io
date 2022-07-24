---
title: raspberry-pi-4-raspbian
date: 2019-10-11 05:00:19
updated: 2019-10-11 05:00:19
tags:
---

## 配置国内源

```bash
cp /etc/apt/sources.list /etc/apt/sources.list.default
sudo cat > /etc/apt/sources.list << DELIM
deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main non-free contrib 
deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main non-free contrib
DELIM

cp /etc/apt/sources.list.d/raspi.list /etc/apt/sources.list.d/raspi.list.default
sudo cat > /etc/apt/sources.list.d/raspi.list << DELIM
deb http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui
DELIM

sudo apt-get update
```

## 从 Windows 连接到 Raspberry 的远程桌面

#### 法一：自带的 VNC Server

raspbian 桌面版自带 VNC，默认不启动。执行以下命令启动：    
`sudo systemctl start vncserver-x11-serviced.service`

然后下载 VNC Viewer：  
[https://www.realvnc.com/download/viewer/](https://www.realvnc.com/download/viewer/)  

用 IP 登录即可。

#### 法二：Windows 的远程桌面

执行以下命令：  
`sudo apt-get install xrdp`

安装完成后，用 Windows 的远程桌面连接即可。

## 从 Raspberry 连接到 Windows 的远程桌面

> 用了 xrdp 和 freerdp 后，选择用 freerdp

执行以下命令：  

`sudo apt-get install freerdp2-x11`

`xfreerdp /u:schaepher@outlook.com /v:home.schaepher.com:48484`

#### 安装 Docker

`curl -sSL https://get.docker.com | sh`

#### 安装 tmux

`sudo apt-get install tmux`

#### 安装 mariadb

`sudo apt-get install mariadb-server`

## 连接无线

#### 法一：通过桌面配置

这种方式会自动设置为开机自动连接。

#### 法二：命令配置

```bash
wpa_supplicant -B -i wlan0 -c <(wpa_passphrase "你要连接的 WiFi 名称（SSID）" "你的密码")
```

只需执行一次，重启后会自动扫描和连接。

wlan0 表示 WiFi 的网卡，可能根据不同情况名称不同。网卡名称通过 `ifconfig -s` 看第一列得到。

SSID 可通过以下命令扫描：  
`iwlist wlan0 scan | grep SSID`

详细的请参考：  
[https://www.jianshu.com/p/e22331d62a16](https://www.jianshu.com/p/e22331d62a16)

## 添加用户并设置为可登录 root

将用户加入组 `sudo` 即可登录 root。

## 基本软件安装

```bash
sudo apt-get install -y vim git lrzsz 
```

## 安装 Docker

```bash
curl -fsSL https://get.docker.com | sh
```

## 外接硬盘

要把 Docker 的目录放到外部硬盘，外部硬盘最好实用 xfs 文件系统。这样可以直接实用 overlay2。  

### XFS

如果想使用 xfs 文件系统，则需要对硬盘格式化。  

1. 安装 `xfsprogs`     
   `yum install -y xfsprogs` 或者 `apt-get install -y xfsprogs`

2. 找到硬盘  
   `fdisk -l | grep dev`  
   找到容量和外置硬盘差不多的。例如 `/dev/sda`

3. 格式化  
   `mkfs -t xfs -f /dev/sda`

> [https://www.cyberciti.biz/faq/how-to-install-xfs-and-create-xfs-file-system-on-debianubuntu-linux/](https://www.cyberciti.biz/faq/how-to-install-xfs-and-create-xfs-file-system-on-debianubuntu-linux/)

### NTFS

如果外部硬盘是 NTFS 系统，则会报错：  
> docker: error creating overlay mount to invalid argument

如果实在想用 NTFS，则把 Docker 的 storage-driver 设置为 vfs。虽然慢，但是能用。  
> 见：  
> [https://github.com/moby/moby/issues/23930#issuecomment-358367075](https://github.com/moby/moby/issues/23930#issuecomment-358367075)

### 设置为开机自动挂载硬盘

1. 获取 PARTUUID    
   `blkid -p /dev/sda`  

   使用 PARTUUID 是为了防止标识变化。

   > 用 UUID 也可以

   > [https://raspberrypi.stackexchange.com/questions/75027/whats-the-difference-between-uuid-and-partuuid/75030#75030](https://raspberrypi.stackexchange.com/questions/75027/whats-the-difference-between-uuid-and-partuuid/75030#75030)

2. 编辑 `/etc/fstab`  
   `PARTUUID=XXXXX /mount-dest-dir xfs defaults,nofail,x-systemd.device-timeout=5 0 0`  
   > [https://askubuntu.com/questions/14365/mount-an-external-drive-at-boot-time-only-if-it-is-plugged-in/1027273#1027273](https://askubuntu.com/questions/14365/mount-an-external-drive-at-boot-time-only-if-it-is-plugged-in/1027273#1027273)

### 设置时区

timedatectl set-timezone Asia/Shanghai

