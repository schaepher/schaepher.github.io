# uefi



如果 Bitlock 没有处于关闭状态，就去关闭 Security ，会导致每次 windows 登录时要求输入解锁密码(如果有登录 Windows 账号，则在 Windows 官网可查询)。这个在登录 Windows 后，进入配置界面关闭。

必须在 UEFI 配置中关闭 Security Boot，否则 Windows 无论如何都会使用默认的 Boot Manager。替换了也没用。

使用支持触屏的 rEFInd 来替换系统自带的 Boot Manager。

rEFInd 默认配置没有开启触屏，必须在 refind.conf 里面把 `enable_touch` 前的注释去掉。

<!-- more -->

## 安装到 SD 卡

在通过 U 盘安装 Android 时，平板电脑的 SD 卡可能识别不到。  

在设备列表界面按 CTRL + ALT + F2 打开新命令行界面，执行 `modprobe rtsx_pci_sdmmc` 之后，按 CTRL + ALT + F1 回到刚才的界面。

选择 `Detect Devices` ， SD 卡就出现了。选它安装。

https://igordc.com/2017/12/android-x86-on-sdcard-with-ntfs-secure-boot-uefi


## Android 启动

编辑启动项。

https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/adding-boot-entries

https://blog.csdn.net/iceteaset/article/details/51855280



