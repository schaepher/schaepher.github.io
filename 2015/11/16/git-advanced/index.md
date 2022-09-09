# Git的其他用法


## 目录：
 
* <a href="#garbage_collection">减少【.git】文件夹的大小和文件数</a> 
* <a href="#editor">更换git for windows的文本编辑器</a> 
* <a href="#rebase_commit_msg">修改已经提交的commit说明</a>
* <a href="#rebase_commit_merge">合并commit</a>
* <a href="#conflict">解决merge时出现的冲突</a> 
* <a href="#back">回退一个merge</a>
* <a href="#pick">获取某一commit的修改</a>
* <a href="#push_force">将低版本push到Github（删掉高版本Commit）</a>

---

<a name="garbage_collection"></a>
### 减少【.git】文件夹的大小和文件数

随着commit次数的增多，`.git`文件夹的文件数和文件夹大小都会不断增大。  

虽然对于小项目，增大的速度极慢，文件夹也基本在10M左右。但如果你和我一样，想减少该文件夹的文件数目（通常不少），可以试试这个命令。当然，git是鼓励你多使用这个命令的。见：[Git - git-gc Documentation](https://git-scm.com/docs/git-gc)  

> Users are encouraged to run this task on a regular basis within each repository to maintain good disk space utilization and good operating performance.  

如何减少？特别简单，就是你进入到一个repository，也就是你项目的根目录，执行 `git gc` 就行了。  

我们来看看执行gc命令前后的对比：  

运行 `git gc` 前：  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115214601697-480279175.jpg)

运行 `git gc` 后：  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115214607510-1147295395.jpg)

文件夹大小变化不大。变化最大的是文件数目（2561 -> 37)和文件夹数(274 -> 18)。  

要讲清楚这个命令，涉及到了git是如何存储你的commit。这就要说到`快照（Snapshot）`。  

我们先看看git的官方说明：[直接记录快照，而非差异比较](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-Git-%E5%9F%BA%E7%A1%80#直接记录快照，而非差异比较)  

> 每次你提交更新，或在 Git 中保存项目状态时，它主要对当时的全部文件制作一个快照并保存这个快照的索引。 为了高效，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。 Git 对待数据更像是一个 快照流。  

那么问题来了：什么是快照？  

来实际感受一下：  

首先我准备了一个大的文件，这样比较能说明问题。刚好今天整理一个文件，有55.3MB，就顺手拿来用了。  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115230551416-1794822309.jpg)

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115230250728-753466185.jpg)

可以看到，源文件是55.3MB，而将其添加到仓库里后，仓库的大小变为46.3MB。这相当于是将整个文件复制到里面去。  

如果这还不能说明问题，再来一次。我删除了文件里的一大部分内容，将其减小至20.5MB。再将其提交到仓库里面。

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115230554228-184799821.jpg)

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115230257994-32768218.jpg)  

增加了19MB，跟20.5MB很接近。  

你可以在 `.git\objects\某个文件夹 ` 里找到这两份快照。  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115232333431-1122489419.jpg)

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115232336666-222754137.jpg)

于是我们可以得出一个近似的结论：在git中，一份快照就是你当前工作目录的状态。当你使用add命令时，它将你当前工作目录的文件进行压缩，形成一份快照。

> 不过，如果你有一些文件完全没有被修改过，它只保存指向之前版本的引用。这样可以减少快照所占用的空间。这里没有试验，但是官方对此有说明：    
> To be efficient, if files have not changed, Git doesn’t store the file again, just a link to the previous identical file it has already stored.

那么这个时候我们再去执行 `git gc` ，会变成什么样呢？  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115232735088-54497085.jpg)

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115233041025-752982170.jpg)

之前说的三个方面都有减少。  

我们再看看`.git\objects`里的文件夹（事先不知道它会删除文件夹，没有截图。。）  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115233042431-557552073.jpg)

可以看到我们上面快照所在文件，即`02`和`f7`文件夹已经不在`objects`这个文件夹里面了。（info和pack两个文件夹一直都在那里）  

点进pack文件夹：  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170115233708353-128671852.jpg)  

`.git` 文件夹的46.5M都在这里了。所以我们可以知道，git将之前两个文件夹的快照文件合并到一起了。

---

<a name="editor"></a>
### 更换git for windows的文本编辑器

git for windows默认使用vim作为文本编辑器，为此我专门写了篇vim的基本操作：[vim编辑器的简单使用][vim编辑器的简单使用]

如果你不想学习vim的使用，也可以把它换掉。  

例如我想把它换成[atom][atom]：  

1. 先找到启动atom的exe文件的路径。我的在 `C:\Users\Schaepher\AppData\Local\atom\app-1.13.0\atom.exe`  
1. 启动git for windows，执行`git config --global core.editor "C:/Users/Schaepher/AppData/Local/atom/app-1.13.0/atom.exe --new-window --foreground --wait"`   
    > 注意，这里路径的斜杠与Windows显示的相反，这是Linux的路径格式。  
    > 后面一串参数`--new-window --foreground --wait`是由各编辑器自己指定的。如果不这样指定，执行`git rebase -i commitId^`的时候会直接退出编辑。

---

<a name="rebase_commit_msg"></a>
### 修改已经提交的commit说明

先用`git log`查看commit信息：

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113151046056-967795774.png)

我打算更改下面那个commit，使用`git rebase -i 版本号^`：

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113151243947-791803325.png)

执行命令后，会进入这样的界面：

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113151051103-1707647553.png)  

它把我们传入的版本号之上的commit条目都显示出来了，这里只关注我们要改的那一条。将第一个`pick`修改为`reword`，保存并退出。  

过一会儿，它会再进入这样的界面：  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113151055353-1678885020.png)  

将第一行的`Android的ListView`改为`这个更改后的message`，保存并退出。  

再用`git log`查看：

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113151102556-1969555440.png)

不仅commit message被更改了，从被更改的commit开始，commit id都会重新生成。

---

<a name="rebase_commit_merge"></a>
### 合并commit

先用`git log`查看commit信息：

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113213803260-630487490.png)  

如果你想把最近的四个commit合并成一个commit，有两种方法。一种是用`git reset --soft d7ac`，在`git commit -m "新的commit message"`，另一种是用`git rebase`。接下来讲第二种。  

首先根据上图的commit id，我想把`afe14f`之后的commit合并到`afe14f`里面，执行 `git rebase -i afe14f^`。进入编辑界面：  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113223346978-204618168.png)

根据提示，`squash`会把所在的commit合并到前一个commit上面。我们要合并到`afe14f`，所以修改后三个。而在合并之后，我们需要修改`afe14f`的commit message，所以使用`reword`。  

> 你也可以用缩写，比如`squash`的缩写是`s`。而`reword`的缩写是`s`。


![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113223351416-502078337.png)

保存并退出，会进入下一个界面。修改第一行的commit message，即`reword`的那个message，为`添加Android学习笔记，特别是ListView的介绍；添加对git commit的修改教程`。如下图：  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113223355588-2133522629.png)  

保存并退出。自动进入下一个界面：  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113223358525-387095125.png)  

此时要将其他三个message去掉，只要在那三行前面加`#`就行了。如下图：

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113223401775-1494057357.png)

保存并退出，等待git处理完成。  

再次使用`git log`查看commit信息：

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170114002320525-763331490.png)

完成！  

> 这里貌似可以不使用`reword`，待实验。

---

<a name="conflict"></a>
### 解决merge时出现的冲突  

当你和其他团队成员对同一个文件进行修改后，merge的时候有可能会出现冲突。你可以打开每个冲突的文件，手工解决冲突；也可以借助冲突处理工具来解决冲突。这里分别介绍这两种方式：

1. 手工解决冲突

    冲突提示如下图所示：  
  
    ![](http://images2015.cnblogs.com/blog/809218/201511/809218-20151116223930593-1760266962.png)
  
    CONFLICT表示有冲突，在这一行的末尾，显示冲突文件。这里有两个文件冲突，分别是README.md和app.iml   
    这里以README.md为例，解决冲突： 
  
    ![](http://images2015.cnblogs.com/blog/809218/201511/809218-20151116223851718-48866874.png)  
  
    被红框框住的符号 `=======` 是冲突的分割线。  
  
    `<<<<<<< HEAD` 和分割线之间的是本地的文本，分割线和 `>>>>>>> upstream/dev` 之间的是远程分支的文本  

    你可以选择保留其中一个版本的文本，然后将三个冲突符号都删除。这样表示已解决冲突。如果你想同时保留两个版本，那么只需将冲突符号删除。  
  
    解决冲突后如下图所示：  
   
    ![](http://images2015.cnblogs.com/blog/809218/201511/809218-20151116223256608-2077380872.png)
   
2. 借助冲突处理工具
    个人认为Meld这个工具比较好用，Android Studio自带的冲突处理工具和它很相似。我用过tortoisegit的工具，感觉没有Meld好用，这里就不介绍了。
    
    （1） 首先去Meld的官网下载安装文件并安装。->[点此进入Meld官网](http://meldmerge.org/)
    
    （2） 安装完后，打开你的git工具，比如msysgit。执行 `git config --edit --global` ，此时会打开一个配置文件。在文件最后添加以下四行：  
    
    ```
        [merge]  
                 tool = meld  
        [mergetool "meld"] 
                 path = e:/software/MeldMergeTool/Meld.exe  
    ```
    
    提示：path是根据你安装Meld的路径来决定的，同时要把路径中的 `\` 改成 `/` 。从上面可以看出我的安装路径为 `e:\software\MeldMergeTool\` 。 
  
    （3） 在merge的时候，如果出现冲突，运行命令 `git mergetool` 这时就会打开Meld。
  
    （4） Meld的界面如下：  
  
    ![](http://images2015.cnblogs.com/blog/809218/201511/809218-20151129212715813-1728290775.png)  
  
    冲突的地方会显示红色，如果你想保留本地的代码，则点击左边的 `→` 箭头。  
  
    把所有红色（冲突）区域解决后，可以根据实际情况去解决绿色（添加）和灰色（更改）。  
  
    一般保存中间的修改就行。如上图红框处。

---

<a name="back"></a>
### 回退一个merge

1. 如果是merge一个GitHub的Pull Request，可以进入要回退的那个Pull Request，在下面有一个revert按钮，可以用来revert一个Pull Request。如下图红框处：  

    ![](http://images2015.cnblogs.com/blog/809218/201511/809218-20151129214048063-2138029364.png)
  
2. 在命令行里revert

    （1）用 `git log` 看commit记录  
  
    ![](http://images2015.cnblogs.com/blog/809218/201511/809218-20151116223326421-1380239590.png)
  
    现在我们要回退 `commit 561dab` （也就是图中第一个commit），该commit将Pull Request #113 merge到项目中。
    
    （2）使用 `git revert HEAD -m 1` 命令回退  
  
    ![](http://images2015.cnblogs.com/blog/809218/201511/809218-20151116223335155-387212738.png)
  
    如果是非merge的回退，用 `git revert 版本号` 就行了。但是这里是对merge操作进行revert，需要加上参数 `-m` 。命令最后加个 `1`。
    
    为什么要加上 `1` 呢？看上面`（1）`的图中的第二个红框，这个 `1` 对应红框中的 `6a3c30c` 版本。而如果填 `2` ，则对应 `b7831df` 。  
    
    继续看log，会发现 `6a3c30c` 是merge这个Pull Request之前的状态。而 `b7831df` 则是当前版本之前的一个merge。
    
    输入命令回车后，会跳出一个文本。  
  
    ![](http://images2015.cnblogs.com/blog/809218/201511/809218-20151116223342436-540832725.png)
  
    目前无视它就行。关闭文本，回到shell，回车。

    ![](http://images2015.cnblogs.com/blog/809218/201511/809218-20151116223354858-2073416423.png)
  
    回退成功！这个回退不会删除掉中间的commit记录，而是将这次revert作为一个commit加到commit记录上面。  

---

<a name="pick"></a>
### 获取某一commit的修改

假设有commit `a b c` ，从左到右，`c` 为最新版。  
这时你发现 `b` 的一个修改有问题，想回退到 `a` 。但是如果回退到 `a` ， `c` 的commit也会被取消。  
这时可以用 `git cherry-pick 版本号` 这个命令获取 `c` 的commit。

下图是示例的log记录，从①可以看出，这里从②回退到⑤。

![](http://images2015.cnblogs.com/blog/809218/201511/809218-20151118150019671-1870975439.png)

现在我想获取④的commit。使用 `git cherry-pick 版本号` 将选定版本的提交合并到当前版本。

![](http://images2015.cnblogs.com/blog/809218/201511/809218-20151118150026327-2034885343.png)

---

<a name="push_force"></a>
### 将低版本push到Github（删掉高版本Commit）
有时候会因为各种原因，想要回退版本。如果没有关联Github或者没有push上去，那问题不大。但是如果你已经push到Github上了，这时候就比较尴尬了，因为普通的push是会被Github拒绝的。虽然Github提供了Revert功能，但是这并不能完全消去一个commit。  

先看看reset后被拒绝的样子：  

![](http://images2015.cnblogs.com/blog/809218/201606/809218-20160604212640196-641381418.png)

解决方法就是：  
1. 先用 `git reset --hard 版本号` 回到你想要的版本  
2. 执行 `git push --force`  
    ![](http://images2015.cnblogs.com/blog/809218/201606/809218-20160604212746321-1639371739.png)   
    
    再看看Github：  
   
    ![](http://images2015.cnblogs.com/blog/809218/201606/809218-20160604212804867-1594519594.png)  
     
    > 当然，一般是推荐用 `git push origin HEAD --force` 的，能防止因为其他没配置好而产生错误。对我来说差别并不大……

[vim编辑器的简单使用]: http://www.cnblogs.com/schaepher/p/6284115.html

[atom]: https://atom.io/
