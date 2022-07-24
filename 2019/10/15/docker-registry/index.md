# Docker 镜像拉取失败的几种解决方法



方法总览：  

- 国内源
- nc + hosts
- Nginx 代理（需要 VPS）
- 官方 registry（需要 VPS，可缓存镜像）
- JFrog Artifactory（需要 VPS，可缓存镜像，需要许可证）

<!-- more -->

## Docker 拉取镜像的流程  

见官方：  
[https://docs.docker.com/registry/spec/auth/token/](https://docs.docker.com/registry/spec/auth/token/)

## 国内源

这个网上的介绍一大堆，不再重复。  

其中注意的是 Docker 官方在国内的镜像（https://registry.docker-cn.com）已经失效。

## nc + hosts

通过修改本地 hosts，将域名指向可以连接到的 IP。  

依次执行下面两条命令：

```bash
nc -v auth.docker.io 443
nc -v registry-1.docker.io 443
```

系统会尝试多个 IP ，直到超出重试次数或者找到能连接上的 IP。

成功的例子：  

```
nc -v auth.docker.io 443
Ncat: Version 7.50 ( https://nmap.org/ncat )
Ncat: Connected to 34.228.211.243:443.
```

失败的例子：  

```
nc -v auth.docker.io 443
Ncat: Version 7.50 ( https://nmap.org/ncat )
Ncat: Connection to 52.70.175.131 failed: Connection timed out.
Ncat: Trying next address...
Ncat: Connection to 52.55.198.220 failed: Connection timed out.
Ncat: Trying next address...
Ncat: Connection to 54.88.231.116 failed: Connection timed out.
Ncat: Trying next address...
Ncat: Connection to 52.87.94.70 failed: Connection timed out.
Ncat: Trying next address...
Ncat: Connection to 34.232.31.24 failed: Connection timed out.
Ncat: Trying next address...
Ncat: Connection to 52.2.186.244 failed: Connection timed out.
Ncat: Trying next address...
Ncat: Connection to 54.210.105.17 failed: Connection timed out.
Ncat: Trying next address...
Ncat: Connection timed out.
```

然后在 /etc/hosts 里面添加：  

```
ip1  auth.docker.io
ip2  registry-1.docker.io
```

ip1 和 ip2 替换为找到的 IP。

之后重启 Docker。

## Nginx 代理

> 没有试过

在 VPS 上搭 Nginx，做代理。

用到的镜像有：  

- nginx:alpine
- jwilder/nginx-proxy
- jrcs/letsencrypt-nginx-proxy-companion  
  可能要换另外一个镜像（paulczar/omgwtfssl），使用自签名证书。let's encrypt 应该不能申请这种官方的证书。  
  使用示例见：  
  https://github.com/nextcloud/docker/blob/master/.examples/docker-compose/with-nginx-proxy-self-signed-ssl/mariadb/fpm/docker-compose.yml

在 nginx:alpine 服务里，`/etc/nginx/conf.d/docker-proxy.conf` 写入：  

```
server {
    listen 80;
    server_name registry-1.docker.io;

    location / {
        proxy_pass https://registry-1.docker.io;
    }
}

server {
    listen 80;
    server_name auth.docker.io;

    location / {
        proxy_pass https://auth.docker.io;
    }
}
```

// 待补充

## 官方 registry

docker-compose.yml  

```yml
version: '3'

services:
    registry:
      image: registry:latest
      ports:
        - "5000:5000"
      restart: always
      volumes:
        - ./config.yml:/etc/docker/registry/config.yml
```

config.yml

```yml
version: 0.1
log:
  fields:
    service: registry
storage:
  cache:
    blobdescriptor: inmemory
  filesystem:
    rootdirectory: /var/lib/registry
http:
  addr: :5000
  headers:
    X-Content-Type-Options: [nosniff]
proxy:
  remoteurl: https://registry-1.docker.io
health:
  storagedriver:
    enabled: true
    interval: 10s
    threshold: 3
```

// 待补充

## JFrog Artifactory

// 待补充
