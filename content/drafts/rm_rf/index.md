---
title: Linux 执行文件删除后的恢复
date: 2019-08-08 09:24:07
updated: 2019-08-08 09:24:07
tags:
---

1. ext3grep
2. ext3undel
3. debugfs 和 dd
   单个文件
4. extundelete
   ext 3 4
   --superblock
   --joural  时间段
   文件、文件夹
5. grep  
   grep -F -A100 -B100 关键字 /dev/sda4   
   会找到被删的文件

先 umount


## 避免

1. rm -rf $dir/  
   检测 $dir 是否为空
1. rm -rf ./  
   可能手抖没写 .
1. 机器重装，注意看数据库是否还有连接    



https://mp.weixin.qq.com/s/-TLfLSbnIIbYnKRfBYCkTA