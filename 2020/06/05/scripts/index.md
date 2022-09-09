# 脚本集合


#### vim 到某一行

```bash
#!/bin/bash

onlyRead=''

while getopts ':R' optchar; do
    case "${optchar}" in
        R)
            onlyRead='-R'
            ;;
        *)
            break
            ;;
    esac
done

shift $((OPTIND-1))

act=$1

result=$(grep -n "act=='$act'" /path/to/dir)

fileName=$(echo "$result" | awk -F ':' '{print $1}')
line=$(echo "$result" | awk -F ':' '{print $2}')

vim $onlyRead +$line $fileName
```

#### bc - 计算器

```bash
echo $(cat a.txt | tr "\n" "+") | bc
cat a.txt | tr "\n" "+" | sed 's/$/\n/' | bc
```

不加换行会报错

#### sort - 排序

```bash
echo -e "$counts" | sort -n -k 1 -r | column -t -s ' ' | cat -n
```

#### Crontab

```
crontab -l > ~/crontab
echo "* * * * * echo test" >> ~/crontab
crontab ~/crontab
```

直接加载指定文件的内容到 crontab 里面


```
crontab -l | sed 's///g' | crontab -
```

跳过输出到文件

#### dmesg(时间转换为可读形式)

新版系统：
```
`dmesg -T`
```

老版本系统：
```
dmesg | sed -r 's#^\[([0-9]+\.[0-9]+)\](.*)#echo -n "[";echo -n $(date --date="@$(echo "$(grep btime /proc/stat|cut -d " " -f 2)+\1" | bc)" +"%c");echo -n "]";echo -n "\2"#e' | less
```

#### 批量重命名

去掉所有文件的 `.new` 后缀

```bash
ls | grep new | xargs -I {} bash -c 'a={}; mv $a $(echo $a | sed "s/.new//")'
```

#### less 命令自动换行（word wrap）

https://superuser.com/questions/272818/how-to-turn-off-word-wrap-in-less
```bash
-S, --chop-long-lines
```

可以直接在查看界面 `-S` 然后 Enter

#### lsof

与某台主机的连接

```
lsof -i@192.168.1.1
```

某个进程 ID 的连接

```
lsof -p 进程ID
```

某个端口的进程

```
lsof -i:端口号
```


#### umount: /mnt: target is busy.

用 `lsof /mnt` 查看占用的进程，kill 掉就行。

#### nohup 命令输出文件太大

```
cat /dev/null > stdout.nohup
```

如果不小心删除了文件，则需要找到打开的文件描述符：

```
pid=$(ps aux | grep your_process | grep -v grep | awk '{print $2}')
lsof -p ${pid}
```

可以看到对应的文件描述符 ID，例如是 fd 为 1 的文件被删除。则执行：

```
cat /dev/null > /proc/${pid}/fd/1
```

#### sed


1. 删除匹配到preSql的行

```bash
sed -i '/preSql/d' a.txt
```

2. 删除第一行

```bash
sed -i '1d' a.txt
```

3. 从第三行开始,每隔一行删除

```bash
sed -i '3~2d' a.txt
```

4. 删除从第４行到第８行

```bash
sed -i '4,8d' a.txt
```

5. 删除最后一行

```bash
sed -i '$d'  a.txt
```

6. 删除所有空行

```bash
sed '/^$/d' a.txt
```

7. 从匹配行到末尾行

```bash
sed -i  '/Website Design/,$d' a.txt
```

8. 删除匹配行和之后两行

```bash
sed -i  '/Storage/,+2d' a.txt
```

#### 应用当前状态

```sh
function status() {
    pid=$(getpid)
    if [[ ! -z "${pid}" ]]; then
        ps_source=$(ps -p ${pid} -o user,pid,ppid,pcpu,pmem,vsize,rssize,etimes,command)
        to_ISO3339=$(echo "${ps_source}" | sed 's/ELAPSED/START/' | awk 'BEGIN{now=systime()} NR>1 {$8=strftime("%Y-%m-%dT%H:%M:%S", now-$8);}{print;}')
        to_MB=$(echo "${to_ISO3339}" |  awk 'NR>1 {$6=int($6/1024)"M";$7=int($7/1024)"M";}{print;}')
        echo "${to_MB}" | column -t
        return
    fi
}
```

#### Systemctl

文件存放位置：

```
/etc/systemd/system/
/usr/lib/systemd/system
/lib/systemd/system
```

#### tcpdump

```bash
#!/bin/bash

tcpdump -i eth1 -w target.cap -c 1000 -s 0 -vv -A '(src host  192.168.1.1 or   src host  192.168.1.2)'
```

#### 文本行从下到上输出（tac）

tac 是 cat 的反向。

这是 cat：

```bash
$ cat thegeekstuff.txt
1. Linux Sysadmin, Scripting etc.,
2. Databases Oracle, mySQL etc.,
3. Hardware
```

这是 tac：

```bash
$ tac thegeekstuff.txt
3. Hardware
2. Databases Oracle, mySQL etc.,
1. Linux Sysadmin, Scripting etc.,
```

#### tmux 强行关闭窗口

ctrl+b &

#### 替换维基百科地址

```js
// ==UserScript==
// @name 替换维基百科地址
// @match *://www.google.com/*
// @match *://cn.bing.com/*
// @grant none
// ==/UserScript==

var links = document.getElementsByTagName("a");
for (var i=0,imax=links.length; i<imax; i++) {
    if (links[i].href.match(/\.wikipedia\.org\/wiki\//) || links[i].href.match(/\.wikipedia\.org\/zh-hk\//) || links[i].href.match(/\.wikipedia\.org\/zh-hans\//)) {
        links[i].href = links[i].href.replace(/en\.wikipedia\.org\/wiki\//i,"en.wanweibaike.com/wiki-");
        links[i].href = links[i].href.replace(/zh\.wikipedia\.org\/wiki\//i,"www.wanweibaike.com/wiki-");
        links[i].href = links[i].href.replace(/zh\.wikipedia\.org\/zh-hk\//i,"www.wanweibaike.com/wiki-");
        links[i].href = links[i].href.replace(/zh\.wikipedia\.org\/zh-hans\//i,"www.wanweibaike.com/wiki-");
        links[i].removeAttribute("onmousedown")
    }
}
```
