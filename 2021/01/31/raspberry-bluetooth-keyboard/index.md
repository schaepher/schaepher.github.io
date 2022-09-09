# 通过树莓派把 USB 键盘变成蓝牙键盘


# 完整代码

[https://github.com/schaepher/keyboard_mouse_emulate_on_raspberry](https://github.com/schaepher/keyboard_mouse_emulate_on_raspberry)

# 大致流程

```
    Bluetooth Keyboard
+------------------------+
|                        |
|   +-----------+        |
|   |    USB    |        |
|   | keyboard  |        |
|   +-----+-----+        |
|         | HID protocol |
|         v              |
|   +-----+-----+        |
|   |Linux input|        |
|   +-----+-----+        |
|         | event        |
|         v              |
|   +-----+-----+        |
|   |   evdev   |        |
|   +-----+-----+        |
|         |              |
|         v              |
|   +-----+-----+        |
|   |event code |        |
|   |    to     |        |
|   |  HID code |        |
|   +-----+-----+        |
|         | dbus         |
|         v              |
|   +-----+-----+        |
|   | Bluetooth |        |
|   | keyboard  |        |           +-----------+
|   | service   |        |           |  Windows  |
|   +-----+-----+        |           +-----+-----+
|         | send         |                 ^ HID protocol
|         v              |                 |
|   +-----+-----+        |           +-----+-----+
|   | Bluetooth |        |           | Bluetooth |
|   | service   |        | +-------> | service   |
|   +-----------+        |   L2CAP   +-----------+
|                        |
+------------------------+
```

<!-- more -->

主要做三件事：

1. 获取 Linux 的输入事件
2. 将输入事件转化为 HID 协议的数据
3. 将转换后的 HID 协议的数据发送到蓝牙服务

下面会先测试获取输入事件和发送数据到蓝牙，即输入输出。然后再处理数据转换。

# 安装依赖

```bash
sudo apt-get install libbluetooth-dev python-gobject bluez bluez-tools bluez-firmware python-bluez python-dev python-pip
pip install pybluez evdev pydbus future
```

# 获取 Linux 的输入事件

当我们直接用 USB 键盘插入到使用 Linux 系统的树莓派上的之后，键盘的输入将会通过 Linux 的输入子系统，以事件的形式发送出去。

我们可以使用 evdev 这个库来监听这些事件。

> evdev 官方文档见：
> https://python-evdev.readthedocs.io/en/latest/usage.html

### 输入事件获取测试

分两步：
1. 查看有哪些输入设备，选择其中一个
2. 获取选择设备的事件，并把事件打印出来

查看设备列表：

```python
import evdev
devices = [evdev.InputDevice(path) for path in evdev.list_devices()]
for device in devices:
    print(device.path, device.name, device.phys)
```

会有类似以下的输出：

```bash
/dev/input/event1    USB Keyboard        usb-0000:00:12.1-2/input0
/dev/input/event0    USB Optical Mouse   usb-0000:00:12.0-2/input0
```

选择键盘输入：

```python
import evdev
device = evdev.InputDevice('/dev/input/event1')
print(device)

for event in device.read_loop():
    print(evdev.categorize(event))
```

> 如果有多个 Keyboard，则需要一个个尝试。

此时按键盘，屏幕将会有输出。例如：

```
event at 1612004615.311680, code 04, type 04, val 458756
key event at 1612004615.311680, 30 (KEY_A), down
synchronization event at 1612004615.311680, SYN_REPORT 
key event at 1612004615.576959, 30 (KEY_A), hold
synchronization event at 1612004615.576959, SYN_REPORT 
key event at 1612004615.616967, 30 (KEY_A), hold
synchronization event at 1612004615.616967, SYN_REPORT 
event at 1612004615.856933, code 04, type 04, val 458756
key event at 1612004615.856933, 30 (KEY_A), up
synchronization event at 1612004615.856933, SYN_REPORT
```

# 发送数据到蓝牙服务

### 启动蓝牙并设置为键盘服务

`hciconfig` 命令用于控制蓝牙**设备**。

`/etc/init.d/bluetooth` 用于控制蓝牙**服务**。

首先确保蓝牙设备已被关闭，然后启动蓝牙服务。

```bash
sudo hciconfig hci0 down
sudo /etc/init.d/bluetooth start
```

现在再次启动蓝牙设备：

```bash
sudo hciconfig hci0 up
# 将蓝牙类型设置为键鼠设备
sudo hciconfig hci0 class 0x0025C0
# 设置蓝牙名称
sudo hciconfig hci0 name my-keyboard
# 让其他蓝牙设备可以发现这个蓝牙设备
sudo hciconfig hci0 piscan
```

### 配置蓝牙服务

Linux 的官方蓝牙协议栈是 BlueZ，我们需要对 BlueZ 做一些配置。一共有两个必要的配置：UUID 和 ServiceRecord。

如果不配置 ServiceRecord，那么连接后键盘的输入会混乱。比如在 Windows 上按 d 这个按钮，会变成 Win + d。

ServiceRecord 是一个 xml 格式的数据。具体内容可以先不理解，直接用就行。内容如下：

sdp_record.xml
```xml
<?xml version="1.0" encoding="UTF-8" ?>

<record>
	<attribute id="0x0001">
		<sequence>
			<uuid value="0x1124" />
		</sequence>
	</attribute>
	<attribute id="0x0004">
		<sequence>
			<sequence>
				<uuid value="0x0100" />
				<uint16 value="0x0011" />
			</sequence>
			<sequence>
				<uuid value="0x0011" />
			</sequence>
		</sequence>
	</attribute>
	<attribute id="0x0005">
		<sequence>
			<uuid value="0x1002" />
		</sequence>
	</attribute>
	<attribute id="0x0006">
		<sequence>
			<uint16 value="0x656e" />
			<uint16 value="0x006a" />
			<uint16 value="0x0100" />
		</sequence>
	</attribute>
	<attribute id="0x0009">
		<sequence>
			<sequence>
				<uuid value="0x1124" />
				<uint16 value="0x0100" />
			</sequence>
		</sequence>
	</attribute>
	<attribute id="0x000d">
		<sequence>
			<sequence>
				<sequence>
					<uuid value="0x0100" />
					<uint16 value="0x0013" />
				</sequence>
				<sequence>
					<uuid value="0x0011" />
				</sequence>
			</sequence>
		</sequence>
	</attribute>
	<attribute id="0x0100">
		<text value="Raspberry Pi Virtual Keyboard" />
	</attribute>
	<attribute id="0x0101">
		<text value="USB > BT Keyboard" />
	</attribute>
	<attribute id="0x0102">
		<text value="Raspberry Pi" />
	</attribute>
	<attribute id="0x0200">
		<uint16 value="0x0100" />
	</attribute>
	<attribute id="0x0201">
		<uint16 value="0x0111" />
	</attribute>
	<attribute id="0x0202">
		<uint8 value="0xC0" />
	</attribute>
	<attribute id="0x0203">
		<uint8 value="0x00" />
	</attribute>
	<attribute id="0x0204">
		<boolean value="false" />
	</attribute>
	<attribute id="0x0205">
		<boolean value="false" />
	</attribute>
	<attribute id="0x0206">
		<sequence>
			<sequence>
				<uint8 value="0x22" />
				<text encoding="hex" value="05010906a101850175019508050719e029e715002501810295017508810395057501050819012905910295017503910395067508150026ff000507190029ff8100c005010902a10185020901a100950575010509190129051500250181029501750381017508950305010930093109381581257f8106c0c0" />
			</sequence>
		</sequence>
	</attribute>
	<attribute id="0x0207">
		<sequence>
			<sequence>
				<uint16 value="0x0409" />
				<uint16 value="0x0100" />
			</sequence>
		</sequence>
	</attribute>
	<attribute id="0x020b">
		<uint16 value="0x0100" />
	</attribute>
	<attribute id="0x020c">
		<uint16 value="0x0c80" />
	</attribute>
	<attribute id="0x020d">
		<boolean value="false" />
	</attribute>
	<attribute id="0x020e">
		<boolean value="false" />
	</attribute>
	<attribute id="0x020f">
		<uint16 value="0x0640" />
	</attribute>
	<attribute id="0x0210">
		<uint16 value="0x0320" />
	</attribute>
</record>
```

配置：

```python
import dbus

bus = dbus.SystemBus()
bluez = bus.get_object("org.bluez", "/org/bluez")
manager = dbus.Interface(bluez, "org.bluez.ProfileManager1")

f_sdp = open("./sdp_record.xml", "r")
opts = {
    "AutoConnect": True,
    "ServiceRecord": f_sdp.read()
}
uuid = "05262649-d40f-483d-b445-73b000d19028"
manager.RegisterProfile("/org/bluez/hci0", uuid, opts)
```

### 创建服务器接收请求

1. 创建蓝牙 Socket
2. 等待连接

蓝牙需要创建两个 Socket，分别是控制管道 (control) 和中断管道 (interrupt)。其中 interrupt 用于发送数据。

> https://blog.csdn.net/zhoutaopower/article/details/82469665  
> 控制管道主要用于下面3个方面：  
> - 接收/响应USB主机的控制请求以及相关的类数据  
> - 在USB主机查询时传输数据（如响应Get_Report请求等）  
> - 接收USB主机的数据  
> 中断管道主要用于下面两个方面：  
> - USB主机接收USB设备的异步传输数据
> - USB主机发送有实时性要求的数据给USB设备

以下端口要与 sdp_record 里面配置的一致。

```python
import socket

PORT_CTRL = 17
s_control = socket.socket(socket.AF_BLUETOOTH, socket.SOCK_SEQPACKET, socket.BTPROTO_L2CAP)
s_control.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
s_control.bind((socket.BDADDR_ANY, PORT_CTRL))
s_control.listen(5)
conn_control, addr_info = s_control.accept()

PORT_INTR = 19
s_interrupt = socket.socket(socket.AF_BLUETOOTH, socket.SOCK_SEQPACKET, socket.BTPROTO_L2CAP)
s_interrupt.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
s_interrupt.bind((socket.BDADDR_ANY, PORT_INTR))
s_interrupt.listen(5)
conn_interrupt, addr_info = s_interrupt.accept()

# 13 是按键 j
message = [ 0xA1, 1, 0, 0, 13, 0, 0, 0, 0, 0 ]
conn_interrupt.send(bytes(message))

message = [ 0xA1, 1, 0, 0, 0, 0, 0, 0, 0, 0 ]
conn_interrupt.send(bytes(message))
```

发送给蓝牙的数据是 HID 协议格式的数据。

第一个数字表示这是一个输入报告。二进制表示为 10100001，前面的 101000 表示 Collection ，后面的 01 表示 Application (mouse, keyboard)。

第二个数字当 1 时表示键盘，2 时表示鼠标。

第三个数字表示 Modifier Keys。二进制的 8 个 bit 分别代表：左 ctrl, 左 shift, 左 alt， 左 Win， 右 ctrl, 右 shift, 右 alt， 右 Win

第四个数字是保留字符。  

最后六个数字分别代表一个普通按键。例如数字键和字母键。这就表示一次按下最多有效的普通按键是 6 个。

> https://www.usb.org/document-library/device-class-definition-hid-111  
> 可下载 pdf 文档。  
> 第一个数字的解释来自于： 6.2.2.4  Main Items  
> 第二个数字的解释来自于： 4.3  Protocols  
> 第三个开始的数字的解释来自于：Appendix B: Boot Interface Descriptors
