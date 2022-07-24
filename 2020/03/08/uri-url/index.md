# URI/URL 分不清？（rfc3305）



这篇主要依据发布于 2002 年的 RFC3305。  

> [https://tools.ietf.org/html/rfc3305](https://tools.ietf.org/html/rfc3305)

对于这些叫法，有两种观点：传统观点和现代观点。

传统的观点是统一资源标识符（Uniform Resource Identifier）有多层结构，在 URI 底下主要还分为两种 URL（Uniform Resource Location）和 URN（Uniform Resource Name）。任何一个 URI 都尽量地再做一次归类，分到 URL 或者 URN。

```
       +---> URL
       |
       |
URI +------> URN
       |
       |
       +---> URC
```

但现代的观点是这种区分并不重要，它们都属于 URI scheme。在 RFC7230 或者 RFC7231 中，见不到 URL 的说法，都是说 URI。

<!-- more -->



