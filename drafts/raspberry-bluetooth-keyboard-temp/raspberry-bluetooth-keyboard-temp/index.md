# 树莓派蓝牙键盘


# 配置

/etc/bluetooth/main.conf

将蓝牙配置为键盘模式：

Class = 0x000500

见：https://www.bluetooth.com/specifications/assigned-numbers/baseband/

| service class | major device class | minor device class | type |
| :------------ | :----------------- | :----------------- | :--- |
| 00000000001   | 00101              | 010000             | 00   |


比特位置关系：

| 23   | 22   | 21   | 20   | 19   | 18   | 17   | 16   | 15   | 14   | 13   | 12   | 11   | 10   | 9    | 8    | 7    | 6    | 5    | 4    | 3    | 2    | 1    | 0    |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 1    | 0    | 0    | 1    | 0    | 1    | 0    | 1    | 0    | 0    | 0    | 0    | 0    | 0    |


| 位置         | 值    | 作用                                       |
| :----------- | :---- | :----------------------------------------- |
| 13           | 1     | Limited Discoverable Mode                  |
| 12 11 10 9 8 | 00101 | Peripheral (mouse, joystick, keyboard, … ) |
| 7 6          | 01    | Keyboard                                   |

顺便一提，如果想要鼠标和键盘都可以，则将 7 和 6 都设置为 1。

# 启动蓝牙

```bash
systemctl restart bluetooth
bluetoothctl power on
bluetoothctl discoverable on
```

# 安装开发包

```bash
sudo apt-get install libbluetooth-dev python-gobject bluez bluez-tools bluez-firmware python-bluez python-dev python-pip
pip install pybluez evdev pydbus future
```

# 蓝牙服务测试

我们的流程是：

键盘 -A-> 树莓派(转换) -B-> 树莓派蓝牙 -C-> Windows 蓝牙

上面已经完成了 A 的部分，现在我们先跳过 B，测试一下 C。也就是在不依赖于上面的键盘事件的情况下，让 Windows 端收到一个键盘输入。

对于蓝牙这类系统服务，与其的通信应该通过系统的进程间通信。D-Bus 是消息总线系统。

我们的目标是获取蓝牙在消息总线上的通信对象，然后将键盘按键信息发送出去。

```python
from pydbus import SystemBus

# 获取系统级别的消息总线对象
system_bus = SystemBus()

# 从消息总线中获取蓝牙对象
bus.get('org.bluez')

# 循环监听或发送
from gi.repository import GLib

loop = GLib.MainLoop()
loop.run()
```

# 蓝牙服务端

我们要实现的是树莓派连接 USB 的键盘，键盘的输入最终到 windows。对于 Windows 来说，它是在跟蓝牙键盘通信。它需要主动连接蓝牙键盘。

此时蓝牙键盘作为蓝牙服务端。因此我们要在树莓派上面配置蓝牙服务端。

蓝牙设备有多种类型，由于我们想要将蓝牙设备当作键盘使用，所以在启动服务端的时候，应该将其设置为键盘类型。

在创建服务端的时候，有多种协议可选择：HCI, L2CAP, RFCOMM 和 SCO。其中 HCI 在链路层之上，L2CAP 在 HCI 层之上。RFCOMM 基于 L2CAP，用于串行设备。SCO 类似于 UDP，用于实时性高的场景。acl 类似 TCP。基于应用场景，选则 L2CAP 。

服务端通信的配置和 TCP 类似，用 socket 那套操作。

```python
import bluetooth
PORT_PSM_INTR = 0x13
server_sock = bluetooth.BluetoothSocket(bt.L2CAP)
server_sock.setblocking(False)
try:
    server_sock.bind(('', PORT_PSM_INTR))
except:
    print("For bluez5 add --noplugin=input to the bluetoothd commandline")
    print("Else there is another application running that has it open.")
    sys.exit(errno.EACCES)
server_sock.listen(1)

client_sock, address = server_sock.accept()
print("Accepted connection from", address)

data = client_sock.recv(1024)
print("Data received:", str(data))

while data:
    client_sock.send("Echo =>", str(data))
    data = client_sock.recv(1024)
    print("Data received:", str(data))

client_sock.close()
server_sock.close()
```

bluetooth 库要求安装 pybluez。

# 参考文章

https://projects-raspberry.com/emulate-a-bluetooth-keyboard-with-the-raspberry-pi/


# 基础知识

## Linux 输入子系统事件

当我们直接用 USB 键盘插入到使用 Linux 系统的树莓派上的之后，键盘的输入将会通过 Linux 的输入子系统，以事件的形式发送出去。

因此我们需要先监听这个些事件。这里选择 evdev 这个库。

> evdev 官方文档见：
> https://python-evdev.readthedocs.io/en/latest/usage.html


```python
import evdev.ecodes
help(evdev.ecodes)
```


> 事件类型：  
> https://www.kernel.org/doc/html/latest/input/event-codes.html


## HID 协议

## BLE 蓝牙

蓝牙键盘是 BLE 设备。

BLE 不使用 socket 连接。

https://www.cnblogs.com/SA226343/p/5995674.html

https://www.cnblogs.com/SA226343/p/6019457.html

BLE 有两种通信，分别是有连接的通信和广播通信。

广播通信信道为 LE Advertisement Broadcast Channel，用于广播

有连接的通信信道 LE Piconet Channel 用在处于连接状态的蓝牙设备之间的通信

在通信过程中，使用 GATT 来通信。其中 Characteristic 表示一个特定的数据。

这样外围设备向中心设备发送 Characteristic 数据。如果外围设备是键盘，则把键盘的数据放到 Characteristic 的 Value 里面。

sudo busctl monitor org.bluez

```bash
sudo apt-get install libglib2.0 libboost-all-dev
sudo pip install gattlib
```
