---
title: Bash 脚本长参数（getopts）
date: 2019-08-08 19:50:30
updated: 2019-08-08 22:00:00
categories:
 - Installation And Configuration
tags:
 - Shell
 - Bash
 - Linux
---

在脚本里面使用 getopts 获取参数。

## 示例

> test2.sh

```bash
#!/bin/bash

function main() {

    local OPTIND

    count=0

    while getopts ab:-: OPT
    do
        echo "current -${OPT}${OPTARG}"

        case "${OPT}" in 
            -)
                case "${OPTARG%%=*}" in
                    atest)
                        echo "option: --${OPTARG}"
                        echo ""
                        let count++
                        ;; 
                    btest)
                        echo "option: --${OPTARG%%=*}"
                        echo "value: ${OPTARG#*=}"
                        echo ""
                        let count=count+2
                        ;;
                esac
                ;; 
            a)
                echo "option: ${OPTIND}"
                echo ""
                let count++
                ;; 
            b)
                echo "option: ${OPTIND}"
                echo "value: ${OPTARG}"
                echo ""
                let count=count+2
                ;; 
        esac
    done

    shift $count

    echo "rest option(s): $@"
}

main "$@"
```

<!-- more -->

执行：  

`bash test2.sh --atest --btest="2 4" -- --ctest=3 --dtest=4`

结果：  

```
current --atest
option: --atest

current --btest=2 4
option: --btest
value: 2 4

rest option(s): --ctest=3 --dtest=4
```

## 解释

与 getopt 相比：  

- while 里面不能使用 shift，必须在结束之后统一 shift
- 长选项不能用纯空格隔开
- 放在 function 里面的时候，必须先执行 `local OPTIND`
- 不必另外处理 `--` 的情况
