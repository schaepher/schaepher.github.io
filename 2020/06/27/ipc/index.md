# 进程间通信（IPC，Inter-process Communication）


当我们开始执行一个程序时，会创建一个进程。这个进程可能需要与其他进程通信。例如向操作系统发送一条消息，让它展示给用户。

如果只是在自己的机器上通信，那就不有趣了。我们还想跟其他机器的进程通信，比如聊天应用就涉及到了多台机器。这种跨多台机器（主机）的通信通过套接字（Socket）实现。

<!-- more -->

> 我还无聊地去查了为什么 Socket 范围为套接字：    
> [https://www.zhihu.com/question/21383903/answer/1024419470](https://www.zhihu.com/question/21383903/answer/1024419470)

## 进程间通信是如何实现的？

通常我们会认为进程间的通信就像是一个进程直接把消息塞给另一个进程。但抽象起来说，其真实过程通常是一个进程将信息发送给某个中介（如通过系统调用复制到内核内存空间），另一个进程从中介获取这些信息。

## 进程间通信有哪几种方式？

按照主要功能，分为主机内进程间通信和主机间进程间通信。主机内的通信会简要介绍，主要的部分在于套接字通信。

主机内：

- 信号  
    内核利用信号通知用户空间的进程发生了哪些系统事件。例如 SIGKLL 表示关闭该进程。

- 管道（半双工）
    + 匿名管道（限于父子进程、子进程间）  
        内核空间开辟的一块内存。写方使用系统调用将数据从用户空间复制到内核空间，读方使用系统调用将数据从内核空间复制到用户空间。  
        > [https://www.cnblogs.com/sparkdev/p/10997135.html](https://www.cnblogs.com/sparkdev/p/10997135.html)  
        匿名管道分为两部分，一个是写专用的文件描述符，另一个是读专用的文件描述符。其中一个进程关闭写描述符，另一个关闭读描述符。因此通信方向是单向的（半双工）。
    + 命名管道  
        存储在文件系统上的一个文件。进程通过指定文件名来选择命名管道。只是把存储方式改为文件，仍是半双工（一个进程以只读方式打开，另一个以只写方式打开）。  
        > [https://www.cnblogs.com/sparkdev/p/11008978.html](https://www.cnblogs.com/sparkdev/p/11008978.html)

- System V IPC
    + 信号量  
        对于互斥的共享资源，使用信号量进行互斥的控制。  
        信号量可大于 1。当等于 0 时，消费者需要等待。如果是写锁，信号量最大设置为 1。  
        服务端申请信号量，并获取信号量 ID。客户端要从服务端获取该 ID ，才能对信号量操作。  
        > [https://www.cnblogs.com/sparkdev/p/8692567.html](https://www.cnblogs.com/sparkdev/p/8692567.html)
    + 共享内存  
        多个进程将同一段物理内存连接到进程自己的地址空间中。可读写。内存处于用户空间。    
        服务端申请共享内存，并获取共享内存 ID。客户端要从服务端获取该 ID，才能对共享内存操作。读或写之前，用信号量实现互斥。
    + 消息队列  
        在内核中消息以链表的形式存储。不同队列以队列 ID 标识。

- Unix 域套接字（Unix domain socket，全双工，应用最广泛）  
    在 TCP/IP 套接字的框架上发展出来。由于主机内部无需做可靠性的保证，因此比 TCP/IP 套接字用于主机内通信时更快。  
    > [https://serverfault.com/questions/124517/whats-the-difference-between-unix-socket-and-tcp-ip-socket](https://serverfault.com/questions/124517/whats-the-difference-between-unix-socket-and-tcp-ip-socket)

主机间：

- TCP/IP 套接字

## 套接字（Socket）通信

为啥要了解 Socket？它是传输层（TCP/UDP）的一种实现方式。对于 web 开发或者一些底层服务开发，想要深刻理解一些协议，总是要了解 Socket 的工作原理。例如 HTTP 协议为啥长这样？HTTP 2 协议为啥是那样？为啥要有 Content-Length 这个请求头？为啥一次连接可以有多个请求？这些在同一个连接上的请求是串行还是并发处理的？

套接字通信基于套接字文件。如果使用 Linux 系统，会经常看到以 `.sock` 结尾的文件。例如 `docker.sock`，这个就是用于套接字通信的文件。

Socket 分为两种类型：

- Unix domain socket 用于主机内部进程间通信
- TCP/IP 套接字主要用于主机之间的进程间通信，也可用于主机内部进程间通信

### Socket 与并发的关系

那么如果是一个 WEB 服务，Socket 如何支持并发的请求呢？它并没有支持。一个 Socket 只能对应一个客户端。当处于并发的状态，服务器会为每个客户端创建一个对应的 Socket。

> [https://zhuanlan.zhihu.com/p/130247159](https://zhuanlan.zhihu.com/p/130247159)

处理这些客户端的请求的方式分为五种：

1. 一次处理一个客户端的连接，其他阻塞其他客户端的连接请求。（并发 1）
2. 主线程负责分发，每个客户端绑定一个工作线程来处理消息业务，并读写套接字。客户端:线程 = 1:1。客户端数量一旦变多，线程数会达到硬件所能支持的上线。（读写并发 n，业务处理并发 n）
3. 仅用一个主线程处理，基于事件的机制（I/O 多路复用）。客户端:线程 = n:1。同一时间只能处理一个客户端的读写。当有一个客户端业务阻塞时，切换到其他客户端。（Redis）（读写并发 1，业务处理并发 ?）
4. 主线程负责分发和读写套接字，工作线程负责处理消息业务。主线程仍然使用 I/O 多路复用，意味着工作线程和客户端的比例是 m:n。（读写并发 1，业务处理并发 m）
5. 如果还想再提高性能，那就从读写并发入手。主线程开启 m 个读写线程，这些线程内部使用多路复用，不额外开工作线程。（读写并发 m，业务处理并发 m）
6. 从安全性考虑，由于线程共享同一内存空间，可能会出现一个线程干扰其他线程。因此将上一条的线程改成进程。（读写并发 m，业务处理并发 m，更安全）（Nginx）
7. 如果要再提高业务处理并发数，可以将 4 和 5 结合起来。但是线程切换会带来大量成本。（读写并发 m，业务处理并发 m*x）

虽然一个 Socket 只能对应一个客户端，但一台主机可以启动多个客户端，所以客户端主机可以同时发起多个请求。

### 为什么 Socket 是全双工的？

这就得看 Socket 的底层实现了。

我们可以从前面的主机内通信的命名管道得到一些灵感。命名管道是只能一个进程读，另一个进程写。如果开启两个命名管道，两边各持有一个作为写，另一个作为读，岂不是逻辑上就是全双工了？

事实上 Socket 在内存中会有两个 FIFO 队列。分别是用于发送的 SendQ，和用于接受的 RecvQ。

> [https://blog.csdn.net/jiaomingliang/article/details/45950591](https://blog.csdn.net/jiaomingliang/article/details/45950591)

### Socket 文件的内容都有些啥？

linux 中的文件有七种类型，除了最常接触到的普通文件类型以及目录，还有管道文件、链接文件、套接字文件、块设备文件、字符设备文件。

由于最经常接触普通文件，以为读写文件最终都会写入磁盘或者从磁盘读取，但套接字文件并不是，它只是一个便于寻找的标记。

网络的一个很重要的知识是 TCP 的建连过程。



对于 TCP/IP Socket 文件并没有存放什么东西。它是用于和 socket 绑定在一起，表示内核中的网络文件。

> [https://blog.51cto.com/weiguozhihui/1585297](https://blog.51cto.com/weiguozhihui/1585297)

底层会调用 tcp_sendmsg() 发送消息，其最终调用 sk.sk_write_space()。sk_write_space 是一个函数指针。根据不同的 driver，会注册不同的函数。

例如：

- [https://github.com/torvalds/linux/blob/master/drivers/net/tap.c](https://github.com/torvalds/linux/blob/master/drivers/net/tap.c)
- [https://github.com/torvalds/linux/blob/master/net/dccp/output.c](https://github.com/torvalds/linux/blob/master/net/dccp/output.c)
- [https://github.com/torvalds/linux/blob/master/drivers/net/tun.c](https://github.com/torvalds/linux/blob/master/drivers/net/tun.c)
- [https://github.com/torvalds/linux/blob/master/net/ceph/messenger.c](https://github.com/torvalds/linux/blob/master/net/ceph/messenger.c)
- [https://github.com/torvalds/linux/blob/master/net/unix/af_unix.c](https://github.com/torvalds/linux/blob/master/net/unix/af_unix.c)

以最后这个 Unix Domain Socket 为例。

```c
static struct sock *unix_create1(struct net *net, struct socket *sock, int kern)
{
    // ...
    sk = sk_alloc(net, PF_UNIX, GFP_KERNEL, &unix_proto, kern);
    // ...
    sk->sk_write_space	= unix_write_space;
    // ...
}

// ...

static void unix_write_space(struct sock *sk)
{
	struct socket_wq *wq;

	rcu_read_lock();
	if (unix_writable(sk)) {
		wq = rcu_dereference(sk->sk_wq);
		if (skwq_has_sleeper(wq))
			wake_up_interruptible_sync_poll(&wq->wait,
				EPOLLOUT | EPOLLWRNORM | EPOLLWRBAND);
		sk_wake_async(sk, SOCK_WAKE_SPACE, POLL_OUT);
	}
	rcu_read_unlock();
}
```


