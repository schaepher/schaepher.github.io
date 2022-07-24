# php+xdebug远程调试（单人）


## 目录

1. 服务器上安装 XDebug 及配置
1. 客户端 PHPstorm 配置
1. 浏览器安装插件

## 服务器上安装 XDebug 及配置

### XDebug 安装

略

### 配置：

打开 php.ini 配置文件：  
vim /etc/php.ini

在最后加上以下内容：

```
[Xdebug]
zend_extension="/usr/lib64/php/modules/xdebug.so"
xdebug.remote_enable=1
xdebug.remote_host="客户端IP地址"
xdebug.remote_port="客户端开启的端口"
```

端口可以自己选，例如选择 5566 端口。

设置完毕后，重启 web 服务。

注：这种方式不支持多人调试，是因为 remote_host 只能填一个 IP 地址。如果需要让团队内其他人也可以调试，参考： [php+xdebug+dbgp远程调试（多人）](http://www.cnblogs.com/schaepher/p/8939616.html)

## 客户端 PHPstorm 配置

![](https://images2018.cnblogs.com/blog/809218/201804/809218-20180425081105882-658573090.png)


设置端口，这里确保和 php.ini 里设置的端口号一致。如果端口没有打开，请按照 [该链接](http://www.xitongcheng.com/jiaocheng/win10_article_12908.html) 打开。

![](https://images2018.cnblogs.com/blog/809218/201804/809218-20180425081122438-206052258.png)

设置服务器。要记得先在服务器上安装 FTP（例如 vsftpd），并配置好。  
例如这里是假设创建了 xdebug 用户，并用该账号登录 192.168.1.100 这台机器。  
Root path 设置为你的项目（这里假设为 test）的根目录。  

![](https://images2018.cnblogs.com/blog/809218/201804/809218-20180425081130732-1304857235.png)

还是设置服务器，选择 Mappings 这个选项。在 Deployment path on server 这一栏填入斜杠即可。

开始监听 debug：  

![](https://images2018.cnblogs.com/blog/809218/201804/809218-20180425081139847-992432790.png)

## 浏览器安装插件

这里以 chrome 为例。  
进入 chrome 商店，搜索 Xdebug helper，安装该插件。或者点击直达链接：[Xdebug helper](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc)  

重启浏览器。  

右键点击 chrome 工具栏上的 Xdebug helper，选择 选项 。在 IDE key 那里选择 PHPstorm，点右边的 save。

## 加断点调试  

打开 PHPstorm ，在想要调试的地方打上断点。

进入想要调试的页面，左键点击 chrome 工具栏上的 Xdebug helper，选择 Debug。

刷新页面或者点击按钮触发请求，一旦有执行到打断点的那一行，就会停下来。如果是第一次， PHPstorm 会跳出一个窗口。

在 Configure local file path 里选择 Import mappings from deployment ，并在 Deployment 那里选择刚才配置的服务器。

点击 Accept。
