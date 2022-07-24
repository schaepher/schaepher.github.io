# NFS 搭建给 openwrt 扩展存储


raspberry:

```bash
groupadd nfs
useradd -m -g nfs nfs

apt-get install rpcbind nfs-kernel-server

vim /etc/exports
```

/etc/exports :
```
/home/nfs 192.168.15.0/24(rw,sync,no_subtree_check)
```

```bash
systemctl restart rpcbind
systemctl start nfs-kernel-server
```

openwrt:

```bash
opkg install kmod-fs-nfs-common kmod-fs-nfs nfs-utils kmod-fs-nfs-v4 portmap
service portmap start
mount -t nfs4  192.168.15.222:/home/nfs /mnt/nfs
```

/etc/fstab :

```
192.168.15.222:/home/nfs /mnt/upan nfs auto,noatime,bg,nfsvers=4,intr,tcp,actimeo=1800 0 0
```
