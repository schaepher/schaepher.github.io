---
title: 树莓派4B + CentOS 7 + Nextcloud
date: 2019-10-03 21:42:16
updated: 2019-10-03 21:42:16
tags:
---

## 前期准备

### 硬件准备

- 树莓派 4B（5V 3A Type-C 电源、class10 TF 闪存卡、读卡器）  
  闪存卡用来装系统，读卡器用于通过 Windows 把系统烧录到闪存卡上  
- （硬盘盒 + 硬盘）或者（移动硬盘）
- USB 3.0 带电源接口的分线器（可选）  
  如果不想用硬盘盒/移动硬盘自带的电源或者有其他用途才选择这个

### 注意点

1. 树莓派的 CPU 是 ARM v8 架构 64 位，因此从系统到软件都要选择支持 ARM 64 的版本    
   详细参数：  
   [https://www.raspberrypi.org/products/raspberry-pi-4-model-b/specifications/](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/specifications/)

2. 树莓派的电流有限（3A），接太多设备或者电流要求高的设备时，会发生故障。因此可以选择购买带电源接口的 USB 分线器。

### 软件准备

- Windows 下的烧录工具： win32diskimager  
  用于烧录 CentOS 7 到树莓派。下载后要安装。    
  [https://sourceforge.net/projects/win32diskimager/](https://sourceforge.net/projects/win32diskimager/)  

- CentOS 7 ARM  
  点下面链接进入官方的镜像列表，选择 `CentOS-Userland-7-armv7hl-RaspberryPI-Minimal-4-1908-sda.raw.xz`  
  [http://isoredirect.centos.org/altarch/7/isos/armhfp/](http://isoredirect.centos.org/altarch/7/isos/armhfp/)   

- Docker ARM  
  `curl -fsSL https://get.docker.com | sh`  
  源自于：  
  [https://docs.docker.com/install/linux/docker-ce/centos/](https://docs.docker.com/install/linux/docker-ce/centos/)

- Nextcloud ARM  
  使用上和 x86 没什么不同  
  [https://hub.docker.com/_/nextcloud](https://hub.docker.com/_/nextcloud)  

## 备份已有系统

1. 把 TF 闪存卡放入读卡器，插到电脑。
2. 打开 win32diskimager ，设备选择闪存卡
3. 在电脑上随便一个地方新建一个文件，命名为 `Raspberry4B.img` （随便命名都行）
4. win32diskimager 上选择刚刚创建的文件，点击【读取（Read）】按钮读取

## 安装 CentOS 7

1. 把 TF 闪存卡放入读卡器，插到电脑。
2. 解压下载的 .xz 文件，得到 .raw 文件。
3. 启动 win32diskimager，选择解压出来的 .raw 文件，目标设备选择闪存卡，点击【写入（Write）】按钮写入，等待写入完成。
4. 闪存卡放树莓派，启动树莓派。用默认账户 root 和默认密码 centos 登录。
5. 执行 `rootfs-expand` 来扩展根文件夹大小，充分利用 TF 卡的空间。否则会发现空间不够用。

可参考：  
[https://zhuanlan.zhihu.com/p/33030757](https://zhuanlan.zhihu.com/p/33030757)  

同步时间：  

```bash
yum -y install ntp ntpdate
ntpdate cn.pool.ntp.org
```

CPU 温度：  

```sh
CUR_TEMP=$(cat /sys/class/thermal/thermal_zone0/temp); echo $[$CUR_TEMP / 1000]"."$[$CUR_TEMP % 1000]°C
```


## 安装 Docker

```bash
curl -o docker.tgz https://download.docker.com/linux/static/stable/armhf/docker-19.03.3.tgz
tar xvzf docker.tgz
mv docker/* /usr/bin/
rmdir docker
```

> https://docs.docker.com/install/linux/docker-ce/binaries/#install-daemon-and-client-binaries-on-linux  
> https://download.docker.com/linux/static/stable/armhf/

如果要使用 systemctl 管理 docker，那么需要三个文件：  

```
/usr/lib/systemd/system/docker.service   
/usr/lib/systemd/system/docker.socket   
/usr/lib/systemd/system/containerd.service  
```

systemctl enable containerd.service && systemctl enable docker.socket && systemctl enable docker.service 

### 安装 Docker Compose

确保已安装 pip。如果没有安装，则执行以下命令安装：  

```bash
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py
```

使用 pip 安装：

`pip3 install docker-compose`

该方式来自：  
[https://docs.docker.com/compose/install/#install-using-pip](https://docs.docker.com/compose/install/#install-using-pip)

注意：  
如果安装时出现错误 `fatal error: Python.h: No such file or directory`，则要安装 python3-devel。  
如果出现 `fatal error: openssl/opensslv.h: No such file or directory`，则要安装 openssl-devel。

## 安装 Nextcloud

public-proxy(443) -> frps(443) --穿透--> frpc(443) -> inner-proxy(443) -> nextcloud(80)  

- public-proxy 和 frps 都放外网机器  
- frpc 放路由器
- inner-proxy 和 nextcloud 放内网服务器

## frpc 配置的影响

注意 frpc 会指定 inner-proxy 的地址（local_ip）。如果 inner-proxy 地址变更，会导致请求得到 502 的返回。

但由于 local_ip 可设置为域名，因此避免 inner-proxy 地址变更造成的影响。

路由器上可设置主机名对应 IP，这样可直接绑定。在 OpenWRT 管理界面的 【 网络 | 主机名 】 菜单可找到。将主机名设置为 nextcloud 的域名。

相同主机名可设置多个 IP，这样就可以同时设置内网服务器的 WiFi 网卡和网线连接的 IP。

## Public Proxy

如果要结合 Frp 使用，一定要将以下内容保存为 proxy.conf ，并放到 /etc/nginx/ 底下。 

```conf
# HTTP 1.1 support
proxy_http_version 1.1;
proxy_buffering off;
proxy_set_header Host $http_host;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $proxy_connection;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $proxy_x_forwarded_proto;
proxy_set_header X-Forwarded-Ssl $proxy_x_forwarded_ssl;
proxy_set_header X-Forwarded-Port $proxy_x_forwarded_port;
proxy_ssl_server_name on;

# Mitigate httpoxy attack (see README for details)
proxy_set_header Proxy "";
```

## 增加最大上传文件限制

Nextcloud 官方示例的配置文件已经包含了该限制的配置，因此无需另外修改。  

> [https://github.com/nextcloud/docker/blob/master/.examples/docker-compose/with-nginx-proxy/postgres/fpm/web/nginx.conf](https://github.com/nextcloud/docker/blob/master/.examples/docker-compose/with-nginx-proxy/postgres/fpm/web/nginx.conf)

以下内容需要修改：  

1. inner-proxy 的 Nginx 需要设置 `client_max_body_size 10G;`  
   具体做法是，新增个 max_body.conf 文件，把 `client_max_body_size 10G;` 写进去。然后把文件放到 `/etc/nginx/conf.d` 里面。

2. Nextcloud fpm 的限制  
   在 Nextcloud 的数据目录下，有个 `.user.ini` 的文件。在文件里面添加以下内容：  
   ```ini
   php_value upload_max_filesize 16G
   php_value post_max_size 16G

   php_value max_input_time 3600
   php_value max_execution_time 3600
   ```  

   > [https://docs.nextcloud.com/server/17/admin_manual/configuration_files/big_file_upload_configuration.html#configuring-your-web-server](https://docs.nextcloud.com/server/17/admin_manual/configuration_files/big_file_upload_configuration.html#configuring-your-web-server)

## 如果应用商店没有展示

查看日志我们可以看到：  

```
Operation timed out after 10001 milliseconds with 0 out of 0 bytes received","url":"https:\/\/apps.nextcloud.com\/api\/v1\/apps.json"
```

默认超时时间为 10 秒。

如果在容器里面请求 `https://apps.nextcloud.com/api/v1/apps.json` 能够得到数据，只是比较久。那么我们就得把超时时间设置长一点。

进入 Nextcloud 容器，编辑 `/var/www/html/lib/private/App/AppStore/Fetcher/Fetcher.php` ，把 fetch 方法里面 timeout 改久一点，比如 60 秒。

## 存储方案

要确保任何一个节点挂掉之后，


## Nextcloud 挂载外部存储  

Nextcloud 自身支持挂载

http://www.bujarra.com/nextcloud-anadiendo-acceso-a-datos-externos/?lang=en

修复文件删除出错，或者备份恢复文件出错：

```
docker exec --user www-data nextcloud php occ files:scan --all
docker exec --user www-data nextcloud php occ maintenance:mode --on
// 进入数据库执行：  delete from oc_file_locks where lock = 1;
docker exec --user www-data nextcloud php occ maintenance:mode --off 
```

https://villekaaria.eu/2019/03/10/hosting-nextcloud-with-docker/

修改 Docker 数据存放文件夹：  
```
sudo vi /etc/docker/daemon.json

{
  "data-root":"/NEWLOCATION"
}
```

## 其他

安装 OpenWRT 把树莓派作为路由器使用：  
[https://www.shuyz.com/posts/install-openwrt-on-raspberry-as-a-wireless-router/](https://www.shuyz.com/posts/install-openwrt-on-raspberry-as-a-wireless-router/)

安装 Windows 10 IoT 系统：  
https://docs.microsoft.com/en-us/windows/iot-core/downloads

https://docs.nextcloud.com//server/14/admin_manual/configuration_files/external_storage_configuration_gui.html#available-storage-backends

https://docs.nextcloud.com//server/14/admin_manual/configuration_files/external_storage_configuration_gui.html

https://hub.docker.com/_/gitlab-community-edition/plans/6a33c5d4-c1cc-48f4-ae30-e033126ffd7f?tab=instructions

https://villekaaria.eu/2019/04/13/nextcloud-filesscan-with-docker/

https://github.com/kahing/goofys

https://www.shuyz.com/posts/install-openwrt-on-raspberry-as-a-wireless-router/


config.txt

http://shumeipai.nxez.com/2015/11/23/raspberry-pi-configuration-file-config-txt-nstructions.html  

https://www.raspberrypi.org/documentation/configuration/config-txt/video.md

VGA:

https://blog.csdn.net/bona020/article/details/79027409

挂载：  

https://techwiztime.com/guide/auto-mount-ntfs-usb-drive-raspberry-pi/

关闭 MAC 随机生成（如果安装了 Network Manager）：  

https://raspberrypi.stackexchange.com/questions/68513/pi-using-a-random-mac-address-after-every-reboot-how-do-i-stop-this-behavior/75497#75497

蓝牙连接：  

https://www.embbnux.com/2016/04/10/raspberry_pi_3_wifi_and_bluetooth_setting_on_console/


CentOS7 arm 中科大源

```
# CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the
# remarked out baseurl= line instead.
#
#
 
[base]
name=CentOS-$releasever - Base
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os
baseurl=http://mirrors.ustc.edu.cn/centos-altarch/$releasever/os/$basearch/
gpgcheck=1
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
       file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-AltArch-Arm32
 
#released updates
[updates]
name=CentOS-$releasever - Updates
# mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates
baseurl=http://mirrors.ustc.edu.cn/centos-altarch/$releasever/updates/$basearch/
gpgcheck=1
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
       file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-AltArch-Arm32
 
#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras
# mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras
baseurl=http://mirrors.ustc.edu.cn/centos-altarch/$releasever/extras/$basearch/
gpgcheck=1
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
       file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-AltArch-Arm32
 
#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$releasever - Plus
# mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus
baseurl=http://mirrors.ustc.edu.cn/centos-altarch/$releasever/centosplus/$basearch/
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
       file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-AltArch-Arm32
```