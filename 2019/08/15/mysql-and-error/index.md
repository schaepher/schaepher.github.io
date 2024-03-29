# 记一个 SQL 导致的问题的处理



### 背景

我们组负责维护一个内部系统，这个系统里面有一个功能：允许管理员在上面执行 SQL 语句，没有任何限制。

14 号下午，同事在这个系统的生产环境执行了一条 SQL 语句，导致部分功能异常。四十分钟后恢复服务。但数据在 15 号早上才完全恢复。

<!-- more -->

### 处理过程

在接受到用户反馈后，我知道了这是数据库的问题，但不知道具体问题在哪。

如果继续提供服务，可能会扩大影响范围。所以我询问组长和其他人看能否先停掉服务。得知有一个功能可以关闭部分系统，但没有操作文档，一时也找不到功能在哪。我就说还是先把服务停掉吧。

停掉服务后，好多人问我们服务号（刚好我值班）为什么 404 了。我一一道歉并说正在处理中。同事也在各大群里说系统先停止服务。

开始排查问题。

先确定当前影响的数据范围。查看表，了解到这是对全表的操作。

然后有个同事帮忙查找代码里面是否有不包含 WHERE 的 UPDATE，发现没有这样的语句。  

然后另一个同事说有没有可能是他刚刚执行的一个 SQL。此时我们并没有注意到这一点。

（原因可能是因为他后面把语句改正确了，再执行了一次。然后他认为导致问题的那条 SQL 不应该生效，因为在他看来是个语法错误）

此时有两种做法：  
1. 查找原因，通过处理根本原因来解决问题
2. 想办法在不知道原因前解决或者缓解当前问题，再去找原因

以往的经验告诉我，先解决当前的问题，减少影响，再去查找根本原因。

1. 我首先去联系联系了 DBA，简要告诉他事情大概是怎么回事。以便等会儿做什么应急操作时，可以避免产生无法恢复的影响。  
2. 然后思考处理方案。

有人提出使用备份数据，恢复到凌晨的数据。DBA 也这么说。然而这是不行的，因为在这期间创建了很多新数据。原来那些 instance 的状态也可能变为结束。如果完全恢复，也会出问题。

此时无法确定是哪条 SQL 导致的，只能有一个大概的执行时间。当时告诉 DBA 的时间是用户反馈的时间（后来发现 SQL 是这个时间点的五分钟前执行的）。

之前已经了解到影响只有这张表。业务上这个字段的问题不会导致太大问题，只是因为某个条件限制，导致无法执行了。

要解除限制，可以把字段置为空字符串。这样主要服务就可以正常。

我先询问组内同事能否把字段值置空。得到确认后，问 DBA ，如果把字段置空会不会影响到后续数据恢复。DBA 说可以先执行。

于是我就执行了一句把那个值为 0 的字段设置为空字符串的 SQL。然后恢复服务。此时比较明显的那个影响也只是小问题。但由于涉及到某些定时任务（后面会说明为什么），所以仍然需要 DBA 帮忙恢复那部分不应该设置为空字符串的数据。

此时已经过去 40 分钟。在这期间，有个大问题，就是外部也有一部分人在使用这套系统。他们要求后续给个故障报告。这时我们才想起来没有通知他们。

目前系统主要功能已经恢复，接下来就是分析原因。

我想到了之前系统有个接口，参数是 SQL 语句，然后无条件执行。估计是认为自己系统调用，也不会有什么人会恶意攻击。我也觉得不是有人恶意攻击，但还是先跟组内其他人说一声。他们有人去看请求日志，没有发现这种请求。

有同事就说，自己排除下是否是在生产环境的那个功能执行了什么语句。有日志功能。自己看了一下也没什么问题。

另一个同事就说是不是有把执行日志记录到数据库里面，有的话直接搜索看看，说不定有符合特征的语句。然后过会儿就放一张截图出来。

同事看了一眼截图，惊讶地说：“xx，是你啊”。没错，指的就是我。我：？？？。吓得我差点心脏承受不住。结果仔细一看，那是我刚刚为了恢复服务执行的语句。虚惊一场。Orz

过一会儿，我们组长把那张截图的范围缩小到了一条记录。发出了截图。一看，终于找到了原因。

后续 DBA 恢复的时候，取 binlog 中 UPDATE 前后数据，并过滤掉已经不需要更新的部分，这只能恢复一小部分数据（这个我得研究看看为啥少了那么多数据）。最后还是通过备份数据加上当前数据的状态，提取出用于恢复的 SQL 并执行，这才成功地恢复了所有数据。

### 操作内容及影响

MySQL 版本：5.6.41

执行的语句（表名和字段名做了替换）：

```mysql
UPDATE instances SET operator = "某人" AND id = 123456;
```

影响：该表所有行（100万条）的 operator 字段的值都被设置为 0。

### 解释

SQL 语句的问题在于操作符的优先级  

> MySQL 操作符优先级：  
> [https://dev.mysql.com/doc/refman/5.6/en/operator-precedence.html](https://dev.mysql.com/doc/refman/5.6/en/operator-precedence.html)

从高到低为：  

```
INTERVAL
BINARY, COLLATE
!
- (unary minus), ~ (unary bit inversion)
^
*, /, DIV, %, MOD
-, +
<<, >>
&
|
= (comparison), <=>, >=, >, <=, <, <>, !=, IS, LIKE, REGEXP, IN
BETWEEN, CASE, WHEN, THEN, ELSE
NOT
AND, &&
XOR
OR, ||
= (assignment), :=
```

可以看到 `AND` 的优先级高于 `= (assignment)`，这样在 MySQL 看来，上面的语句就是：  

```mysql
UPDATE instances SET operator = ("某人" AND id = 123456);
```

这里的 `"某人"` 在做 AND 运算时，会被转换为 false。

```mysql
SELECT IF("某人", TRUE, FALSE);
```
得到的结果是 0，也就是 FALSE。  

> https://dev.mysql.com/doc/refman/5.6/en/boolean-literals.html

这样虽然后面的 `id = 123456` 在某一条会得到 TRUE 的结果，但由于 AND 的结果必然为 FALSE，最终还是会是 FALSE，然后被转为 0 。

### 为何会影响定时任务

对于 instance 表来说，每条记录都是一个任务的相关信息。里面包括了这个任务预定在什么时间执行。  

由于系统设计时，没有考虑到这点。所以后来要加上预定执行的功能时，就直接把时间放入 operator 。  
> 例如： `xxxx@2019-08-13 15:00:00`

如果把这个字段置空，定时的这些任务就没办法到指定时间执行，而是直接不执行了。

### 影响到外部

系统并不是由同一批人使用的，用术语来说就是多租户。

由于系统设计之初（十年前）并没有考虑到多租户的需求，这是去年才有的需求，并且由于数据和业务各种复杂的原因，导致多个租户用同一套服务和数据库。

因此数据库数据出错以及在暂停服务的时候，都会影响到其他租户。

这次我没做好的地方就是在停服务之前，没有事先通知这些租户。

### 教训

这次大家也总结了一些处理方案。

1. 涉及到更新操作的，都要审核。  
   这个其实之前就有这个规范，只是这次同事因为觉得这语句太简单，就给忽略了。  
   我认为如果实在要做，也应该做成一个人提交要执行的语句，另一个人点击审核通过之后才能执行。这样就避免了某个人可以不走审核流程就能执行的问题。
2. UPDATE 之前先用 SELECT 获取影响范围，再从 SELECT 语句的基础上改为 UPDATE。  
   这个其实还可以用 EXPLAIN 来确定影响范围。配合上面在审核过程中自动执行 EXPLAIN 让审核人得知影响范围，能更有效地避免问题。
3. UPDATE 如果不带 WHERE 语句，执行之前提示用户。  
   这个可以直接禁掉不包含 WHERE 的 SQL。实在想全表操作，用 `WHERE 1 = 1` 就行了。  
   但其实还是应该避免线上直接执行 SQL。最好对想要的操作做个单独页面，通过界面化操作来从根本上解决问题。
4. 服务停止时应通知所有租户。

好像还少了一条：出现问题时的处理方案。比如说这次出现问题，没有一个文档可以指导我们正确地停止服务，减小影响范围。  
