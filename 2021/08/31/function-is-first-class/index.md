# 编程语言把函数作为 First Class


要求返回接口，但创建对象需要更多参数。

Golang 的 gin 的 Router 的参数：

```go
func (group *RouterGroup) GET(relativePath string, handlers ...HandlerFunc) IRoutes {
	return group.handle(http.MethodGet, relativePath, handlers)
}

type HandlerFunc func(*Context)
```

要求传入以 `*Context` 为参数且无返回值的函数。

正常情况：

```go
func example(c *gin.Context) {
    // ...
    c.JSON(200, "")
    return
}

func InitRouter() {
    r.GET("/test", example)
}
```

如果要用到其他 service，由于函数参数无法传入，通常只能用全局。

但是现在可以：

```go
func exampleWithService(service Service) func(c *gin.Context) {
    return func(c *gin.Context) {
        service.CallMethod()
        c.JSON(200, "")
        return
    }
}

func InitRouter(service Service) {
    r.GET("/test", exampleWithService(service))
}
```
