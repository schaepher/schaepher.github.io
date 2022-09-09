# 设计模式


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

# 访问者模式

对同一个对象的不同目的的操作。例如访问人的姓名、年龄等。避免太多操作放到对象里面会污染到对象。

两种方式：

1. 传被访问数据自身
2. 被访问数据定义访问者必须实现的接口，由被访者决定要传哪部分数据给接口，不需要被访者的接口与访问者的接口一致。被访问者只需调用 me.Visit(Visitor)

抽象的被访问者可以通过 `visitor.Visit(this)` 把自己这个具体的类型传入进 Visitor，这样 Visitor 就可以知道访问者的具体类型。  
> https://stackoverflow.com/a/63652850

返回计算结果：

1. 把计算结果存入 Visitor
2. 把计算结果存入被访问者

# 策略模式

为了完成同一个动作，采取的不同方式。例如压缩文件，可以压缩为 tar，也可以压缩为 zip，或者 rar。

由被访问者定义策略应该实现的接口，其接口与被访问者的接口一致，类似于代理。被访问者调用实际的方法，并传入参数。

如果各种策略所需参数不一致，则需要使用访问者模式。
