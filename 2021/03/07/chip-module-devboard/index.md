# 芯片、模组、开发板以及业余爱好者如何选择


## 芯片

芯片又称为集成电路（Integrated Circuit，IC），处理器是一种芯片，CPU 一种处理器[[1][1]]。

通常我们看到的芯片是经过封装的，目前主流的封装类型有 SOP 、 QFN 、 BGA 三种[[2][2]][[3][3]]。下面会展示经过不同方式封装的芯片。

<!-- more -->

### 中央处理器

中央处理器（Central Processing Unit，CPU）是一种芯片。

下图是经过 DIP 封装的 Intel 8086 CPU。

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307145715371-1866906600.jpg)
> 图 1：Intel 8086 CPU

### 单片机

单片机又称为微控制单元（MicroController Unit，MCU），在处理器的基础上集成了 ROM、RAM、计数器等芯片。单片机也是芯片。

例如下图是经过 QFN 封装后的 ESP32 MCU[[4][4]]：

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307143543719-106384166.png)
> 图 2：ESP32 的正面和背面

ESP 32 的内部[[5][5]]：

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307145829878-1992424588.png)
> 图 3：ESP32 的内部

可以看到 ESP32 使用的是 Xtensa 的 32 位处理器[[6][6]]，内部含有 448KB ROM 和 520KB RAM。

虽然 ESP32 支持 WiFi 和蓝牙，但这个芯片本身并不能直接发送 WiFi 和蓝牙信号。

## 模组

模组由芯片和外围设备组成。例如 ESP32-WROOM-32 模组[[7][7]]：

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307145947485-480523055.jpg)
> 图 4：ESP32-WROOM-32 模组的正面和背面

ESP32-WROOM-32 模组在 ESP32 芯片的基础上添加了 4MB 的闪存（Flash） 、 MIFA 天线[[8][8]][[9][9]]（发送蓝牙和 WiFi 信号）、 40 MHz 晶振等等[[10][10]]。

顺便提一句，模组顶部的那个弯弯曲曲的就是 MIFA 天线（板载天线）。另一种模组 ESP32-WROOM-32U 使用的是 U.FL 天线，如下图右上角是一个 U.FL 天线座，使用时需要接上一条天线。

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307150115406-1781381210.jpg)
> 图 5：ESP32-WROOM-32U 模组的正面

可以直接把程序通过串口写入模组，不过需要自己买 USB 转串口工具。

## 开发板

开发版主要是用于开发测试，测试完毕后再换成模组，将模组集成到最终的线路板上。

开发板通常添加了 USB 转串口编程接口（也可用于供电）、按钮、LED 灯等组件。

下图是 ESP32 DevKitC V4 开发板[[11][11]]：

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307150225092-1340378716.jpg)
> 图 6：ESP32 DevKitC V4 开发板的正面

## 业余爱好者如何选择

对于只是自己做点东西玩的非专业人士，最好一开始就买开发板，不要因为模组体积小就选择它。

选开发板至少有以下几个好处：

1. 不用自己买 USB 转串口工具，只要有 USB 线就行了  
   而且就算自己买了 USB 转串口工具，还需要面对选择引脚高低电平表示下载模式（刷入固件）还是工作模式。  
   开发板上有按键可以完成这种切换，例如 ESP32 DevKitC V4 开发板的 Boot Button。
2. 买模块的时候可能买到只有少数几个 GPIO 引脚的模组。  
   GPIO 比较麻烦的一点是在使用时需要先选择 IO 引脚，例如选择 5，那就是让 GPIO = IO5。  
   上面的 ESP32-WROOM-32 模组的背面可以看到有多个 IO 引线，不需要像 GPIO 那样还需要先选择。  
3. 网络上大多数教程都基于开发板  

总的来说，最主要的还是避免因各种麻烦让信心受到打击。等做出一些东西后，再考虑自制 PCB 板放模组，缩小体积。

## 参考

```
[1]: https://blog.csdn.net/weixin_41939983/article/details/105893225 (半导体元件、芯片、处理器、CPU、MCU的区别)
[2]: http://www.openpcba.com/web/contents/get?id=278 (BGA、QFN、SOP，不同封装，怎么使用？-燚智能硬件开发周教授)
[3]: https://blog.csdn.net/LEON1741/article/details/104783084 (浅谈各种常见的芯片封装技术DIP/SOP/QFP/PGA/BGA)
[4]: https://blog.csdn.net/wangyx1234/article/details/107300913 (芯片、模组、开发板的区别与联系-结合ESP32浅谈)
[5]: https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_cn.pdf (ESP32 系列芯片 技术规格书)
[6]: https://blog.csdn.net/whatday/article/details/87268727 (XTENSA处理器介绍)
[7]: https://docs.espressif.com/projects/esp-idf/zh_CN/latest/esp32/hw-reference/modules-and-boards.html#esp32-wroom-32 (ESP32 系列模组和开发板)
[8]: https://blog.csdn.net/ASKLW/article/details/99687718 (PCB天线知识)
[9]: https://www.cypress.com/file/437221/download (天线设计和射频布局指南)
[10]: https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_cn.pdf (ESP32­-WROOM­-32 技术规格书)
[11]: https://docs.espressif.com/projects/esp-idf/zh_CN/latest/esp32/hw-reference/esp32/get-started-devkitc.html#id5 (ESP32-DevKitC V4 入门指南)
```

[1]: https://blog.csdn.net/weixin_41939983/article/details/105893225 (半导体元件、芯片、处理器、CPU、MCU的区别)
[2]: http://www.openpcba.com/web/contents/get?id=278 (BGA、QFN、SOP，不同封装，怎么使用？-燚智能硬件开发周教授)
[3]: https://blog.csdn.net/LEON1741/article/details/104783084 (浅谈各种常见的芯片封装技术DIP/SOP/QFP/PGA/BGA)
[4]: https://blog.csdn.net/wangyx1234/article/details/107300913 (芯片、模组、开发板的区别与联系-结合ESP32浅谈)
[5]: https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_cn.pdf (ESP32 系列芯片 技术规格书)
[6]: https://blog.csdn.net/whatday/article/details/87268727 (XTENSA处理器介绍)
[7]: https://docs.espressif.com/projects/esp-idf/zh_CN/latest/esp32/hw-reference/modules-and-boards.html#esp32-wroom-32 (ESP32 系列模组和开发板)
[8]: https://blog.csdn.net/ASKLW/article/details/99687718 (PCB天线知识)
[9]: https://www.cypress.com/file/437221/download (天线设计和射频布局指南)
[10]: https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_cn.pdf (ESP32­-WROOM­-32 技术规格书)
[11]: https://docs.espressif.com/projects/esp-idf/zh_CN/latest/esp32/hw-reference/esp32/get-started-devkitc.html#id5 (ESP32-DevKitC V4 入门指南)
