# OpenWRT NAS


1. 安装
   1. 安装 smb 服务  
      `opkg install samba36-server`
   2. 安装 LuCI 配置界面
      `opkg install luci-i18n-samba-zh-cn`

<!-- more -->

2. 配置服务器
   1. 创建账号并设置密码
   2. 创建组
   3. 给 Samba 添加账号密码
   4. 启动 Samba 服务
      `/etc/init.d/samba start`
   5. 设置开启自启动
      `/etc/init.d/samba enable`

3. 打开路由器 WEB 界面。进入【服务】->【网络共享】。
   添加一个共享目录。  
   名字随便填  
   目录选择路由器里的目录。这个目录要给刚才创建的账号读写权限。
   允许的用户填刚才创建的用户  
   权限掩码都填 777  
   保存

4. Windows 10 配置
   1. 在【启用或关闭 Windows 功能】，在【SMB 1.0/CIFS 文件共享支持】->【SMB 1.0/CIFS 客户端】选项前面打勾
   2. 重启 Windows 10
   3. 在【控制面板\用户帐户\凭据管理器】里点击【添加 Windows 凭据】
   4. 填完地址、用户名、密码后，点确定即可。
      这里的地址是路由器地址。或者打开 Windows 文件浏览器里左边菜单栏的【网络】里看到的名称。


参考：  

win10 无法访问samba，没有权限，登录会话解决: https://jingyan.baidu.com/article/c146541382b6950bfcfc4ca5.html
