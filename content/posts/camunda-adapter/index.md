---
title: 一种 Camunda 流程引擎 Adapter 层的实现 
date: 2020-03-27 21:27:00
updated: 2020-04-20 06:52:00
tags:
- Camunda
- BPMN
---

上一篇说明了选择 Camunda 的理由。这一篇说明如何实现适配层。

> 当前还没有专门写一篇对 Camunda 各个功能的详细介绍。如果要获得比较直观的感受，可以下载 Modeler 或者使用在线版的 Modeler 。  
> [https://demo.bpmn.io/](https://demo.bpmn.io/)

目录：

1. 为什么要做适配层？
2. 要对 Camunda 做扩充的部分
3. 数据表的扩充
4. 流程实例的操作
5. 前端动态表单的渲染
6. 结语

# 为什么要做适配层？

- 现有引擎无法满足业务  
    如果能满足，加个代理层就够了。
- 避免改源码导致升级困难  
    我们部门有个基于 k8s 源码修改的项目，当年拿过公司的大奖。现在由于没人维护的来，已经凉了。
- 可以兼容其他流程引擎  
    当前选的引擎即使能满足当前业务需要，但未必满足其他业务的需要。更何况要形成一个基础设施给其他组件使用。  

<!-- more -->

```
+---------+
|         |
| System  |
|         |
+--+--+---+
   |  ^
   v  |
+--+--+---+
|         |
| Adapter |
|         |
+--+--+---+
   |  ^
   v  |
+--+--+---+
|         |
| Camunda |
|         |
+---------+
```

# 要对 Camunda 做扩充的部分

- 各业务系统有自己的系统界面，也有各自需要展示的内容，不能直接使用 Camunda 自带的管理界面。

- Camunda 内置的表单支持使得业务系统对其有一定的依赖。要改成在业务层处理。

- Camunda 在一次请求跳转时只能对原任务和目标任务同时应用或者不应用参数检测。但其实应该要在取消原任务的执行时不检测参数，在创建目标任务的执行时检测参数，因此要分两次。

- 流程和流程实例 ID 是 UUID，但要展示整数 ID 给用户。

- 流程实例自动化任务出错时，要转交给运维处理。

- 制定 External Task Client 的规则

# 数据表的扩充

为了适应业务需要，需要另外创建几张数据表：  

- 流程定义信息表
- 流程实例信息表
- 流程节点日志表
- 服务定义表
- 服务请求客户端管理表

### 流程定义信息表

无论是团队内部沟通还是和需求方沟通，最经常用到的用于区别流程的信息是流程的 ID。大家都不太喜欢用流程的名称来沟通，除非是比较少见的流程。而且在各种文档中也是使用流程的 ID。因此这个 ID 信息需要展示给用户。

由于是从旧系统迁移过来的，所以要保证原先流程的 ID 不变。所以不适用自增 ID 作为流程 ID，而是新增一列专门存储这些 ID。

以下 pd 表示 process definition，e 表示 engine 。

|字段|作用|
|:--|:--|
|id|自增 ID|
|pd_id|流程 ID，兼容旧系统|
|e_pd_key|底层流程引擎的流程名称，也用于翻译后作为名称展示|
|e_pd_version|当前使用的流程版本号|
|e_pd_version_max|底层流程引擎的流程最高版本号|
|category|流程分类|
|maintainer|维护人|
|doc_link|文档地址|
|note|备注|

Camunda 可以通过流程名称和流程版本确定一个特定的流程定义 UUID，所以不需要在这里加上 UUID。  

如果要加入其他引擎，且这些引擎不是用 key 和 version 确定，则可以加入 UUID 字段。并且还需要加入 engine 字段用于标识使用哪个引擎。

当新版本发布时，e_pd_version_max 加一， e_pd_version 保持不变，只能人为修改。这样便于做测试。

这一部分没有什么特别的点，实现起来不难。

### 流程实例信息表

pi 表示 process instance

|字段|作用|
|:--|:--|
|id|自增 ID，作为流程实例 ID|
|pd_id|流程 ID|
|e_pi_id|流程引擎的流程实例 ID，用于与流程引擎的实例保持关联|
|e_pd_key|底层流程引擎的流程名称，也用于翻译后作为名称展示|
|e_pd_version|当前使用的流程版本号|
|e_pi_activity_name|当前所在的节点名称|
|name|流程实例名称，由创建人填写|
|creator|创建人|
|source|创建来源，其他系统可调用 Restful API 创建流程实例|
|priority|优先级|
|handlers|处理人，可以有多个|
|status|当前流程实例状态|
|tags|标签，作为补充信息|

流程实例状态：  

|类型|作用|
|:--|:--|
|创建|流程实例刚创建|
|待提交表单|需要等待用户提交表单|
|等待执行器|自动化执行步骤，需要等待 External Task Client 获取任务|
|执行中|任务执行中|
|出错|执行时报错|
|暂停|暂停流程实例执行|
|结束|正常流程结束|
|终止|人工关闭流程或者其他非正常结束关闭|

**自增 ID**：

一开始打算直接用 UUID 作为流程实例的 ID，但产品经理说使用跟原系统一样的数字 ID 比较好，用户用起来也比较习惯。

> 举个例子，这个有点像 B 站以前用 AV 号而现在用 BV 号给用户带来的区别。

由于流程实例本身有权限控制，用自增 ID 也爬不了多少。就算爬了也没有什么影响，所以还是保留了自增 ID，并且初始 ID 设置为比当前流程实例多一个数量级，以保证迁移过程中不会出现 ID 冲突。

**当前所在的节点名称**：

用户在查看列表的时候想直到流程实例的进度，可以用这个名称展示给用户。

另外还可以作为重启流程实例时跳转的节点。

**创建来源**：

流程实例有时候碰到问题会回退给创建人，这就要求创建人必须是一个具体的用户。而如果不标注来源，则该具体用户可能无法获取相关信息来解决问题。

**优先级**：

这个字段用于给 External Task 标注优先级，优先级越高越先执行。

**处理人**：

分为两种情况：

- 填写表单的人
- 自动化步骤出现一些意外的问题，将会转交给相关运维人员处理

**流程实例状态**：

对底层引擎流程实例状态的缓存，用于列表查看时减少对底层引擎的查询。

但是什么时候更新这个状态就成了一个问题。如果没有及时更新，会给用户带来疑惑。比如说流程实例在底层引擎已经结束了，但是这个状态却不是结束状态。后续会对此做详细说明。

**标签**：

目前作为一些业务信息的补充，仅用于展示。

### 流程节点日志表

这个信息用于展示哪些节点执行过，以及相关时间点和输出信息。

由于各种数据或者业务问题，或者确实是正常的执行但用户误认为流程实例的流向有问题，这个时候可以参考这些信息。

|字段|作用|
|:--|:--|
|id|自增 ID，没有额外作用|
|name|节点标识，用于确定唯一节点|
|i18n|翻译标识，用于翻译并展示节点名称|
|pi_id|流程实例 ID，便于关联和应对底层引擎 ID 的变化|
|status|执行状态。等待执行、执行中、成功、失败、超时|
|operator|操作人。可以是用户，也可以是 External Task Client 的 ID|
|message|结果信息|
|started_at|开始执行的时间|
|ended_at|结束执行的时间|
|timeout_at|超时的时间|

**节点标识**：

用于确定流程中的一个唯一节点，在绘制流程图的时候配置。

由于同一个功能的节点在流程中可能被使用多次，因此该字段会加上一些无关紧要的信息来相互区分。

**翻译标识**：

由于同一个功能的节点在流程中可能被使用多次，在不同位置的同一个功能的节点所代表的业务含义不一定是相同的，所以翻译标识要另外指定。

**流程实例 ID**：

由于特殊业务需求，有些流程实例在被强行关闭或者正常结束后，需要重新激活。

Camunda 提供了这种支持，但它创建了新的流程实例，其流程实例 ID 自然也就和之前的不同。

这时有两种选择：

- 学 Camunda 将流程实例相关信息复制一份，创建新实例
- 保持当前实例不变，仅变更实例绑定的底层引擎实例

我选择了第二种。因为第一种成本比较高，且在当前业务场景下没有带来价值，用户也不愿意接受。

**超时时间**：

设置超时时间是为了避免由于各种不确定性原因导致没有正常结束时，该节点状态没有得到更新，而用户会觉得困惑。

### 服务定义表

该表用于管理节点和 API 的映射关系。

Camunda 有一种叫做 External Task 的节点类型，表示该任务是外部任务。需要外部系统主动拉取任务并提交结果。外部系统可以将这个拉取并提交结果的功能抽取出来，单独创建一个 External Task Client （以下将其简称为 ETC） 。

ETC 从 Camunda 拉取特定 Topic 的 External Task，然后执行业务逻辑。

External Task 的 Topic 在配置流程图的时候指定。ETC 在启动时需要指定 Topic。

最开始写 ETC 的时候，是参照官方的 JAVA 版本写了一个 PHP 版本。

整个流程大致如下：

```
+-----------------------------------------+
|                                         |
| Adapter            (5)                  |
|                   Submit                |
|                                         |
|      +--------------------------+       |
|      |                          |       |
|      v             (1)          +       |   (3)
|              Fetch And Lock             | Request
| +----------+               +----------+ |         +--------+
| |          | <-----------+ | External | | +-----> | API    |
| |  Camunda |               | Task     | |         | System |
| |          | +-----------> | Client   | | <-----+ +--------+
| +----------+               +----------+ |
|              External Task              | Response
|                    (2)                  |   (4)
|                                         |
+-----------------------------------------+
```

使用这种方式时要解决的一个问题是：如何通过流程图配置的节点信息来判断该节点执行时要请求哪个接口？

有一个简单的做法是在节点的 Task ID 上应用一些规则。

> 这里使用 “Task ID” 这个表述，是为了和 Camunda 保持一致。这个 Task ID 是一串由英文单词组成的有意义的字符串。

例如将 Task ID 设置为：`Users_Decisions_ShouldDoSomething` 

在 ETC 获取该节点任务执行时，配置 ETC 将 ID 转化为 `POST /users/decisions/should-do-something` 。

它的优点在于实现起来简单，缺点是：

- 难以控制请求方式。  
    只能用 POST。不过如果要用其他的方法，可以将 Task ID 的第一个部分设置为方法，但 Task ID 会变得很长。如 `Post_Users_Decisions_ShouldDoSomething` 。
- 难以做到近似的 Restful API 。  
    比如实现 `/users/{uid}` 这种在 URL 上放用户 ID 的功能，需要再对 Task ID 做定制。
- 难以控制超时时间。  
    超时时间是为了在各种问题导致 ETC 无法 complete 一个任务时，只要等待过了超时时间， ETC 就可以重新拉取到该任务。

超时时间是在第一步拉取任务的时候设置的，也就是在 ETC 上做配置。但是每个 ETC 只能配置一种超时时间。

最初的做法是每一种超时时间都设置一个特定 Topic，比如 XXX_3MIN 表示超时时间为 3 分钟。然后启动一些 ETC ，通过启动参数配置对应的超时时间。但是从实践的结果看，这样更新起来不灵活，有时候还需要重启 ETC。

上面这些问题虽然在 Task ID 上或者 Topic 上多做一些定制化就能完成，但是会使得它们自身变得越来越复杂。并且因为它们都是配置在流程图上的，随着 Task 越来越多，越难以更改。一旦要新加一个规则，会导致所有流程都得改一遍。

怎么优化呢？

在 Adapter 层加一个 External Task 定义表。在 ETC 获取到任务后查询这个表，根据查询结果做相应调整。

|字段|作用|
|:--|:--|
|id|自增 ID，没有额外用途|
|task_id|External Task ID |
|method|HTTP 方法|
|url_path|URL 的 Path 部分|
|url_query|URL 的 Query 部分|
|timeout|超时时间|

优化后的流程如下：

```
+-------------------------------------------+
|                                           |
| Adapter              (7)                  |
|                   Complete                |
|                                           |
|        +--------------------------+       |
|        |                          |       |
|        v             (1)          +       |   (5)
|                Fetch And Lock             | Request
|   +----------+               +----------+ |         +--------+
|   |          | <-----------+ | External | | +-----> | API    |
|   |  Camunda |               | Task     | |         | System |
|   |          | +-----------> | Client   | | <-----+ +--------+
|   +----------+               +----------+ |
|                External Task              | Response
|                      (2)        +    ^    |   (6)
|                                 |    |    |
|                      (3)        |    |    |
|                 Fetch API Info  |    |    |
| +------------+                  |    |    |
| | External   | <----------------+    |    |
| | Task       |                       |    |
| | Definition | +---------------------+    |
| +------------+                            |
|                    API Info               |
|                      (4)                  |
|                                           |
+-------------------------------------------+
```

### 服务请求客户端管理表

这个表用于管理 ETC 客户端。

主要解决两个问题：

- 关闭前等待执行中的任务结束
- ETC 数量动态调整

**关闭前等待执行中的任务结束**：

有时候要重启 ETC，但是因为 ETC 总是会获取任务执行，所以只能等深夜没有流程在执行的时候重启。

如果直接关闭的话，会导致任务虽然执行成功了，但由于没有调用 Camunda 的 complete 而超时。超时就会重新执行。

如果是幂等的接口倒是不会出问题，但有些幂等难度大或者消耗的资源大，二次执行会出问题。

那么让 Camunda 在 ETC 请求任务的时候不给任务是否可行？因为获取不到新任务后，总是能等到所有 ETC 执行中的任务都结束。

Camunda 提供了挂起（Suspend）流程实例的功能，虽然能避免流程实例的任务被 Fetch，但同时也使得正在执行的任务无法执行 complete。

那怎么办？

有两种方式：

- ETC 每次执行完一个任务后，就自动重启
- ETC 在向 Camunda 获取任务前，都先查询一下自己能否获取任务

这里选择第二种，需要额外的表格维护 ETC 的信息。

|字段|作用|
|:--|:--|
|id|自增 ID，没有其他作用|
|etc_id|客户端 ID|
|topic|客户端获取的任务的 topic|
|switch|on/off 控制是否继续获取任务|

**ETC 数量动态调整**：

调整的依据来自于两方面：

- 流程实例的数量
- 业务系统 API 的负载情况

如果流程实例的量大，且业务系统 API 负载比较低，可以添加更多 ETC ，加快整体的速度。

|字段|作用|
|:--|:--|
|id|自增 ID，没有其他作用|
|topic|客户端获取的任务的 topic|
|count|启动客户端的数量|

手动控制的话，这样就够了。如果要通过采集信息自动控制，那么可以再加两个参数：

|字段|作用|
|:--|:--|
|count_max|启动客户端的最大数量|
|count_min|启动客户端的最小数量|

### 动态表单定义表

Camunda 自身支持以下几种类型的表单：  

- 嵌入式 HTML 表单  
    对 Camunda 依赖性强。
- 基于 XML 生成表单  
    在流程图绘制工具里面定义表单，只能做简单的功能。
- JSF 表单  
    和嵌入式 HTML 表单类似。
- 通用表单  
    功能太少。

由于业务上的表单比较复杂，又不能太过于依赖 Camunda，因此表单的定义和渲染需要另外做。

表单的功能至少需要包括：

- 选择项动态加载
- 丰富的支持  
    如上传文件和图片展示。
- 前端页面数据格式校验

表单有两种形式：

- 静态表单  
    把表单定义放在前端，前端直接渲染。
- 动态表单  
    把表单定义放在后端，前端提供基本组件。前端获取后端对表单的配置，根据这个配置做渲染。

我们选的是动态表单。一是因为原先的系统就是这么做的，同时也比较灵活；二是因为我们团队没有专门的前端。  

动态表单可以放业务层，也可以放流程引擎 Adapter 层。

如果想要多个接入流程引擎的系统都可以使用，可以放 Adapter 层。就算有的系统不想用这个动态表单，也完全不影响。流程引擎中台的同事倒是对我们动态表单的实现比较感兴趣。

分为两张表：  

- 表单项组件表
- 表单定义表

表单项组件表：  

|字段|作用|
|:--|:--|
|id|自增 ID|
|name|组件名称|
|config|组件的配置（Json），主要是数据校验|
|default|默认值|

前端用的是 Vue，每个表单项直接对应一个 Component 。

表单定义表：  

|字段|作用|
|:--|:--|
|id|自增 ID|
|p_id|流程定义 ID|
|form_key|表单名|
|version|表单版本|
|group|表单内部分组，支持翻译|
|cpn_id|Component ID，表单项组件表中的 ID|
|order|在表单中所处的位置|
|field|变量名|
|label|渲染表单时，该组件的展示名称，支持翻译|
|config|组件的配置（Json），主要是数据校验|

### 表单暂存表

用户在编辑完表单时，可能因为各种原因无法全部填写完，又想保存当前已填写的数据。

可以创建一个数据表用于存储这些暂存数据，当表单提交后删除这些数据。

|字段|作用|
|:--|:--|
|id|自增 ID，没有其他作用|
|pi_id|流程实例 ID|
|form_key|表单 ID|
|name|变量名称|
|value|变量值，以 json 形式存储|

提交后的表单数据去哪了？  

Camunda 里的每个流程实例都可以有对应的流程实例变量集合，可以从下面的接口中获取：  

> Get Process Variables  
> [https://docs.camunda.org/manual/latest/reference/rest/process-instance/variables/get-variables/](https://docs.camunda.org/manual/latest/reference/rest/process-instance/variables/get-variables/)  

为了便于理解，我画了一张图：  

```
+-------------------------+
|                         |
| Process Instance        |
|                         |
| +----------+            |
| |          |            |
| | Global   +<-+         |
| | Variable |  |         |
| | Box      |  | Publish |
| |          |  |         |
| +--------+-+  |         |
|    fetch |    |         |
|          |    |         |
| +--------------------+  |
| |        |    |      |  |
| | Nodes  |    |      |  |
| |        |    |      |  |
| | +---------------+  |  |
| | |      |    |   |  |  |
| | | Node |    |   |  |  |
| | |      v    |   |  |  |
| | | +----+----++  |  |  |
| | | |          |  |  |  |
| | | | Local    |  |  |  |
| | | | Variable |  |  |  |
| | | | Box      |  |  |  |
| | | |          |  |  |  |
| | | +----------+  |  |  |
| | |               |  |  |
| | +---------------+  |  |
| |                    |  |
| +--------------------+  |
|                         |
+-------------------------+
```

即流程实例里面会包含一个全局的流程实例变量盒子，所有流程实例级别的变量都会放进去。

然后每个节点都有自己的本地变量盒子。它可以从全局盒子获取变量映射到本地盒子，也可以把本地变量发布到全局盒子。

# 流程实例的操作

- 创建
- 暂停和恢复
- 节点跳转
- 表单处理
- 关闭流程实例
- 重启流程实例

### 创建

先在自建流程实例表添加一条记录，然后把流程实例的 ID 、创建人等一些基本信息作为变量，调用流程引擎创建实例的接口时一起传进去。

> Start Process Instance  
> [https://docs.camunda.org/manual/latest/reference/rest/process-definition/post-start-process-instance/](https://docs.camunda.org/manual/latest/reference/rest/process-definition/post-start-process-instance/)

这些流程实例基本信息的变量在存储到 Camunda 里面时，会给变量名加一个 meta 前缀。

例如 id 加上前缀后变成 `meta__id` 。

注意，如果变量名使用下划线，在搜索变量的时候不能用 GET 接口，要用 POST 接口。  

> Get Variable Instances  
> [https://docs.camunda.org/manual/latest/reference/rest/variable-instance/get-query/](https://docs.camunda.org/manual/latest/reference/rest/variable-instance/get-query/) 
> Get Variable Instances (POST)   
> [https://docs.camunda.org/manual/latest/reference/rest/variable-instance/post-query/](https://docs.camunda.org/manual/latest/reference/rest/variable-instance/post-query/) 

### 表单处理

#### 先创建流程实例再填表单还是反之？

两种都可以。

我选择的是先创建流程实例再填写表单。

接下来分析两者的优缺点。

**先填写表单再创建流程实例**：  

优点：

- 如果表单填写一半时发现没有必要走流程或者由于数据不足不能填完整，就不会创建流程实例

缺点：

- 如果流程里有其他表单，则初始表单与其他表单的处理逻辑不统一

**先创建流程实例再填表单**：  

优点：

- 所有表单处理逻辑统一

缺点：

- 必须创建流程实例才能填写表单，如果最终不需要该流程实例，则流程实例列表会多出一个无用的实例

这个缺点可以缓解。  

我见过一种实现：先创建实例，填完第一个表单后才在自己扩展的实例表中添加该实例。这样用户看流程实例列表就不会有无用的实例。

但是这个实现有个问题。用户很有可能经常创建流程实例后不提交第一个表单，可能直接返回或者刷新页面丢失该信息。经过一段时间会发现底层引擎保留大量流程实例，以至于流程引擎处理速度变慢。

#### 获取当前表单

由于 Camunda 做的是标准的流程引擎，因此界面中每个用户都会有自己要处理的 UserTask（表单） 列表。

我们的场景是流程实例只会有一个节点执行，并且表单是和流程实例放在一起的。并且用户要求要一次性查看所有已填表单，包括其他人的表单。所以要从流程实例的角度处理。

我们需要一个 “获取当前表单” 的接口，但由于上面的原因， Camunda 没有现成的接口。只能自己根据 Camunda 已有接口封装了。 

1. 获取流程实例当前节点  

    > Get Activity Instance  
    > [https://docs.camunda.org/manual/latest/reference/rest/process-instance/get-activity-instances/](https://docs.camunda.org/manual/latest/reference/rest/process-instance/get-activity-instances/)

2. 根据节点 ID 获取 Form Key 

    > Get Form Key   
    > [https://docs.camunda.org/manual/latest/reference/rest/task/get-form-key/](https://docs.camunda.org/manual/latest/reference/rest/task/get-form-key/)

获取 Form Key 后就可以到动态表单定义表里面获取表单的定义，传给前端渲染。

#### 表单的暂存

前面提到表单提交后要删除暂存的数据，因为如果没有删除这些数据，会碰到一个问题：

当用户将流程实例驳回到前面的表单节点时，用户修改表单但是不选择提交而是暂存，下次用户进入这个表单界面时数据是以 Camunda 里面为准还是暂存的数据为准？

- 如果选择以暂存的数据为准，那么要考虑一个场景：  

    用户初次提交表单后，流程实例后面的步骤修改了表单里的某些数据。接着有用户将流程实例驳回到这个表单，此时如果选择以暂存数据为准，会导致表单展示的是未修改的数据，在业务上会出现问题。

- 如果选择以 Camunda 的数据为准，那么就会导致用户发现其修改并暂存的数据不见了

所以删除暂存数据是一种解决方案，如果暂存表里面有数据，就以暂存表为准，否则以 Camunda 为准。

#### 表单数据校验

数据校验分为两部分：  

- 数据类型校验
- 业务关系校验

Camunda 自身支持数据类型校验，但如果有复杂的类型就得在引擎层面自定义校验类。

并且由于业务关系校验不能放在引擎层面，所以两者一起放在业务系统层面处理。

```
                  数据格式
 数据格式          业务关系
 校验             校验

+-------+        +--------+        +---------+
|       | submit |        | submit |         |
| front |        | system |        | engine  |
|  end  | +----> |        | +----> | adapter |
|       |        |        |        |         |
+-------+        +--------+        +---------+
```

暂存的接口一般只会执行数据格式的校验，并且不对是否必填做校验。

#### 提交表单

提交表单到 Adapter 层的时候要做以下校验：  

- 当前节点是否是表单节点
- 当前表单节点的 Form Key 是否与提交的 Form Key 一致

#### 流程实例转交

转交分为两种类型：  

- 表单节点转交
- 自动化节点转交  
    指的是将操作权交给其他人，一般自动化节点出现错误的时候，会转交给运维人员处理，运维人员可以转给其他运维同事帮忙处理。

两者都需要修改流程实例信息表中的处理人字段。

表单节点除此之外还要调用 Camunda 设置操作人的接口：  

> Set Assignee  
> [https://docs.camunda.org/manual/latest/reference/rest/task/post-assignee/](https://docs.camunda.org/manual/latest/reference/rest/task/post-assignee/)

### 暂停和恢复

Camunda 提供了一个 suspended 接口，用于挂起整个流程实例。使流程实例处于暂停状态。

> [https://docs.camunda.org/manual/latest/reference/rest/process-instance/put-activate-suspend-by-id/](https://docs.camunda.org/manual/latest/reference/rest/process-instance/put-activate-suspend-by-id/)

官方文档有关于挂起流程实例的完整说明。  

> [https://docs.camunda.org/manual/latest/user-guide/process-engine/process-engine-concepts/#suspend-process-instances](https://docs.camunda.org/manual/latest/user-guide/process-engine/process-engine-concepts/#suspend-process-instances)

一旦挂起流程实例，会产生以下影响：  

- 用户无法提交表单
- External Task Client （以下简称 ETC） 的 complete 无效
- 用户无法执行跳转节点

虽然无法变更流程实例的执行节点，但是可以修改流程实例的全局变量。

最初由于节点跳转的需要，没有把挂起直接作为流程实例的暂停功能，下面会对此做出解释。

### 节点跳转

节点跳转最常用的就是驳回功能。之所以不直接说驳回，是因为除了驳回外，有时还需要跳转到后面的节点。

这是因为自动化流程中，有一些节点会出现难以预测的问题。有的可以通过优化流程图来解决，有的难以通过优化流程图解决。所以需要人工干涉，跳过当前节点的执行或者返回前面的节点执行。

#### 跳转的接口

Camunda 对节点跳转的支持是在流程实例修改接口。

> [https://docs.camunda.org/manual/latest/reference/rest/process-instance/post-modification/](https://docs.camunda.org/manual/latest/reference/rest/process-instance/post-modification/)

它可以取消一个节点的执行（cancel），也可以开启一个节点的执行（startBeforeActivity）。

执行修改接口时，有一个参数需要注意： skipIoMappings 。这个参数表示是否跳过节点输入输出映射的校验。为了解释这个参数，得先做个补充说明。

External Task 有个输入输出变量（Input/Output Variable）配置。用于将全局变量映射到本地变量（Input），或者将本地变量发布到全局变量（Output）。

当开始执行一个 Task 之前，会对 Input Variable 执行映射。此时如果映射配置中的全局变量不存在，就会报错。因为变量不存在是一个错误的状态，不能强行执行。结束一个 Task 则会对 Output Variable 执行映射。

如果一个 External Task 没有执行完，就不会生成 Output Variable 所需的本地变量。这个时候如果取消该执行，会默认进入映射变量的逻辑，导致出错。所以用 cancel 的时候需要开启 skipIoMappings 。

而跳转到目标节点时，又需要校验 Input Variable 映射所需的全局变量是否存在，否则强行执行会有问题。此时应该关闭 skipIoMappings 。

但 Camunda 这个 modification 接口的 skipIoMappings 放在最外层，表示一次只能设置一种 skipIoMappings 。  

另外 skipCustomListeners 总是开启。

因此想要实现跳转，就得分为两步：

- 在目标节点 startBeforeActivity ， 请求时关闭 skipIoMappings ，开启 skipCustomListeners  
- 如果上一步成功，则在当前节点 cancel ， 请求时开启 skipIoMappings ，开启 skipCustomListeners  

需要注意一个问题：  

执行跳转的接口前要保证流程已处于暂停状态。否则如果 cancel 节点时，节点已经完毕并转入下一个节点，就会出现 cancel 失败并且此时流程有两个执行的节点。  

但是如果用流程实例挂起接口使流程实例处于暂停状态，也会受到挂起状态的限制而没办法执行跳转。

#### 支持跳转的暂停状态

暂停的实现经历过两个版本。

最初版本中，节点跳转前要求用户必须先手动暂停流程实例。

前面提到挂起流程实例后无法跳转节点，所以专门为当时的流程实例设置一个暂停的状态。

如何实现可跳转节点的暂停？

这里要处理流程实例节点的两种状态：  

- 还未被 ETC 获取。此时可以想办法让 ETC 没办法获取到处于暂停状态的流程实例的任务。
- 已经被 ETC 获取。此时可以让 ETC 不执行 complete 

接下来详细说明。

首先是 **还未被 ETC 获取** 的场景。

如何让 ETC 不获取暂停状态的流程实例？

通过查询文档得知流程实例碰到 `failedExternalTask` 这种 Incident 的时候， ETC 不会获取该流程实例的任务。  

> [https://docs.camunda.org/manual/latest/user-guide/process-engine/incidents/#incident-types](https://docs.camunda.org/manual/latest/user-guide/process-engine/incidents/#incident-types)

那么如何生成这种 Incident ？

Incident 没有一个 create 的接口，所以无法直接创建。

从刚才的文档上可以看到当 retries <= 0 的时候会生成 `failedExternalTask` 类型的 Incident 。

每个 External Task 的 retries 值默认为 1 。当 ETC 报告一个错误的时候，将 retries 减一。

但是用户如果想要跳转节点，不会想要等到当前节点出错，万一它不出错怎么办？

通过找文档发现 External Task 有一个设置 retries 的接口。  

> [https://docs.camunda.org/manual/latest/reference/rest/external-task/put-retries/](https://docs.camunda.org/manual/latest/reference/rest/external-task/put-retries/)

尝试直接将 retries 设置为 0 ，发现可以生成 `failedExternalTask` 类型的 Incident 。

这样节点还未被 ETC 获取的场景就得到了处理。

接下来是 **已经被 ETC 获取** 的场景。

在 ETC 获取任务执行后设置 Incident 就没法阻止，并且 Incident 的情况下 ETC 仍然可以 complete ，使得流程继续往下走。所以如果只有上面的处理，点击暂停可能会出现失败的情况。

这就得在 Adapter 层加一个处理。当 ETC 执行 complete 的时候请求给 Adapter，Adapter 查询流程实例是否有 Incident，如果有就不提交给 Camunda。

但如果在查询到没 Incident 和提交给 Camunda 之间设置了 Incident 呢？

这个问题在于没办法通过接口请求对 Camunda 的表直接加锁。

不过我们可以在自定义的流程实例信息表里的 status 上想办法。

- 在执行暂停的时候，将该流程实例所在行加排他锁，然后更新为暂停状态，更新完释放锁。  
- ETC 执行 complete 之前，对流程实例加排他锁，查询到的状态如果是暂停状态，则放弃 complete，否则执行 complete 。之后释放锁。

已经被 ETC 获取的场景也处理了。

上述的暂停只能针对 External Task，其余的就无法暂停了。

于是我后来重构了这部分代码，把 Incident 和 Suspend 结合在一起，让跳转的时候不需要先手动暂停。

步骤为：

1. 设置 Suspend ，防止 ETC 获取任务
2. 流程实例信息表设置状态为 incident
3. 设置流程引擎实例 Incident
4. 取消 Suspend
5. 设置新节点位置
6. 取消当前节点，这个动作会连同 Incident 一起删除

#### 如何获取跳转获取目标节点的 Task ID

有三种做法。

> 以下 “用户” 表示运维人员或者某个用户部门的公共账号，不是所有人都有跳转的权限。

- 通常的做法，即把执行过的节点以下拉菜单的形式列出来，用户选择一个，然后执行。  

    要实现这个功能，可以使用节点日志的信息。将节点执行日志中的 Task ID 取出来去重。它的缺点是只能跳转到已经执行过的节点。

- 将流程中所有节点列出来，让用户选择。

    解决了第一种无法跳转到未执行过的节点的问题。但带来新的问题：流程所有节点的信息如何获取？

    Camunda 的接口没有提供这个信息，最多只有流程图的 xml 。解析 xml 是一种方法，不过也比较麻烦。

    如果在发布流程定义的时候将所有节点信息放入一张记录节点信息的表。这不仅需要解析 xml ，还需要添加一张数据表，更麻烦。

- 直接将流程图展示给用户，用户在流程图上选择一个节点，然后点击跳转。

    不仅直观，而且不用自己写解析，直接用 Camunda 的 bpmn-js 。

    > [https://github.com/bpmn-io/bpmn-js](https://github.com/bpmn-io/bpmn-js)

    bpmn-js 提供了很多示例。 

    > [https://bpmn.io/toolkit/bpmn-js/examples/](https://bpmn.io/toolkit/bpmn-js/examples/)  
    > [https://github.com/bpmn-io/bpmn-js-examples](https://github.com/bpmn-io/bpmn-js-examples)  

    例如： 

    + interaction： 与流程图的交互，点击节点
    + overlays： 添加覆盖层。可以在流程节点上加悬浮图标来表示当前所在节点
    + colors： 给节点加颜色。比如将所有未执行过的节点设置为灰色，将执行过的节点设置为黑色。

我选择第三种方式。

#### 驳回功能

节点跳转的另一个应用是驳回。驳回是流程实例当前具有控制权的用户可以做的动作。

驳回通常有两种场景：

- 用户选择驳回到已经执行过的某个节点  
    前端限制流程图中只能选择已执行过的节点，后端在跳转前查询执行日志判断该节点是否已执行过。  
- 所有流程实例只会驳回到第一个节点  
    绘制流程图的时候，为所有流程图的开始节点设置相同的 ID

#### 跳过当前节点

有的节点只执行一个操作，不生成任何对流程实例流转有影响的数据。这种节点会因为各种奇怪的原因执行出错，运维人员需要介入处理这些问题。处理完后跳过这些节点。

Camunda 有一个接口可以直接做到这件事：  

> [https://docs.camunda.org/manual/latest/reference/rest/signal/post-signal/](https://docs.camunda.org/manual/latest/reference/rest/signal/post-signal/)  

相关说明文档：  

> [https://docs.camunda.org/manual/latest/reference/bpmn20/events/signal-events/](https://docs.camunda.org/manual/latest/reference/bpmn20/events/signal-events/)  

最开始用过这个接口，不过后来取消了。还是让运维人员选择目标节点比较安全。

### 流程实例迁移（升级）

当流程发布新版本之后，不会对已有的流程实例造成影响。如果想应用最新版本流程，则需要升级旧流程实例。  

流程实例迁移分为三个步骤：  

1. 生成迁移计划  
    > Generate Migration Plan   
    > [https://docs.camunda.org/manual/latest/reference/rest/migration/generate-migration/](https://docs.camunda.org/manual/latest/reference/rest/migration/generate-migration/)
2. 验证迁移计划
    > Validate Migration Plan  
    > [https://docs.camunda.org/manual/latest/reference/rest/migration/validate-migration-plan/](https://docs.camunda.org/manual/latest/reference/rest/migration/validate-migration-plan/)
3. 执行迁移计划  
    > Execute Migration Plan  
    > [https://docs.camunda.org/manual/latest/reference/rest/migration/execute-migration/](https://docs.camunda.org/manual/latest/reference/rest/migration/execute-migration/)

生成迁移计划和验证迁移计划的时候，不会涉及具体的流程实例 ID。

执行迁移计划的时候，可以选择要迁移的具体流程实例 ID，也可以用查询的方式指定要迁移的流程实例。

### 关闭流程实例

使用 Camunda 的 Delete 接口就行了。  

> Delete Process Instance  
> [https://docs.camunda.org/manual/latest/reference/rest/process-instance/delete/](https://docs.camunda.org/manual/latest/reference/rest/process-instance/delete/)

### 重启流程实例

Camunda 会用旧流程实例的信息来启动一个新的流程实例。

> Restart Process Instance  
> [https://docs.camunda.org/manual/latest/reference/rest/process-definition/post-restart-process-instance-sync/](https://docs.camunda.org/manual/latest/reference/rest/process-definition/post-restart-process-instance-sync/)

由于会创建一个新的流程实例，其 ID 与旧实例的 ID 不一致，因此得将流程实例信息表中的引擎流程实例 ID 替换掉。

这里会碰到一个问题： Camunda 重启实例的接口不会返回新实例的 ID 。

还好我们之前在创建流程实例的时候，会往底层 Camunda 的全局变量盒保存自增 ID ： `meta__id`。

可以通过流程实例搜索接口找到有保存 `meta__id` 为指定 ID 的流程实例。  

> Get Instances (POST)   
> [https://docs.camunda.org/manual/latest/reference/rest/process-instance/post-query/](https://docs.camunda.org/manual/latest/reference/rest/process-instance/post-query/)

然后将获取到的流程实例 ID 更新到流程实例信息表里面。

# 前端动态表单的渲染

写一个主 Component，然后在里面写具体的各个组件。

遍历后端传的各组件名称，创建多个主 Component。然后用组件名称依次匹配里面的各个组件，如果匹配到则展示。这里用到了 Vue 的 `v-if` 。

# 结语

目前能想到的基本上都写了。有一些细节的地方没有深入讨论，待后续继续完善。

这篇没有完全地按照当前项目写的适配层的实践来写，而是在此基础上做了一些优化。
