# CentOS7 读取 NTFS 格式硬盘



### 查看磁盘

`fdisk -l`

### 挂载

安装支持程序：  
```bash
yum install -y ntfs-3g
mkdir /mnt/hd
mount -t ntfs /dev/sdb /mnt/hd
```

### 格式化磁盘

```
yum install -y ntfs-3g ntfsprogs
mkntfs -F --fast --label myDisk /dev/sdb
```

### 从源码安装  

https://www.tuxera.com/community/open-source-ntfs-3g/


https://blog.csdn.net/qiushisoftware/article/details/79520869


