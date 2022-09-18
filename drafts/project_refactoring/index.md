# 项目重构（重写）的问题


在经过了一年半的项目开发之后，今年年初我开始负责我们项目的重构工作。虽然是叫重构，但实际上项目已经无法重构，只能重写。以下都称之为重写。

在这之后的半年时间，我犯了很多错误。而这些错误实际上大多数都是可以避免的。我现在都不好意思说我曾经学过软件工程了。

我会分成项目管理和所涉及的技术这两个方面来写。这一篇先讲项目管理，后续技术部分再分几次写。

## 项目介绍

这是一个强业务弱技术的流程项目。原先项目涉及到的技术点非常少，进不到几个类，都是面向过程。整个项目都是业务的堆砌。

没有专职前端。因为基本都只需要配置流程里的表单信息，且很多都是简单的文本框，所以都是在后端人员需要的时候自己写。原先框架允许开发人员快速配出简单的表单。

这是一个 PHP 项目，整个项目的代码量大致为 **57万** 行。

## 人员

在定计划的时候，今年上半年将会有三个开发，下半年会再加入两到三个。所有开发人员中，只有一个前端，其余后端。


在最初定计划的时候，我就