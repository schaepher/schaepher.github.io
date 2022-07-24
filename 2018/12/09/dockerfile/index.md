# Dockerfile


Dockerfile 的官方文档：[https://docs.docker.com/engine/reference/builder/](https://docs.docker.com/engine/reference/builder/)

# 1 示例

当你想要一个镜像，但它没有办法满足你的所有要求时，就得在它的基础上做一些定制化的修改。此时就得用到 Dockerfile 。

你有两种选择：一种是获取这个镜像的原始 Dockerfile 文件，并在上面修改，从头开始构建镜像；另一种是直接指定已存在的镜像，并添加内容。  

<!-- more -->

例如 `schaepher/frps` 这个镜像：  

```Dockerfile
FROM alpine:latest

ENV FRP_VER 0.20.0
ENV FRP_FULL_VER frp_${FRP_VER}_linux_amd64

RUN cd /root \ 
    && wget https://github.com/fatedier/frp/releases/download/v${FRP_VER}/${FRP_FULL_VER}.tar.gz \
    && tar vxzf ${FRP_FULL_VER}.tar.gz \
    && rm ${FRP_FULL_VER}.tar.gz \
    && mv ${FRP_FULL_VER} frps \
    && rm -rf ./frps/frpc* ./frps/frps.ini

WORKDIR /root/frps

CMD [ "./frps", "-c", "./frps.ini" ]
```

由于 frp 自身不支持在读取配置文件的时候解析环境变量，因此无法在运行 Docker 镜像的时候指定环境变量来完成配置。  

有四种方式可以选择，最常用的一种就是写个 Dockerfile 把 `frps.ini` 文件复制到 `/root/frps/` 这个文件夹。如下所示：

```Dockerfile
FROM schaepher/frps

COPY frps.ini /root/frps/frps.ini
```

写完 Dockerfile 后，要把自己写好的 `frps.ini` 放到这个 Dockerfile 所在的文件夹。然后执行下面这个命令来构建一个新的镜像：  

```shell
docker build . -t frps
```

> 记住这个 frps 镜像，后面会用到

# 2 Dockerfile 解释

## 2.1 基于哪个基础镜像 —— FROM  

定义：`FROM <镜像>`  

用于指明在哪个镜像的基础上继续添加镜像层。  

例如第一个 Dockerfile 是基于 `alpine:latest` 这个镜像，并在构建后生成 `schaepher/frps` 这个镜像。  
接着第二个 Dockerfile 是基于 `schaepher/frps` 镜像，再继续构建生成 `frp` 这个镜像。  

我们可以通过下面这个命令来查看这个镜像的修改历史：  

```shell
$ docker history schaepher/frps
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
ed08390ad317        4 months ago        /bin/sh -c #(nop)  CMD ["./frps" "-c" "./frp…   0B
<missing>           4 months ago        /bin/sh -c #(nop) WORKDIR /root/frps            0B
<missing>           4 months ago        /bin/sh -c cd /root     && wget https://gith…   8.89MB
<missing>           4 months ago        /bin/sh -c #(nop)  ENV FRP_FULL_VER=frp_0.20…   0B
<missing>           4 months ago        /bin/sh -c #(nop)  ENV FRP_VER=0.20.0           0B
<missing>           5 months ago        /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B
<missing>           5 months ago        /bin/sh -c #(nop) ADD file:25f61d70254b9807a…   4.41MB
```

> Dockerfile 中的每个指令都会创建一个新的镜像层。

其中最底下两层是 `alpine:latest` ，再往上就和第一个 Dockerfile 所执行的一样了。

## 2.2 环境变量 —— ENV

定义：`ENV <varname> <value>`

用于设置环境变量。也可以同时设置多个：

```Dockerfile
ENV <varname1>=<value1> <varname2>=<value2>...
```

如果进入 `schaepher/frps` 这个镜像的容器执行 `env` 这个命令，就能看到 ENV 设置的环境变量：  

```shell
~/frps # env
...省略无关内容...
FRP_VER=0.20.0
FRP_FULL_VER=frp_0.20.0_linux_amd64
```

当然，ENV 用在这里并不是很合适。因为实际上这两个 ENV 只在构建的时候用到，后续不会再需要。因此可以把 ENV 改为 ARG ，ARG 的变量不会在容器中出现。

### 构建时用的环境变量 —— ARG

定义：`ARG <varname>[=<default value>]`

这意味着如果有值，必须用等号连接变量名和值，且不能多个。  

值是可选的，因为这可以在构建的时候，加上下面这个参数来指定：  

```shell
--build-arg <varname>=<value>
```

如果填写了默认值，也可以通过这个选项来覆盖默认值。

## 2.3 基于基础镜像执行命令 —— RUN

定义：`RUN <command>`

用于执行 shell 命令。

在第一个 Dockerfile 中有如下内容： 

```Dockerfile
RUN cd /root \ 
    && wget https://github.com/fatedier/frp/releases/download/v${FRP_VER}/${FRP_FULL_VER}.tar.gz \
    && tar vxzf ${FRP_FULL_VER}.tar.gz \
    && rm ${FRP_FULL_VER}.tar.gz \
    && mv ${FRP_FULL_VER} frps \
    && rm -rf ./frps/frpc* ./frps/frps.ini
```

> 每一行后面的 `\` 用于分行

为什么写成多行的呢？上面有提到 **Dockerfile 中的每个指令都会创建一个新的镜像层** ，如果拆成很多个 RUN 的话，会有很多层。而层数是有限制的，例如默认的 overlay2 这种 Stroage Driver，最多支持 128 层。

但是层数不是问题最大的地方。之前提到过，就算你在上一层删了下一层的文件，这个文件仍然会存在。如果你在下一层安装了一些编译工具，这些文件就会一直存在于这一层。这会导致镜像的大小比所需的还大。

回到上面的 RUN 命令，这个命令在最后把一些不再需要的文件删除，这样就减少了这一层的大小。

## 2.4 sh 默认工作目录 —— WORKDIR

定义：`WORKDIR </path/to/workdir>`

用于指定进入镜像的容器后所在的文件夹。  

如果指定 `WORKDIR /root/frps`，那么当用户进入 `schaepher/frps` 的镜像后，执行 pwd 会得到以下结果：  

```shell
~/frps # pwd
/root/frps
```

## 2.5 容器启动时的默认命令 —— CMD

定义：`CMD ["executable","param1","param2"]`

用于指定启动镜像时默认执行的命令。

```Dockerfile
CMD [ "./frps", "-c", "./frps.ini" ]
```

上面这一行其实就是去执行：  

```shell
./frps -c ./frps.ini
```

下面这一条是新建并启动容器时的命令格式：  

`docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`

如果指定了 COMMAND ，则会覆盖 Dockerfile 里 CMD 指定的内容。

### 默认的可执行文件或脚本 —— ENTRYPOINT

定义：`ENTRYPOINT ["executable", "param1", "param2"]`

与 CMD 相似。

CMD 和 ENTRYPOINT 可以同时存在，此时 CMD 变为 `CMD ["param1","param2"]` ，也就是 CMD 的内容都会作为 ENTRYPOINT 的参数。

例如：  

```Dockerfile
ENTRYPOINT [ "./frps" ]
CMD [ "-c", "./frps.ini" ]
```

也是执行 `./frps -c ./frps.ini`。

从上面对 `docker run` 的解释，结合有 ENTRYPOINT 之后 CMD 的作用，可以这样使用：  

在 Dockerfile 里面这样写：  

```Dockerfile
ENTRYPOINT [ "./frps" ]
```

然后 `docker run -it frps -c ./frps.ini`。  

如果换做是一次性执行的应用，就可以让镜像变成命令一样使用。

## 2.6 复制宿主机文件到容器 —— COPY

定义：`COPY [--chown=<user>:<group>] <src_dir1>... <dest_dir>`

用于将 Dockerfile 所在文件夹内的文件或文件夹复制到镜像内。镜像内目录如果不存在，会自动创建。  

源路径可以使用通配符。

文件的元信息会被保留，但可以通过 `--chown` 参数修改权限。

### 解压宿主机压缩包到容器 —— ADD

定义：`ADD [--chown=<user>:<group>] <src_dir1>... <dest_dir>`

在添加压缩文件时使用，会自动解压。

## 2.7 ONBUILD

定义：`ONBUILD [INSTRUCTION]`

当该镜像作为其他镜像的基础镜像时，执行 INSTRUCTION 指定的内容。在作为多个类似镜像的基础镜像时很有用处。  

对于第二个 Dockerfile 中的内容：  

```Dockerfile
FROM schaepher/frps

COPY frps.ini /root/frps/frps.ini
```

可以将 COPY 写到第一个 Dockerfile：  

```Dockerfile
FROM alpine:latest

ENV FRP_VER 0.20.0
ENV FRP_FULL_VER frp_${FRP_VER}_linux_amd64

RUN cd /root \ 
    && wget https://github.com/fatedier/frp/releases/download/v${FRP_VER}/${FRP_FULL_VER}.tar.gz \
    && tar vxzf ${FRP_FULL_VER}.tar.gz \
    && rm ${FRP_FULL_VER}.tar.gz \
    && mv ${FRP_FULL_VER} frps \
    && rm -rf ./frps/frpc* ./frps/frps.ini

WORKDIR /root/frps

ONBUILD COPY frps.ini /root/frps/frps.ini

CMD [ "./frps", "-c", "./frps.ini" ]
```

这样第二个 Dockerfile 就简化成：  

```Dockerfile
FROM schaepher/frps
```

没错，就这么简单的一行！

## 2.8 容器执行时的用户 —— USER

定义：`USER <user>[:<group>] 或者 USER <UID\>[:<GID>]`

用于切换到指定用户。会影响 Dockerfile 这一行之后的命令。

## 2.9 数据卷声明 —— VOLUME

定义：`VOLUME <path>`

用于防止用户忘记挂载目录导致动态文件被写到容器存储层。

这个命令将指定 path 挂载到匿名卷。

在执行 `docker run` 的时候可以用 `-v` 参数将其覆盖。

## 2.10 端口声明 —— EXPOSE

定义：`EXPOSE <port> [<port>/<protocol>...]`

用于让镜像使用者知道这个镜像用到了哪几个端口，方便镜像使用者配置端口映射。

EXPOSE 实际上不会开启端口。

## 2.11 为镜像添加说明 —— LABEL

定义：`LABEL <key1>=<value1> <key2>=<value2> ...`

用于说明镜像的一些信息。例如维护者、版本、镜像描述等等。

如果有空格，需要加引号。例如：  

```Dockerfile
LABEL name="a b"
```

如果不包含空格，可以不加引号。

原来还有个 `MAINTAINER <name>` 用于指定维护者，但现在已经被弃用了，应该使用下面这个来代替： 

```Dockerfile
LABEL maintainer=<name>
```
