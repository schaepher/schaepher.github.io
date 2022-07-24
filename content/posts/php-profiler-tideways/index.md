---
title: PHP7 非侵入式性能分析工具套件 tideways & xhgui
date: 2019-08-16 11:46:52
updated: 2019-08-16 11:46:52
categories:
 - PHP
tags:
 - PHP
 - PHP7
 - Profile
---


https://hub.docker.com/r/sroze/tideways

https://github.com/sroze/dockerfiles/tree/master/tideways

https://blog.it2048.cn/article-tideways-xhgui/

两种方式：

1. Nginx 指定入口脚本
2. 开放端口，在插件里指定 tcp 连接

<!-- more -->

## 步骤

1. 安装 MongoDB
2. 安装 PHP tideways 模块并配置
3. 安装 PHP MongoDB 模块并配置
4. 安装 Xhgui
5. Nginx 配置将性能分析脚本附加到执行
6. Nginx 配置 Xhgui 网页访问

### 安装 PHP 源

https://rpms.remirepo.net/wizard/

```
yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install -y https://rpms.remirepo.net/enterprise/remi-release-7.rpm
yum install -y yum-utils
yum-config-manager --enable remi-php73
yum makecache fast
```

> 如果发现其他 repo 被关闭了。先执行 `yum repolist all`，看要开启哪些。然后执行 `yum-config-manager --enable xxx` 。

### 安装 PHP tideways 模块并配置

```bash
yum install -y php-devel

cd /tmp
curl -o xhprof.zip -L https://github.com/tideways/php-xhprof-extension/archive/master.zip
unzip xhprof.zip

cd php-xhprof-extension-master
phpize
./configure
make && make install
```

### 安装 PHP MongoDB 模块并配置

安装 MongoDB 模块：

yum install php-mongodb -y

不需要额外配置

### 安装 Xhgui

```
cd /tmp
curl -o xhgui.zip -L https://github.com/laynefyc/xhgui-branch/archive/master.zip
unzip -d / xhgui.zip 

cd /xhgui-branch-master
php install.php
```

如果有问题，用 composer 安装 `alcaeus/mongo-php-adapter` 。

### Nginx 配置将性能分析脚本附加到执行

将这一句加到 server 块：

```
fastcgi_param PHP_VALUE "auto_prepend_file=/xhgui-branch-master/external/header.php";
```

### Nginx 配置 Xhgui 网页访问

xhgui.conf

```
server {
    listen       80;
    server_name  xhgui.mydomain.net;
    root  /xhgui-branch-master/webroot;

    location / {
        index  index.php;
        if (!-e $request_filename) {
            rewrite . /index.php last;
        }
    }

    location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
}
```


### 初始化 mongo

```
use xhprof
db.results.ensureIndex( { 'meta.SERVER.REQUEST_TIME' : -1 } )
db.results.ensureIndex( { 'profile.main().wt' : -1 } )
db.results.ensureIndex( { 'profile.main().mu' : -1 } )
db.results.ensureIndex( { 'profile.main().cpu' : -1 } )
db.results.ensureIndex( { 'meta.url' : 1 } )
```