# Repository 模式


从模型的角度看问题。站在调用 Repository 的用户的角度去看待这个东西。

从代码结构来看： Repository -> ORM(Store)

例如 Laravel 中的 Cache 用到的 Store。每个 Store 的存储介质不一样，但提供统一的接口。

```php
Cache::store("redis")->get("")
```

Repository 就像是一个 Collection，用户不知道它底层是用什么存储的。Repository 应该让使用者感觉对象就好像驻留在内存中一样。

## Repository 用于管理对象

可以在 Repository 层给数据加缓存。用于把查询的细节放到中间层，客户端无需关心查询细节。

## 面向集合资源库和面向持久化资源库

面向集合资源库没有“保存(save)”这一操作，而是有“添加(add)”这一操作，面向持久化资源库反之。

当对象被加入到面向集合资源库后，对于对象的直接修改，会影响到资源库中的对象。find -> modify -> find。第二次 find 可以查看到修改后的数据。

面向持久化资源库则是 find -> modify -> save -> find。

## 为不同存储介质创建不同的 Repository 实现

与 DAO 冲突。

## Repository 和 DAO 的区别

DAO 只负责将数据存储到特定存储介质中，不负责管理对象。

同一个对象在不同存储介质对应不同的 DAO，此时的 DAO 为 Store。如果直接用 DAO 而不是注册到 Repository 里面，则在 DAO 更换时，需要在所有用到的地方进行替换。而如果使用 Repository 模式，则只需替换 Repository 里面的 DAO。

直接用 ORM： ORM(Repository/Store)

如果想要在多个 Store 之间切换，则需要把 Repository 里面的单一逻辑下放到 Store，两者拥有相同接口。Repository 仅作为代理，此时编程三层：Repository -> Store -> ORM。

一开始可以先使用两层的方式，等到有切换的需求时，再切换到三层。如果没有切换的需求，则保持在第二层就行。毕竟如果只是更换，则两者的修改量是一样的。

什么情况下只使用一层？单文件项目之类的短期小项目。

其他时候首先考虑二层。有需要再转三层。

## Repository 和 Factory 的区别

Factory 负责制造新对象，Repository 负责查找已有对象。

Client --create_obj--> Factory   
Client --add_obj--> Repository --insert--> Database

## 参考文档

1. [https://developer.aliyun.com/article/758292](https://developer.aliyun.com/article/758292) 殷浩详解DDD系列 第三讲 - Repository模式
2. [https://www.baeldung.com/java-dao-vs-repository](https://www.baeldung.com/java-dao-vs-repository) DAO vs Repository Patterns
3. [https://github.com/eugenp/tutorials/tree/master/patterns/design-patterns-architectural/src/main/java/com/baeldung/repositoryvsdaopattern](https://github.com/eugenp/tutorials/tree/master/patterns/design-patterns-architectural/src/main/java/com/baeldung/repositoryvsdaopattern) 
