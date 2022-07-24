---
title: UUID
date: 2018-10-08 00:19:00
updated: 2018-10-08 00:19:00
categories:
 - Development
tags:
 - UUID
---

[https://stackoverflow.com/questions/20342058/which-uuid-version-to-use](https://stackoverflow.com/questions/20342058/which-uuid-version-to-use)  

- version 3/5：  
    根据某个命名空间和名称生成，名称相同则会产生相同的 UUID。可用于设置用户的 UUID（跟用户名唯一绑定）。一般用 version 5。
- version 4:  
    获取随机数。用得最多的一种。会重复的概率几乎可以忽略不计。  
    > [https://en.wikipedia.org/wiki/Universally_unique_identifier#Collisions](https://en.wikipedia.org/wiki/Universally_unique_identifier#Collisions)  

    “除非你每秒生成十亿个 UUID，并且持续一个世纪”

<!-- more -->

## 同时使用 UUID 和自增 ID

接口提供以 UUID 为条件的查询方式。自增 ID 作为后端特定的场景使用，接口不提供这个参数，避免被顺序遍历。

## 分布式 UUID

一次生成多个 ID，放到 Redis 里面。需要 UUID 的时候，从 Redis 里取。这样可以加快速度。

## 分布式顺序 ID

用数据库。数据库只有一列自增 ID。一次插入多行，获取这些行的 ID，放入 Redis。

