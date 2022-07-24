---
title: 设计模式
date: 2020-03-27 01:05:00
updated: 2020-03-27 01:05:00
tags: 
- 设计模式
---

## 概念说明

在了解各种模式之前，要把自己代入一个基础库的开发者（库作者）的角度。

客户端：  使用库的人  

主体：  实际实现功能的库类

## 代理模式（Proxy） & 适配器模式（Adapter）

两者都是在客户端和主体之间构建一个中间层，让客户端间接访问主体。

```
客户端 ---> Proxy/Adapter ---> 主体
```

它们在客户端视角的区别是： 是否与主体实现了同一个接口（interface）。

```
Proxy implements AInterface

主体 implements AInterface

Adapter implements BInterface
```

### 代理模式  

客户端不直接访问主体，而是通过代理访问主体。即客户端创建代理对象和操作代理对象，不直接接触主体对象。

要从客户端和库作者的角度和不同场景去理解。

代理分为正向代理和反向代理。  

- 正向代理：  客户端创建代理类，弥补基础库的缺陷
- 反向代理：  库作者创建代理类，隐藏主体的一些方法，避免客户端调用到这些方法

#### 正向代理

对于客户端来说，基础库有可能写得不够完善。这里举两个例子：  

- 创建主体对象的成本很高  
  例如创建主体对象需要花 10 秒钟，或者需要消耗 10 MB 内存。  
  由于业务原因，客户端必须先创建主体对象。但如果太早创建主体对象，会影响到用户体验或者影响系统整体性能。  
- 主体没有对操作的结果做缓存  
  例如主体负责下载一个视频，但客户端如果多次发起下载同一个视频的请求，主体仍然会触发多次下载。  

如果创建成本高，那么可以先创建代理对象。当要做真正的操作的时候，代理对象创建主体对象，然后调用主体对象的操作。

```php
interface Graphic {
    public function draw();
}

class ImageProxy implements Graphic {
    private image;
    public function draw() {
        if ($this->image === NULL) {
            $this->image = new Image();
        }
        $this->image->draw();
    }
}

class Image implements Graphic {
    public function draw() {
        // ... 绘制
    }
}
```

如果是主体没有对操作的结果做缓存，则用 Proxy 维护缓存。

```php
interface UserQueryService {
    public function allUserInfo();
}

class UserQueryServiceProxy implements UserQueryService {
    private $userQueryServiceImpl = new UserQueryServiceImpl();
    private $cache = [];
    public function allUserInfo() {
        if (! isset($this->cache['all-user'])) {
            $this->cache['all-user'] = $this->userQueryServiceImpl->allUserInfo();
        }
        return $this->cache['all-user'];
    }
}

class UserQueryServiceImpl implements UserQueryService {
    public function allUserInfo() {
        // ... 调用 HTTP 接口获取所有用户信息
    }
}
```

#### 反向代理

对于库作者来说，他不想让客户端调用类的某些 Public 方法，但想在库内部调用这些方法。



# 构建器模式

类生成的构建器，做成类似于多级菜单，减少每次所需要看到的对象。

缺点是编写库的人要写很多类。优点是使用库的人很清晰。

