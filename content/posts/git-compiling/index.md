---
title: CentOS7 编译 Git
date: 2019-10-09 19:26:00
updated: 2019-10-09 19:26:00
categories:
 - Installation And Configuration
tags:
 - Linux
 - CentOS7
 - Compiling
 - Git
---

```bash
yum install -y make autoconf gcc zlib-devel gettext-devel
make config
./configure --prefix=/usr
make all
make install
```

https://git-scm.com/book/en/v2/Getting-Started-Installing-Git