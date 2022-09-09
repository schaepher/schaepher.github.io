# AWK 命令


awk 是文本处理工具。

awk 命令接收的参数分为四个部分：

1. 选项
2. 脚本代码
3. 变量
4. 待处理文件

大多数 awk 命令只用到选项、脚本代码、待处理文件。

## 示例文本

`test.txt`

```
name,age
xiaoming,20
xiaohong,18
```

## 选项

最常用的选项是 `-F field-separator`，用来选择以什么字符串作为分割字段的依据。例如 `-F ','` 表示按照 `,` 分割行。

另一个常用选项是 `-f script-file`，用来选择分析脚本文件。如果脚本代码太多，不适合写在命令参数里面，选择写在文件里面，则使用这个参数加载脚本。

## 脚本代码

如果没有使用 `-f script-file` 参数，则需要在命令参数里写脚本代码。

脚本代码由单引号括起来，例如 `'{print $1}'`。这是因为在 shell 里写命令时，`$` 符号用来表示使用一个变量。如果用双引号，则会被解释为使用某个变量。如果用单引号，则不会被解释，而是原样传入 awk 命令。

脚本代码使用 `$数字` 的方式表示第几个字段，例如 `$1` 表示分割后的第一个字段。

脚本代码由模式+动作组成，动作的代码由花括号包裹，组合起来的为`pattern{action}`。可以有多个这样的组合，组合之间不需要间隔符（可自己加空格便于阅读），每个组合都会对一行分别执行一次。满足模式的时候，就会执行相应的动作。

例如：

```bash
awk -F ',' '$2 >= 18 {print $1,$2} $2 == 20 {print $1,"is",$2}' test.txt
```

结果是：

```
name age
xiaoming 20
xiaoming is 20
xiaohong 18
```

模式可以省略，表示对于每行都执行动作。

例如：

```bash
awk -F ',' '{print $1,$2}' test.txt
```

结果是：

```
name age
xiaoming 20
xiaohong 18
```

模式有很多种，常用的有：

1. BEGIN
2. END
3. 条件表达式
4. 正则表达式

BEGIN 表示读取文件之前，通常用于初始化变量。END 表示不再读取文件之后，通常用于打印最终的结果。

例如：

```bash
awk -F ',' 'BEGIN{sum=0} {sum += $2} END{print sum}' test.txt
```

结果是：

```
38
```

## 内建变量

有时候会对处理的行数有要求，例如前面的结果中把第一行也打印出来了，如果要把某一行去掉，可以自己声明一个变量记录行数：

```bash
awk -F ',' 'BEGIN{line=0} {line++} line != 1 {print $1,$2}' test.txt
```

结果：

```
xiaoming 20
xiaohong 18
```

每次都这样写麻烦，因此 awk 内置了一个变量 `NR` 用于表示当前行数。awk 默认把每行看作一条记录，NR 是 Number of records 的缩写。

于是上面的命令就简化为：

```bash
awk -F ',' 'NR != 1 {print $1,$2}' test.txt
```

awk 默认把每行看作一条记录，是因为其记录分隔符被默认为换行符 `\n`。可以通过给内置变量 `RS` （Record separator）赋值改变记录分隔符。

例如：

```bash
awk 'BEGIN{RS=","} {print $1}' test.txt
```

结果是：

```
name
age
20
18
```

这里的 "xiaoming" 和 "xiaohong" 丢失是因为每次按照 `,` 分割，得到的是 `age\nxiaoming` 这样的结果。然后默认的 `FS`（Field separator），也就是 `-F` 参数，是空白字符。空白字符包括空格和换行，因此 `$1` 就只包含 age。

如果要展示完整，则使用 `$0`。它表示一个 record 里的所有 field。

```bash
awk 'BEGIN{RS=","} {print $0}' test.txt
```

结果是：

```
name
age
xiaoming
20
xiaohong
18
```

如果一行中间的字段数不同，但要打印最后一个字段呢？

有一个内置变量表示当前 Record 的字段数，`NF`（Number of field）。

```bash
awk -F ',' '{print $NF}' test.txt
```

结果是：

```
age
20
18
```

同理，倒数第二个字段为：

```bash
awk -F ',' '{print $(NF-1)}' test.txt
```

#### 计算五分钟带宽

```awk
'{sum+=$6} END {print "sum=",sum*8/300/1000/1000}'
```

