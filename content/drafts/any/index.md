---
title: any
date: 2020-02-24 03:34:54
updated: 2020-02-24 03:34:54
tags:
---


## docker 保存镜像和恢复镜像：

docker save myimage:latest | gzip > myimage_latest.tar.gz

docker load < busybox.tar.gz

## sed

删除空行：  

sed -i '/^\s*$' tmp.txt

## 并行 parall

https://www.jianshu.com/p/cc54a72616a1

## 并行 xargs

https://www.cnblogs.com/f-ck-need-u/p/9752365.html

## 终端复用 tmux

https://www.cnblogs.com/kevingrace/p/6496899.html

## nginx 连接数判断

https://blog.csdn.net/qq_42303254/article/details/89512198

## 移动硬盘被占用无法弹出

可能是 Everything 的后台程序占用了，关闭程序就好了。