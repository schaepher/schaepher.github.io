# 工程思想方法在软件工程分支的教学上的体现


前几天写了一篇跟软工课程相关的博客[^1]，有一位能够促成具有建设性对话的同学问了我一个问题：

> 能展开讲讲你说的`工程思想和方法`么，以及从软工的哪些环节可以获得？

这位同学问了一个很好的问题。好在哪里呢？好在他试图详细地了解和分析一个抽象的表面上看起来高大上而且美好的概念，从而提出了一个往具体方向上讨论的引导问题。

> 同学们在面对类似的抽象的表面上看起来高大上而且美好的概念（例如“自由”和“平等”）时，一定要向自己或者向别人提出类似的往具体和细节上引导的问题。

<!-- more -->

在正文开始前，我要向各位老师和助教道歉。很抱歉在没有事先跟你们沟通的情况下，就冲动地答应回答这个问题。希望我这个越俎代庖的行为能得到大家的原谅。

另外我想跟同学们澄清一件事，我大多是在纸上谈兵，老师和助教们是在实践。大家要谨记“实践是检验真理的唯一标准”，当理论和实践不一致的时候，要以实践为准。

以下是我个人的看法，不一定代表老师和助教们的看法，也不一定对。

## 工程思想和方法

在正式展开我个人看法之前，我想再次重复我在 **当前阶段** 总结的工程的目标：在当前社会环境中，工程实施者使用有限的资源，把能创造的价值最大化，并将其凝固在一个商品里面。

我想请读者试着回忆我在上一篇博客中反复强调的一个跟工程相关的行为是什么？

大家的回答应该都是差不多的，否则就是我的表达能力有问题。尽管回答可能差不多，但以我 **对自己的要求和标准** 来看，我分成了四个层级：

第一层是舍弃，第二层是取舍，第三层是为了创造最多的价值而取舍，第四层是在理解资源是有限的且了解了当前社会环境提供了哪些资源以及自己掌握了哪些有限的资源的情况下为了创造最多的价值而取舍。

对我来说，这就是工程思想的核心。

接下来我会列出其他思想中的 **一部分**。其中有些是前辈们在他们各自所处的时代中通过实践总结的，有些是我自己总结的（因为我没有系统地学过工程学）。

- 分类讨论思想
- 迭代思想
- 快速迭代思想（快速试错、快速同步）
- 可持续思想
- 分而治之思想
- 动态调整思想
- 折中思想
- 矛盾思想
- 可预期思想

接下来我尝试对这些思想做一些展开：这些思想是为了解决什么问题以及符合这些思想的方法有哪些。然后将这些思想结合到软件工程的教学中。

## 分类讨论思想

对于同学们来说，分类讨论思想再熟悉不过了。数学考试中经常要用到分类讨论思想，而且通常是一道比较难的题目。但我们这里不讨论纯粹的数学，我希望能够立足于课本知识，但超越课本知识。另外我数学成绩也只能算是中等（逃

分类讨论思想的通俗化表达是“具体问题具体分析”，它的反面是“在任何条件下都使用同一种具体的解决方法”。

分类讨论思想所要解决的是将一个抽象的问题根据不同条件转化为多个具体的问题，再根据具体问题的不同特点分别用不同的方式解决。

举个生活中的例子： A 和 B 说头疼了，B 应该怎么回答？或者有人跟你说头疼了，你应该怎么回答？

这是一个非常抽象的问题，需要分好几层的分类讨论。

首先要对双方的性别做一个分类，做这个分类在当前社会环境下具有一定风险。我在这里根据国内大部分人的共识将其分为两类，男和女。由于缩小了数据集，因此只有四种情况。

这里使用分类讨论思想的图表法，把四种情况列出来。

||男|女|
|:--|:--|:--|
|男|A男、B男|A男、B女|
|女|A女、B男|A女、B女|

接着要对问题的主体双方的关系进行分类，可以有以下几种类型（我只列出部分）：

- 师生关系
- 情侣关系
- 普通朋友关系
- 损友关系
- 同事关系

其中这些类型有的是非对等关系（比如师生关系），换个顺序很可能得到不一样的结果；有的是对等关系（比如损友），换个顺序很可能得到一样的结果。

非对等关系通常使用排列的方式展开，对等关系通常使用组合的方式展开。这个可以根据实际情况调整。

通常我们看到一个问题，会下意识地采用社会共识所选择的类型加以判断。例如有人问 1+1 等于多少？根据社会共识，这个问题的完整表述是：在数学中，1+1 等于多少？于是我们回答，等于 2。

回到这个具体问题，社会的共识是，这个对话通常是在情侣关系中由女方发起的。我们可以先从最主要的这个分类开始讨论。

接下来我们对头疼这个现象进行分类。可以大致分为：真的头疼和假的头疼两类。然后再对女方的心理活动进行大致分类：想要解决头疼问题、想要男朋友的关心、两者都要。

现在我们使用分类讨论思想中的连线法进行组合：

![](https://img2020.cnblogs.com/blog/809218/202104/809218-20210424172601642-1290130554.jpg)

再从男方的角度做一些分类：

- 想解决头疼问题
- 想关心女朋友
- 两者都想

还可以再做进一步分类，例如想解决头疼问题：

- 可以想出很多种方法
- 只能想出“多喝热水”

> 写得我好累。不想再展开了。

从这些分类中，根据不同的连线大致写出对应的解决方法。

- 比如男女双方是情侣，女方对男方说头疼，但不是真的头疼，她想要男朋友的关心，但男方想解决头疼问题，又没办法想出很多方法，于是回答“多喝热水”。
- 再比如男女双方是情侣，女方对男方说头疼，但不是真的头疼，她想要男朋友的关心，男方想关心女朋友，于是说了一些关心的话，还可以做一些她喜欢吃的东西，以及其他 N 中解决方法。

我们通常说一个男生是直男，有一部分原因是他们对于问题的理解停留在了表面，同时试图解决这个表面的问题，又找不到合适的解决方法。这是一下子犯了 N 个错误才导致了 “多喝热水” 这种答案。把问题分析到这种地步的时候，就会知道不是只有男性这个群体才会出现的问题，这是人类这个群体会出现的问题。

分类讨论思想不仅仅是用来解决工程上的问题，还可以用来解决思想上的问题。

我花这么长的篇幅来举这个例子，是为了以下内容不必过多展开。

## 迭代思想

迭代思想指的是在原有的基础上有计划地不断改进以接近完美，与之相对的是一次性完美思想。

认为一个完美的东西才有价值，是人的缺点，需要通过后天的努力去改正。迭代思想要求人们接受不完美，看到不完美的东西的价值。

迭代的方法之一是把一个工程分成多个阶段，每个阶段设定一个可交付的标准，当前阶段的每个事项做到预设标准就停下来，不继续往下做。

不完美至少有两种情况：

1. 同一个功能有速度快的粗糙实现方案（比如手工调整），也有速度慢的灵活实现方案（比如自动调整）。粗糙的方案在这种情况下不是完美的选择，但是可以在前面的迭代中实现，后续迭代中用灵活的实现方案替代。
2. 在同一个方案中，有些重要的功能先实现，有些不那么重要的功能放到以后实现。同一个方案没有全部实现也不是完美的选择。

迭代思想通常与分而治之思想配合。

## 分而治之思想

当我们明确了一个具体的问题之后，需要开始解决问题。但是如果这个问题非常大，无从下手，怎么办？分而治之。

分而治之思想还会和迭代思想以及矛盾思想进行配合。

详细地分析这个具体的问题，会发现这个大的具体的问题可以分成几个中等的具体问题。然后再去分析这些中等的具体问题，就会发现一个中等的具体问题还可以分成几个小的具体问题。接着继续一直划分下去，得到了一颗多个层级的树。如果要开始解决这个大的问题，那么就去解决叶子节点上的问题。

可是这个时候又发现叶子节点实在太多了，如果随便选一些完成，可能要到所有叶子节点的问题解决之后，才能影响到大的问题的解决。

这时我们需要挑选叶子节点中对大问题影响程度大的那些，每次都尽量挑选一批影响程度最大的叶子节点出来解决。挑选影响程度大的叶子体现了矛盾思想，分次挑选体现了迭代思想。

## 矛盾思想

矛盾思想这里指的是主要矛盾和次要矛盾。

主要矛盾是当前阶段中对结果影响最大的一个点，其他的点都是次要矛盾。当解决了主要矛盾，会进入下一个阶段，此时在上一个阶段中的次要矛盾中会有一个对结果影响最大，此时该次要矛盾成为了当前阶段的主要矛盾。

区分主次矛盾不是为了忽略次要矛盾，而是把更多精力用来解决主要矛盾。比如 80% 精力用来解决主要矛盾， 20% 精力用来解决次要矛盾。在实践中，通常解决次要矛盾有助于解决主要矛盾。

## 快速迭代思想（快速试错、快速同步）

快速迭代与迭代的区别在于迭代的期限很短。为啥要缩短迭代的期限？

因为我们通常在迭代结束的时候，才会交付当前迭代的成果。但是由于对问题理解上存在偏差，很可能导致这个成果无法解决问题，需要重新做。

为了减少这种反复重做导致的资源浪费，可以缩短迭代的期限。这样可能在某个行动项上只完成了 20% 就发现这个行动项无法解决问题，此时只浪费了 20% 的资源。迭代的期限如果拉长，等到完成 80% 才发现无法解决问题，那么就浪费了 80% 的资源。

快速迭代思想还不止于此，在具体的实践中，会有一些优化方案。我会在结合软工时补充上这一点。

## 可持续思想

同学们对可持续思想也比较熟悉，经常背到。不知道同学们对可持续的重要性有多少思考？

可持续思想能够解决的是随着时间的推移，系统会自毁的问题。人就是一个系统，而且会不停地作死。

可持续思想是怎么解决这个问题的？通过限制效率。一个项目的推进有多种选择，其中必定有一种效率最高的推进方式。可持续思想就是要阻止你选择这个效率最高的推进方式。

比如有一个高效率获取快乐的方式（大家应该都懂，我怕文章被和谐就明确指出来了），为什么所有人都不使用这种方式去获取快乐呢？因为它不可持续。高效率带来的是快速的消灭。人类将其加入刑法，就是阻止人类高效率地作死。

## 动态调整思想

动态调整思想能够解决因对有限资源的误判或者有限资源临时变动出现的问题。

比如在迭代前选定了一批要解决的具体问题，但是在迭代中工程的施工人员数量发生变化。如果按照原先安排，可能会导致人员数量继续发生变化。于是需要重新组合有限资源，并且对选定的问题做一些动态调整。

## 折中思想

折中思想面对的是单一的完全的选择没有比多个的部分的选择的价值高的问题。形象的表达是 0.5 + 0.5 > 1。

在计算机历史中，最不缺的可能就是折中了。同学们应该深有体会。

比如既然内存速度那么快，为啥还要用到硬盘？你可能说因为内存断电数据就丢失了呀。那我用一大堆设备确保它不断电不就行了？

其实这总体上是一个性能和成本的折中问题（往深了讲还有发展水平问题）。只用内存的产品不是没有，但是很贵，难以推广到全世界大多数人使用。只用硬盘也可以，但是速度会很慢，如果大家都只用硬盘，那就没关系。问题就在于有人用少量内存和大容量硬盘结合起来，速度既可以很快，价格又能接受，于是更多人选择了这个折中的产品。

## 预期管理思想

> 说实话没想好准确的词，凑合着用吧。

预期管理思想是让自己成为一个可预期的存在，以此管理其他人的行为。大致分为时间预期和行为预期。

时间预期就是完成一个事项需要多少时间。这样在工程迭代过程中，可以做出不同的调整。

- 例如根据事项的预期完成时间和迭代的时间限制来挑选事项；
- 或者发现所有事项的预期时间之和超过了所有迭代时间之和，那么就可以做不同的调整。
 + 例如舍弃掉某些事项；
 + 或者增加施工人数。

大家对行为预期比较熟悉的一个子类应该是底线思维。就是让对方知道，一旦跨过这个底线，我方一定会让对方付出巨大的代价，这个代价大概率是对方无法接受的，除非对方想同归于尽。这样对方就处在我方的管理之下，最多只能在底线之上蹦哒。

举个我自身的例子。我会让领导知道我在当前阶段主要想通过编程（包括学习技术、系统设计、编码）解决问题，如果领导在这个阶段强行给我一个没什么时间编程的岗位（例如产品经理或者管理岗），那么我会立刻提出离职；而如果让我把大部分时间花在编程上，那么我剩余的时间会帮助领导解决很多系统之外的问题。这样领导可以评估他的这个行为会对项目和他自己产生多大的影响，以及是否有消除影响的方法。如果有消除影响的方法，那么可以逼我去没时间编程的岗位，或者直接裁掉我。

为了避免误导大家，希望大家要注意，行为预期管理思想对个人的硬实力要求高。比如我自身的例子要求我能够创造足够多的价值，以及我能够承受离职带来的影响。

## 工程思想和方法在软工课程的各个环节上的体现

这里的软工课程指的是参考《构建之法》开展的软工课程，因为不同的软工课程的开展方式不一样。

同学的原问题是“从软工的哪些环节可以获得（这些思想方法）”。为了严谨，我把思想和方法分开。方法可以从软工的环节中获得，思想则需要提醒和思考总结。

由于《构建之法》本身提供了很多方法，满本都写着两个字“方法”（皮一下，如果邹欣老师觉得这么说不妥，我再换种表达），而且肯定比我一篇博客所能讲的还来的详细，感觉没多大必要做这样的重复。不知道下面的回答能否算是提供了一个令人满意的答案。

#### 课前

老师和助教通过可预期思想方法，让同学们知道自己大概会在课程结束后得多少分。

#### 个人技术和流程

这里涉及了测试。测试是为了阻止开发者以最高的效率完成一个既定任务，让工程稳定可持续地推进，避免出现重大问题导致工程失败，体现可持续思想。

这个阶段对需求分析的要求还不是很高，放团队项目说明。

#### 结对编程

制定代码规范、代码复审和结对编程过程是软件工程中为了可持续推进项目而要求实践的工程方法，都是为了阻止开发者以最高的效率完成一个具体任务，体现可持续思想。

可以在两人合作过程中使用分类讨论思想的方法以提高合作效率。

#### 团队项目

老师和助教可以通过分类讨论思想的方法，大致确定各团队选题方案的合理性。可以通过可预期思想方法，让同学们再次对自己的最终得分有一个较之前更准确的认识。

以下是与同学们相关的内容。

可以实践分类讨论思想的方法提高合作效率。

需求分析的时候：

1. 用分类讨论思想方法分析用户群体
2. 用矛盾思想方法筛选出核心用户群体
3. 找到具体的用户，通过分类讨论思想方法了解用户，交流需求
4. 用分而治之思想拆解问题，和用户确认重要具体问题的细节，产出软件功能规格说明书
6. 用快速迭代思想的方法快速绘制原型，尽快与用户确认，避免浪费开发资源

设计系统的时候：

1. 用分而治之思想拆解具体问题
2. 用折中思想的方法平衡完成时间和软件性能或者功能

做工程规划的时候：

1. 用迭代思想、分而治之思想、矛盾思想、可预期思想的方法规划各阶段任务（Alpha 和 Beta 版本），避免系统无法按时交付

施工的时候：

1. 结合可预期思想和动态调整思想的方法，调整迭代任务  
   同学们通过站立式会议，及时准确地同步项目进展。PM 通过当前进展调整迭代任务，并反馈给老师和助教。让老师和助教对团队的进展有一个清晰的认识，并及时提供指导意见。
2. Alpha 做完后快速交付给用户，得到及时反馈，尽快调整 Beta 迭代的任务。这个是快速迭代思想的方法
3. Alpha 和 Beta 做完后专门做了事后分析，阻止了同学们试图采取最高效率的方法继续推进项目，确保项目可持续

## 关于课程总结

我们当时在上张栋老师的课时，最后一次作业[^2]中，有一个内容：

> 写下属于自己的人月神话——项目实践中的经验总结+实例/例证结合的分析

现在想起来，觉得很妙。且听我具体解释。

大多数理论都是不完美的，特别是工程类的理论。理论总是要结合实践，通过实践来验证理论的正确性，但仅仅这样还不够。

世界的复杂性决定了一个理论难以适用所有的情况。可以说任何人所具备的“有限的资源”都是不一样的。一旦条件不一样，那么在实践一个理论时，很容易就得到不同的结果。

理论只有指导作用，指导不是强制。理论不一定和实践一致，而且往往与实践不一致。如果理论和实践不一致，要以实践为准，并通过实践反过去补充和完善理论。正是在实践中得到的不同的结果，推动了理论的完善，进而推动人类的进步。

人们想要把具体实践对理论的影响固化下来，想出了一种方法：写论文。从上述内容看，一个实践可以通过验证在不同条件下理论仍然成立来补充理论；也可以验证在不同条件下理论不成立，以及如何调整理论来包括这种条件以补充理论。

同学们认为软工改革的时候，自己是“小白鼠”，这似乎是比较悲观的看法。在我看来，同学们以及老师和助教都是在通过自己“有限的资源”实践软件工程理论。在实践的过程中会碰到属于自己的问题。在解决各自问题的过程中，形成了属于自己的软件工程理论，最终通过总结把自己的“有限资源”以及软件工程理论在这些“有限资源”的条件下的实践情况表述出来。这样在客观上推动了软件工程理论的完善，进而为整体人类的进步做出自己的贡献。

你们还未察觉到你们正在做的事情有多么伟大。

这不是安慰，也没有其他乱七八糟的想法。我是通过上述的事实和逻辑（虽然很粗糙）得到这个结论的，也就是说我是真的这么认为的。

## 写在最后

写完这篇博客后，除了工作上的一些总结之外，我在 2021 年不会再像这样大量输出跟软工课程相关的内容了。我现在最需要的是输入而不是输出，从这两篇博客的内容上大家就可以看得出来。

客观上，这两篇的博客会在一定程度上（虽然很低）提高我个人的影响力，这是我目前阶段应该尽量避免的，因为我必须承担由此带来的本不必要的风险和代价。

不过也正是因为之前的那篇博客，使我和恩师张栋老师的关系得到进一步加深，所以我认为承担这个风险和代价是值得的。

最后的最后，提前给大家拜个早年。祝大家身体健康，事业顺利，学业顺利！

## 参考

[^1]: https://www.cnblogs.com/schaepher/p/14687730.html (软件工程与“足够好”)
[^2]: https://www.cnblogs.com/easteast/p/5058155.html (软件工程实践总结作业——个人作业)
