# ESP32 MicroPython


## 找到板子

先搜索到：https://www.banggood.com/LOLIN32-Lite-V1_0_0-WiFi-and-bluetooth-Board-Based-ESP-32-Rev1-MicroPython-4MB-FLASH-Module-p-1237861.html?akmClientCountry=CN&cur_warehouse=CN

再搜索到：https://smalldevices.com.au/products/wemos-lolin32-lite?variant=5091850682401

然后确定：https://www.wemos.cc/en/latest/

从 Edit on GitHub 进入 GitHub。

搜索：LOLIN32 Lite pdf

<!-- more -->

找到：

https://www.adrobotica.com/wp-content/uploads/2018/03/schematics_lolin32.pdf

https://skule.sormo.no/index.php/eshop/eshop-download-pdf?product_id=274

http://blog.pagefault-limited.co.uk/wemos-lolin32-pinout-vs-wemos-lolin32-lite-pinout

https://web.archive.org/web/20190105015433/https://wiki.wemos.cc/products:lolin32:lolin32_lite

https://web.archive.org/web/20190105005432/https://wiki.wemos.cc/_media/products:lolin32:sch_lolin32_lite_v1.0.0.pdf

## 板上元器件

### Micro USB

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210318003722334-596333408.png)

### CH340C （USB 转 TTL）

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210318015151669-2008962552.png)

http://www.wch.cn/download/CH340DS1_PDF.html

> CH340 芯片支持 5V 电源电压或者 3.3V 电源电压。当使用 5V 工作电压时，CH340 芯片的 VCC 引脚输入外部 5V 电源，并且 V3 引脚应该外接容量为 0.1uF 的电源退耦电容。当使用 3.3V 工作电压时，CH340 芯片的 V3 引脚应该与 VCC 引脚相连接，同时输入外部的 3.3V 电源，并且与 CH340 芯片相连接的其它电路的工作电压不能超过 3.3V。

图中 V3 和 Vcc 连接，因此该处使用 3.3V 电源。

### ME6211 （线性稳压器）

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210318014306780-371435881.png)

https://pdf.ic37.com/icpdf_datasheet_6/ME6211_datasheet_6920387/

从数据手册关于引脚的介绍来看，这里使用的是 SOT23-5。

对应选型应该是：ME6211C33MX。

不过我这块板上的是另一个线性稳压器 4B2X。

https://b2b.baidu.com/land?id=153794d074372de7ee5e9f947b68b0a610



### CJ2301 （PMOS 管）

https://item.szlcsc.com/9042.html

https://www.21ic.com/article/878884.html

https://blog.csdn.net/AirCity123/article/details/102810255

### TP4054 （锂电池充电控制电路）

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210318014435862-1055190168.png)


提供充电过充保护，充电电流设定。

http://www.tp-asic.com/te_product_a/2008-04-10/24.chtml

http://www.tp-asic.com/res/tp-asic/pdres/201203/tp4054_42.pdf


