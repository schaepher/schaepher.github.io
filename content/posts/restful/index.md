---
title: RESTful 程度
date: 2018-10-08 00:19:00
updated: 2018-10-08 00:19:00
categories:
 - RESTful
tags:
 - RESTful
---

REST = REpresentational State Transfer

<!-- 本文参考 **REST-API-Design-Guide** 的内容。  
> [https://github.com/NationalBankBelgium/REST-API-Design-Guide/wiki](https://github.com/NationalBankBelgium/REST-API-Design-Guide/wiki) -->

<!-- more -->

## 逐步接近 REST  

Martin Fowler 在博客《steps toward the glory of REST》中提到

> [https://martinfowler.com/articles/richardsonMaturityModel.html](https://martinfowler.com/articles/richardsonMaturityModel.html)

简单的说：  

- level 0 ：  
    没有资源的概念。url 上面最后一个部分经常是个动词。例如：`POST /appointmentService`  。  

    甚至只有一个

    HTTP 头部不涉及业务逻辑，相当于降级为传输层协议。
- level 1 ：  
    有了资源的概念，在 url 上面使用名词。但只用到了两个 web 操作：GET、POST。  

    当发生错误时，仍然返回 `200 OK` 并附上错误信息。例如某个资源已被其他人创建（医生的预约名额），这是一个不相容（incompatible）的资源，你无法再创建。
- level 2：  
    除了 POST 之外，还使用更多的操作：DELETE、PUT、HEAD、OPTIONS、PATCH  

    出现错误时，不再使用 `200 OK`。例如上面的错误会返回 `409 Conflict` ，不用带上错误信息调用方也能知道是什么错误。  

    当资源创建成功时，不再返回 `200 OK`，而是返回 `201 CREATED` 。  
    这样就让 HTTP code 有更多的表达空间。  
- level 3：  
    返回的结果不仅包含了所请求的信息，还包含了该资源其他操作的链接。   

    > [http://olivergierke.de/2016/04/benefits-of-hypermedia/](http://olivergierke.de/2016/04/benefits-of-hypermedia/)
    
    客户端在请求的时候，从这些链接中取出想要的链接，并执行操作。客户端不应将这样的链接硬编码到代码里面，否则将来接口变动会很麻烦。  

    如果没有这些信息，它不能叫做 REST API，只能称之为 REST-like API。  

    > [https://github.com/NationalBankBelgium/REST-API-Design-Guide/issues/8](https://github.com/NationalBankBelgium/REST-API-Design-Guide/issues/8)  
    
    不能把所有操作的链接都暴露出来，而是根据用户的访问权限暴露出他所能访问的所有连接。  

    > [https://github.com/NationalBankBelgium/REST-API-Design-Guide/issues/9](https://github.com/NationalBankBelgium/REST-API-Design-Guide/issues/9)

## PUT 和 POST 的区别

[https://stackoverflow.com/a/630475](https://stackoverflow.com/a/630475)  

两者都可以用来创建资源，但是场景不同。  
- POST 让服务端决定资源的名称 `POST /questions`  
    服务器返回这样的链接： `/questions/<question_id>`
- PUT 由客户端决定资源的名称 `PUT /questions/<new_question>`  
    服务器返回这样的链接： `/questions/<new_question>`
    PUT 是幂等的。这意味着执行多次 PUT 的结果都一致。但是如果用 POST，就会产生很多个资源。    
    例如：x=5 是幂等的，这个赋值运算执行一百次， x 都是等于 5。但 x++ 不是幂等的。    
    [https://stackoverflow.com/a/2691891](https://stackoverflow.com/a/2691891)  
    除了 PUT ， GET 和 DELETE 也是幂等的。  
    PUT 可以用于替换已有的资源。而如果是部分更新，则使用 PATCH。

用 POST 还是用 PUT，主要还是看是否要求幂等。

其他的可以去看 RFC 7231。  

> [http://www.rfcreader.com/#rfc7231](http://www.rfcreader.com/#rfc7231)

> 2014 年 RFC 7230 - 7235 将原来的 RFC 2616 拆成六个单独的协议说明。    
> [https://www.infoq.cn/article/2014%2F06%2Fhttp-11-updated](https://www.infoq.cn/article/2014%2F06%2Fhttp-11-updated)  
> [http://www.rfcreader.com/#rfc7230](http://www.rfcreader.com/#rfc7230)  

> The fundamental difference between the POST and PUT methods is highlighted by the different intent for the enclosed representation. The target resource in a POST request is intended to handle the enclosed representation according to the resource's own semantics, whereas the enclosed representation in a PUT request is defined as replacing the state of the target resource. Hence, the intent of PUT is idempotent and visible to intermediaries, even though the exact effect is only known by the origin server.  
> POST 和 PUT 之间的根本区别突出在封装表征（enclosed representation，即请求体）具有不一样的目的。 POST 请求中的目标资源根据资源自身的语义处理封装表征，而 PUT 请求中的封装表征则是用于替代目标资源的状态。因此， PUT 的目的是幂等和对中介可见，即使确切的影响只有服务端知道。

## 无状态  

RESTful API 必须是无状态的。这意味着服务器不保存客户端的会话信息，而是由客户端来保存。  

例如：JWT（JSON Web Token）  
> [https://en.wikipedia.org/wiki/JSON_Web_Token](https://en.wikipedia.org/wiki/JSON_Web_Token)

服务端有一串密钥，将用户的登录信息加密，生成密文，并发给客户端。客户端在请求的时候，将密文放到 HTTP Header。服务端用密钥解密客户端发来的密文。如果无法解密，则说明这个密文不是由服务端的密钥加密的，是伪造的；如果能够解密，则表示该密文是由服务端的密钥加密的。

如果服务端有多台机器，那么每台机器只要用相同的密钥加密，其他机器就能解密。这样就能愉快地使用负载均衡了。

## url 形式

如果一个资源的名称由超过一个单词组成，那么单词间用减号（-)连接。例如：`/contract-types`。  

资源总是用复数命名，并且每个资源都有一个 ID

当 url 带 ID 时，获取的是单个资源；不带  ID 时，获取所有资源（或者说想要获取）。

## ID

在URL上使用 UUID ，但数据库里面的主键还是要用自增 ID。 
> [https://www.zhihu.com/question/43500172/answer/95903244](https://www.zhihu.com/question/43500172/answer/95903244)

理由是：  

- MySQL 的 InnoDB 对主键采用聚集索引。如果使用 UUID 作为主键，索引插入的位置是乱序的，会导致索引树节点的频繁分裂。同时由于相邻主键的数据存放在磁盘同一个或者相邻的页中，也会导致页的分裂，影响 IO。  
- InnoDB 的非主键索引叶子节点存储的是主键值。 UUID 比自增 ID 所占的存储空间大，使用存储占用大的主键会导致非主键索引的总体空间变大。  

## 资源间的关系

如果资源 A 必须依赖于资源 B，那么应该设计成这样：  

GET /tickets/12/messages

表明 messages 必须依赖于 tickets

## 名词 URL

搜索：Search  

执行：Execution  

批量执行： Bulk 

批量的另一种：例如创建一个删除的资源 POST /xxx/delete-requests

> Delete multiple records using REST  
> [https://stackoverflow.com/questions/21863326/delete-multiple-records-using-rest](https://stackoverflow.com/questions/21863326/delete-multiple-records-using-rest)


