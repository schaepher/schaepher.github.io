# Docker 介绍



## Docker 是用来干嘛的？

帮助开发者和系统管理员使用容器开发、部署和运行应用。

对于开发者而言，最直观的感受就是原先我们要跑起来一个已有项目，必须装一大堆依赖。  
在没有 Docker 的时候，可以有两种方式：  
1. 写一个自动化脚本。安装的时候去执行这个脚本。
2. 将依赖安装到虚拟机，导出镜像。需要的时候去下载镜像。

第一种方式可能会因为网络原因或者版本变更导致安装失败。第二种方式的虚拟机会占用大量资源，而且使用上还要对虚拟机做配置。

而如果使用 Docker，这些依赖的安装命令将会由运维人员定义在一个脚本（Dockerfile）。并且通过脚本构建镜像。开发人员安装 Docker 引擎后，拉取镜像并运行。

<!-- more -->

跟虚拟机很像，但是也有区别。

## Docker 和虚拟机的区别

主要有两点：宿主机磁盘占用和资源占用

先说宿主机磁盘占用：  

虚拟机由于包含了一个完整的系统，因此镜像会比较大。例如 CentOS 7 的镜像大小为 1GB 左右。  

> CentOS 7 虚拟机镜像下载地址：  
> [https://www.osboxes.org/centos/](https://www.osboxes.org/centos/)

而 CentOS 7 的 Docker 镜像大小为：70 MB 左右。  

> CentOS 7 的 Docker 镜像：  
> [https://hub.docker.com/_/centos?tab=tags](https://hub.docker.com/_/centos?tab=tags)

能否再小一点？能！Alpine 镜像的大小不到 3 MB。  
> Alpine 的 Docker 镜像：  
> [https://hub.docker.com/_/alpine?tab=tags](https://hub.docker.com/_/alpine?tab=tags)

再从复用性来讲。每启动一个新的虚拟机，就得再消耗一份镜像大小的空间。而每启动一个 Docker 容器，就只需要加一个容器层。这个我们后面再说。

从资源占用的角度讲两者的区别：  

由于虚拟机是装一个完整的系统，因此系统内核的运行消耗会增加宿主机的资源消耗。另外一个显著的问题就是系统启动时，很慢。可达分钟级别。  
在分配资源时，虚拟机需要通过一个虚拟机管理系统(Hypervisor)分配硬件资源。  

而 Docker 镜像不是一个完整的操作系统，它使用宿主机的内核。Docker 容器的启动时间是秒级别，甚至可以是毫秒级别。  
Docker 容器的资源分配是通过 Docker 直接向宿主机获取的。  

虚拟机：[ App -> Bins/Libs -> Guest OS ] -> Hypervisor -> Host OS -> Infrastructure  
Docker：[ App -> Bins/Libs ] -> Docker -> Host OS -> Infrastructure  

你甚至可以在镜像内只安装一个小应用，然后把这个镜像当做一个软件。

## Docker 基于什么样的技术

Linux Kernel 3.10+：Namespace 和 Control Groups  
Windows 10：Hyper-V

Docker 现在要求如果是 Linux 系统，内核版本要大于 3.10。对应就是 CentOS 7。如果感兴趣我们可以讲讲为什么。

Docker 用到的 Linux 内核技术是命名空间（Namespace）和控制组（Control Groups）。总结起来就是资源隔离和资源控制。    

- 命名空间就跟我们 Java 包名或者 C++ 和 PHP 里面的那个命名空间有点相似。  
  命名空间可以隔离系统资源，包括：文件系统挂接点、nodename 和 domainname、进程间通信资源、进程 ID 数字空间 、网络相关的系统资源、用户和组 ID 空间。  
  举个例子，在各个容器里面都可以有进程号为 1 的 root 进程。就像不同命名空间可以有同名的类。  
  但不同的是，这里的命名空间还使得处于不同空间的对象无法直接互相访问。这样就提供了一定程度的安全性。    

- 控制组的功能包括对硬件资源的：资源限制、优先级分配、资源统计、进程控制。

## Hello World

我们试着下载镜像并启动。  

执行命令：  
`docker run hello-world`  

会有以下输出：  
```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete 
Digest: sha256:b8ba256769a0ac28dd126d584e0a2011cd2877f3f76e093a7ae560f2a5301c00
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

执行 run 的时候，Docker 会在本地找 hello-world 镜像。由于我们没有指定镜像版本，因此默认使用 latest 版本。  
接着因为 Docker 没有找到要执行的镜像，它会到远程镜像仓库里面找这个镜像。如果找到镜像，则下载并执行；找不到就报错。  

https://github.com/docker-library/hello-world  

https://github.com/docker-library/hello-world/blob/master/arm64v8/hello-world/Dockerfile

https://github.com/docker-library/hello-world/blob/master/hello.c

## 轻量基础镜像 Alpine  

前面提到 Alpine 的大小只有 3 MB。如果想尽可能地使构建出来的镜像小的话，则优先考虑使用 Alpine。  

如果能够确定不需要依赖于任何系统，连这 3 MB 都省去。例如前面一节的 hello-world 就不基于任何基础镜像，但是这样一来就得自己做好安全控制和增加必要的便捷性。除非必要，否则都会基于一个基础镜像。  

拉取 Alpine 镜像：  
`docker pull alpine`  

如果你 run 这个 alpine，它会立即退出。因为没有什么命令使得它必须处于运行状态。  

> 如何使它保持运行状态？等说完镜像层和容器层，会详细说明。  

你可以把它当成一个执行 Linux 命令的工具：  
`docker run alpine echo "hello"`  

如果你想要有交互，可以加上 `-it`：  
`docker run -it alpine sh`  

这样就进入了交互状态，就好像进入了另一台机器。

关于 `-it` 选项：

`-i` 是 --interactive 的缩写，表示将当前输入连接到容器执行的进程的标准输入（STDIN）里面。  
`-t` 是 --tty 的缩写。表示申请一个伪终端（PTY），并连接到容器。可以接受 STDOUT 和 STDERR。 

> 关于 i 和 t 的详细解释见：  
> [https://stackoverflow.com/questions/30137135/confused-about-docker-t-option-to-allocate-a-pseudo-tty/54254380#54254380](https://stackoverflow.com/questions/30137135/confused-about-docker-t-option-to-allocate-a-pseudo-tty/54254380#54254380)

当你执行 exit 退出时，容器就结束了。

## 镜像层和容器层

先说镜像层。

一个镜像通常由多个只读（read only）的镜像层组成，每个镜像层表示构建这个镜像时的每一步操作。

```
+------------------------+
|                        |
|  Image Layer 1 (ro)    |
|                        |
+------------------------+
|                        |
|  Image Layer 2 (ro)    |
|                        |
+------------------------+
```

执行 run 的时候，发生了什么？  

run 包含了两个步骤：create 和 start。如果还加了 -i -t 两个参数，那还有第三个步骤 attach。

1. create 时， Docker 会在镜像的基础上创建一个可读写(read and write)的容器层。  
   ```
   +------------------------+
   |                        |
   |  Container Layer (rw)  |
   |                        |
   +------------------------+
   |                        |
   |  Image Layer 1 (ro)    |
   |                        |
   +------------------------+
   |                        |
   |  Image Layer 2 (ro)    |
   |                        |
   +------------------------+
   ```
2. start 启动容器。可以加入 -i -a 来进入交互模式。-i 会连接标准输入，-a 会连接标准输出和标准错误。    
3. attach 会将你的终端接入正在执行中的容器，连接到标准输入输出和错误。STDIN,STDOUT,STDERR。

创建多少容器，就有多少份容器层。但它们没有依赖关系，共用镜像。  
当我们销毁容器的时候，会把这一个读写层完全删除。里面的数据会全部被删除掉（这点很重要）。 

```
+------------------------+   +------------------------+   +------------------------+
|                        |   |                        |   |                        |
|  Container Layer (rw)  |   |  Container Layer (rw)  |   |  Container Layer (rw)  |
|                        |   |                        |   |                        |
+------------------------+   +------------------------+   +------------------------+
           X                             X                            X
           XXXXXXXXXXXXXXXXXXXXXXX       X        XXXXXXXXXXXXXXXXXXXXX
                                 X       X        X
                                 X       X        X
                             +------------------------+
                             |                        |
                             |  Image Layer 1 (ro)    |
                             |                        |
                             +------------------------+
                             |                        |
                             |  Image Layer 2 (ro)    |
                             |                        |
                             +------------------------+

```


## 如何保持运行状态？

当从镜像创建容器后，这个容器相当于一个程序。你执行这个程序，等执行完后，它就退出了。就像最开始的 hello-world ，当它打印完说明后，就结束了。然后容器退出。

我们在创建容器的时候，会指定一个程序来执行。启动容器时，会启动这个程序，分配一个进程（主进程）。容器将会跟踪这个进程的状态。  

当进程退出时，容器也会随之退出。例如我们在执行 `docker run -it alpine sh` 后进入了 sh 的交互状态。当我们继续执行 exit 时，退出了 sh 的进程，容器也跟着退出了。

如果想让容器不退出，就得将进程保持在执行状态，不让它退出。  

最简单的一种方式就是让容器启动时执行 `tail -f /dev/null` 这个命令。这个命令表示不断读取 `/dev/null`，这样它永远都不会退出，并且不会产生多余的输出。  

但是如果所有的镜像都指定容器启动时执行上面这个命令，那就不合适了。  

这是由于我们让容器提供的服务有可能会因为各种异常而退出，这时我们希望它可以自动重启。  

我们可以让 Docker 在发现容器退出时自动重启容器，但是 `tail -f /dev/null` 这个命令使得容器不会因为其他进程的退出而退出。

后面会详细说明其他保活方法。

## 定制镜像  

上文在对比 Docker 和虚拟机的时候说过。虚拟机可以进入安装所有依赖，然后保存镜像。Docker 也可以。Docker 可以将容器层（可读写）转换为镜像层（只读）。

我们可以通过 `docker run -it alpine sh` 进入 alpine ，然后做一些依赖的安装操作。

这里举个不是安装依赖的简单例子：在 home 底下创建一个 test 文件夹。然后退出。  

如果你再执行 `docker run -it alpine sh` 进入 alpine 。你会发现这个文件夹不在了。在【镜像层和容器层】这一节有提到，每次 run 都会生成新的容器。

该如何找到刚刚创建的容器？可以用 `docker ps -a`。-a 表示显示所有容器，包括启动的和已退出的。因为我们没有给容器加上保活的机制，所以在退出主进程的时候就会变为退出状态。

如果我们想把对这个容器的更改保存起来，防止被删除，可以执行：  

`docker commit <container-id> <tag>`

例如对 id 为 33ebad6f23d5 的容器，在宿主机执行：  

`docker commit 33ebad6f23d5 test`

然后再去 run 这个名字为 tag 的新镜像，就可以在 home 底下看到 test 文件夹了。  

`docker run test ls /home`  

## 使用 Dockerfile 基于基础镜像构建新镜像

使用 commit 定制镜像有一个问题。  

通过 `docker history 镜像名` 来查看上一节中 commit 的镜像的历史，可以看到最顶层是这样的：  

```
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
25b2ad442d41        6 days ago          sh                                              31 B                
```

这样看不出来这一层究竟执行了哪些命令，增加了维护的难度。

有的同学就会说了：那写到脚本里面不就行了？

写到脚本里面也是可以的，但这不是最优的做法。

在【镜像层和容器层】一节中，我们知道镜像是分层的。这样做有什么好处呢？

1. 当 Docker 直到你即将构建的这一层与原先已构建的一层所执行的命令一样，那它就直接使用原先的镜像层。这样加快了构建的速度。
2. 当镜像传输时，本地已有的镜像层不会再下载。加快了镜像下载的速度。  
   比如你已经下载了一个最新版的 alpine 镜像，然后又下载两个都是基于当前最新版本的 alpine 构建的镜像。那么下载的时候会跳过 alpine 镜像的下载。

如果使用脚本去构建，总是会只生成一层镜像层。那么每次构建时都得从头开始。传输时也是全部重新传一次。

我们可以像写 bash 脚本那样把命令都放在一个文件。这就是 Dockerfile。  

在使用 Dockerfile 构建镜像时，FROM 以外的命令都会生成一个镜像层。这样就能享受到分层的好处了。

对于刚才使用 commit 的定制，我们可以换成 Dockerfile 的方式：  

```Dockerfile
FROM alpine:latest

RUN mkdir /home/test
```

这样我们就可以通过查看这个文件得知这个镜像都做了哪些修改。

这里的 FROM 的意思是基于哪个镜像。在那个镜像上执行操作。  

RUN 后面跟上相关命令。

文件以 Dockerfile 为名并保存。然后在宿主机执行构建：  

```
# docker build . -t testv2
Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM alpine:latest
 ---> 965ea09ff2eb
Step 2/2 : RUN mkdir /home/test
 ---> Running in e2548722ecbe
Removing intermediate container e2548722ecbe
 ---> 9678e6e6b110
Successfully built 9678e6e6b110
Successfully tagged testv2:latest
```

从 Step 1/2 可以看到使用的基础镜像 ID 为 965ea09ff2eb。  

从 Step 2/2 可以看到 Docker 在构建镜像的时候启动了一个容器 e2548722ecbe，然后执行 `mkdir /home/test`。在 commit 后生成镜像 9678e6e6b110，并且删除刚刚创建的容器 e2548722ecbe。

镜像已经创建了。由于执行构建的时候，还指定了镜像的 tag，因此会将 9678e6e6b110 的名称设置为 `testv2:latest`。

执行下面的命令可以看到镜像 testv2 在 home 底下有个 test 文件夹：

`docker run testv2 ls /home`  

## 端口映射

由于命名空间对网络资源的隔离，宿主机无法直接访问容器内进程的端口。

我们要做的就是分配一个宿主机的端口，让它与容器的端口关联起来。  

下面的命令将宿主机的 60044 端口与容器的 80 端口关联起来：

`docker run -d -p 60044:80 nginx:alpine`

这样当我们访问宿主机的 60044 端口时，就相当于在访问容器的 80 端口。

有的同学会问：那我多个容器内部能不能使用一样的端口？比如启动两个 nginx 容器，都监听 80 端口。  

当然可以。由于命名空间对网络资源的隔离，容器之间使用的端口都不影响。但是当它们与宿主机端口建立关联时，不能使用同一个宿主机端口。

有时候下载了一个镜像，不知道这个镜像的作者提供了哪些可用的端口怎么办？

可以找到构建这个镜像的 Dockerfile，里面会有 EXPOSE 命令：

```Dockerfile
EXPOSE 80
```

EXPOSE 仅用于提示使用该 Dockerfile 构建出的镜像的用户有哪些端口可以映射，它不会自己映射端口。

没有 Dockerfile 怎么办？`docker history 镜像名`。

## 数据卷映射  

在【镜像层和容器层】一节提到，删除容器时会把容器里面的数据全删除掉。那么如何才能让想要的数据不被删除呢？

可以选择映射到宿主机的目录或者放到数据卷里面。  

你可以把数据卷想象成一个专门存放数据的空间，将多个数据卷挂载到容器的不同目录下。容器被删除时，这些数据卷不会被删除。

执行 `docker volume create 数据卷名称` 来创建数据卷。然后执行下面命令将数据卷映射到 `/home/test`。

`docker run -it -v 数据卷名称:/home/test testv2 sh`

其中第一步创建数据卷可以省略，第二步在数据卷未创建时，会自动创建。

下面命令将当前所在的宿主机目录映射到容器的 `/home/test` 目录。

`docker run -it -v "${PWD}:/home/test" testv2 sh`

`${PWD}` 可以替换为相对路径或者绝对路径。

Dockerfile 的 VOLUME 类似于 EXPOSE：

```Dockerfile
VOLUME /home/test
```

但它不仅有提示用户的作用。如果用户没有在创建容器的时候指定映射目标，它会创建一个随机命名的数据卷，并挂载到 /home/test。  

## 更多的 Dockerfile 构建命令

看另一篇： [Dockerfile](https://schaepher.github.io/2018/12/09/dockerfile/)

## 直观地感受 Docker 资源

Docker 的数据存放在一个特定的目录里面。例如 CentOS 7 的 Docker 数据默认存放在 `/var/lib/docker` 里面。

```
# ls /var/lib/docker
builder  buildkit  containers  image  network  overlay2  plugins  runtimes  swarm  tmp  trust  volumes
```

之前创建的数据卷在 volumes 里面。

这个存放位置可以更改（这在将树莓派作为 NAS 的时候非常有用）：

vim /etc/docker/daemon.json

```json
{
    "data-root": "/mnt/docker-data"
}
```
