# 锐捷Linux版的下载和使用（福大客户端）


1. 下载锐捷程序包  
    [点此下载](http://files.cnblogs.com/files/schaepher/Linux_V1.30.rar)  
    没有连接到锐捷里就进不了这个安装包的官方下载界面（好矛盾啊这个），所以我把它上传到博客园了。

2. 解压文件

    ```Shell
    schaepher:~$ cd Downloads/

    schaepher:~/Downloads$ ls

        Linux_V1.30.rar

    schaepher:~/Downloads$ rar x Linux_V1.30.rar

        RAR 5.30 beta 2   Copyright (c) 1993-2015 Alexander Roshal   4 Aug 2015
        Trial version             Type RAR -? for help


        Extracting from Linux_V1.30.rar

        // ... 中间太长省略

        All OK

    schaepher:~/Downloads$ ls

        Linux_V1.30
        Linux_V1.30.rar

    schaepher:~/Downloads$ cd Linux_V1.30/

    schaepher:~/Downloads/Linux_V1.30$ ls
        
        rjsupplicant

    schaepher:~/Downloads/Linux_V1.30$ cd rjsupplicant/

    schaepher:~/Downloads/Linux_V1.30/rjsupplicant$ ls

        README  rjsupplicant.sh  x64  x86
    ```

3. 修改脚本的可执行属性

    一开始 `rjsupplicant.sh` 是无法执行的，需要使用 `chmod a+x ./rjsupplicant.sh` 来修改可执行属性。  
    > 如果你的 bash 是有着色的，你会发现使用这个命令之前这个文件是白色的，而使用之后变为绿色。

    ```Shell
    schaepher:~/Downloads/Linux_V1.30/rjsupplicant$ sudo chmod a+x ./rjsupplicant.sh 

        [sudo] password for schaepher: 

    schaepher:~/Downloads/Linux_V1.30/rjsupplicant$ ls

        README  rjsupplicant.sh  x64  x86
    ```

4. 获取网络适配器名称

    ```Shell
    schaepher:~/Downloads/Linux_V1.30/rjsupplicant$ ifconfig -s
    Iface     后面还有一大堆
    enp8s0    后面还有一大堆
    lo        后面还有一大堆
    ```

    在 Iface 这一列下面选择一个。比如我选的是 enp8s0

4. 第一次登录

    ```Shell
    schaepher:~/Downloads/Linux_V1.30/rjsupplicant$ sudo ./rjsupplicant.sh -a 1 -n enp8s0 -d 1 -u 输入你的用户名 -p 输入你的密码 -S 1

    AuthMode    Wired Authentication
    Adapter     enp8s0
    UserName    显示你的用户名
    2017-03-16 10:07:26 Initializing.....
    2017-03-16 10:07:26 Lookup the switch...
    2017-03-16 10:07:26 Connecting radius server...
    2017-03-16 10:07:26 Authenticating now...
    2017-03-16 10:07:26 Geting IP Address...
    2017-03-16 10:07:29 Lookup the switch...
    2017-03-16 10:07:29 Connecting radius server...
    2017-03-16 10:07:29 Authenticating now...
    2017-03-16 10:07:29 Success
    2017-03-16 10:07:31 Management Tips:
                        福州大学官方论坛：  bbs.fzu.edu.cn 福州大学校园网报修电话:38
                        201299,38201295,网上报修http://59.77.132.125

    ```

    - `-a 1` ：表示使用有线的方式接入
    - `-n enp8s0` ：这个就是刚才获取的名称
    - `-d 1` ：设置为 1 表示从 dhcp 服务器获取 ip
    - `-u 输入你的用户名` 
    - `-p 输入你的密码`
    - `-S 1` :设置为 1 表示保存密码
    - 可以执行 `sudo ./rjsupplicant.sh --help` 来获取更详细的内容

1. 以后登录

    ```Shells
    schaepher:~/Downloads/Linux_V1.30/rjsupplicant$ sudo ./rjsupplicant.sh -u 你的用户名
    ```

1. 退出登录

    按一下 q 再按回车键

1. 在后台运行锐捷  

    如果按照上面的方法执行锐捷，它会占用一个 terminal 。如何在关闭 terminal 的情况下还能保持锐捷客户端的执行呢？  
    
    只需要在命令的最后面加上 `&` 就行了。

1. 免去每次输入用户名的麻烦

    创建一个脚本来执行。例如创建 `rjApplication.sh` 。  
    
    文件内容为：  
    ```Shells
    #!/bin/bash
    rjsupplicant的绝对路径/rjsupplicant.sh -u 你的用户名 & 
    ```

    你可以先进入 rjsupplicant 文件夹，执行 `pwd` 来获取绝对路径。

1. 在任何地方都可以启动锐捷  

    将 `rjApplication.sh` 脚本所在的目录添加到 PATH 里面。

    执行 `PATH=$PATH:脚本所在目录` 。

    添加完毕后，在任何地方执行 `sudo rjApplication.sh` 就能启动了。


