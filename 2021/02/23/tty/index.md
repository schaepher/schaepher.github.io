# 终端发展过程及 tty、pty、pts 的区别


终端是一种输入输出设备。把终端连接到计算机上，就可以跟计算机进行交互。当今个人电脑最常用的两种终端设备分别是作为输入终端的键盘以及作为输出终端的显示器。

<!-- more -->

## 各种概念的关系

在 Windows 上的 CMD、 Powershell、 XShell 或者 PuTTY 被称为终端模拟器（Terminal Emulator）。

使用终端模拟器登录到 Linux 时，使用的是伪终端（PTY，Pseudo TTY）。

伪终端分为主和从两个部分，与终端模拟器交互的部分是主（PTM，Pseudo TTY Master），与用户进程交互的部分是从（PTS，Pseudo TTY Master）。

与机器相连接的终端设备，被称为远程打字机（TTY，TeleTYpewriter）。

在 Linux 操作系统里面，物理设备被对应到 TTY 串口（TTYS，TTY Serial）上。将一套物理的终端设备模拟为多套终端设备，在系统里面表示为 TTY。

## 电报机

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307161520577-1397943523.jpg)
> 图 1：电报机

电报是一种最早用电的方式来传送信息的、可靠的即时远距离通信方式。

1837 年发展出了电报机以及电报系统[[1][1]]。电报机的发送设备只有一个发报按键（如图 1 所示），通过短按表示短信号（“.” 滴）和长按表示长信号（“-” 嗒）。发送方按下按键后，信号会立马发送出去，接收方很快就能收到消息。

将长短信号按照一定顺序排列得到不同的组合，这些组合可以各自对应一种信息，这些对应关系的对应表称为电码。最出名的电码是摩尔斯电码。

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307161758079-775168784.png)
> 图 2：摩尔斯电码表

有兴趣的话，可以听听看：

> 三分钟教你学会摩尔斯电码  
> https://www.bilibili.com/video/BV1Hk4y1y7RH

国际通用求救信号是 SOS，S 由三个“滴”表示，O 由三个“嗒”表示，则 SOS 的摩尔斯电码为 `...---...`（滴滴滴 嗒嗒嗒 滴滴滴） 。

电码只有包括滴、嗒、停顿等少数信息，因此需要发送者先 **人为地** 将字母转换为电码（编码），接收者再 **人为地** 将电码转换为字母（解码）。接收者需要带上耳机听电报音。

我们希望能有设备代替收发双方做编码和解码的工作，直接与 abcd 这种字母交互。于是找上了打字机。

## 机械打字机（typewriter）

第一台商业化的机械打字机出现于 1874 年[[2][2]]。打字机主要由键盘、印字机组成。键盘提供了更多地按键，包括了 26 个字母、数字和其他一些按键。

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307163117077-1132117036.jpg)
> 图 3：机械打字机

机械打字机通过机械的转动将字母打在纸上。如果你有看过《紫罗兰永恒花园》，女主的工作就是使用机械打字机帮别人写信。比如下面这个视频里的：

> 【开箱】我把京紫女主用的打字机给买回了家   
> https://www.bilibili.com/video/BV18W411v7x9

你会发现看到的打字机的键盘布局是 QWERT 布局。现在 QWERT 的键盘布局实际上是继承于机械式打字机。机械打字机使用 QWERT 布局是因为如果在机械式打字机上打字太快会发生卡壳，而这种布局能减缓使用者的打字速度。

> 如果看了打字机的使用过程，你就能知道现代换行用 `\r\n` 表示的含义了。  
> `\r` 表示 carriage return。carriage 的英文释义为 “A moving part of a machine that carries other parts into the required position”[[3][3]]。因此 carriage return 是让打字机印字时移动的那块返回到行首。   
> 接着由表示 Newline 的 `\n` 让印字机旋转到下一行。`\n` 也称为 line feed。  
> 因此文本编辑器里的 CRLF 是 carriage return + line feed 的缩写，表示 `\r\n`。

从机械打字机的使用者的角度看，按下字母 a 的按键后纸条上就显示 a，不需要使用者做编码和解码工作。这正好做电报机的编码解码器，只需要设计一个转换器，将字母按键的机械转换为对电报机的操作就行了。

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307165046211-42946595.png)
> 图 4：打字机、摩尔斯电报机发送器、电传打字机

## 电传打字机（teletypewriter，teleprinter）

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307165844348-2050817568.jpg)
> 图 5：电传打字机

首次用于发送电报的电传打字机出现于 1887 年[[4][4]]。它主要由键盘、印字机和收发报机等组成。看起来是打字机 + 电报机的组合对吧？

感受一下电传打字机的运行：  

> \[转载\]在30多年前的电传打字机上聊天是怎样一种体验?  
> https://www.bilibili.com/video/BV1Xx41137Tp  

电传打字机将信号通过收发报机发送出去。上面那个视频 04:04 时间点，能听到电报机的声音。虽然电传打字机也是用电报机，但它通常使用五单位电码（博多电码），而不是长短不一的摩尔斯电码。

电传打字机传送方式有两种：
- 一种可以看作电报的改进版，即连接的双方有一方按下按键时，会把电码立即传送到另一方的印字机上；
- 另一种用打字机把消息信号以在穿孔纸带[[5][5]]上凿孔，再把纸带放到发报器上发报（如图 5）。 

下面这个视频就是第二种方式的演示：

> Teletype Model 35ASR 电传打字机   
> https://www.bilibili.com/video/BV1Gt411B7Xf

如果只将电传打字机看作电报的改进版，你会发现少了个东西：看不到已经打了什么字。不过打字机自身有带打印功能，可以让打字机在收发报时将字打印在纸上。这个步骤称为“回显”。

由于电传打字机没有缓冲，如果发送方太快，接收方可能来不及打印。于是发送方允许接收方回传两个控制信号，一个告诉发送方停止发送，一个告诉发送方继续发送。现在这两个特性仍然被终端模拟器保留，快捷键分别是 `ctrl + s` 和 `ctrl + q`。这就是有时候按错按键发现终端模拟器“卡住了”的原因[[6][6]]。

随着技术的发展，计算机出现了。

## 把电传打字机改造为计算机的终端

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307172702581-549272830.png)
> 图 6：把电传打字机改造为计算机的终端

第一台计算机在 1946 年问世，但它是通过操作按钮来控制。不过后来的大型机发展到包含了控制台、终端和主机。控制台用于管理设备的硬件，终端则用于和计算机交互。这个时候现代键盘还没出现，用到的终端是从电传打字机改造而来的，而且和整台机器组合在一起。

UNIX 系统就是用电传打字机写出来的[[7][7]][[8][8]]。

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307173040436-2035014270.png)
> 图 7：Ken & Den

现在也可以把电传打字机接到电脑上作为输入终端和显示终端，只是需要调制解调器（modem，猫）连接到收发报机：

> 用电传打字机作为 Linux 的显示终端    
> https://www.bilibili.com/video/BV1aK4y187yp  

前面说过，计算机包含了控制台和终端，这两者在现在似乎没有区别，但以前是有区别的。如下图：

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307175521428-1704736372.png)
> 图 8：控制台和终端[[9][9]]

## 多终端

计算机数量少，运行的费用高，且一个终端未必能完全利用 CPU 资源。于是出现了分时操作系统，允许有多个终端，且可以是远程终端。这样可以在只有一台终端设备连接到计算机的情况下，模拟出有多套终端设备连接的样子。同时也可以让其他人付费通过远程使用多出来的终端。

在本地接多个终端的图片不好找，不确定下面这篇文章里的图片算不算：

![](https://img2020.cnblogs.com/blog/809218/202103/809218-20210307173958495-1561591420.png)
> 图 9：IBM System/390 [[10][10]]

硬件的部分就到这里，接下来是跟 Linux 操作系统相关的内容。

## 串行终端 ttyS (ls /dev/ttyS*)

Linux 系统里面有表示接入的硬件设备的文件，用 `ls /dev/ttyS*` 查看。这些文件与计算机的串口（serial port）对应。

## 终端 tty (ls /dev/tty) 和控制台 console (ls /dev/console)

在大型机时代，终端和控制台是分开的，分别表示一台物理设备，但现在两者的界线没有那么清晰。

tty 在经过模拟后得到多个虚拟设备，统称为虚拟终端，就好像有多套物理的输入输出设备，而 console 只有一个。

通过 `ls /dev/tty[0-9]*` 可以看到所有虚拟终端，将这个集合表示为 ttyN，其中 N 表示数字。用 `ctrl + alt` 加上 `F1` ~ `F6` 其中一个快捷键来切换到 tty1 ~ tty6。执行 `tty` 会显示当前所在 tty。

> 注：如果通过类似 XShell 的终端模拟器远程连接，得到的结果与上述不同。到伪终端的部分就知道为什么了。

你会发现少了 tty0。`/dev/tty0` 和 `/dev/console` 的行为类似，都是表示当前终端，但只允许操作系统和 root 用户写入数据。而对于普通用户，`/dev/tty` 这个文件就是表示当前终端，且当前用户可以写入数据。

如何使用“当前终端文件”？可以试试执行 `echo "test" > /dev/tty`。你会发现屏幕输出了 test。如果执行 `tty` 得到的是 `/dev/tty3`，那么执行 `echo "test" > /dev/tty3` 将得到相同结果。`/dev/tty` 是 `/dev/tty3` 的别名。

Linux 是多用户操作系统，可以切换到不同的终端登录不同的用户。执行 `ls -l /dev/tty[0-9]*` 能查看各终端的拥有者。例如执行 `ls -l /dev/tty3` 可以看到：

```
crw--w---- 1 schaepher tty 4,  3 Feb  24  12:20 /dev/tty3
```

这表示 schaepher 这个用户持有 `/dev/tty3` 这个设备。

到目前为止，仍然是使用文本终端，并且在虚拟出的多套输入输出设备中选择。通俗地说，一个屏幕同一时刻只能展示其中一个终端的输出。在有图形界面后，出现了如何在图形界面里使用文本终端的问题。也就是想让输出到某个设备的内容单独地展示在屏幕的某一块区域，以及聚焦到这块区域后，可以输入内容到设备。

我们希望在图形界面里单独创建一个进程，让它在屏幕的一块区域内作为文本终端运行，于是这个进程就作为一个终端模拟器来使用了。

说到终端模拟器，上述的虚拟终端就是经过模拟多套设备后得到的。不过问题是图形界面运行在用户空间，而终端模拟器运行在内核空间。我们需要将终端模拟器移动到用户空间，但同时又要避免用户空间绕过内核直接操作设备。

于是伪终端 pseudo tty 被发明出来解决这个问题。

## 伪终端 pty (ls /dev/pts/*)

伪终端被分为主（master）从（slave）两个部分。pty slave 用于模拟硬件文本终端设备，pty master 提供了一套终端模拟器进程控制 pty slave 的方法。

终端模拟器运行于用户空间，与 pty master 交互，pty master 再通过 LDISC 与 pty slave 交互，pty slave 再与用户进程交互。

例如登录到 Linux 图形界面后打开终端窗口执行 tty，可以得到 `/dev/pts/0`。或者使用 ssh 登录到远程服务器执行 tty，也会得到 `/dev/pts/某个数字`。这里的 pts 指的是 pty slave。

执行 `ls -l /dev/pts/` 能看到都有哪些用户使用了 pty。

## 参考

```
[1]: https://en.wanweibaike.com/wiki-Electrical_telegraph (Electrical telegraph)
[2]: https://en.wanweibaike.com/wiki-Typewriter (Typewriter)
[3]: https://www.lexico.com/search?utf8=%E2%9C%93&filter=en_dictionary&dictionary=en&s=t&query=carriage (carriage)
[4]: https://site.xavier.edu/polt/typewriters/tw-history.html (A Brief History of Typewriters)
[5]: https://www.ccf.org.cn/Computing_history/Updates/2020-09-10/720617.shtml (我的计算机收藏之旅（9）：你见过或没有见过的存储器)
[6]: https://unix.stackexchange.com/questions/137842/what-is-the-point-of-ctrl-s/137846#137846 (What is the point of Ctrl-S?)
[7]: https://www.bell-labs.com/usr/dmr/www/picture.html (An amusing photo)
[8]: https://www.zhihu.com/question/59318669/answer/164408260 (为何 Linux 的系统 API 相比 Win32 到处是缩写？有何优劣? 造成两者差别的原因是什么？)
[9]: https://www.cnblogs.com/pluse/p/6897830.html (关于Unix/Linux的终端、伪终端、控制台和shell)
[10]: https://servers.pconline.com.cn/gc/1202/2679853_5.html (人类登月不可或缺 大型机半个世纪发展史)
```

其他：

> Linux 终端(TTY)  
> [https://blog.csdn.net/smilefxx/article/details/102766993](https://blog.csdn.net/smilefxx/article/details/102766993)  
> Pseudo TTY  
> https://en.wanweibaike.com/wiki-Pseudo%20TTY  
> The TTY demystified  
> http://www.linusakesson.net/programming/tty  
> Linux TTY/PTS概述  
> [https://segmentfault.com/a/1190000009082089](https://segmentfault.com/a/1190000009082089)   
> 扫盲 Linux＆UNIX 命令行——从“电传打字机”聊到“shell 脚本编程”    
> [https://blog.csdn.net/JunSIrhl/article/details/104374649](https://blog.csdn.net/JunSIrhl/article/details/104374649)  

[1]: https://en.wanweibaike.com/wiki-Electrical_telegraph (Electrical telegraph)
[2]: https://en.wanweibaike.com/wiki-Typewriter (Typewriter)
[3]: https://www.lexico.com/search?utf8=%E2%9C%93&filter=en_dictionary&dictionary=en&s=t&query=carriage (carriage)
[4]: https://site.xavier.edu/polt/typewriters/tw-history.html (A Brief History of Typewriters)
[5]: https://www.ccf.org.cn/Computing_history/Updates/2020-09-10/720617.shtml (我的计算机收藏之旅（9）：你见过或没有见过的存储器)
[6]: https://unix.stackexchange.com/questions/137842/what-is-the-point-of-ctrl-s/137846#137846 (What is the point of Ctrl-S?)
[7]: https://www.bell-labs.com/usr/dmr/www/picture.html (An amusing photo)
[8]: https://www.zhihu.com/question/59318669/answer/164408260 (为何 Linux 的系统 API 相比 Win32 到处是缩写？有何优劣? 造成两者差别的原因是什么？)
[9]: https://www.cnblogs.com/pluse/p/6897830.html (关于Unix/Linux的终端、伪终端、控制台和shell)
[10]: https://servers.pconline.com.cn/gc/1202/2679853_5.html (人类登月不可或缺 大型机半个世纪发展史)
