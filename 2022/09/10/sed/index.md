# sed 命令 —— Linux


如果想将 sed 操作的结果写入源文件，加上 `-i` 参数即可。

## 行删除

行删除表达式主要包含两部分：

1. 匹配规则
2. 表达式以 `d` 或者 `!d` 结尾，前者表示删除匹配到的行，后者表示删除未匹配到的行

匹配规则是一个范围，用逗号隔开，左右闭区间。例如表达式 `1,3d` 表示删除 1, 2, 3 这三行。逗号和后面的行号省略时，表示匹配单行。例如 `1d` 表示删除第一行。

匹配规则可以是一个正则表达式，正则表达式左右使用斜杠包裹。例如 `/a/d` 表示删除所有包含字符 `a` 的行。左区间和右区间都可以是正则表达式。表示一直删除到匹配到右区间的正则表达式为止，然后继续搜索左区间。


### 示例

```
cat a.txt
hello
world
three
four
five
six

eight
nine
```

1. 删除匹配到 world 的行

```bash
sed '/world/d' a.txt
```

```
hello
three
four
five
six

eight
nine
```

2. 删除第一行

```bash
sed '1d' a.txt
```

```
world
three
four
five
six

eight
nine
```

3. 从第三行开始,每隔一行删除

```bash
sed '3~2d' a.txt
```

```
hello
world
four
six
eight
```

4. 删除从第４行到第８行

```bash
sed '4,8d' a.txt
```

```
hello
world
three
nine
``

5. 删除最后一行

```bash
sed '$d' a.txt
```

```
hello
world
three
four
five
six

eight
```

6. 删除空行

```bash
sed '/^$/d' a.txt
```

```
hello
world
three
four
five
six
eight
nine
```

有些空行其实包含了空格或者 tab

```bash
sed '/^\s+$/d' a.txt
```

7. 从匹配行到末尾行

```bash
sed '/eight/,$d' a.txt
```

```
hello
world
three
four
five
six
```

8. 删除匹配行和之后两行

```bash
sed '/hello/,+2d' a.txt
```

```
four
five
six

eight
nine
```

