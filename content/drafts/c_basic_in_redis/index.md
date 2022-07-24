---
title: Redis 用到的 C 语言
date: 2019-05-28 21:53:00
updated: 2019-05-28 21:53:00
---

## 编译时命令

所有以 `#` 开头的命令都是预处理命令，在编译时处理。

### 定义

### \#define

用于替换

`#define X1 X2`

将所有出现 X1 的地方替换为 X2。

`#define` 是可覆盖的，以最近一次出现的定义为准。

- 纯替换
- 函数替换
- 替换为字符串

### 条件编译：

#### \#ifdef
> 出现在 `server.c` 的 main() 里面。

```c
#ifdef XXXX
    // codes
#endif
```

如果定义了 XXXX，则编译这段代码，否则忽略。

## <string.h>

### strcasecmp(str1, str2)
> 出现在 `server.c` 的 main() 里面。

忽略大小写的字符串比较。

若参数 str1 和 str2 字符串相同则返回0。
str1 长度大于 str2 长度则返回大于 0 的值，str1 长度若小于 str2 长度则返回小于 0 的值。

## "zmalloc.h"

封装了多平台的内存申请。

- zstrdup()  
  复制字符串。strcpy() 只有遇到 `\0` 才会结束，容易内存溢出。 



