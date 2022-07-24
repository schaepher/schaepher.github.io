# 【RFC】HTTP/1.1 系列（7230 - 7235）


HTTP（Hypertext Transfer Protocol，超文本传输协议）是应用层的无状态的请求和响应协议。它使得基于网络的超文本信息系统彼此可以灵活地进行交互。它包含了可拓展的语义（extensible semantics）和自描述的有效报文载荷（self-descriptive message payloads)。

- 应用层：OSI 七层模型的顶层；
定义请求头；
- 自描述的：指报文本身描述了处理这个报文的方式，例如 HTML 最开始的 `<!DOCTYPE`；
- 有效报文载荷：真正需要的数据，HTML 内容或者 JSON 串；
- 注：从表示上看，像解释型语言（与编译型语言相对）。其内容可以被所有编程语言处理，因此不受限于特定编程语言和特定平台。基于不同编程语言的系统可以通过 HTTP 进行交互。

<!-- more -->

## 历史

最早对 HTTP/1.1 做出说明的 RFC 文档是 1997 年发布的 RFC2068。在 1999 年发布的 RFC2616 对 RFC2068 做了更新。

当前关于 HTTP/1.1 最新的文档是 2014 年发布的 RFC7230、RFC7231、RFC7232、RFC7233、RFC7234、RFC7235 ，它们将 RFC2616 的内容拆分开来并做详细的解释与更新。

在 RFC INDEX 页面可以看到它们之间的关系：  

> https://www.rfc-editor.org/rfc-index.html  

> 2068	Hypertext Transfer Protocol -- HTTP/1.1 R. Fielding, J. Gettys, J. Mogul, H. Frystyk, T. Berners-Lee [ January 1997 ] (TXT, HTML) (Obsoleted-By RFC2616) (Status: PROPOSED STANDARD) (Stream: IETF, Area: app, WG: http) (DOI: 10.17487/RFC2068)  
> 2616	Hypertext Transfer Protocol -- HTTP/1.1 R. Fielding, J. Gettys, J. Mogul, H. Frystyk, L. Masinter, P. Leach, T. Berners-Lee [ June 1999 ] (TXT, PS, PDF, HTML) (Obsoletes RFC2068) (Obsoleted-By RFC7230, RFC7231, RFC7232, RFC7233, RFC7234, RFC7235) (Updated-By RFC2817, RFC5785, RFC6266, RFC6585) (Status: DRAFT STANDARD) (Stream: IETF, Area: app, WG: http) (DOI: 10.17487/RFC2616)  
> 7230	Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing R. Fielding, J. Reschke [ June 2014 ] (TXT, HTML) (Obsoletes RFC2145, RFC2616) (Updates RFC2817, RFC2818) (Updated-By RFC8615) (Status: PROPOSED STANDARD) (Stream: IETF, Area: app, WG: httpbis) (DOI: 10.17487/RFC7230)  

具体的内容见：  
- [https://tools.ietf.org/html/rfc2068](https://tools.ietf.org/html/rfc2068)：过时的
- [https://tools.ietf.org/html/rfc2616](https://tools.ietf.org/html/rfc2616)：过时的
- [https://tools.ietf.org/html/rfc7230](https://tools.ietf.org/html/rfc7230)
- [https://tools.ietf.org/html/rfc7231](https://tools.ietf.org/html/rfc7231)
- [https://tools.ietf.org/html/rfc7232](https://tools.ietf.org/html/rfc7232)
- [https://tools.ietf.org/html/rfc7233](https://tools.ietf.org/html/rfc7233)
- [https://tools.ietf.org/html/rfc7234](https://tools.ietf.org/html/rfc7234)
- [https://tools.ietf.org/html/rfc7235](https://tools.ietf.org/html/rfc7235)

## 内容

本文会对 RFC7230-7235 的内容做个大概的说明（翻译），并且在必要的时候做详细说明（翻译）。

- RFC7230：语法和路由  
  语法：描述了一个 HTTP 请求或者响应长什么样。即第一行写什么怎么写、第二行写什么怎么写...  
  路由：资源标识（URI）如何确定？通过什么方式获取到想要的内容？是直接从本地缓存获取？还是通过代理（Proxy）获取？还是直接请求？
- RFC7231：语义和内容（最需要关注的内容，RESTful-like）  
  各种请求方法（GET、POST、DELETE 等等）和请求头（Expect、Accept-Language、User-Agent 等等）表达了什么意图？  
  响应体的状态（200 OK、201 Created、403 Forbidden 等等）和响应头（Location、Retry-After、Allow 等等）表达什么意思？
- RFC7232：条件请求  
  响应体告知客户端某些数据条件（Last-Modified、ETag 等等），客户端可以在下次请求的时候带上这些信息（If-Modified-Since、If-Match 等等）。在符合条件或者不符合条件的情况下，服务端应该如何处理；
- RFC7233：范围请求  
  由于各种因素而只得到部分响应的时候，发起范围请求以获取剩下的内容，避免从头请求而浪费资源；
- RFC7234：缓存  
  通过减少请求避免网络资源的浪费；
- RFC7235：认证  
  用户认证。Basic Auth、Token 等等。

## RFC7230：语法和路由

### 客户端和服务端

客户端发起连接请求给服务端，服务端接收来自客户端的请求，并建立连接。

`用户代理（User Agent）` 用于表示各种客户端程序，例如浏览器、爬虫、命令行工具、手机应用等等。  

`源服务器（Origin Server）` 用于表示对客户端请求的资源生成一个权威性的响应的程序。

HTTP 通过 URI 确定目标资源和资源间的关系。

### 请求的语法

例子：  

```
GET /hello.txt HTTP/1.1
User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3
Host: www.example.com
Accept-Language: en, mi
```

- 第 1 行（请求行）包含三个信息：请求方法、URI、HTTP 版本  
- 第 2-4 行是请求头（Headers）
- 请求头以一个空行作为结束标志
- 在空行后面是真正想要发送的报文——有效载荷体（payload body），如果没有就放空。

### 响应的语法

例子：  

```
HTTP/1.1 200 OK
Date: Mon, 27 Jul 2009 12:28:53 GMT
Server: Apache
Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
ETag: "34aa387-d-1568eb00"
Accept-Ranges: bytes
Content-Length: 51
Vary: Accept-Encoding
Content-Type: text/plain

Hello World! My payload includes a trailing CRLF.
```

- 第 1 行（状态行）包含三个信息：HTTP 版本、状态码、原因
- 第 2-9 行是响应头（Header）
- 响应头以一个空行作为结束标志
- 在空行后面是客户端想要的报文——有效载荷体（payload body），如果没有就放空。

### 中转（Intermediaries）

从 User Agent 到 Origin Server，中间可以经过各种中转。中转通常有三种：代理（Proxy）、网关（Gateway）和隧道（Tunnel）。

```
    >             >             >             >
UA =========== A =========== B =========== C =========== O
            <             <             <             <
```

- 入站（Inbound）和出站（Outbound）  
  入站表示朝向源服务器，出站表示朝向用户代理。
- 代理（Proxy）  
  一种由客户端选择的报文转发代理（message-forwarding agent）。按照一定规则让请求通过同一个中转。
- 网关（Gateway）  
  又称为反向代理（Reverse Proxy）。对于出站连接来说，网关就像是源服务器。经常被用于拦截不被信任的服务、提高服务器性能、负载均衡等等。
- 隧道（Tunnel）  
  通常被用于建立一条虚拟的连接。通过这条连接的报文不会发生变化。
- 透明代理（Transparent Proxy）  
  不是由客户端选择的代理。例如在路由器上建立代理，电脑的浏览器感知不到这个代理。

### 无状态

HTTP 是无状态的协议。这意味着每个请求都能够被独立地理解。  

但是由于代理会复用连接或者动态负载均衡的存在，服务端不应该认为来自同一条连接的请求来自于同一个用户代理（User Agent）。

### 缓存

缓存用于存放先前的响应报文，它还作为子系统管理着缓存的抽取和删除。

使用缓存的目的是减少未来发起与先前等价的请求时所带来的响应耗时和网络带宽的消耗。

```
    >             >
UA =========== A =========== B - - - - - - C - - - - - - O
            <             <
```

在 B 缓存了先前的响应报文后，UA 发出的请求就不必再经过 C 和 O 了。

一个响应是否会被缓存，由多个因素决定。在 RFC7234 里有详细的说明。

### 协议版本

格式是：`<major>.<minor>`  

但从 HTTP/2 开始，仅保留 major 。例如 HTTP/3。

> [https://www.ruanyifeng.com/blog/2016/08/http.html](https://www.ruanyifeng.com/blog/2016/08/http.html)

## RFC7231：语义和内容  

### 请求方法

请求方法表明客户端发起请求的目的，以及客户端所预期的成功结果。

> Representation （表征）：  
> the way that someone or something is shown or described.    
> 人或物被展示或者描述的方式。

```
+---------+-------------------------------------------------+-------+
| Method  | Description                                     | Sec.  |
+---------+-------------------------------------------------+-------+
| GET     | 传输目标资源的一种表征                            | 4.3.1 |
| HEAD    | 和 GET 相同，但只传输状态和头部                   | 4.3.2 |
| POST    | 执行请求有效载荷中特定于资源的处理                 | 4.3.3 |
| PUT     | 用请求有效载荷替换资源的所有表征                   | 4.3.4 |
| DELETE  | 删除目标资源的所有表征                            | 4.3.5 |
| CONNECT | 建立一条与目标资源指定的服务器之间的隧道            | 4.3.6 |
| OPTIONS | 描述与目标资源相关的选项                          | 4.3.7 |
| TRACE   | 执行一个沿着客户端到目标资源路径的消息回送测试      | 4.3.8 |
+---------+-------------------------------------------------+-------+
```

这些方法可以按照不同属性分类：

1. 安全（safe）和非安全（unsafe）  
    安全的方法不会造成目标资源的状态改变。方法包括 GET/HEAD/OPTIONS/TRACE。
2. 幂等（idempotent）  
    同一个请求执行一次或者多次，对服务端资源的影响是一致的。  
    幂等的方法包括所有的安全方法，还有 PUT/DELETE。例如多次 DELETE 同一个资源，对于服务端来说，最终的结果都是该资源不存在。执行一次或者执行多次都一样。    
    幂等容易被误解为对客户端来说的幂等，导致难以理解为什么 GET 也是幂等的：毕竟每次 GET 返回的结果都可能不一样。因此要注意站在服务端资源的角度来看。
3. 可缓存（cacheable）  
    响应结果可存储起来供后续使用。方法包括 GET/HEAD/POST。  
    大多数的缓存实现都只实现 GET/HEAD，但 RFC 7231 多定义了一个 POST。  
    这部分内容在 RFC 7234 有详细介绍。

### 方法定义

#### GET

#### HEAD

#### POST

POST 根据结果选择合适的状态码：  

- 201 Created  
    一个或多个资源创建成功后，返回该状态码。同时要在头部加上 Location，指向创建的主要资源。
- 206 Partial Content  
- 303 See Other  
    如果 POST 的处理结果与一个已存在资源的某一种表征一致，那么服务端在处理完 POST 后，可以用 303 重定向到已存在的资源。  
    这是为了共享缓存，但如果客户端代理之前没有缓存该已存在资源的表征，则会因为 303 而额外地发起一次请求。  
- 304 Not Modified
- 416 Range Not Satisfiable

#### PUT

服务端应校验服务端对目标资源的配置，例如内容的类型。

PUT 根据结果选择合适的状态码：  

- 200 OK  
    目标资源已存在，此次更新成功
- 201 Created  
    目标资源先前不存在，此次执行创建了该资源。
- 204 No Content
    目标资源已存在，此次更新成功
- 400 Bad Request  
    客户端请求头包含 Content-Range。部分更新应使用 PATCH。
- 409 Conflict  
- 415 Unsupported Media Type  
    服务端对资源配置的 Content-Type 与客户端配置的不一致。例如服务端限定只能是 `text/html`，而客户端在 HTTP 头部配置的是 `image/jpeg`。  
    这只是一种处理方式，其他两种处理方式为：  
    + 服务端将客户端传输的类型转换为服务端配置的类型，然后存储  
    + 服务端变更配置，将 Content-Type 配置为客户端设置的类型


#### DELETE

DELETE 表达的是源服务器 URL 映射的一种删除操作，而不是一种删除先前关联信息的期望。和 rm 命令类似，只删除映射，并没有将数据清除。

一个资源如果有一种或者多种表征，源服务器可以选择是否清除数据，也可以选择是否回收数据的存储空间。

当使用 PUT 创建资源和 POST 创建资源后，可以用 DELETE 来撤销（undo）这些操作。

DELETE 根据结果选择合适的状态码：  

- 200 OK  
    操作成功，且响应体包含了描述结果的信息
- 202 Accepted  
    操作很可能成功，但还未执行或者还未执行完成。
- 204 No Content  
    操作成功，且不需要返回更多的信息给客户端

由于删除操作是幂等的，因此多次删除同一个资源让源服务器对于该资源处于同一个状态。  

#### OPTIONS

OPTIONS 用于获取目标资源所支持的选项。OPTIONS 没有对目标资源做出修改。

OPTIONS 支持两种资源类型：

- `*`  
    用于类似 ping 或者空操作。
- 非 `*` 
    用于获取可用的适用于目标资源的选项。  

服务端在生成响应的时候，应该发送服务端实现的适用于目标资源的任何可选特性的头部。例如 Allow。此外还包括潜在的没有定义在 RFC 7221 的扩展。

OPTIONS 响应允许包含响应体，用于描述通信选项。如果不包含响应体，其 Content-Length 必须设置为 0。

OPTIONS 请求允许包含请求体。此时请求头必须包含 Content-Type 头部描述请求体的媒体类型。

#### CONNECT

CONNECT 用于建立从参与者到源服务器之间的通道。

#### TRACE

TRACE 请求应用层级别的回环


### 请求头字段

#### 起控制作用的请求头  

```
+-------------------+
| Header Field Name |
+-------------------+
| Cache-Control     |
| Expect            |
| Host              |
| Max-Forwards      |
| Pragma            |
| Range             |
| TE                |
+-------------------+
```

- Max-Forwards  
    只用于 TRACE 和 HEAD 请求方法。它的值是一个十进制整数，用于表示代理剩余可转发次数。  

#### 起条件作用的请求头（RFC 7232）

```
+---------------------+
| Header Field Name   |
+---------------------+
| If-Match            |
| If-None-Match       |
| If-Modified-Since   |
| If-Unmodified-Since |
| If-Range            |
+---------------------+
```

服务端响应一个资源的时候，可以包含响应专用的 ETag 和 Modified-Since 两个响应头，表示资源的版本。  

客户端可以在后续请求时，将 ETag 的值放在 If-Match 或者 If-None-Match 上，将 Modified-Since 的值放在 If-Modified-Since 或者 If-Unmodified-Since 上。

- If-Match
    If-Match 的值可以加双引号，值可以有多个，多个值用逗号隔开。值还可以是 `*`，表示匹配任意 ETag，但如果一个都没有的时候，为 false。匹配方式使用强匹配。  

    + 当客户端要更新一个资源，使用了 If-Match 头，它要求当前服务端该资源的 ETag 应该是刚才 GET 资源时所获得的 ETag。避免覆盖掉其他请求对该资源的更新，或者避免更新请求的响应丢失时重试。  
    + 当 If-Match 用于安全的请求方法（如 GET）时，如果服务端资源的 ETag 与之不匹配，则终止该请求。   

- If-None-Match  
    + 使用弱匹配。  
    + 如果客户端要初始化一个资源，使用了 If-None-Match 头，它要求当前资源的 ETag 不是刚才获得的 ETag 才能更新。例如将 If-None-Match 设置为 `*`，避免多个初始化请求时后者覆盖前者。  
    + 当 If-None-Match 为 false 时：  
        * 如果使用 GET 或者 HEAD，返回 304 Not Modified  
        * 如果使用其他请求方法，则返回 412 Precondition Failed

- If-Modified-Since  
    如果请求头还包含 If-None-Match，则忽略 If-Modified-Since  
    如果服务端发现资源的最后一次修改时间早于或者等于 If-Modified-Since 指定的时间，则不执行操作而是返回 304 Not Modified 

- If-Unmodified-Since  
    如果请求头还包含 If-Match，则忽略 If-Unmodified-Since  
    避免覆盖其他的修改  
    如果服务端发现资源的最后一次修改时间晚于 If-Modified-Since 指定的时间，则不执行操作，返回 412 Precondition Failed 或者 2xx。返回 2xx 的场景是请求的操作给资源带来的最终状态与当前状态一致。

如果客户端使用 GET 或者 HEAD 时，想要通过请求头来尝试命中缓存，则应该使用以下两个请求头：  
- If-None-Match 表示 “如果不匹配该 ETag，则返回最新的数据”。如果响应的状态码是 304 Not Modified ，则表示客户端传送的 ETag 与服务端的一致。
- If-Modified-Since 表示 “这个时间之后资源如果已被修改，则返回最新的数据”。如果响应的状态码是 304 Not Modified ，则表示资源在客户端指定的时间之后没有再被修改了。

#### 起内容协商作用的请求头  

主要协商服务端应该返回的数据类型。

```
+-------------------+
| Header Field Name |
+-------------------+
| Accept            |
| Accept-Charset    |
| Accept-Encoding   |
| Accept-Language   |
+-------------------+
```

- Accept  
    媒体类型，例如 text/plain。  
    对应响应头为： Content-Type
- Accept-Charset  
    字符集 unicode
- Accept-Encoding  
    字符编码，例如 gzip。  
    对应响应头为： Content-Encoding
- Accept-Language  
    语言

协商头的值可以多个，用逗号隔开，表示服务端可以根据情况选择。每种选项都有一个比重（0 ~ 1），用分号与选项隔开，放在分号之后。可以省略比重，此时会被解释为 1。  

例如：  

Accept: text/plain; q=0.5, text/html, text/x-dvi; q=0.8, text/x-c

表示更希望获取 text/html 或者 text/x-c 这两种媒体类型。如果服务器不支持这两种类型，则返回 text/x-dvi 这种类型。如果也不支持 text/x-dvi，则返回 text/plain 这种类型。如果都不支持，则返回 406 Not Acceptable 。

### 响应状态码

#### 1xx 信息

- 100 Continue  
    当客户端的 Expect 头部包含 100-continue 的时候，服务端返回该状态码表示知道客户端要发送大量的数据，并且初始数据已被接收，服务端当前不打算拒绝该请求，客户端可以继续发送请求。  
    > RFC 7231 对 Expect 的值只定义了 100-continue 这一种。如果客户端传送了其他值，服务端可能返回 417 Expectation Failed。

- 101 Switching Protocols  
    客户端头部包含 Upgrade 时，服务端返回该状态码表示愿意切换协议。

#### 2xx 成功

- 200 OK
- 201 Created  
    成功创建资源后，在响应头 Location 中返回资源的位置。  
    在实践中，会碰到一个问题：客户端并不总是关心该资源的位置，而是关注查看该资源内容的前端地址。不能将该地址放在响应体，因为 201 要求响应体必须为空。应该把这个链接信息放到响应头 Link 里面。  
- 202 Accepted   
    服务端接受客户端的请求，但请求未处理完。服务端返回当前处理的状态，以及指向该处理的状态监测器。客户端可使用该监测器获取执行状态。
- 203 Non-Authoritative Information  
    由代理返回。表示请求成功，服务端返回了 200，但由于响应有效载荷被转换代理修改，因此返回该状态码。  
- 204 No Content  
- 205 Reset Content  
    让客户端将导致刚刚请求被发送的那部分页面（例如表单）重置为它的初始状态。

#### 3xx 重定向

表示用户代理需要再做其他动作来满足刚才的请求。比如 Location 字段指定了一个 URI，用户代理可能自动重定向到该 URI。  

重定向有四种类型：  

- 资源可能在一个不同的 URI 上可以用。属于这种类型的状态码包括：  
    + 301 (Moved Permanently)
    + 302 (Found)
    + 307 (Temporary Redirect)
- 请求的资源有多种表征，客户端可以选择最合适的表征。属于这种类型的状态码包括：  
    + 300 (Multiple Choices)  
- 重定向到一个不同的资源，该资源代表了对请求的间接响应。属于这种类型的状态码包括：  
    + 303 (See Other)
- 重定向到一个已缓存的结果。属于这种类型的状态码包括：  
    + 304 (Not Modified)

以下是各个状态码的补充说明：  

- 300 Multiple Choices  
    请求的资源存在，但是有多种表征。由于客户端没有明确表示需要哪种表征，服务端无法替客户端决定。服务端将这些不同表征的 URI 放在头部 Link 中。 
    服务端可在 Location 指定服务端倾向的其中一种表征，供客户端自动重定向。
- 301 Moved Permanently  
    目标资源被分配了新的 **永久** 的 URI，后续请求应该使用新的 URI。服务端将新的 URI 放在 Location 中，客户端可以根据这个字段的值自动重定向。  
    由于历史原因，用户代理一旦收到该状态码，后续请求可能将 POST 转为 GET。如果不能接受这样的转换，则应该使用 307 Temporary Redirect。  
- 302 Found  
    目标资源 **暂时** 存放在不同的 URI，后续请求应该使用原先的 URI。服务端将新的 URI 放在 Location 中，客户端可以根据这个字段的值自动重定向。  
    由于历史原因，用户代理一旦收到该状态码，后续请求可能将 POST 转为 GET。如果不能接受这样的转换，则应该使用 307 Temporary Redirect。
- 303 See Other  
    服务端让客户端重定向到一个不同的资源，该资源的 URI 放在 Location 中，目的是为原始请求提供一个间接的响应。这种重定向可能持续多次，并且用户代理应该将最终的结果作为原始请求的响应。  
    例如 POST 创建资源后，可以使用这个状态码将客户端重定向至新资源的地址。  
- 304 Not Modified（RFC 7232）  
    当 GET 或者 HEAD 请求附带 Last-Modified 或 ETag 时，如果满足条件，则返回该状态码。表示客户端数据的版本已是最新，服务端不再返回这些数据。  
    响应头应包含以下头部的任何一个：Cache-Control， Content-Location， Date， ETag， Expires 和 Vary 。
- 305 Use Proxy（已废弃）  
- 306 Unused（已废弃）  
- 307 Temporary Redirect  
    目标资源 **暂时** 存放在不同的 URI，后续请求应该使用原先的 URI。服务端将新的 URI 放在 Location 中，客户端可以根据这个字段的值自动重定向。  
    用户代理在自动重定向的时候 **禁止改变** 请求方法。  
- 308 Permanent Redirect（RFC 7238）  
    目标资源被分配了新的 **永久** 的 URI，后续请求应该使用新的 URI。服务端将新的 URI 放在 Location 中，客户端可以根据这个字段的值自动重定向。  
    用户代理在自动重定向的时候 **禁止改变** 请求方法。 

需要特别注意的是：

|状态码|暂时/永久|可能改变请求方法|RFC|
|:--|:--|:--|:--|
|301|永久|是|7231|
|302|暂时|是|7231|
|307|暂时|否|7231|
|308|永久|否|7238|

#### 4xx 客户端错误

凭据（credential）：登录过的证明。如 Cookie，Token。

- 400 Bad Request  
    请求的句法有问题（例如请求的第一行不按照标准来）、欺骗性的请求路由、不合法的请求内容等。当其他 4xx 无法表达错误类型的时候，也使用该状态码。
- 401 Unauthorized（RFC 7235）  
    不包含有效的凭据。服务端的响应头必须包含 WWW-Authenticate，告知具体原因。无效的凭据：空凭据、过期凭据。
- 402 Payment Required  
    仅作为保留状态码，以便未来对此状态码做具体定义。
- 403 Forbidden  
    资源存在，但客户端没有权限访问。分为带有效凭据和无效凭据的情况。但最终都要求客户端提供一个有效且具有权限的凭据。
- 404 Not Found  
    服务端当前没有找到请求的资源。404 并不意味着资源在未来不会出现。如果服务端通过一些信息知道该资源永远不会再出现，则应返回 410 Gone。  
    **未必找不到资源才返回 404。在实践中，如果服务端不想暴露 “资源存在” 这一信息给客户端，则可以返回该状态码。**  
- 405 Method Not Allowed  
    目标资源不支持该请求方法。例如某个资源不支持 DELETE，而客户端对该资源发起 DELETE 请求。
- 406 Not Acceptable    
    客户端请求头包含 Accept、Accept-Charset、Accept-Encoding、Accept-Language 时，服务端发现资源无法满足客户端的要求，且不想返回一个默认的资源表征。  
    服务端应该在响应的有效载荷中列出可用的选择。  
- 407 Proxy Authentication Required（RFC 7235）  
    类似于 401，但 407 用于客户端和代理之间。用于表示如果要使用代理，必须提供有效凭据。代理的响应头必须包含 Proxy-Authenticate，告知具体原因。
- 408 Request Timeout  
    服务端未能在特定时间内接收一个完整的请求，并且要关闭该连接。  
- 409 Conflict  
    请求与目标资源当前的状态产生冲突。  
    常出现在对版本化的资源做 PUT 时，资源已被其他请求变更，当前请求不是基于资源最新版本变更的。服务端可以在响应的有效载荷里面包含帮助客户端合并两个版本的信息。  
    **这个状态码在一些地方被用于 POST 请求的响应，用于表示要创建的资源已存在。**
- 410 Gone  
    与 404 相似，但 410 表示资源很可能永远都不存在。  
- 411 Length Required  
    客户端请求头不包含 Content-Length
- 412 Precondition Failed（RFC 7232）  
    请求头中一个或者多个测试条件不满足。客户端想要在目标资源处于某种状态的时候才更新该资源，而如果客户端所预期的状态和该资源当前的状态不一致，则返回该状态码。
- 413 Payload Too Large  
    请求体（有效载荷）的大小超过了服务端设置的限制。如果这种限制是临时的，则服务端响应头应包含 Retry-After 表示客户端可以过一段时间再尝试。
- 414 URI Too Long  
    URI 太长。可能是由于重定向导致 POST 转为 GET，也可能是客户端恶意攻击，还可能是客户端不小心传了过多的数据。
- 415 Unsupported Media Type  
    客户端请求头 Content-Type 或者 Content-Encoding 指定的值，或者服务端根据请求体的内容来识别，发现其类型不被目标资源所支持。  
- 417 Expectation Failed  
    跟客户端请求头 Expect 对应（只定义了 100-continue 一种）。如果客户端传送了服务端不支持的 Expect 类型，则报错。  
- 422 Unprocessable Entity（RFC 4918）  
    导致 400 的条件都不满足的情况下，服务端仍然无法处理该请求。  
    **可以用于业务校验不通过的场景。**  
- 426 Upgrade Required  
    客户端的请求由于 HTTP 版本过低被服务端拒绝执行，如果客户端愿意升级 HTTP 版本，服务端才会执行。  
    响应头必须包含 Upgrade。例如 Upgrade: HTTP/3.0  

需要特别注意的是： 
- 401 和 403 的区别（登录、权限）
- 404 和 410 的区别（是否永久不存在）
- 408 和 504 的区别（服务端接收客户端超时、代理接收服务端超时）
- 409 的场景（资源支持版本）

#### 5xx 服务端错误

- 500 Internal Server Error  
    客户端请求没问题，但服务端碰到了错误，导致无法执行完请求。
- 501 Not Implemented   
    客户端使用的请求方法服务端没有实现，即对任意资源都不能使用该请求方法。
- 502 Bad Gateway  
    网关或者代理服务器收到了一份来自上游服务器的非法响应。  
- 503 Service Unavailable  
    服务端因为暂时性的负载过高或者临时维护导致服务无法使用。  
    如果负载过高，服务端不一定使用该状态码，而是直接拒绝连接。  
- 504 Gateway Timeout  
    网关或者代理服务器未能在指定时间内收到上游服务器的响应。
- 505 HTTP Version Not Supported  
    服务端不支持或者拒绝支持客户端使用的 HTTP 主版本。

### 响应头字段





