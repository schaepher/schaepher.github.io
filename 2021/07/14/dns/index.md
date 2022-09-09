# DNS



# DNS 缓存

https://segmentfault.com/a/1190000017962411

chrome://net-internals/#dns可以查看chrome浏览器的dns缓存信息

https://www.zhihu.com/question/23042131/answer/66571369


# DNS

让域名解析的时候，引入自己的 DNS 服务器

DNS 解析请求会得到多种类型的响应，例如 A、CNAME、NS。

当 DNS 服务器得到 CNAME 时，它会发起解析 CNAME 的请求。

将一个域名 CNAME 到 CDN 厂商的 CDN 域名。

CNAME 请求的结果是 CDN 厂商的 DNS 服务器 IP，响应类型为 NS。

于是 DNS 服务器向厂商的 DNS 服务器发起查询请求，查询的域名是 CDN 厂商域名。

CDN 厂商的 DNS 服务器收到请求，根据请求第一跳的用户 IP 去 IP 库查询 IP 的地址。根据该地址选择最近的机房，返回机房里的 IP。


