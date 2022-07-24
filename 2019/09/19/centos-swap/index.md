# CentOS7 添加 Swap



```sh
cd /
fallocate -l 1G swapfile
chmod 600 swapfile 
mkswap  swapfile 
swapon  swapfile 
```

如果执行 swapon 的时候，提示 `swapon failed: Invalid argument`

则把 `fallocate -l 2G swapfile` 替换为 `dd if=/dev/zero of=/swapfile count=4096 bs=1MiB`

```sh
cd /
dd if=/dev/zero of=/swapfile count=1024 bs=1MiB
chmod 600 swapfile 
mkswap  swapfile 
swapon  swapfile 
```

参考：  
https://blog.csdn.net/zstack_org/article/details/53258588

https://unix.stackexchange.com/questions/294600/i-cant-enable-swap-space-on-centos-7
