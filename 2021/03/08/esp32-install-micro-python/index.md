# ESP32 安装 MicroPython


## 安装 USB 转 TTL 芯片驱动

我的 ESP32 开发板用的 USB 转 TTL 芯片是 CH340，因此需要安装 CH340 的驱动。

CH340 芯片的官方网站是：

> http://www.wch.cn/product/CH340.html

Windows 驱动在以下页面下载：

> http://www.wch.cn/downloads/CH341SER_EXE.html

下载完后默认安装即可。如果提示失败，那就关掉程序重新打开。实在不行就重启操作系统再试。

<!-- more -->

安装后查看 Windows 能否识别。

1. 把 ESP32 开发板连接到 Windows。
2. 打开 Windows 的设备管理器，在【端口（COM 和 LPT）】底下可以看到 CH340，后面的 COM 带了个数字。  
   这个数字不固定，比如我的是 COM7，实际以设备管理器显示的为准。
3. 打开 Arduino 或者其他串口工具，选择刚刚看到的 COM 口进行连接，选择 115200 波特率。就可以看到输出了[^1]。  
    此时的输出可能是：

    ```
    rst:0x10 (RTCWDT_RTC_RESET),boot:0x13 (SPI_FAST_FLASH_BOOT)
    flash read err, 1000
    ets_main.c 371 
    ```

    现在可以忽略这个错误。

## 刷入 MicroPython 固件

第一步：下载 MicroPython 固件

进入 MicroPython 的官方网站下载页面：

> https://micropython.org/download/

找到 ESP32，例如 “Generic ESP32 module”。点进去。

> https://micropython.org/download/esp32/

找到 `Firmware with ESP-IDF`。这个表示它包含了 ESP 官方的 ESP-IDF[^2]，不用怕下载错。选择 bin 文件的方式：

- 如果买的开发板是基于 ESP32-WROVER 模组，则选择 GENERIC-SPIRAM，否则选 GENERIC。
- v 版本选最新，但不选包含 unstable 的 bin 文件，因为不稳定。

第二步：电脑安装 Python （不是 ESP32）。电脑如已安装 Python 则跳过。

Python 的官方网站：

> https://www.python.org/downloads/

随便下载个版本，最新的也行。按默认选项的安装。

可以先将软件源设置为清华大学的镜像（也可以不配置）：

```
pip install pip -U
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

第三步：安装 ESP 工具

通过 Python 的 pip 安装 ESP 工具。

```
pip install esptool
```

安装过程会出现以下内容：

```
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting esptool
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/dd/3d/d1d4c004927e6e6807c441ce70330ed969c725d2906053fbd2ff994b4439/esptool-3.0.tar.gz (149 kB)
     |████████████████████████████████| 149 kB 1.1 MB/s
Collecting bitstring>=3.1.6
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/c3/fc/ffac2c199d2efe1ec5111f55efeb78f5f2972456df6939fea849f103f9f5/bitstring-3.1.7.tar.gz (195 kB)
     |████████████████████████████████| 195 kB 6.4 MB/s
Collecting cryptography>=2.1.4
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/64/03/b2a66da95d0a0acac2b5348526f9b92302136563444b33c7049cbdfecf69/cryptography-3.4.6-cp36-abi3-win_amd64.whl (1.6 MB)
     |████████████████████████████████| 1.6 MB 6.4 MB/s
Collecting cffi>=1.12
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/aa/0c/20c3ccdb32fdf86e38901d548f0e11b47d7e037b95373efc1c2379129358/cffi-1.14.5-cp39-cp39-win_amd64.whl (179 kB)
     |████████████████████████████████| 179 kB 6.4 MB/s
Collecting ecdsa>=0.16.0
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/98/16/70be2716e24eaf5d81074bb3c05429d60292c2a96613a78ac3d69526a     |████████████████████████████████| 104 kB 6.4 MB/s
Collecting pyserial>=3.0
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/07/bc/587a445451b253b285629263eb51c2d8e9bcea4fc97826266d186f96f558/pyserial-3.5-py2.py3-none-any.whl (90 kB)
     |████████████████████████████████| 90 kB 2.6 MB/s
Collecting reedsolo<=1.5.4,>=1.5.3
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/c8/cb/bb2ddbd00c9b4215dd57a2abf7042b0ae222b44522c5eb664a8fd9d786da/reedsolo-1.5.4.tar.gz (271 kB)
     |████████████████████████████████| 271 kB 6.4 MB/s
Collecting six>=1.9.0
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/ee/ff/48bde5c0f013094d729fe4b0316ba2a24774b3ff1c52d924a8a4cb04078a/six-1.15.0-py2.py3-none-any.whl (10 kB)
Collecting pycparser
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/ae/e7/d9c3a176ca4b02024debf82342dab36efadfc5776f9c8db077e8f6e71821/pycparser-2.20-py2.py3-none-any.whl (112 kB)
     |████████████████████████████████| 112 kB 6.8 MB/s
Using legacy 'setup.py install' for esptool, since package 'wheel' is not installed.
Using legacy 'setup.py install' for bitstring, since package 'wheel' is not installed.
Using legacy 'setup.py install' for reedsolo, since package 'wheel' is not installed.
Installing collected packages: pycparser, six, cffi, reedsolo, pyserial, ecdsa, cryptography, bitstring, esptool
    Running setup.py install for reedsolo ... done
    Running setup.py install for bitstring ... done
    Running setup.py install for esptool ... done
Successfully installed bitstring-3.1.7 cffi-1.14.5 cryptography-3.4.6 ecdsa-0.16.1 esptool-3.0 pycparser-2.20 pyserial-3.5 reedsolo-1.5.4 six-1.15.0
```

看到 `Successfully installed` 表示安装成功。

使用这个工具查看 ESP32 的串口：

```
esptool.py chip_id
```

比如我的输出是：

```
esptool.py v3.0
Found 4 serial ports
Serial port COM7
Detecting chip type... ESP32
Chip is ESP32-D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
MAC: xx:xx:xx:xx:xx:xx
Uploading stub...
Running stub...
Stub running...
Warning: ESP32 has no Chip ID. Reading MAC instead.
MAC: xx:xx:xx:xx:xx:xx
Hard resetting via RTS pin...
```

`Serial port COM7` 表示 ESP32 在 COM7。

第四步：清除 ESP32 开发板的 flash 芯片已有的内容

这一步是为了确保 MicroPython 刷入 flash 时的成功率。

```
esptool.py --chip esp32 --port COM7 erase_flash
```

以上的 COM7 替换为设备管理器里显示的 ESP32 串口。下同，不赘述。

第五步：刷入 MicroPython

```
esptool.py --chip esp32 --port COM7 --baud 460800 write_flash -z 0x1000 D:\esp32-idf4-20210202-v1.14.bin
```

上面的 `D:\esp32-idf4-20210202-v1.14.bin` 换成刚才下载的 bin 文件的实际位置。

得到以下输出：

```
esptool.py v3.0
Serial port COM7
Connecting......
Detecting chip type... ESP32
Chip is ESP32-D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
MAC: xx:xx:xx:xx:xx:xx
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Compressed 1484624 bytes to 951640...
Wrote 1484624 bytes (951640 compressed) at 0x00001000 in 84.3 seconds (effective 140.9 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
```

中间需要等一阵子。

第六步：验证 MicroPython

现在，用串口工具连接到 ESP32。

如果没有什么反应，那么按一下 Enter 键看看。会出现：

```python
>>>
```

打印个 hello world：

```python
>>> print("hello world")
```

得到输出：

```python
hello world
```

## 参考

[^1]: http://www.1zlab.com/wiki/micropython-esp32/flash-firmware-windows10/ (Windows10下的固件烧录)
[^2]: https://docs.espressif.com/projects/esp-idf/zh_CN/latest/esp32/get-started/index.html (ESP-IDF 编程指南)
[^3]: https://docs.espressif.com/projects/esp-idf/zh_CN/latest/esp32/hw-reference/modules-and-boards.html#esp32-wrover (ESP32-WROVER 系列模组)
