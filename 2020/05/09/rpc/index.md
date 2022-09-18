# RPC


Remote Procedure Call Protocol （RPC，远程过程调用），与进程内本地函数调用区分，只跨进程的函数调用。  

调用方将函数和入参序列化为字节流，并发送给服务方。服务方将字节流反序列化为函数和参数，并调用函数。将结果序列化为字节流，返回给调用方。调用方将结果的字节流反序列化，得到结果。  

RPC 框架封装了这个过程。并且提供更多的功能。

RPC 客户端的职责有：  

- 序列化/反序列化
- 连接池管理
- 负载均衡
- 故障转移
- 队列管理
- 超时管理
- 异步管理










