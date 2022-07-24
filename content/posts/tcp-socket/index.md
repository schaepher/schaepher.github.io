---
title: TCP 协议和 TCP Socket 
date: 2020-07-02 12:56:00
updated: 2020-07-11 11:54:00
tags: 
- TCP
- Socket
---

TCP 位于计算机网络七层模型中的传输层。 TCP 协议在操作系统层面实现，实现方式为 TCP Socket。

> 除了 TCP Socket 之外，还有同样是**主要**用于主机间进程通信的 UDP Socket 和用于本机进程间通信的 Unix Domain Socket。它们提供的接口是一样的，但底层实现细节不一致。本文主要内容是 TCP Socket ，因此以下默认 Socket 都是表示 TCP Socket。

<!-- more -->

操作系统向应用开发程序员隐藏 Socket 的具体实现细节，仅提供一套统一的操作接口。WEB 应用或者基础应用开发人员（操作系统开发人员除外）通常能操作的最底层的通信接口就是 Socket 接口。如果了解 Socket 的工作原理，对理解其他上层协议（如 HTTP 协议）有很大的帮助。

在正式介绍前，如果读者对操作系统实现 Socket 的细节感到好奇，想先看看代码长什么样，可以进入以下链接查看 Linux 的相关源码。本文的后面部分会介绍一些源码相关的内容。**以下都以 Linux 为例**。

> [https://github.com/torvalds/linux/blob/master/net/ipv4/af_inet.c](https://github.com/torvalds/linux/blob/master/net/ipv4/af_inet.c)

## 两台不同主机上的进程通信

此处主要关注传输层，跳过物理层、数据链路层和网络层的内容。

前文我多次使用"主机间进程通信"这样的表述，而不是"主机间通信"，是因为主机间的通信问题已在网络层中解决。因此我们脑海中应该始终有一张图：只有两个进程，以及一条连接这两个进程的管道。

于是我们就有了第一个问题：

### 客户端进程怎么把管道接到服务端进程上的？

在网络层，客户端所在主机已经可以通过 IP 找到了服务端主机。接下来需要传输层找到服务端进程了。

假设我们不知道已有的实现方式，需要从头设计。该怎么做？

1. 进程不都有个进程 ID 嘛，让客户端带上这个进程 ID 就能找到了  
    但问题是进程 ID 不是固定的，程序重启后就变了。而让程序和进程 ID 始终绑定则会导致更多问题。
2. 既然 ID 会变，那选择相对稳定的进程名呢？客户端传一个服务端的进程的进程名，让服务端主机根据进程名找到服务端进程  
    但问题是这限制了服务端主机只能开启一个拥有该进程名的进程。同时每个进程只能提供一个服务。

这样我们很自然地想到添加一个相对固定的机制。就像数据库里面除了自增 ID 外，有时会添加一列 UUID。在进程间通信的问题上，由于一台机器可以同时提供的服务有限，用 16 位二进制就够用了（0 - 65535）。我们称这个 ID 为“端口”。

服务端进程启动时，绑定由服务提供者指定的端口。客户端或用户从服务提供者那里获取服务端进程绑定的端口，请求时带上该端口 就能找到目标进程了。

只要服务端的配置不变，进程重启后仍然会绑定同样的端口。如果想开启多个相同服务，只需给这些不同的进程绑定不同的端口就行了。

以上解决了第一个问题。客户端进程通过端口找到位于服务端的进程。

在实践中，不可能每个服务端进程仅与一个客户端进程通信，因为这会浪费资源。我们希望服务端进程能同时与同一台客户端服务器或者多台不同服务器上的多个客户端进程建立通信。这样当某个通信进入等待状态时，可以让服务端进程切换到与另一个客户端进程的通信，之后再切回来继续处理。

于是我们就有了第二个问题：

### 服务端进程如何知道自己是在和哪个进程通信？

同样地，我们得给客户端进程在建立通信的时候绑定一个 ID。为了方便，也使用与服务端进程相同的端口机制。不过由于客户端可能同时需要与多个服务端进程通信，如果每次都要手动分配端口，那就太麻烦了，于是改为由进程向操作系统申请一个随机的端口。通常情况下用户并不需要知道这个端口是啥。

这样就有了【<客户端 IP ：客户端进程端口>，<服务端 IP ：服务端进程端口>】这样的关联。客户端和服务端操作系统都会在内存的内核空间中保存该信息。服务端进程通过客户端 IP 和客户端进程端口知道自己当前在和哪个进程通信。为了描述方便，我们把这个用于描述通信双方进程信息的关联称之为“套接字”，对应英文单词 Socket。

> “套接” 是指它像连接两条水管的套接管一样，提供一个通道让它们可以连通。而 “字” 在计算机里面通常表示 “一对” 或者 “两个” 的意思，这就是为了说明必须有一对标识，也就是双方的 IP + 端口。这里是参考以下的内容：  
> [https://www.zhihu.com/question/21383903/answer/1024419470](https://www.zhihu.com/question/21383903/answer/1024419470)

以上解决了第二个问题。

第三个问题：

### 两个进程如何通过套接字进行通信？

两者的通信就像是双方进程往套接字读写数据。

一旦涉及到读写，对于 Linux 这样把一切都抽象成文件的系统来说，套接字也会被关联到文件上。我们将套接字关联的文件称之为“套接字文件”。

套接字文件与我们通常使用的文件不一样。操作系统不会将套接字文件的数据刷入到磁盘，而是将数据放在内存的内核空间中的缓冲区（队列），然后程序通过内核接口读写缓冲区。缓冲区是一个字节数组，在 C 语言中用 `char[n]` 表示，这里的 n 用于限制缓冲区最多能存放多少字节。

> 其他 Linux 文件类型可到搜索引擎搜索 “Linux 文件类型”

如果每个套接字只有一个缓冲区用于读写，则同一时刻只能有一方在写。为了提高通信效率，双方的操作系统为每个套接字分配了两个缓冲区以便通信的双方进程同时写，这两个缓冲区分别为读缓冲区和写缓冲区。

通信的过程是这样的：客户端进程通过系统调用将数据写入套接字文件，操作系统将对套接字文件的写操作转化为对套接字的写缓冲区的写操作，然后产生一个写事件，加入到操作系统内核的写队列。操作系统会将写缓冲区的数据打包到 TCP 报文中，通过网络接口控制器（NIC，我们通常叫网卡）发送出去。服务端操作系统会从 NIC 收到 TCP 报文，从报文中获取到套接字信息，并用它找到操作系统内核中保存的与之对应的套接字，然后把数据复制到套接字的读缓冲区。然后通知套接字绑定的进程，服务端进程再通过系统调用对套接字文件执行读操作，操作系统会将其转换为对套接字读缓冲区的读操作，位于内核空间的套接字读缓冲区的数据复制到进程内的缓冲区。

## 进程如何读写套接字文件？

操作系统创建的套接字对应的文件的文件描述符会存放在 `/proc/进程ID/fd/` 底下。

```
[root@localhost /]# ls -l /proc/7376/fd
total 0
lr-x------. 1 root root 64 Jun 18 15:51 0 -> /dev/null
lrwx------. 1 root root 64 Jun 18 15:51 1 -> socket:[13119730]
lrwx------. 1 root root 64 Jun 18 15:51 2 -> socket:[13119730]
lrwx------. 1 root root 64 Jun 18 15:51 3 -> socket:[14312193]
lrwx------. 1 root root 64 Jun 18 15:51 4 -> anon_inode:[eventpoll]
lrwx------. 1 root root 64 Jun 18 15:51 5 -> socket:[14312194]
lrwx------. 1 root root 64 Jun 18 15:51 6 -> socket:[13119755]
lrwx------. 1 root root 64 Jun 18 15:51 7 -> socket:[14311807]
lrwx------. 1 root root 64 Jun 18 15:51 8 -> socket:[14311808]
```

0 ~ 8 是 fd （file descriptor，文件描述符，在 Windows 中叫做句柄），箭头后面指这个文件描述符指向的文件。

你可以执行命令 `ss -t -l -p` 来查看到关于 Socket 更详细的信息。这里以某台机器上进程号（pid）为 7376 的进程为例子，直观地感受一下两者的关联：  

```
[root@localhost /]# ss -t -l -p
State      Recv-Q Send-Q                                       Local Address:Port                                                        Peer Address:Port                
LISTEN     0      100                                              127.0.0.1:smtp                                                                   *:*                     users:(("master",pid=29939,fd=13))
LISTEN     0      128                                                      *:ssh                                                                    *:*                     users:(("sshd",pid=2419,fd=3))
LISTEN     0      100                                                  [::1]:smtp                                                                [::]:*                     users:(("master",pid=29939,fd=14))
LISTEN     0      128                                                   [::]:55554                                                               [::]:*                     users:(("test",pid=7376,fd=6))
LISTEN     0      128                                                   [::]:31689                                                               [::]:*                     users:(("test",pid=7376,fd=5))
LISTEN     0      128                                                   [::]:35849                                                               [::]:*                     users:(("test",pid=7376,fd=8))
LISTEN     0      128                                                   [::]:31085                                                               [::]:*                     users:(("test",pid=7376,fd=7))
LISTEN     0      128                                                   [::]:35728                                                               [::]:*                     users:(("test",pid=7376,fd=3))
LISTEN     0      128                                                   [::]:ssh                                                                 [::]:*                     users:(("sshd",pid=2419,fd=4))
```

最后一列中也有 fd。

对于进程来说，它关注的是对套接字文件的读写。

双方在执行系统调用的时候，都是传入文件描述符，由操作系统去找对应的 Socket。

> 这里面说得比较详细：  
> [https://colobu.com/2019/07/27/How-TCP-Sockets-Work/](https://colobu.com/2019/07/27/How-TCP-Sockets-Work/)

## 操作系统提供了哪些套接字文件的接口？

既然是文件，那就得有创建文件、打开文件、关闭文件、删除文件的接口吧？于是就有了：

- int socket(int domain, int type, int protocol) 
    相当于创建和打开。此时 `socket()` 会为套接字随机分配一个端口号。
- int close(int fd)
    相当于关闭和删除

这样客户端和服务端就可以各自打开一个 Socket 文件了。

由于服务端进程需要绑定由服务提供者指定的端口，所以得加上一个操作：

- int bind(int sockfd, const struct sockaddr* myaddr, socklen_t addrlen)

myaddr 包含了本地 IP 地址和端口号，将其绑定到 Socket 上面。

由于服务端套接字不是主动发起连接，它需要让系统


的处理逻辑是不一样的，所以两者得区分开。

当使用 socket() 接口创建和打开 Socket 时，它默认将其设置为主动类型。主动和被动在之后的处理逻辑是不一样的，所以两者得区分开。那么服务端要怎么将其改成被动的呢？于是就有了：

- int listen(int sockfd, int backlog)

那么主动和被动有啥区别？其中一个区别是因为客户端和服务端是 n:1 的关系，服务端需要维护一些队列，用于存放客户端的连接请求，backlog 指定的就是这个队列的长度。listen() 会初始化这些队列，同时也把套接字转成 **监听套接字**。

终于可以开始联系了。总得给客户端提供一个主动联系的接口吧？于是就有了：

- int connect(int sockfd, struct sockaddr *serv_addr, int addrlen)

这时候趁机指定了对方的 IP 地址和端口。

服务端咋知道有人想要联系它？我们先简要说一下 tcp 的连接过程，即三次握手。

1. 客户端发送 SYN 包。
2. 服务端收到 SYN 包，创建 **请求套接字**，放入到半连接队列。回复 ACK + SYN。
3. 客户端发送 ACK。服务端收到 ACK，将请求套接字放到全连接队列。

此时的服务进程需要有一个接口，将套接字取出来。于是就有了：

- int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen)

如果全连接队列不为空，则从中取出一个请求套接字。然后重新获取一个文件描述符，以及一个新的 Socket，并将两者绑定起来。新的 Socket 会从请求套接字中取出必要的信息，如客户端的 IP 和端口。以后和客户端的交流都通过这个新的 Socket。

> 为每个连接分配一个专用的 Socket，清晰又方便。



叹了口气，双方可算是联系上了。

为了能互相说话。得再提供两个接口：

- int send(int sockfd, const void *msg, int len, int flags)  
    用于发送数据  
- int recv(int sockfd, void *buf, int len, unsigned int flags)  
    用于接收数据  

总结一下， TCP 套接字共有以下这些接口：  

- int socket(int socket_family, int socket_type, int protocol)
- int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen)
- int listen(int sockfd, int backlog)
- int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen)
- int aaccept(int sockfd, struct sockaddr *addr, socklen_t *addrlen)
- ssize_t send(int sockfd, const void *buf, size_t len, int flags)
- ssize_t recv(int sockfd, void *buf, size_t len, int flags)
- int close(int fd)

可以从 `net/ipv4/af_inet.c` 这个文件作为入口。如果没有读过开源项目的 C 源码，需要注意源码中对 Socket 的操作，所以一旦需要看更底层的细节，必须到 `static int __init inet_init(void)` 这个函数底下看各种 Socket 的操作函数的注册。

> af 是 address family 的缩写。

对套接字借口的调用都会进入到 `net/socket.c` 的 kernel_xxx 系列函数。例如 connect 进入到 kernel_connect 函数，并且在里面调用 `sock->ops->connect()`，这会调用在 inet_init 里注册的对应的 connect 函数。例如在 `net/ipv4/tcp_ipv4.c` 里的 tcp_prot ：

```c
struct proto tcp_prot = {
	.name			= "TCP",
	.owner			= THIS_MODULE,
	.close			= tcp_close,
	.pre_connect	= tcp_v4_pre_connect,
	.connect		= tcp_v4_connect,
	.disconnect		= tcp_disconnect,
	.accept			= inet_csk_accept,
	.ioctl			= tcp_ioctl,
	.init			= tcp_v4_init_sock,
	.destroy		= tcp_v4_destroy_sock,
	.shutdown		= tcp_shutdown,
	.setsockopt		= tcp_setsockopt,
	.getsockopt		= tcp_getsockopt,
	.keepalive		= tcp_set_keepalive,
	.recvmsg		= tcp_recvmsg,
	.sendmsg		= tcp_sendmsg,
    // 以下省略
};
EXPORT_SYMBOL(tcp_prot);
```

其中 tcp_v4_connect 函数注册到 connect 上面。在调用 `sock->ops->connect()` 的时候，实际调用的是 `tcp_v4_connect()` 函数。

为什么选择协议的时候，通常都没有让人选择 HTTP 或者 HTTPS 之类的，而是只给出 TCP 和 UDP。正是因为 HTTP 这种应用层协议是基于 TCP 或者 UDP 的。

__sys_socket -> socket()


Linux 系统调用

系统调用表：sys_call_table  

x64 架构的系统调用表位于 `arch/arm64/include/asm/unistd32.h`。修改的时候不直接修改这个文件，而是下面这个文件。

系统调用实际定义 `include\uapi\asm-generic\unistd.h`： 

```c
/* net/socket.c */
#define __NR_socket 198
__SYSCALL(__NR_socket, sys_socket)
#define __NR_socketpair 199
__SYSCALL(__NR_socketpair, sys_socketpair)
#define __NR_bind 200
__SYSCALL(__NR_bind, sys_bind)
#define __NR_listen 201
__SYSCALL(__NR_listen, sys_listen)
#define __NR_accept 202
__SYSCALL(__NR_accept, sys_accept)
#define __NR_connect 203
__SYSCALL(__NR_connect, sys_connect)
```

系统调用定义 `net/socket.c`：

```c
SYSCALL_DEFINE3(socket, int, family, int, type, int, protocol)
{
    return __sys_socket(family, type, protocol);
}
```

实际定义 `net/socket.c`：

```c
int __sys_socket(int family, int type, int protocol)
{
	int retval;
	struct socket *sock;
	int flags;

	/* Check the SOCK_* constants for consistency.  */
	BUILD_BUG_ON(SOCK_CLOEXEC != O_CLOEXEC);
	BUILD_BUG_ON((SOCK_MAX | SOCK_TYPE_MASK) != SOCK_TYPE_MASK);
	BUILD_BUG_ON(SOCK_CLOEXEC & SOCK_TYPE_MASK);
	BUILD_BUG_ON(SOCK_NONBLOCK & SOCK_TYPE_MASK);

	flags = type & ~SOCK_TYPE_MASK;
	if (flags & ~(SOCK_CLOEXEC | SOCK_NONBLOCK))
		return -EINVAL;
	type &= SOCK_TYPE_MASK;

	if (SOCK_NONBLOCK != O_NONBLOCK && (flags & SOCK_NONBLOCK))
		flags = (flags & ~SOCK_NONBLOCK) | O_NONBLOCK;

	retval = sock_create(family, type, protocol, &sock);
	if (retval < 0)
		return retval;

	return sock_map_fd(sock, flags & (O_CLOEXEC | O_NONBLOCK));
}
```

上面的 SYSCALL_DEFINE3 表示定义一个有三个参数的函数。其完整定义在 `include/linux/syscalls.h`：

```c
#ifndef SYSCALL_DEFINE0
#define SYSCALL_DEFINE0(sname)					\
	SYSCALL_METADATA(_##sname, 0);				\
	asmlinkage long sys_##sname(void);			\
	ALLOW_ERROR_INJECTION(sys_##sname, ERRNO);		\
	asmlinkage long sys_##sname(void)
#endif /* SYSCALL_DEFINE0 */

#define SYSCALL_DEFINE1(name, ...) SYSCALL_DEFINEx(1, _##name, __VA_ARGS__)
#define SYSCALL_DEFINE2(name, ...) SYSCALL_DEFINEx(2, _##name, __VA_ARGS__)
#define SYSCALL_DEFINE3(name, ...) SYSCALL_DEFINEx(3, _##name, __VA_ARGS__)
#define SYSCALL_DEFINE4(name, ...) SYSCALL_DEFINEx(4, _##name, __VA_ARGS__)
#define SYSCALL_DEFINE5(name, ...) SYSCALL_DEFINEx(5, _##name, __VA_ARGS__)
#define SYSCALL_DEFINE6(name, ...) SYSCALL_DEFINEx(6, _##name, __VA_ARGS__)

#define SYSCALL_DEFINE_MAXARGS	6

#define SYSCALL_DEFINEx(x, sname, ...)				\
	SYSCALL_METADATA(sname, x, __VA_ARGS__)			\
	__SYSCALL_DEFINEx(x, sname, __VA_ARGS__)
```

`net/socket.c`

```c
int __sock_create(struct net *net, int family, int type, int protocol,
			 struct socket **res, int kern)
{
}
```

`net/ipv4/af_inet.c`

```c
static int inet_create(struct net *net, struct socket *sock, int protocol,
		       int kern)
{
}
```

`net/core/sock.c`

```c
struct sock *sk_alloc(struct net *net, int family, gfp_t priority,
		      struct proto *prot, int kern)
{
}
```

`net/core/sock.c`

```c
void sock_init_data(struct socket *sock, struct sock *sk)
{
	sk_init_common(sk);
    // ...
	sk->sk_rcvbuf		=	sysctl_rmem_default;
	sk->sk_sndbuf		=	sysctl_wmem_default;
    // ...
}
```

`net/core/sock.c`

```c
static void sk_init_common(struct sock *sk)
{
	skb_queue_head_init(&sk->sk_receive_queue);
	skb_queue_head_init(&sk->sk_write_queue);
	skb_queue_head_init(&sk->sk_error_queue);

	rwlock_init(&sk->sk_callback_lock);
	lockdep_set_class_and_name(&sk->sk_receive_queue.lock,
			af_rlock_keys + sk->sk_family,
			af_family_rlock_key_strings[sk->sk_family]);
	lockdep_set_class_and_name(&sk->sk_write_queue.lock,
			af_wlock_keys + sk->sk_family,
			af_family_wlock_key_strings[sk->sk_family]);
	lockdep_set_class_and_name(&sk->sk_error_queue.lock,
			af_elock_keys + sk->sk_family,
			af_family_elock_key_strings[sk->sk_family]);
	lockdep_set_class_and_name(&sk->sk_callback_lock,
			af_callback_keys + sk->sk_family,
			af_family_clock_key_strings[sk->sk_family]);
}
```

`net/ipv4/tcp_ipv4.c`

```c
static int tcp_v4_init_sock(struct sock *sk)
{
}
```

`net/ipv4/tcp.c`

```c
void tcp_init_sock(struct sock *sk)
{
    // ...
	WRITE_ONCE(sk->sk_sndbuf, sock_net(sk)->ipv4.sysctl_tcp_wmem[1]);
	WRITE_ONCE(sk->sk_rcvbuf, sock_net(sk)->ipv4.sysctl_tcp_rmem[1]);
    // ...
}
```

系统调用过程：

```c
syscall(__NR_socket)
```

### 安全调用

```
security_socket_create()
--> selinux_socket_create()

LSM_HOOK_INIT(socket_create, selinux_socket_create)
```


## Socket 文件（sock_map_fd）

在为 socket 分配文件时，主要有三个步骤：

1. 找一个未被使用的文件描述符 fd（file descriptor）
2. 申请一个新文件，这个文件的 iNode 为 socket 之前预先分配的 iNode。socket 和文件会互相把对方的指针保存到自己的结构体中。
3. 把一开始获取到的 fd 和申请的新文件建立映射关系，并返回 fd

这样在用户程序传入 fd 的时候，可以找到该文件，并且从该文件的结构体里面找到对应的 socket。