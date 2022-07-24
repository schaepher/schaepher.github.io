---
title: Docker Compose
date: 2019-10-11 10:22:28
updated: 2019-10-11 10:22:28
categories:
 - Learning Docker
tags:
 - Docker
 - Docker Compose
 - YAML
---


## Docker Compose 是用来做什么的

1. 最直接的就是把原先要在命令行跑容器所需的参数整合到一个文件（docker-compose.yaml）里面，组织起来。这样就不用怕忘记某个参数了。
2. 可以使用一行简单的命令（docker-compose）同时启动（up）、重启（restart）、关闭（stop）多个服务。

开发和测试环境使用另外安装的 `docker-compose` 命令，单机的生产环境也可用。  
生产环境的集群如果是 Docker Swarm，则使用 Docker 自带的 `docker stack deploy` 。  

<!-- more -->

## Docker Compose 和 Docker Stack 的区别和共同点

最显著的区别是：`docker-compose` 可以构建镜像，也可以使用已构建镜像，而 `docker stack deploy` 只能使用已构建镜像。

另外还有一些配置上的区别，后面会讲到。

他们有一个共同点，那就是服务的配置文件都是用 yaml （发音 /ˈjæməl/ ）语言写的。并且如果他们发现传入的配置文件中的配置不是自己支持的，会选择忽略。这样我们就可以把 Compose 和 Stack 的配置写在同一个文件。  

## 简单介绍 YAML 语法

> YAML 语言教程  
> [http://www.ruanyifeng.com/blog/2016/07/yaml.html](http://www.ruanyifeng.com/blog/2016/07/yaml.html)

- YAML 包含三种数据类型：标量、数组、对象  
- 使用缩进来区分配置块（类似于 Python）  
- 缩进只能使用空格  

> 标量类型有：字符串，布尔值，整数，浮点数，Null，时间（ISO8601），日期（ISO8601）  

```yaml
version: '3'
services:
  web:
    build: .
    ports:
    - "5000:5000"
    volumes:
    - .:/code
    - logvolume01:/var/log
    links:
    - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```

上面是 Docker 官方给出的 Compose 文件示例。  

其中 `version: '3'` 表示字段 version 的值为字符串的 3。  
> docker-compose 在读取 version 这个字段时，限制其类型必须为字符串，否则报错。  

继续往下看，字段值可以是一个 **对象**：  

```yaml
services:
  web:
    build: .
```

build 的值写的是一个标量：点，表示当前目录。  

像这种没有明显特征的都会被当做 **字符串**。  

继续往下看：  

```yaml
ports:
- "5000:5000"
```

这里 ports 的值是一个 **数组**。数组元素用一个减号开头。

继续往下：  

```yaml
volumes:
  logvolume01: {}
```

`{}` 表示空对象。顺便一提，`[]` 表示空数组。

## Docker Compose 文件的结构

```yaml
version: '3'
services:
  service-name1:
    build: .
  service-name2:
    image: redis

volumes:
  logvolume01: {}

networks:
  hostnet:

configs:
  my_first_config:

secrets:
  my_first_secret:
```

一个 docker-compose.yaml 文件中，通常至少包含：  

- version ：用于标识该文件使用的配置版本。不同版本的配置项有一些差异。
- services ：用于配置服务

version、services、volumes、networks、configs、secrets 这几个都属于顶层（top-level）配置，当前总共也就这几个。

具体 service 可以使用 volumes、networks、configs、secrets 定义的资源，不能在 service 里定义这些资源。

## 举个例子

// 待补充

## Docker Compose 和命令行参数的对应关系

|命令行|Docker Compose|值类型|
|:--|:--|:--|
|`-v`|volumes|对象数组或者字符串数组|
|`-p`|ports|对象数组或者字符串数组|
|`-l`|labels|对象或数组|
|`--expose`|expose|字符串数组|
|`-e`|environment|对象或数组|
|COMMAND|command|字符串或数组|

> 补充个命令行没有的：  
> entrypoint 字符串或数组

## Docker Compose 独用的 Service 选项

> 官方文档：  
> [https://docs.docker.com/compose/compose-file/#not-supported-for-docker-stack-deploy](https://docs.docker.com/compose/compose-file/#not-supported-for-docker-stack-deploy)


|选项|作用|Stack类似功能|
|:--|:--|:--|
|build|指定构建文件夹|无|
|container_name|指定启动后的容器名|无|
|restart|重启策略。no、always、on-failure、unless-stopped。设置为 always 会使得该服务在宿主机开机后启动。|restart_policy|
|tmpfs|映射目录到容器 tmp 目录||
|devices|映射外部设备（例如 USB）||
|links|连接到某个服务，会影响服务启动顺序。类似于修改 hosts 给依赖的服务添加别名。推荐用 network 代替 links||
|external_links|外部链接||
|cgroup_parent|||
|network_mode|||
|security_opt|||
|userns_mode|||

## Docker Stack 独用的 Service 选项

只有一个：deploy  

> 官方文档：  
> [https://docs.docker.com/compose/compose-file/#deploy](https://docs.docker.com/compose/compose-file/#deploy)

其子选项有：  

|选项|类型|作用|
|:--|:--|:--|
|restart_policy|Object|重启策略。condition: none、on-failure、any（默认，总是重启）|
|mode|String|设置服务部署模式。global 表示所有节点都部署，replicated 表示仅部署指定数量的节点|
|replicas|Integer|配置改服务部署多少个实例|
|placement|Object|见下|
|placement.constraints|`Array<String>`|只有满足条件的节点才会部署。例如：`engine.labels.operatingsystem == ubuntu 14.04`|
|placement.preferences|Object|分部模式。针对某个节点 label 的不同值做分部。当前策略只有 spread 一种，即平均分部|
|resources|Object|服务使用宿主机资源的限制。有 limit 和 reservations，分别代表和最小值|
|resources.limits|Object|允许使用的资源最大值|
|resources.reservations|Object|允许使用的资源最小值|
|labels|`Array<String>`|和 Dockerfile 的 LABLE 相似，但仅作用于服务的容器|
|endpoint_mode|String|设置 Virtual IP 或者 DNSRR|
|rollback_config|Object|服务升级失败时的回滚策略|
|update_config|Object|服务升级时的策略|

placement.constraints 选项具体见：  
> [https://docs.docker.com/engine/reference/commandline/service_create/#specify-service-constraints---constraint](https://docs.docker.com/engine/reference/commandline/service_create/#specify-service-constraints---constraint)

placement.preferences 示例：  

集群有 6 个节点，他们都有一个 lable 叫做 zone。条件形式为 node.labels.zone 。  
其中三个节点的 node.labels.zone=A  
两个节点的 node.labels.zone=B  
一个节点的 node.labels.zone=C  

要发布 9 个实例，设置 spread=node.labels.zone，就会给 A B C 每个分配三个实例。  
对于 A，会给每个节点一个实例。  
对于 B，会给一个节点两个实例，另一个节点一个实例。  
对于 C，会给这个节点三个实例。


## 很有用的配置 

### 服务启动先后顺序 —— depends_on

类型：`Array<String>`

如果 A depends_on B ,那么 B 就会先启动，之后再启动 A。
