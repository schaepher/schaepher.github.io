# 分布式的几个要点


# 过载保护

http://sharecore.net/post/%E8%BF%87%E8%BD%BD%E4%BF%9D%E6%8A%A4%E7%AE%97%E6%B3%95%E6%B5%85%E6%9E%90/

## 令牌桶算法

按一定速率往桶里放令牌，收到请求的时候从桶里取出。如果取不到令牌，则拒绝处理请求。

```go

import (
    time
    sync
)

var tokens = 0
var capacity = 100
var rate = 10
var latestPutTime = time.Now().Unix()
var lock sync.Mutex

func min(a,b int) int64 {
    if a > b {
        return a
    }

    return b
}

func getToken() bool {
    lock.Lock()
    defer lock.Unlock()

    // 放入令牌
    now := time.Now().Unix()
    tokens = (now-latestPutTime)*rate
    latestPutTime = now

    // 桶如果溢出，使用固定限制
    tokens = min(capacity, tokens)
    
    if tokens > 0 {
        token--
        return true
    }

    return false
}
```


## 漏桶算法

与桶令牌算法相似。不再是放入令牌取，而是往里面塞令牌。桶定时漏掉一些令牌。

## 定期刷新可用数

设定每个间隔可以处理的请求数，定时刷新数量。

无法处理在刷新的前后两秒暴涨的问题。


# 柔性可用
