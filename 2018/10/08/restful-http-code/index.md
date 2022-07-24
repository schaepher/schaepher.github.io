# RESTful API HTTP Code


本文内容主要参考 Github 上的 NationalBankBelgium/REST-API-Design-Guide 项目以及 MDN

> [https://github.com/NationalBankBelgium/REST-API-Design-Guide/wiki/HTTP-Status-Codes](https://github.com/NationalBankBelgium/REST-API-Design-Guide/wiki/HTTP-Status-Codes)  
> [https://developer.mozilla.org/zh-CN/docs/Web/HTTP](https://developer.mozilla.org/zh-CN/docs/Web/HTTP)

<!-- more -->

## 2xx Success 成功

### 201 Created

当 POST 成功时返回。并且头部要带上 Location ，其值为该资源的地址。  

例如：  

Request：  

```
POST /apples
```

Response： 

```
HEADER：  
    Location: /apples/1
```

场景：  
- 资源创建成功

误用的场景：  
- 暂无

### 202 Accepted

当服务端无法立即返回处理结果的时候使用。  

例如：耗时操作，批量操作，删除操作无法立即返回

头部需要带上 Location， 其值为获取该结果的地址。

如果请求 Location 指向的地址时，资源还没有处理完毕，则仍然返回 202。

### 204 No content

当删除操作能够立即返回时使用。

## 3xx Redirection 重定向

### 301 Moved permanently

本次请求的资源已经被关联到新的 url 上，客户端以后的请求都应该向新的 url 发送。可以用于 API 的版本管理。  

新的 url 会放在 Header 的 Location 。

### 303 See other

服务端已经处理完客户端的请求，但是响应体并不包含任何内容。因为服务端认为客户端很可能不需要这些内容。

在响应的头部中 Location 带有这些内容的 URL ，客户端如果需要，可以向该 URL 发起请求。


### 304 Not modified

客户端已经拥有所请求资源的最新版本。当客户端用 GET 或 HEAD 发起请求，且可以使用缓存的内容时。

请求的要求：  
- 在 Header 中带上 If-None-Match 或 If-Modified-Since 参数

响应的要求： 
- 响应体应为空

场景：  
- 条件请求

## 4xx Client Error 客户端错误

### 400 Bad request  

请求异常、请求是不完整的时候使用。或一次请求有多个错误时使用。

这要求客户端不能重复发送该请求，应该在修改请求后再发送。

### 401 Unauthorized

客户端没有登录，但请求需要登录才能获取的数据或操作。

客户端应该在请求头加上服务端要求的身份信息。如 token。

### 403 Forbidden

客户端有登录，但没有访问或修改该资源的权限。  

如果某个资源存在，但是不能让没有权限的客户端知道该资源存在，则应该使用 404。

### 404 Not Found

请求的资源不存在。

当客户端请求资源的集合，但资源不存在时，不应返回 404，而是 200 加上空数组。

### 405 Method Not Allowed

客户端使用了不被允许的 HTTP 方法（GET POST PUT PATCH DELETE）。

场景：  
- 该资源尚未支持这种 HTTP 方法
- 不允许使用这个操作

### 406 Not Acceptable

无法按照客户端所要求的响应体格式生成数据。

请求的要求：  
- Header 必须带上 Accept 参数，用于表示使用哪种格式。例如 Accept: application/json
- Header 可以带上 Accept-Language 参数，用于表示使用哪种语言。例如简体中文： Accept-Language: zh_CN;q=0.8

场景：  
- 不支持 Accept 指定的格式
- 不支持 Accept-Language 指定的语言

### 422 Unprocessable Entity

请求没有问题，但由于业务上不满足条件，不给予处理。用于业务检查。
