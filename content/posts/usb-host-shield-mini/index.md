---
title: 给模块添加 USB 支持的 USB Host Shield Mini
date: 2021-03-07 21:03:00
updated: 2021-03-14 16:11:00
tags:
- Board
- USB
---

## 简介

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210314062438236-1684400332.png)
> 图 1：USB Host Shield Mini

USB Host Shield Mini 是一块基于 `MAX3421E 芯片` 的模组。MAX3421E 芯片是带 SPI 接口既可以用作外设也可以用作主机的的 USB 2.0 控制器[[1][1]][[2][2]]。

<!-- more -->

> 不想每次都输入一大段名字，下面用缩写 UHS 表示 USB Host Shield Mini。

对于要扩展 USB 通信功能的模组来说，需要使用 SPI 协议[[3][3]]与 UHSM 通信。

UHSM 是 USB Host Shield 的简化版本，拥有更小的体积，避免成品体积过大。

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210314062507618-2017542697.png)
> 图 2：USB Host Shield

体积小是优点，缺点是网络上比较难找到各个焊盘对应的引脚，只能自己标。

可以在 Arduino 上面找到这块板的资源[[4][4]]。在其他网站上面有 Mini 的资源[[5][5]]，不过 PCB 板的文件版本过老，打不开。

于是我决定先把这个缺点干掉。

## 引脚与焊盘的对应关系

板上大多数孔都直接连接到了中间的芯片，芯片上写着 MAX3421E 。

找到 MAX3421E 芯片的官方网站：

> [https://www.maximintegrated.com/cn/products/interface/controllers-expanders/MAX3421E.html](https://www.maximintegrated.com/cn/products/interface/controllers-expanders/MAX3421E.html)

里面的【下载数据手册】可以查看芯片引脚信息。以下引脚图来自数据手册：

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210314062546159-1044868231.png)
> 图 3：MAX3421E 芯片引脚图

现在需要把引脚的关系对应起来。注意到 Mini 板上背面有一个 RST，这是 Reset 的缩写。从图 3 中找到 RES（也是 Reset 的缩写），就是芯片右侧从下往上数第四根引脚。

回到板上找到连接 RST 焊盘的导线连接的引脚，会发现如果旋转到如图 4 的角度，就能和芯片图对上。

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210314063118514-712883056.png)
> 图 4：UHSM 模组焊盘与芯片引脚对应

把正背面的**过孔**[[6][6]]对应起来：

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210314063217228-315204136.png)
> 图 5：UHSM 正背面过孔对应

注意，图 5 中左边的那些 VBUS、INT、GPX、MAX_RST、SS 都是对焊盘的标记，跟它们所覆盖到的导线没有关系。

根据过孔的对应关系推出正背面导线的连接关系，把各个焊盘对应的引脚标注出来：

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210314063306362-1024972109.png)
> 图 6：UHSM 焊盘对应引脚名称

- `取反的 SS`、MOSI、MISO、SCLK 用于 SPI 通信[[3][3]]。
- INT 是用于 SPI 的可选项，用于发送中断（INTerrupt）信号，告知主设备有 USB 事件发生。

- VL 是逻辑电平[[7][7]]的参考电压，是 SPI 接口和所有其他数字输入及输出的参考电平。以 MAX3421E 用于 SPI 的输出引脚 MISO 为例子。在 VL ≥ 2.5V 且 VL 引脚电流为 +10mA 的时候，MISO 引脚的电压要高于 `VL-0.4` 才算输出高电平。

  从 USB Host Shield 的电路图来看（Mini 的看不了），MAX3421E 芯片的 Vcc 和 VL 用导线连接在一起，共同连接到 3.3V 的电源。

- GPIN 0~7 以及 GPOUT 0~7。对于一些不含 SPI 硬件接口的 SPI 主设备，跟这块芯片通信时需要使用 I/O 引脚模拟，占用了宝贵的 I/O 引脚资源。不过这个芯片提供了 8 个通用输入（GPIN）和 8 个通用输出（GPOUT），让 SPI 主设备不仅不会因为接入该芯片而减少总体 I/O 引脚数量，反而增加了。可以说是非常贴心。

- `取反的 RES` 为低时，会把一些寄存器的状态设置为默认状态。

- GPX 能表示五种信号，根据一个寄存器的某两个位选择（其中两种信号互斥，由另一个寄存器的某一位决定）。

## 从设备还是主设备？

它作为 USB 端的接收者，是 USB 主设备。同时它作为 SPI 数据发送方，是 SPI 从设备。

## SPI 通信

SPI 协议占用四个引脚，从设备选择（取反的 SS，Slave Select），时钟信号（SCLK），主设备输出（MOSI），从设备输出（MISO）。

关于 SPI 协议的介绍以及四个引脚的作用，可以看上一篇：

> [https://www.cnblogs.com/schaepher/p/14521055.html](https://www.cnblogs.com/schaepher/p/14521055.html) (设备间数据通信 —— 串行外设接口（SPI）协议)

文章中提到主设备在编程时，需要根据从设备的信息配置两个选项：

- SPI 模式
- First Bit

从数据手册[[1][1]][[2][2]]的SCLK（串行时钟）部分写着：
> MAX3421E 在 SCLK 的下降沿改变其输出数据（MISO），在 SCLK 的上升沿采样输入数据（MOSI）
 
因此主设备选 (0,0) 或者 (1,1) 都行。

数据手册的应用信息一节里的 SPI 接口部分写着：
> 所有 SPI 传送都是 MSB 在前

所以设置 First Bit 时，应设置为 MSB。

另外 MAX3421E 对 SCLK 最高频率限制在 26MHz。

## 供电

MAX3421E 的工作电压范围为 3.0V ~ 3.6V，通常约定使用 3.3V 的电源[[8][8]]。

由于 USB 外设（如键盘）的工作电压通常为 5.0V，因此不能使用板上提供的电压。

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210314064604707-657447566.png)
> 图 7：USB 四条导线及供电焊盘

USB 的 Vcc 连接着一个焊盘，即图 7 中标号 1 的地方。这个是 PCB 板设计者预留的一个供电口。

如果只需要 3.3V 的电源，则不需要任何改造，使用默认的导线即可。但如果需要更高的电压，则需要使用这个预留的供电口。

如果要使用这个供电口，则应先把原先的供电导线切断。如图 7 中的黄色标记所示，用小刀或者其他工具按照指示将导线切断。这样需要把 5.0V 的电源接到标号 1 的焊盘上。

在这样操作后，总共需要引入两个电压不同的电源到这块板上。一个 5.0V 的电源引到图 7 标号 1 的焊盘，另一个 3.3V 的电源引到 VL 焊盘。

## 编程

UHSM 自身不支持写入程序，但接入 UHSM 的模块（例如 Arduino、ESP32）在编程时可以使用 Github 上开源的库通过 SPI 协议操作 MAX3421E 芯片里的寄存器。

> [https://github.com/felis/USB_Host_Shield_2.0](https://github.com/felis/USB_Host_Shield_2.0) (USB_Host_Shield_2.0)

## 参考

```
[1]: https://datasheets.maximintegrated.com/cn/ds/MAX3421E_cn.pdf (MAX3421E 数据表（第三版）——中文)
[2]: https://datasheets.maximintegrated.com/en/ds/MAX3421E.pdf (MAX3421E 数据表（第四版）——英文)
[3]: https://www.cnblogs.com/schaepher/p/14521055.html (设备间数据通信 —— 串行外设接口（SPI）协议)
[4]: https://www.arduino.cc/en/Main/ArduinoUSBHostShield&lang= (Arduino USB Host Shield)
[5]: https://chome.nerpa.tech/downloads/#Arduino_USB_Host_Shield_Documentation (
Circuits@Home)
[6]: https://www.cnblogs.com/schaepher/p/14492102.html (快速了解线路板（PCB）基础知识)
[7]: https://baike.baidu.com/item/%E9%80%BB%E8%BE%91%E7%94%B5%E5%B9%B3 (逻辑电平)
[8]: https://www.zhihu.com/question/22687846/answer/31508409 (为什么很多低功耗的芯片都采用3.3v的电源，这个电压有什么科学依据吗？)
```

其他：

https://www.pjrc.com/teensy/td_libs_USBHostShield.html  

https://www.itead.cc/wiki/Arduino_USB_Host_Shield

https://chome.nerpa.tech/arduino_usb_host_shield_projects/

[1]: https://datasheets.maximintegrated.com/cn/ds/MAX3421E_cn.pdf (MAX3421E 数据表（第三版）——中文)
[2]: https://datasheets.maximintegrated.com/en/ds/MAX3421E.pdf (MAX3421E 数据表（第四版）——英文)
[3]: https://www.cnblogs.com/schaepher/p/14521055.html (设备间数据通信 —— 串行外设接口（SPI）协议)
[4]: https://www.arduino.cc/en/Main/ArduinoUSBHostShield&lang= (Arduino USB Host Shield)
[5]: https://chome.nerpa.tech/downloads/#Arduino_USB_Host_Shield_Documentation (
Circuits@Home)
[6]: https://www.cnblogs.com/schaepher/p/14492102.html (快速了解线路板（PCB）基础知识)
[7]: https://baike.baidu.com/item/%E9%80%BB%E8%BE%91%E7%94%B5%E5%B9%B3 (逻辑电平)
[8]: https://www.zhihu.com/question/22687846/answer/31508409 (为什么很多低功耗的芯片都采用3.3v的电源，这个电压有什么科学依据吗？)