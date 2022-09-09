# Docker


### 安装

https://docs.docker.com/install/linux/docker-ce/centos/


### 配置国内镜像

```
vim /etc/docker/daemon.json
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
```

Error response from daemon: Get https://registry-1.docker.io/v2/: net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)

### 在运行时通过 envsubst 替换配置文件中的变量

CentOS 要安装 gettext 才能执行 envsubst

### 构建多种架构的镜像

https://engineering.docker.com/2019/04/multi-arch-images/

https://github.com/docker/buildx/#installing

### docker-compose 服务多实例


https://stackoverflow.com/questions/39663096/docker-compose-creating-multiple-instances-for-the-same-image  

https://pspdfkit.com/blog/2018/how-to-use-docker-compose-to-run-multiple-instances-of-a-service-in-development/

https://docs.docker.com/compose/reference/up/

