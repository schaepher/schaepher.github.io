---
title: Mariadb 授权与回收
date: 2019-08-18 11:29:22
updated: 2019-08-18 11:29:22
categories:
 - MySQL
tags:
 - MySQL
 - Grant
---


1. 创建用户

   ```sql
   CREATE USER "username"@"host" IDENTIFIED BY 'password';
   ```

<!-- more -->

1. 授权
   
   ```sql
   GRANT ALL PRIVILEGES ON dbname.* TO "username"@"host";
   ```

1. 回收

   ```sql
   REVOKE ALL PRIVILEGES ON dbname.* FROM "username"@"host";
   ```

