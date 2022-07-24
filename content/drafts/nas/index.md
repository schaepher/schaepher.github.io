---
title: NAS 硬件选购
date: 2019-10-03 21:42:16
updated: 2019-10-03 21:42:16
tags:
---

硬件知识：http://madaimeng.com/article/NAS-Assemble-1-hardware-ref/#  
选购：https://post.smzdm.com/p/120480/  
软件：https://www.zhihu.com/question/21359049/answer/34375825

烧录软件：https://sourceforge.net/projects/win32diskimager/

一大堆相关网站集合：https://post.smzdm.com/p/andg4g90/

## 选硬件

两个重要因素：  

1. 安静
2. 低功耗

安静是因为 7x24 小时都在运作，太吵了影响心情。低功耗也是因为 7x24 小时，耗电量不小。

要安静就得尽量选择无风扇的方案。

挑选硬件时，电源放最后选。


防护方案：  

1. UPS   
   用于断电防护。分在线式和后备式。  
   在线式切换无延迟，价格贵 4~5 倍。后备式有 10 毫秒左右延迟，NAS 供电电源质量不差的情况下不影响。  
   UPS 内置的电池只能撑一小段时间。因此真正断电后，要尽快将 UPS 接到备用电源（电池）上。100W 功率能撑 22 分钟。  
   APC BK500-CH  
   如果不能保证在 UPS 电池用完之前给 UPS 供电，那么要接入自动关机的方案。否则 UPS 电池耗尽，对寿命有影响。    
   思路是让路由器来控制给 NAS 和 UPS 关机。因此要求路由器能刷系统（OpenWRT）。    
   > https://post.smzdm.com/p/508308/
2. 

AMD 速龙 3000G 处理器 2核4线程 搭载Radeon Vega Graphic 3.5GHz AM4接口 盒装CPU  
https://item.jd.com/100005955855.html  

桌面CPU性能排行榜  
https://rank.kkj.cn/dcpu.shtml

神舟K580C-i5 D1参数  
https://product.pconline.com.cn/notebook/hasee/553230_detail.html


nas系列 篇三：nas主板新选择-华擎E350M1  
https://post.smzdm.com/p/a5k67ee3/

正版 Windows 10  
https://www.microsoftstore.com.cn/software/windows

重新激活  
https://support.microsoft.com/zh-cn/windows/%E5%9C%A8%E6%9B%B4%E6%8D%A2%E7%A1%AC%E4%BB%B6%E5%90%8E%E9%87%8D%E6%96%B0%E6%BF%80%E6%B4%BB-windows-10-2c0e962a-f04c-145b-6ead-fb3fc72b6665  


基于 AMD 平台的家用 NAS 方案综述  
https://post.smzdm.com/p/a6lrz7v0/

浅谈家庭NAS的组装与应用 篇一：硬件选购篇  
https://post.smzdm.com/p/120480/

CPU 比较  
https://cpu.userbenchmark.com/Compare/Intel-Core-i5-4200M-vs-AMD-Athlon-3000G/m2341vsm968952  

文菌装NAS E1：手把手教您组装2021全能NAS，ALL IN ONE 配置清单  
https://www.bilibili.com/read/cv10629149

## 待看

https://detail.zol.com.cn/motherboard/s1280/

https://mall.jd.com/index-1000000225.html?from=pc

https://mall.jd.com/index-1000000266.html?from=pc

https://asus.jd.com/view_search-416883-2981961-99-1-20-1.html

https://msigaming.jd.com/view_search-392505-14790148-99-1-20-1.html


## 定位

1. 安装一些不想安装在 pad 上的软件
2. 下载文件
3. 同步和备份文件
4. 装一些 Windows 软件，供在外远程使用
5. Windows 管理工具


下载文件：uTorrent，迅雷，Free Download Manager，百度网盘

同步文件：Free File Sync，NextCloud

远程使用：Keepass

不想装 pad：WinHtTrack Website Copier，立创EDA

Windows 管理工具：Win32 Disk Imager，USB Burning Tool，Fiddler

文档编辑：Notepad++，OneNote，印象笔记

Postman

Comics++

XShell

WSL