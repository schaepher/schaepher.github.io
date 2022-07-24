# BPMN 流程引擎 —— Camunda


2019 年初我在重新设计我们组负责的流程系统时，选择了 Camunda 流程引擎，并基于该流程引擎实现了一套适配方案。以前就想做一次总结，但总拖着。

最近公司中台在做流程引擎选型，相关同事找我了解 Camunda 以及基于 Camunda 的应用方案。经过我一番说明，对方表示收获很大。我想着也是时候把这些经验写下来了。

我把内容分为两部分：

- Camunda 自身的介绍（为什么选 Camunda ？）
- 基于 Camunda 的一种适配层实现方案

这一篇只包括第一部分的内容。

<!-- more -->

为什么选 Camunda ？

做选型的时候，需要说明我们需要什么样的功能和不需要什么样的功能。

我们项目的特点是什么？

1. 流程以自动化为主  
   极少数节点需要人工操作（审批、补充信息）  
2. 使用 PHP 作为业务层语言  
   流程引擎必须作为一个服务存在，不能为了使用流程引擎而更改语言。  
   必须有一个机制，使得流程实例执行自动化操作时，请求业务层 API。  
3. 流程同一时间最多只有一个节点在执行  
   不需要支持并行加签、多分支同时执行、单节点多并发执行。  
4. 可以强行跳转到其他节点执行  
   由于业务的不确定性因素，难以或无法通过优化流程来预先规划好各种情况下的分支。  
   因此需要在自动化步骤出现某些无法预知的情况时，由运维修改流程实例的状态，跳过当前节点的执行或者回到前面的节点重新执行。  
5. 可以重启一个处于结束或终止状态的流程实例  
   同样是业务的要求。
6. 支持多分支  
   有些流程引擎只能选择 “是” 或者 “否” 这两个分支，无法支持多种情况。
7. 支持失败重试  
   当自动化任务节点失败后，流程引擎需要支持重试当前节点。  

接下来了解比较常见的流程引擎。例如 JBPM 、 Activiti 、 Flowable 、 Camunda 、 Zeebe 。

更多流程引擎请见：  
> https://github.com/meirwah/awesome-workflow-engines

它们之间的关系是：

```
  2004   2006   2009      2010      2013      2015       2017      2018            2020
+---------------------------------------------------------------------------------------->  JBPM

    2     3      4         5         6                     7       7.15            7.34

                 +      推 翻 架 构
                 | 继 承
                 | 架 构
                 |        2010      2013      2015       2017      2018            2020
                 +----------------------------------------------------------------------->  Activiti

                           5                   6                    7              7.1

                                     +                    +
                                     |                    |
                                     |                    |
                                fork |              fork  |        2018            2020
                                     |                    +------------------------------>  Flowable
                                     |
                                     |                    6        6.4             6.5
                                     |
                                     |
                                     |
                                     |
                                     |         2015      2017      2018            2020
                                     +--------------------------------------------------->  Camunda

                                   7.0          7.3      7.8       7.10            7.12     ^
                                                                                            |
                                                                                            | 同 团 队
                                                                                            |
                                                                                            v
                                                         2017      2018            2020
                                                         +------------------------------->  Zeebe

                                                         0.1       0.14            0。22
```

如果从 GitHub 的 start 数看，Camunda 是远远没有优势的。以下数据是 2020-03-25 的数据。

- Activiti： 6.4k
- Flowable： 2.8k
- Camunda ： 1.3k

在其他数据上的比较： 
> https://www.openhub.net/p/_compare?project_0=Activiti&project_1=camunda+BPM+platform&project_2=Flowable

从功能上看呢？

CSDN 有一篇对比写得很详细： 
> https://blog.csdn.net/qq_30739519/article/details/86682931

我比较关注的点有以下几个：

- 支持外部任务（External Task）  

  External Task 应该和 HTTP Task 做对比。   

  对于 HTTP Task ，在执行的时候会请求一个 HTTP API。等待这个请求结束后，流程继续往下走。这里的问题是：  

  + API 超时如何处理？如果业务修改导致 API 处理时间变长时，要修改所有流程里配置的超时时间吗？  
  + 如何区分测试环境和正式环境？  

  当 Camunda 执行到外部任务节点时，会发布一个任务单元。外部系统定时向 Camunda 获取外部任务单元，然后做一些业务逻辑或者请求 HTTP API。做完之后，再提交给 Camunda，流程继续往下走。  

  外部任务具有超时时间。这个时间后，其他客户端请求接口可能获取到该任务。但可以请求 API 延长超时时间。  

  一个外部任务只能被一个客户端获取，获取后会加上一个锁。除非超时，否则只有获取到该任务的客户端可以继续操作。 

  外部任务可以配置优先级，并且这个优先级可以动态修改。  

  外部任务支持重试。当以任务处理失败的方式提交给 Camunda 后，Camunda 会检查配置的重试次数有多少，当前剩下多少。如果还有次数，则再次将该任务发布出去。

  可以专门实现一个 External Task Client ，实现一套根据情况请求业务 API 的方式。虽然同样是请求 HTTP API ，但是可以拥有更灵活的配置。  

- 支持任意节点的跳转  
  
  实际上 Camunda 不是直接支持跳转。它支持取消某个节点的执行，也支持在任意节点创建一个执行。

  如果要实现节点的跳转，需要封装两个操作：  

  - 在目标节点创建一个执行  
  - 取消当前节点的执行

- 支持重启（Restart）已经关闭的流程实例  

  虽然是叫重启，但实际上是创建一个新实例，然后将已关闭的流程实例的信息复制一份到这个新实例。  

- 支持流程实例的迁移（Migration）  
  
  随着流程的更新，流程会有多个版本。每个流程实例会固定绑定一个流程版本，按照该版本的方式走。  
  Camunda 可以让旧版本的流程实例迁移到其他版本的流程，目标流程版本可以是更新的，也可以是更旧的。  
  迁移分为两步： 

  1. 生成迁移计划  
  2. 执行迁移

  执行迁移的时候，可以从迁移计划中选择一部分流程实例做迁移。并且可以指定迁移后从哪个节点开始走（继续）。

- 支持批量（Batch）操作的 API  

  例如批量挂起流程实例、批量激活流程实例、批量重启流程实例

- 流程图绘制工具有桌面版本  
  
  你可以把流程图绘制工具下载到 Windows 系统上（其他系统也支持），绘制完流程图后，通过这个工具把流程图发布到 Camunda 。  

  你可以直接把这个软件丢给需求方，让他们把理想中的流程图绘制出来。 Camunda 的流程绘制工具对业务方和开发者都是友好的。   

  甚至如果你不是为了将流程图发布到 Camunda ，仅仅想绘制一个流程图，这个工具也很好用。

  Activiti 需要搭建后端服务才能通过 web 的方式绘制流程图，而且它是偏向于开发者的。  

除此之外， Camunda 和其他流程引擎一样，支持以下功能：  

- 定时节点（Timer Intermediate Catch Event）  

  可以选择相对时间或者绝对时间。例如 10 分钟之后继续往下走或者 2021-11-11 的 11:11:11 的时候往下走。 

  时间的语法采用 ISO 8601 标准。这个标准在编程语言库中基本都会支持。  

  可以设置时间常量，也可以引用流程引擎变量。在执行到定时节点之前设置或者修改时间。

- 网关节点（Gateway）  

  汇聚多个分支。不同网关有不同的作用。常用的互斥网关（Exclusive Gateway）表示与其相连的下游分支的条件中，一旦有一个分支的条件符合要求，就走那个分支，并且不再继续判断其他分支条件。  

- 消息接收节点（Receive Task）  

  流程引擎在执行到该节点的时候，会等待一条消息。客户端向该流程实例发送这条消息，流程继续往下走。

- 执行监听器（Execution Listener）  

  当以下事件发生时，会触发一次通知：  
  - 流程实例的开始和结束
  - 流程实例内一个节点的开始和结束  

  可以为 Camunda 写一个扩展，用于通知流程实例的状态。  
  参考：  
  > https://github.com/camunda/camunda-bpm-reactor/tree/master/examples/bpmn-execution-listener


从业务的角度上讲，其他流程引擎满足的部分 Camunda 也满足，其他流程引擎不满足的部分 Camunda 也满足，因此选择 Camunda 。

下一篇会详细介绍一种基于 Camunda 做适配层的方案。

如果想快速了解 Camunda 的功能，可以下载 Camunda Modeler 了解其流程图支持的各种组件，以及查看官方文档。

直接访问官方文档会很慢，于是我把官方文档做成 Docker 镜像，可以下载到本地访问。

```
docker pull schaepher/camunda-docs:latest
docker run -d -p "8080:80" schaepher/camunda-docs:latest
```

# 扩展阅读

Camunda 官方文档：  
> https://docs.camunda.org/manual/latest

Camunda Rest API：  
> https://docs.camunda.org/manual/latest/reference/rest/

Activiti Rest API：
> https://www.activiti.org/userguide/#_rest_api

Camunda External Task：  
> https://docs.camunda.org/manual/latest/user-guide/process-engine/external-tasks/

Camunda Execution Listener：
> https://docs.camunda.org/manual/latest/user-guide/process-engine/delegation-code/#execution-listener

Camunda Modeler（流程图绘制工具）：  
> https://camunda.com/download/modeler/

Camunda Docs Docker Image：  
> https://hub.docker.com/r/schaepher/camunda-docs
