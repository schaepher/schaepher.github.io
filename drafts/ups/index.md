# 确保重要设备供电


## 减少电脑耗电

在断电后，需要让电脑尽可能少用电。

有两种方式：

- 休眠
- 关机

关机最省电，但需要主板支持 WOL（Wake-on-LAN）。休眠可以由 WOL 唤醒，也可以通过定时任务唤醒。

#### WOL 方式

WOL 方式要求直接用网线将路由器和电脑的网卡连接起来。

1. 开机时进入 BIOS  
   各种主板进入 BIOS 的按键不一样，大多是 Esc 和 F12 [[1][1]]。主要看开机时屏幕的提示。
1. 找到跟 WOL 相关的选项，设置为 ON 或者 Enable[[2][2]]  
   选项可以是以下的任意一种：  
   - "Wake PCI Card"
   - "Boot on LAN"
   - "PME Event WakeUp"
   - "Power On by PCI Card"
   - "Power On By PCI Devices"
   - "Wake-Up by PCI card"
   - "WakeUp by Onborad LAN"
   - "Resume by MAC LAN"
   - "Resume By PCI or PCI-E Ddevice"
1. 重启进入 Windows 系统
1. [Win 键 + r] 打开“运行”，输入 `devmgmt.msc` 并确定，这样进入了设备管理器。  
   在【网络适配器】里面找到有线网卡，通常名字包含 Realtek，对该网卡执行以下两个操作：  
   - [ 右键 | 属性 | 高级 ]，找到【关机 网络唤醒】和【魔术封包唤醒】，如果值不是“开启”，则应设置为“开启”。  
   - [ 右键 | 属性 | 电源管理 ]，【允许计算机关闭此设备以节约电源】和【允许此设备唤醒计算机】的前面都打上勾。
1. [Win 键 + r] 打开“运行”，输入 `control panel` 并确定，这样进入控制面板。  
   把查看方式从【类别】改为【大图标】，进入 [ 电源选项 | 选择电源按钮的功能 | 更改当前不可用的设置 ]，把【启用快速启动（推荐）】前面的勾去掉，保存修改。  
1. [Win 键 + r] 打开“运行”，输入 `cmd` 并确定，这样进入命令提示符。  
   执行命令 `ipconfig /all`，找到网卡的物理地址，大概是 `08:BA:AD:F0:00:0D` 这样的。复制下来。  
1. 关机
1. 在局域网内另一台机器上面，对刚才的物理地址发送魔术封包[[3][3]]。需要将这个 UDP 包发送到 9 这个端口。  
   可以用 https://github.com/sabhiram/go-wol 这个工具。如果之前安装过 go，那么直接执行以下命令就可以安装了：  
   ```bash
   go get github.com/sabhiram/go-wol/cmd/wol
   ```  
   然后执行唤醒命令：
   ```bash
   wol wake 08:BA:AD:F0:00:0D
   ```  
   此时可以看到刚才那台机器启动了。
1. （非必需）如果需要远程启动，则
    1. 需要有公网 IP
    2. 在路由器上，将目标机器的 IP 和 MAC 地址绑定起来
    3. 路由器将 9 这个端口映射到目标机器 IP 的端口 9 上面

#### 定时任务方式

看下面这篇就够了：

> [https://jingyan.baidu.com/article/4e5b3e1930bff091901e24d9.html](https://jingyan.baidu.com/article/4e5b3e1930bff091901e24d9.html) (利用任务计划实现计算机定时开关机(休眠唤醒))


[1]: https://www.cnblogs.com/awakenedy/articles/10688902.html (WOL（Wake On LAN - 局域网唤醒）外网唤醒 配置教程 — 远程开机)
[2]: https://zhuanlan.zhihu.com/p/183704557 (网络唤醒WOL（Wake On LAN）)
[3]: https://www.cnblogs.com/zhanggaoxing/p/9657545.html (网络唤醒（WOL）全解指南：原理篇)
