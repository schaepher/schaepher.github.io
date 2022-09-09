# WEB 服务热更新


已知：

1. 在一个进程启动子进程的时候，可以将父进程文件描述符复制给子进程
2. 在 Socket 层面，当进程监听某个端口时，会为其创建一个对应的 TCP_LISTEN Socket，用于监听来自客户端的请求。
3. TCP_LISTEN Socket 会绑定一个 Socket 文件，该文件位于系统内核空间。文件可以独立于这个 TCP_LISTEN Socket 存在。

做法：

1. 父进程启动子进程，将父进程的标准输入、标准输出、标准错误、Web 服务的 TCP_LISTEN Socket 的文件描述符复制给子进程，忽略其他的 REQUEST Socket 文件描述符。

2. 子进程根据继承的 TCP_LISTEN Socket 文件描述符创建对应 Listener。启动服务，调用 `Accept()` 接收请求。  
   此时父进程和子进程都在接收请求，父进程还未关闭它的 Listener。  
   操作系统允许多个进程监听同一个地址和端口，负载均衡。  
   https://lwn.net/Articles/542629/

3. 子进程发送信号给父进程，要求其关闭服务。

4. 父进程关闭 TCP_LISTEN Socket 的 Listener，不再接收新请求。  
   关闭 Listener 不会关闭 Socket 文件，不影响子进程继续接收请求。

5. 父进程处理完子进程监听请求之前的所有已接收的请求，关闭进程。

## 启动子进程

父进程：

```go
func (a *app) signalHandler(wg *sync.WaitGroup) {
	ch := make(chan os.Signal, 10)
	signal.Notify(ch, syscall.SIGINT, syscall.SIGTERM, syscall.SIGUSR2)
	for {
		sig := <-ch
		switch sig {
		// ...
		case syscall.SIGUSR2:
			// ...
			if _, err := a.net.StartProcess(); err != nil {
				a.errors <- err
			}
		}
	}
}
```

## 继承文件描述符

`gracenet/net.go`

```go
func (n *Net) StartProcess() (int, error) {
	listeners, err := n.activeListeners()
	if err != nil {
		return 0, err
	}

	// Extract the fds from the listeners.
	files := make([]*os.File, len(listeners))
	for i, l := range listeners {
		files[i], err = l.(filer).File() // <-- 这里的 File() 是 TCPListener 类的方法。
		if err != nil {
			return 0, err
		}
		defer files[i].Close()
	}
    // ...
}
```

`net/tcpsock.go`

```go
func (l *TCPListener) File() (f *os.File, err error) {
	if !l.ok() {
		return nil, syscall.EINVAL
	}
	f, err = l.file()
	if err != nil {
		return nil, &OpError{Op: "file", Net: l.fd.net, Source: nil, Addr: l.fd.laddr, Err: err}
	}
	return
}
```

## 关闭父进程

`gracehttp/http.go`

子进程：

```go
func (a *app) run() error {
    // ...
	// 开始提供服务
	a.serve()

	if didInherit && ppid != 1 {
    	// 关闭父进程
		if err := syscall.Kill(ppid, syscall.SIGTERM); err != nil {
			return fmt.Errorf("failed to close parent: %s", err)
		}
	}
    // ...
}
```

`gracehttp/http.go`

父进程：

```go
func (a *app) signalHandler(wg *sync.WaitGroup) {
	ch := make(chan os.Signal, 10)
	signal.Notify(ch, syscall.SIGINT, syscall.SIGTERM, syscall.SIGUSR2)
	for {
		sig := <-ch
		switch sig {
		case syscall.SIGINT, syscall.SIGTERM:
			signal.Stop(ch)
			a.term(wg) // <-- 会调用 server.Stop()
			return
		// ...
		}
	}
}
```

## 父进程等待当前所有请求处理完毕

`httpdown/httpdown.go`:

```go
func (s *server) Stop() error {
	s.stopOnce.Do(func() {
        // ...
		stopDone := make(chan struct{})
		s.stop <- stopDone

		select {
		case <-stopDone:
		case <-s.clock.After(s.stopTimeout):
			// ...
		}
        // ...
    }
	return s.stopErr
}
```

`httpdown/httpdown.go`:

```go
func (s *server) manage() {
    // ...
	var stopDone chan struct{}
    // ...
	for {
		select {
            // ...
        case c := <-s.closed:
			decConn(c)
			delete(conns, c)

			if stopDone != nil && len(conns) == 0 {
				close(stopDone)
				return
			}
		case stopDone = <-s.stop:
			if len(conns) == 0 {
				close(stopDone)
				return
			}

			for c, cs := range conns {
				if cs == http.StateIdle {
					c.Close()
				}
			}
        // ...
        }
    }
    // ...
}
```

当发起关闭的时候，向 s.stop 中发送一个消息。在 `manage()` 中接收后，判断是否所有请求都已处理，如果处理完了就关闭 stopDone，让 `Close()` 继续执行。

如果没有处理完毕，那么就让循环继续执行。每次有一个请求处理完毕，都检查是否所有连接都已处理完毕，如果是，就关闭 stopDone，让 `Close()` 继续执行。

