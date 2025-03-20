# v2ray


## 客户端配置

1. 配置文件
2. 代理工具（v2rayN）

## 服务端配置

1. 配置文件
2. 开放端口  
    ```
    firewall-cmd --zone=public --add-port=25535/tcp --permanent
    firewall-cmd --reload
    ```

## too many open files

需要在所有的 outbound 里面添加：  
```json
      "streamSettings": {
        "sockopt": {
          "mark": 255
        }
      }
```  
否则会死循环，导致：  
```
2019/10/16 17:53:27 [Warning] v2ray.com/core/transport/internet/tcp: failed to accepted raw connections > accept tcp [::]:1088: accept4: too many open files
```

来源：  
https://github.com/v2ray/v2ray-core/issues/1574#issuecomment-539429974

## 卡在 Read config

日志配置问题。删掉看看。

## 参考资料

v2ray 完全配置指南：  

https://ailitonia.com/archives/v2ray%e5%ae%8c%e5%85%a8%e9%85%8d%e7%bd%ae%e6%8c%87%e5%8d%97/
