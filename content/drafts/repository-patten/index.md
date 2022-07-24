---
title: Repository 模式
date: 2019-09-07 14:38:34
updated: 2019-09-07 14:38:34
tags:
---

从模型的角度看问题。

Factory 负责制造新对象，Repository 负责查找已有对象。

Repository 应该让使用者感觉对象就好像驻留在内存中一样。

Client --create_obj--> Factory   
Client --add_obj--> Repository --insert--> Database


