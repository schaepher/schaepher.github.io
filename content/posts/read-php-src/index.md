---
title: 阅读 PHP 源码
date: 2020-03-30 23:25:00
updated: 2020-03-30 23:25:00
tags: 
- PHP
- 源码
---

从数组入手。

数组相关函数是 PHP 扩展的一部分，扩展名为 `standard`，执行 `php -m` 可以看到该扩展。

该扩展的源码在 PHP 源码包的 `ext/standard` ，其中数组相关函数的定义在 `ext/standard/array.c` 。




