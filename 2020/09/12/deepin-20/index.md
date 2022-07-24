# deepin 20(深度系统社区版)


## 桌面使用

#### 1. 任务栏

Windows 样式：

右键任务栏 | 模式|高效

任务栏放在屏幕下方：

右键任务栏 | 位置|下

<!-- more -->

#### 2. 输入法

右键任务栏输入法图标

输入法 | 注：仅保留 “拼音” 和 “键盘” 两项

全局配置 | 快捷键 | 切换激活/非激活输入法 | 左 shift

全局配置 | 快捷键 | 额外的激活输入法快捷键 | 禁用

全局配置 | 快捷键 | 上一页 | , 

全局配置 | 快捷键 | 下一页 | .

全局配置 | 快捷键 | 显示高级选项 | 注：尽量清除其他所有快捷键，避免和其他快捷键冲突。方式是选中后按 Esc。

#### 3. 文件管理器

隐藏系统盘：

`文件管理器右上角汉堡图标 | 设置 | 高级设置 | 其他 | 隐藏系统盘` 打勾

#### 3. 应用商店下载应用

- 微信
- 网易云音乐
- VS Code
- 迅雷 / Free Download Manager
- Chrome

#### 4. Chrome

关闭顶部标题栏：

配置 | 外观 | 使用系统标题栏和边框

#### 5. 其他软件

- 看图：XnView Multi Platform

#### 6. Surface Go 


## 类似 yum whatprovides

https://askubuntu.com/questions/481/how-do-i-find-the-package-that-provides-a-file

```
sudo apt-get install apt-file
sudo apt-file update
apt-file find kwallet.h
```

## 桌面快捷方式

```
[Desktop Entry]
Exec=xfreerdp /u:username -wallpaper -themes +clipboard /sec:nla /w:1920 /h:1080 /v:192.168.1.1
Icon=dde-file-manager
Terminal=true
Type=Application
```
