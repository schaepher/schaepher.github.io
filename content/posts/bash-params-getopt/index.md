---
title: Bash 脚本长参数（getopt）
date: 2019-08-08 19:42:55
updated: 2019-08-08 20:59:00
categories:
 - Scripts
tags:
 - Shell
 - Bash
 - Linux
---


在脚本里面使用 getopt 获取参数。

## 示例 

> test.sh  

```bash
#!/bin/bash

ARGS=$(getopt --option ab: --long atest,btest: -- "$@")
eval set -- "${ARGS}"

while true
do
    echo "current $1"

    case "$1" in
        -a|--atest)
            echo "option: $1"
            echo ""
            shift 1
            ;;
        -b|--btest)
            echo "option: $1"
            echo "value: $2"
            echo ""
            shift 2
            ;;
        --)
            shift
            echo "break"
            echo ""
            break
            ;;
    esac
done

echo "rest option(s): $@"
```

<!-- more -->

如果执行： 
 
`bash test.sh --atest --btest=2 -- --ctest=3 --dtest=4`

则会得到：  

```bash
current --atest
option: --atest

current --btest
option: --btest
value: 2

current --
break

rest option(s): --ctest=3 --dtest=4
```


## 解释  

`getopt --option ab: --long atest,btest: -- "$@"`


- 当想使用 getopt 获取长长选项时，必须带 `--option` 或其简写 `-o`，虽然指定的选项未必和长选项一一对应。
- `ab:` 是短选项 a 和 b
- b 后面加一个冒号，表示 b 这个参数必须携带值。例如 `-b 2` 或者省略空格 `-b2`  
  如果加两个冒号，则表示值是可选的。例如对于 `c::`，则可以传 `-c` 也可以 `-c 3`
- `atest,btest:` 是长选项，选项间用英文逗号隔开。冒号的作用同短选项  
  传参时，可用空格或等号隔开选项和参数值
- `--` 表示其后内容就算是以 `-` 开头，也不作为选项解析，当做纯文本
- `"$@"` 表示传入脚本除了路径 `$0` 外的所有参数。加双引号是为了处理参数值包含空格的情况。  
  例如如果不加双引号， `--btest="2 4"` 解析出来的值就是  

  ```
  option: --btest
  value: 2
  ```

  如果加引号，结果就是：  

  ```
  option: --btest
  value: 2 4
  ```

`eval set -- "${ARGS}"`

使用 set 命令刷新参数列表。直观上就是等号被替换为空格。例如 `--btest=2` 被替换为 `--btest 2`。

后面就是普通的 switch-case 了。加上 `shift [num]` 使得每次都从 `$1` 开始，不用担心参数顺序问题。

参数的解析是从左到右按顺序的，所以我们也可以处理 `--` 的情况。直接 break 停止解析即可。

由于使用了 shift，所以 `--` 之后的内容都保存在 `$@` 里面。

## 长选项对单横杠的支持

如果使用上面的解析，`--btest=2` 没有问题。但是 `-btest=2` 就会报错。

可以给 getopt 加一个 `--alternative` 选项：

`getopt --alternative --option ab: --long atest,btest: -- "$@"`

## 选项简写

上述命令可简写为：  

`getopt -a -o ab: -l atest,btest: -- "$@"`