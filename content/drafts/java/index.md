---
title: java
date: 2019-12-01 10:10:47
updated: 2019-12-01 10:10:47
tags:
---

mybatis plus 查询构造器

https://mybatis.plus/guide/wrapper.html#alleq

spring boot 配置文件多环境

https://blog.csdn.net/davis2015csdn/article/details/75220046

响应体 Header   

https://www.baeldung.com/spring-rest-http-headers

注解全介绍

https://cloud.tencent.com/developer/article/1507070

分页 Header 构造

https://www.baeldung.com/rest-api-pagination-in-spring  
https://www.javadevjournal.com/spring/rest-pagination-in-spring/

对 Mybatis 的吐槽

https://zhuanlan.zhihu.com/p/45044649



决策：
- 包名中有多个单词组成的，要用下划线连接吗？     
  全部用小写，并且不包含下划线（参考谷歌）。例如 helloworld

- 配置文件使用 properties 还是 yml？  
  使用 yml，结构清晰，易读  

- 如何依据环境来获取不同的配置文件？  
  application.yml 中有 spring.profiles.active 可以配置。  
  如配置为 dev，则使用文件 application-dev.yml

- Bean 使用 xml 配置还是使用注解？  
  使用注解。

- 依赖注入使用何种方式？  
  Service 使用字段注入，并添加 set 注入方式  
  Controller 使用方法参数注入  
  构造器注入会使得在为 Service 添加新的依赖时，也必须修改测试类。

- 不支持 Controller 方法参数的注入

- 注解的解释  
  https://www.cnblogs.com/tanwei81/p/6814022.html

- 多数据源  
  使用 dynamic-datasource-spring-boot-starter ，要使用 2.5.6，最新版本配置有问题。使用 2.5.6 必须在配置文件里加上：  
  ```
  #去除druid配置
  spring.autoconfigure.exclude=com.alibaba.druid.spring.boot.autoconfigure.DruidDataSourceAutoConfigure
  ```  
  https://www.jianshu.com/p/0b408e4e14a4

- mybatis 配置  
  # mapper 路径  
  mybatis-plus.mapper-locations=classpath\:sqlMapperXml/*Mapper.xml

- 依赖注入    
  https://www.cnblogs.com/joemsu/p/7688307.html  
  https://spring.io/blog/2007/07/11/setter-injection-versus-constructor-injection-and-the-use-of-required/  
  避免使用字段注入。可选构造函数注入和 set 方法注入。  
  构造函数注入的字段可用 final 修饰，因此该方法通常用于那些必要的注入（或者说几乎每个方法都会用到的那种）。  
  set 方法注入的字段不能用 final 修饰，因此该方法通常用于那些非必要的注入。  

  依赖注入对测试的影响：  
  构造函数的注入每次增加时，都需要修改测试类，在创建服务类的地方添加参数。但通常情况下，一个类不会经常地添加其他依赖，所以这不是个大问题。  
  set 方法仅需要在使用这个服务类的测试调用 set 。  

  结论是：  
  如果是 Controller 这种无需单元测试的，直接使用构造函数注入  
  对于 Service 这种，优先使用构造函数注入。如果是有多种实现的接口或者那种只有少数地方用到的类，则选择 set 注入。

- 返回 created 的 path

- mybatis plus 的 mapper.xml 要放在 resource 里面，并且和 Mapper.java 有相同的目录结构
- mybatis 的 ResultMap 支持将表字段映射到另一个类的字段，并且 ResultMap 可以不用处理两者的关联关系  
  这意味着可以映射到值对象而不是另一个实体
  映射方式为：  
  ```xml
  <resultMap id="xxxx" type="xxx">
    <id column="id" property="id">
    <result column="name" property="name">
    <sssociation javaType="xxx2" property="displayName">
        <result column="aliases" property="displayName">
    </association>
  </resultMap>
  ```
- mybatis 的 ResultMap 只能在 xml 里面指定使用。如果想用 mybatis plus 的 lambda 表达式查询也能得到相同的映射，需要在 @TableName 里面加上 resultMap = "BaseResultMap"
- mybatis plus 的 TableField 仅对 lambda 有效，不影响使用 xml 定义的查询结果。  
  可以完全抛弃 TableField，只要用上 @TableName 的 resultMap 就能得到正确的映射