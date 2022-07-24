---
title: wampserver3.0.6+花生壳（Windows端）
date: 2017-02-03 20:44:00
updated: 2017-02-03 20:44:00
categories:
 - Server
tags:
 - Server
---

### 下载

wampserver官网： http://www.wampserver.com/en/  

花生壳官网： http://hsk.oray.com/download/  
下载花生壳3最新版  

### 花生壳的配置

花生壳可注册和使用“免费版”，加引号是因为，整个过程下来仍然需要8块钱还是9块钱的费用（我注册的时候）  

注册完账号后，到软件界面点“域名列表”，注册个域名。可以选择免费的 `.imwork.net` 域名。  

注册完域名后，确保域名列表的界面“开启花生壳”是打开的状态。

如果**软件不能登录**，则按以下步骤操作：

1. 控制面板 -> 网络和 Internet -> 网络连接  

1. 选择当前连接的网络，右键 -> 属性 -> 双击图左红框部分，修改图右部分：
 
    ![](http://images2015.cnblogs.com/blog/809218/201702/809218-20170203202926089-1229065485.png)


如果**能登录**，那么继续：  

1. 点击软件界面中间的“内网穿透”，进入网页  
1. 点击右上的“添加映射”  

    ![](http://images2015.cnblogs.com/blog/809218/201702/809218-20170203202941870-1692054814.png)

    > 使用windows时，可以通过cmd的ipconfig命令查看当前机器的ip地址  
    > 如果是给wampserver用的，上面不选“自定义端口”，而是选择“网站80端口”  
    
### wampserver的配置  

1. 打开其他机器对服务器的访问权限

    打开wampserver后，右下角单击wampserver图标：  

    ![](http://images2015.cnblogs.com/blog/809218/201702/809218-20170203203211792-74631282.png)

    打开httpd-vhosts.conf后，添加一行：  

    ```
    # Virtual Hosts
    #

    <VirtualHost *:80>
    	ServerName localhost
    	DocumentRoot D:/software/wamp64/www
    	<Directory  "D:/software/wamp64/www/">
    		Options +Indexes +Includes +FollowSymLinks +MultiViews
    		AllowOverride All
    		Require local
            # 添加下面这行
            Require all granted
    	</Directory>
    </VirtualHost>
    #
    ```

1. 安装Apache服务（如果未安装的话）    

    ![](http://images2015.cnblogs.com/blog/809218/201702/809218-20170203203011667-944373341.png)

    如果提示80端口被占用，则按以下步骤： 
     
    打开cmd，执行 `netstat -aon | findstr :80` 
    
    ![](http://images2015.cnblogs.com/blog/809218/201702/809218-20170203203022839-919133548.png)

    调出任务管理器：  
    
    ![](http://images2015.cnblogs.com/blog/809218/201702/809218-20170203203029323-1970536584.png)
    
    ![](http://images2015.cnblogs.com/blog/809218/201702/809218-20170203203035323-1867184400.png)
    
    右键关闭这个进程，再尝试安装服务。  
    
    如果仍然不行，则把所有名称为 `httpd.exe` 的进程关掉。

1. 安装MySQL服务（如果未安装的话）  

    略。
    
1. 启动服务  
    
    左键wampserver图标，“重新启动所有服务”
    
### 网页存放  

1. 打开目录：

    ![](http://images2015.cnblogs.com/blog/809218/201702/809218-20170203204446198-93160607.png)

1. 新建文件：  
    
    文件名：`index.html`
    
    内容：`hello world`
    
1. 打开浏览器访问：  

    ![](http://images2015.cnblogs.com/blog/809218/201702/809218-20170203204131323-786059447.png)
