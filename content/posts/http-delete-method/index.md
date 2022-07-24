---
title: HTTP 两次 DELETE 同一个资源应该返回什么
date: 2020-05-04 17:31:00
updated: 2020-05-04 17:31:00
tags:
- HTTP
- HTTP Methods
---

在实践 RESTful API 设计的时候，会碰到很多需要选择的地方。而这些在 RFC 7230 - 7235 里面没有说明。例如这次要说的 DELETE 方法。

根据 RFC 7231 的说法， DELETE 是幂等的。

<!-- more -->

> 幂等（idempotent）是什么？在 RFC 7231 定义幂等方法的时候，是这样说的：    
> A request method is considered "idempotent" if the intended effect on the server of multiple identical requests with that method is the same as the effect for a single such request. —— RFC 7231  
> 如果使用同一种请求方法的多个等效请求对服务器的预期影响，与一个等效请求对服务器的预期影响一样，那么这种请求方法被认为是幂等的。

## DELETE 幂等带来了什么问题？ 

问题是：多次使用 DELETE 方法作用于同一个资源，除了第一个成功对服务端造成影响（删除了资源）的请求，其他请求应该返回什么状态码？

针对这个问题，有两种观点。一种观点认为应该返回 404 Not Found；另一种观点认为应该返回 2xx 状态码。

第一种观点的理由是：  

不能删除一个不存在的资源，因为它已经不存在了。而表示资源不存在的状态码是 404，应该返回 404 Not Found。

第二种观点的理由是：  

客户端删除一个资源的意图是使得该资源不存在或者不可用。那么删除一次还是多次，都会让服务端对于该资源处于同一个状态。无论是客户端还是服务端，都认为这个结果是合理的，所以应该返回成功的状态码。

从经验上来看，我赞成第二种观点。

## 返回 4xx 会有什么问题？

在项目中，我们需要调用其他系统的 API 来操作资源。在某些场景下当多次调用删除同一个资源的 API 时，第一个响应是删除成功，但后续响应都是资源不存在的错误。

这个时候应该认为执行成功还是执行失败？

如果认为成功，那么应该捕获这个异常并且不做任何处理。既然我不需要做任何处理，为何服务端不返回成功的状态码呢？

如果认为失败，那么应该捕获异常并且做处理。但是要处理什么呢？“使服务端的该资源不存在” 明明就是预期的结果，却还要做错误处理。这让人很矛盾。

服务端返回 404 暴露了对该请求的处理方式，而客户端并不关心这个信息。客户端只想要该资源不再存在，即使该资源从未存在过。如果执行过后，该资源确实不存在了，就达到了客户端的目的。应该告诉客户端成功的消息。

## 应该返回什么状态码？

1. 如果操作立即成功，且无需给客户端更多的信息，则返回 204 No Content 
2. 如果操作立即成功，且需要给客户端更多的信息，则返回 200 OK 并在响应体里附带信息 
3. 如果操作被接受了，但可能需要比较长的时间才能执行结束，则返回 202 Accepted

## 多次操作成功是否应该返回不同的成功状态码？

有这个考虑是因为要识别这个删除成功的状态究竟是否由这一次请求所造成的。

但绝大多数情况下，并不关心这一点。所以返回同一个状态码就行了。


## 参考

> PayPal 的 API 风格指南：  
> [https://github.com/paypal/api-standards/blob/master/api-style-guide.md#http-method-to-status-code-mapping](https://github.com/paypal/api-standards/blob/master/api-style-guide.md#http-method-to-status-code-mapping)

> Is a HTTP DELETE request idempotent?  
> [http://leedavis81.github.io/is-a-http-delete-requests-idempotent/](http://leedavis81.github.io/is-a-http-delete-requests-idempotent/)



