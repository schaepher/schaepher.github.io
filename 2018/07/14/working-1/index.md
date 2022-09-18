# 入职一年啦


从入职到现在已经过了一年，然而博客几乎没有更新。本来毕业时和过年前后是打算写点总结什么的，写着写着就没有继续。

但不写点回顾的话，心里总感觉难受。以后要是想回忆一下当初都做了啥，结果没想起什么，感觉都是在浪费时间，这就不好了。  

这几天刚好是我们这批新人入职满一年，脑中“写点什么回顾一下吧”的想法频繁浮现。索性就把周末时间拿来写这篇博客了。

<!-- more -->

## 公司、部门

在同班同学的安利下，来到现在就职的这家公司面试。现在我们在同一个小组。

当初是冲着说不用加班来的（然而后来却经常加班，虽然是自找的）。此外，待遇好也是非常吸引我的地方~

同事之前的氛围很好。大家人都挺好的。此外我们老大（我们都叫他大大~）经常会请我们吃下午茶，有时候会组织部门聚餐，上周六还一起去看了《我不是药神》。小组的聚餐也组织过几次。前面说过，这几天我们这批新人入职满一年，大家会买下午茶请部门的同事。于是我们就这样吃了一周下午茶，哈哈哈。在这样的部门里面，感觉很幸福~

也有不好的地方。我所在的小组就编程而言，我的水平是最高的了，其他技术方面的也差不多。这也就意味着在这个小组里面，没有大腿可以抱，只能通过自学来提高自己。自学的进步速度比不上有人带的速度。这也是我经常感到压力的原因——进步速度太慢了。

所幸的是，从去年十二月开始，我们部门有同事组织起了知识分享会，成立了学习小组。每周五下午会抽出两个小时的时间给知识分享会。期初是针对特定议题，大家各自学习，并在会上针对议题讲述所学内容或发表看法。后来则是由每个人自定主题，然后上台演讲。主题的范围很广，非技术相关的例如：时间管理、如何做好演讲、团队合作等；技术相关的例如：代理服务、分布式、存储组件等；不知道怎么分类的例如：人工神经网络介绍（我讲的），三维地图重建，密码学入门等。

总的来说，能学到东西，但还是不够。通常只有讲师学到的东西最多，其他人能学到多少，还是要看讲师讲得如何。像我讲的人工神经网络，虽然全程都是有画图讲解的（完全没有PPT），但是到了后半部分往深讲的时候，还是有一半同事懵圈了。

## 项目

一年间接触的项目总共有三个，姑且称作项目 A B C。用的语言都是 PHP。
- 主要参与的项目是 A ，是一个用 PHP 写的至少有十年历史的任务系统（是不是有点可怕？）。
- 项目 B 是参与了其中一个模块的重构，但重构得不彻底。因为这次重构的目的主要是加个流程的流转引擎进去。
- 项目 C 是个聊天机器人，用到了人工神经网络。然而我并没有负责核心部分（泪）。

项目 A 放后面讲，另外两个内容比较少。

### 项目 B

项目用的是 Zend Framework 框架，1.10.8 版本，2010 年 8 月发布的。现在最新版本是 3。

旧代码很少用到框架已经写好的东西，还有不少东西是框架已经写好，但还是自己写的。应该只是为了用上 MVC 和部分功能吧。

和其他模块的重构是把原来的代码拷一份，然后在上面修修补补的方式不同。我基本重写了所有代码。把业务相关的东西抽出来，简化复杂的逻辑，把大块的代码拆解成几个部分。然而这是有代价的，我为此加班了好多天。不过最后还是按期交付了。如果不重写的话，我可以不加班也能完成同样的功能，但是过不了自己这一关。自己经手过的代码，让它们保持以前那种糟糕的状态，实在不能接受。

不过我也知道自己这样做的风险。从公司的角度讲，自然是项目越快完成越好。万一要是因为我想把代码写好一些，导致项目进度变慢，那问题就大了。虽然在不少地方我克制了冲动，但还是经常忍不住去重构代码。幸运的是，项目的进度要求都没有紧张到没有时间来做优化。这也是受到公司氛围的影响吧~

### 项目 C

一开始冲着机器学习来的，兴冲冲地加入到项目里面，想着学点有深度的东西。但果然还是太年轻了。自身并没有相关的技术积累，想通过加入项目来提高技术的想法，是不是太幼稚了呢？

在这个项目组里面，到目前为止我都是负责后台的简单工作。例如提供知识库的录入界面等各种界面及其配套的后台逻辑代码，大部分工作都是前端相关。后端框架用的 EasySwoole ，因为涉及到通信，需要用 swoole 扩展。不过我这一部分的工作跟这个框架其实没什么关系。前后端接口用的 Restful API 标准，但是 GET 查询的支持不完善。

其他同事有的负责模型训练，有的是负责通讯模块。虽然原理我懂不少，但没有实践。后面我们会交换工作内容，我到时争取换到模型训练去。

说到我在这个项目所做的事情，可以引出一个话题：

#### 前端 VS 后端

其实我只想好好地做一个后端开发人员。嗯！前端是要了解一点，但是也不必要这么早吧。等这次做完，以后再有其他前端的事情，我都推掉。这次没有早点推掉，把自己给坑了。

待我成为后端大佬，需要拓展技术面的时候再去多了解和实践前端。

### 项目 A

由于是主要参与的项目，所以可以说的东西就比较多了。这是一个流程系统，用于 CDN 相关的运维操作。包括机器上下架，故障登记、发起部署等流程。涉及了公司几乎所有主要业务相关系统。  

事先说明，这是个内部系统，用户量不会大到哪去，但使用频率很高，而且跟绝大部分提供给用户的线上的机器有关。

前面说过，这个项目的历史有十年以上。想象一下十年前的开发吧，现在流行的几个框架中，最早的是在 2007 年左右发布第一个版本。没错，也就是说这个项目没有用到任何框架。最常见的 MVC 也是不存在的，基本所有东西都写在一起，面向过程。据说这个项目的开发人员基本都是从运维转到开发，包括目前组内的几个成员都是从运维转到开发的。

不过神奇的是，我参与的这部分（也是整个系统最有业务价值的部分）可以说是隔离的还不错。前辈们已经把前端相关的东西封装好了，只需要到配置界面配置一下，就能组合成一个简单的表单界面。剩下的就是写后端部分，你可以把它看成是一个接近纯 API 形式的系统，最终只要 return 一个 json 字符串就行了。这点实在是令人佩服。这也为我接下来的改造提供了便利，因为在整个请求中，会有一个地方成为主入口，只要在这个地方做个拦截，把部分请求重定向到另一个位置，最后返回的时候是一个符合规定的 json 字符串就行。

这个系统的开发面临几个问题：
- 代码管理方式落后
- 本地环境搭建复杂
- 单个代码文件过大
- 难以测试
- 维护成本高
- 没有文档

据说在我来之前的一年，已经有说要重构项目了，但一直没有行动。因为维护本身就要花去很多时间，再加上需求一直做不完。这周才又开始提起这件事，因为组内目前有几个同事，他们负责的部分没有需求了。而且我在最近的半年间也做了不少事情，对他们也会有帮助。

接下来说说我怎么逐个解决上面那几个问题吧。

#### 1. 代码管理方式落后

原本可以说是没有什么管理方式。事实上我们改代码基本都是直接到线上用 vim 改（导致我现在 vim 几个快捷键用得 66 的）。一旦保存，就会自动生成一份备份文件到指定的备份目录。然后我们会有代码审核，要调用 linux 的 diff 比较两个文件的不同，然后截图发到讨论组让其他人审核。有时候改的地方多，要截图好几屏幕。

连 svn 都没有，更不用说 git 了。

今年三月，我开始推动代码管理方式的变化，改成用 git 管理代码。当然，老大是支持滴。我做了几件事：  
1. 准备工作  
    - 找其他组了解到我们这边内部有搭了一个 Gitlab，于是到上面建了个仓库。
    - 线上代码整份备份，拷贝一份到我本地。把线上代码目录下，一些没用的东西都移动到一个备份文件夹。例如文件名为：！或者`这一类奇奇怪怪的文件；还有一些开发者个人的备份文件、测试文件等等，统统移出去。这些在移动之前都会把列表发出来，让其他人确认过才移动。
    - 找到程序运行时产生的文件夹，这些是要放到 .gitignore 里面的。
    - 原本超过 100G 的项目文件夹，只有大约 80 MB 的有用文件。大部分都是 log。这 80 MB 的文件里面，还有可以排除掉的，但可能有危险，就算了。这样以后要搭建新环境的时候，只要下载 80 MB 的文件就行了。之后把这些文件提交到 Gitlab 仓库上。
1. 代码同步  
    如果使用 Gitlab ，那么要怎么把代码同步到线上机器呢？最简单的就是在线上目录下直接用 git pull 了，只是要记得把 .git 目录屏蔽掉，不然别人直接把你 .git 下载过去，就能得到你整套代码了。当然，也可以在另外一个目录 pull ，然后用 rsync 同步到线上目录。后一种方式会比较安全，不过没有采用，可能是因为要支持线上修改代码？  
    线上修改代码是为了在上线代码后出现问题时能够立即在线上修改代码，然后不能影响到后续代码上线。要补充一点，这个项目没有定期发布版本的概念，一旦完成需求，就立即上线。既然是这样，就不能直接 git pull 。于是我写了个脚本专门用来同步。当线上代码和要更新的代码有冲突时，自动处理冲突——其实就是自动用冲突部分的线上代码覆盖上线的代码。
1. 培训  
    上面准备工作做完了，就得向组内其他人推广了。组内只有我那同学有接触过git，但也是那种 push 和 pull 的程度。这次用的是 GitHub Flow 的方式，就是 Pull Request + 审核，没有人可以直接 push 代码上去。  
    我总共组织了三次培训，每次半个小时到一个小时。把 git 的基本使用和 GitHub Flow 的方式都介绍了。然后还写了篇教程。之后大家就开始用起来。

前后大概一个月的时间，前期准备花去大概三周（毕竟还有需求要做）。培训前后跨度一周。培训完的下一周开始使用。算起来应该要从四月初开始算起，到目前为止合并了 760 个 Pull Request。

我们组四月份的时候来了个新人。当后来谈起 git 的时候，我说了在三月底才逐渐开始使用 git 以及以前是怎样管理代码的时候，她都惊呆了。

#### 2. 测试机

让我们回到还没使用 git 的时候。

上面说了修改代码时通常要在线上修改，为什么不在测试机上修改呢？  

- 测试机代码跟线上代码有很多不同的地方。数据库也有很多不同。我那个同学就曾经栽在数据库表字段不统一上。
- 我们的系统依赖于其他系统提供的数据，在测试机上难以获取所需数据，虽然他们也有提供测试机，但不好找到合适的数据。

不过我也有一段时间是在测试机上修改，然后复制到线上。但是 vim 编辑虽然挺熟悉的，但还是不舒服。后来就下载 PHPStorm ，在本地电脑上修改，然后通过它内置的 ftp 传到测试机上测试。

为啥不在本地搭建个环境呢？这其实也挺困难的。  
- 代码有很多依赖，甚至于有些代码写的是用 linux 的路径。你在 windows 下根本没法跑。
- 把系统跑起来的数据库表要先建好，数据要先准备好，但不好找到需要哪些表。

第一点还好解决，毕竟有虚拟机呀。第二点就比较麻烦，全部数据都同步的话，要几十个 G 吧。

于是本地搭建环境这点就先搁置了。要等到接下来说的这件事做完才有继续的可能。

#### 3. 调试

先说之前的开发是如何调试代码的。首先肯定是在线上调试，调试的手段是 echo var_dump print_r 这些，直接把数据打印到界面上。是的，你没看错。用户都能看到他们打印出来的信息。

大量的数据暴露给用户，而且我之前还看到把一个接口请求的 key 暴露出来。更惨的是，这是已经调试完，没有删掉的。也就是说存在相当长的一段时间。事实上代码里面有大量的这种输出信息没有删除。所幸直接用户都是公司内部员工，这要是外部人员使用，早炸了。

对于开发者而言，如果是自己写的代码，echo 看一下可能很快就找到问题。但如果是别人写的代码，可能要 echo 一大堆才知道问题在哪。更可怕的是，这如果是系统基础层面的问题，根本不知道在哪找 bug，那代码一坨坨（来自同事的描述）的。

有个比较好的地方是，这个系统有备机。我在备机上装了个 Xdebug，这才使得断点调试成为可能。当然，为了支持多人能同时调试，还去装了个 dbgp。这些在我之前的博客中有写了：[php+xdebug+dbgp远程调试（多人）](https://www.cnblogs.com/schaepher/p/8939616.html)。当时发到博客园首页，还被管理员踢掉哈哈哈。

此后我都是使用 IDE 来断点调试，这才能知道系统到底是怎么运行的。

#### 4. 本地环境

能够断点调试意味着我能够知道它连接了哪些数据库，查了哪些表。这样就可以开始做配置了。

为了方便以后新搭建系统，我还写了个半自动初始化的脚本。把要修改的配置组织好，然后转化成原系统可用的数据。还提示了要把系统跑起来，需要同步哪几个表格。但是碰到路径依赖的代码时，仍然要再去手动修改代码，然后重试。

这种方式持续很长一段时间，直到我最近接触 Docker 才得到解决。我在 Windows 10 上面装了 Docker。然后对 PHP 镜像做了定制，其实就是额外装了 xdebug 、 composer（PHP 的包管理工具）、一些项目会用到的 php 插件。

经过一些配置的调整，总算是跑起来了。效果还不错~不过还有几个地方需要调整和添加的，后续再继续处理。

#### 5. 单个文件太大

看以下几个数字：

19264  17622  13223  12160  6621  6067  4655

这些是几个主要文件的行数，最大一个将近两万行了。用 PHPStorm 打开后有点吃力，解析要好一会儿。

里面其实是很多个 if-elseif-else 组合成的，每个分支完成一件事情。其实可以把它们看为一个个 function，事实上把它们抽取为 function 也能正常执行。最大的一个文件由大概 200 个分支组成，平均每个分支 100 行代码。但是也有不少分支有 5~6 百行代码，3 百行的 foreach 循环了解一下？

后来我做了个改变。前面有提到，它在某一个地方会有一个统一的入口，然后也有一个统一的出口。我另外建了个文件夹，然后建了一个文件作为新的入口，把满足条件的请求转发到这个入口。就像是进入一个子系统。

这个子系统可以直接使用 PHP 的一些特性，例如命名空间。在里面写代码直接用面向对象的方式，只要最后返回的结果是 json 就行了。这样可以为以后的重构（其实是重写）做准备，提前写好一些工具类，积累一些需要注意的点。

在实现上面，没有直接使用开源框架。一个是编码问题，我们项目是 GBK 编码（其实也不是很难解决）；另一个是以后项目重写的成本问题。目前不用框架，把骨架搭建起来还是蛮快的。在一些实现上面会去参考开源框架，像 Yii2 和 Laravel ，也会往 PSR 上面靠。

这样单个文件的大小就变小了，变成多个小文件。很多可以重用的代码也可以封装起来，放到类里面。前面那么多年，没有留下什么有价值的代码，实在是可惜。如果以前有封装一些业务相关的代码，现在要了解业务也比较方便些。

新的代码会写在这里面。如果有旧代码需要维护，且感觉可以重构的时候，也会把代码重构到子系统里面。

这个是在 git 之后。因为做这种大规模添加和变更的时候，有 git 会比较好处理。

#### 6. 测试

这项目的测试基本都是在测试机上直接进入网页测试，没有什么单元测试的概念。有时候测试机没办法测试，只能到线上测。Emmm...是挺危险的。

嗯对，没有专门的测试人员。

现在 git 有了、IDE 有了、面向对象也有了，可以了解一下单元测试。正好公司有这方面的绩效要求。

以前那些代码很难测，我先处理的是面向对象这部分的单元测试，引入 PHPUnit。先把工具类的单元测试搞定了。

接着想着怎么测试以前的代码。还是从单一入口那里入手，一些全局变量都事先声明好，还有一些文件都导入进来，然后调用。当然还要处理其他问题，例如原先的代码里面，会直接 echo 出东西，这些要用 ob_start() 这种拦截下来。不过 PHPUnit 也有对这方面的支持。

#### 7. 文档

这项目没有什么文档，同事的理由是业务经常变化，文档要经常改，麻烦。不过连基础的业务无关的开发文档都没有，确实麻烦。新人来了还得找导师问，因为并没有相关的培训课程。

后来我写了篇开发文档，填补了这个空白。（据说写得不错）

自从引入了子系统，也补充了篇开发文档。不过因为结构挺清晰了，不用文档也能开发。

至于业务上的文档还没有写。之前公司的机器在做集群架构调整，目前我们这边还在做相应改变。调整完成后，我会逐渐把业务文档补充上去。

#### 8. 重构

上面提到这个项目要重构（重写）。这个其实才是我最感兴趣的地方，因为能学到不少东西。到时要向大佬们多请教。如果到时有大腿来指导就好了。

## 结束

你可能会问，哪来时间做这些事情？不用做需求吗？我说一个数据。我们加班是没有加班费的，但是有一个误餐补贴。每天加班到八点半后就有 20 块钱，而我上个季度的补贴是 1k+。

这一年间做的事情看起来不是很多，也不是很少，唯一能确定的是学到的东西不多。这是最让我忧虑的地方。这一点之前我们部门的一个大佬跟我聊的时候有说过，孤军奋战进步很慢。其实部门里面的高手也是有的，但我不善于使用已有资源这一点是硬伤，要想办法有所突破。

希望接下去能有更多进步的机会~我也会去多争取这样的机会。