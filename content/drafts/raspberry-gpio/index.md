---
title: 树莓派编程
date: 2019-10-06 09:10:52
updated: 2019-10-06 09:10:52
tags:
---

## GPIO 基础

在不依赖 SDK 的情况下操作 GPIO：

https://www.cnblogs.com/vamei/p/6751992.html

## GPIO 库 —— Wiring PI

http://wiringpi.com/

这是个 C 语言库。

Wiring PI 的官方库没有维护在 Github 上，但是有镜像仓库：

https://github.com/WiringPi/WiringPi

目前还没有添加树莓派 4 的识别，可参照：  

https://github.com/WiringPi/WiringPi/pull/65

你可以在下面这个链接里面找到其他语言对 Wiring PI 的包装：

https://github.com/WiringPi

C 语言和 Python 的示例：  

https://www.oschina.net/question/1425530_140979

## 编程要点

1. 树莓派有 40 个针脚（PIN），每个针脚的作用见针脚图  
   特别注意：5V 电源、接地针脚、GPIO 针脚
2. 使用 GPIO 针脚时，要先设置该针脚是用于读还是用于写
3. GPIO 有两种模式：板上（BOARD）模式和 BCM 模式。  
   两者的区别是 GPIO 编号和板上编号的对应关系不同。  
   非 GPIO 针脚不受影响。

