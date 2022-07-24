# vim编辑器的简单使用


写这篇文章是因为在更新我的一篇博客 [Git的其他用法][Git的其他用法] 的时候，里面的`修改已经提交的commit说明`这一部分需要用到vim。

在使用`git config --global --edit`或者`git rebase -i commiteId^`的时候，git会进入文本编辑模式。默认的编辑器是vim，你可以在`Git安装的上层目录\Git\usr\bin`里找到vim.exe。   

这让我想起以前使用VI（Visual Interface）和VIM（VI IMproved）编辑器时的懵逼。现在干脆把vim的基本使用整理出来。  

vim编辑器有两种模式，分别为`命令模式`和`编辑模式`。  

## 一、命令模式  

当你刚进入文本编辑器的时候，处于编辑器的命令模式。这个命令模式可以做很多事情。这里介绍几个常用的：  

|命令|对应英文单词|说明|
|:--|:--|:--|
|`i`|insert|进入编辑模式，将光标定位在当前字符的前面|
|`v`|visual mode|按一下v相当于你平时在MS Word里面按住shift，用来选择（高亮）一段文本|
|`y`|yank|和复制的功能一样（英文意思为：猛拉）|
|`p`|paste|粘贴到当前字符前面|
|`x`|x就是"叉"（或者“干掉”）的意思|删除被高亮的字符（光标所在的字符也算是被高亮的字符）|
|`yy`|yank|复制光标所在行|
|`dd`|delete|删除光标所在行|
|`u`|undo|撤销上一个修改|
|`ctrl + r`|redo|不小心撤销过多的时候使用|
|`/想搜索的字符串`||`/`之后无空格，按Enter键开始搜索。按`n`（即next）往下搜索，按`N`往上搜索|
|`:1,$ s /text1 /text2 /c`|substitute|把`text1`替换成`text2`。`1,$`表示行数范围，其中 `$` 表示文档末尾。当你把数字`1`换成小数点`.` 时，表示从当前位置开始搜索（跟 bash 中用 `.` 表示当前位置一样）。`/c`表示让你选择找到之后的动作：`y`（yes）表示替换当前所选；`n`（next）表示跳过当前所选；`a`（all）表示当前所选及剩下的全部替换，不再确认；`q`（quit）表示停止替换。注意前面的冒号，与下面的命令类似。|
|`:q!`|quit discard|舍弃修改并退出|
|`:wq`|write then quit|保存修改并退出|

看到`:q!`这个命令，可能有点懵圈。你没看错，得先输入一个冒号`:`，再去输入`q!`。最开始的时候我不知道要输入冒号，结果半天退不出来。

**重要的说明**：  
在`i`的说明中，你可能不太理解为什么说“将光标定位在当前字符的前面”。在vim编辑器的命令模式下，光标是覆盖在字符上的。当你按`i`，它就将光标定位到当前字符的前面。与此相对的，按`a`（即append）时，光标就定位到当前字符的后面。 

如图所示：  

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170114124205275-1826474896.png)  

找了半天终于找到一个不错的在线vim编辑器：[Vim.js][Vim.js]    
还有一款加载比较慢的：[Interactive Vim tutorial - sandbox][Interactive Vim tutorial - sandbox]

点进去后你能直观地看到光标是覆盖到字符上的。你可以分别按`i`和`a`来查看效果。

至于其他命令，还是**看图比较直观：**

![](http://images2015.cnblogs.com/blog/809218/201701/809218-20170113185019338-657844358.png)

[中文版图源链接][中文版图源链接]

[英文版图源链接][英文版图源链接]

当然，你也可以下载vim的文档。这里是官方文档：[vimbook-OPL.pdf][vimbook-OPL.pdf]


## 二、编辑模式  

当你按`i`进入编辑模式的时候，基本上就可以照常编辑文本了。

除了正常的输入外，这些按键也可以正常使用：`del`（往光标后删除），`back`（也就是键盘上的←，往光标前删除），`enter`（回车键），`tab`（制表符）

但是注意，**想要选择字符或者复制粘贴等的时候，必须退出编辑模式**，到命令行模式去执行操作。  

当你想要退出编辑模式的时候，按`esc`键。注意，这时是退到命令模式，不是完全退出。你得在命令模式输入命令来完全退出编辑。  

知道了以上这些介绍，你可以进行基本的编辑了。

## 三、正则表达式

在命令模式点击 `/` 后，会进入搜索模式。它会搜索 `/` 之后的 pattern 。  

在搜索和替换的时候，如果不能用正则表达式，极可能耗费大量时间。Vim 是支持正则表达式的，不过 Vim 正则表达式的写法跟通常的写法有点不一样。

比如你要匹配 `dekkkl` 和 `detttl` ，你可以这么写：  

`/de.\+l `

这里的 `/` 是之前输入的，表示搜索功能。后面的 `de.\+l` 是正则表达式。这里与普通的正则表达式不同的地方在于用 `\+` 来表示匹配一次或多次，而不是 `+`。

详细的规则可以看：[VIM 正则参考][VIM 正则参考]

除了搜索之外，替换也能使用正则表达式。替换的语法和上面表格中的一致， `text1` 这个部分可以是正则表达式。

[Git的其他用法]: http://www.cnblogs.com/schaepher/p/4970291.html

[中文版图源链接]: http://blog.ngedit.com/vi-vim-cheat-sheet-sch.gif

[英文版图源链接]: http://www.viemu.com/vi-vim-cheat-sheet.gif

[vimbook-OPL.pdf]: ftp://ftp.vim.org/pub/vim/doc/book/vimbook-OPL.pdf

[Vim.js]: http://coolwanglu.github.io/vim.js/emterpreter/vim.html
[Interactive Vim tutorial - sandbox]: http://www.openvim.com/sandbox.html

[VIM 正则参考]: https://docs.google.com/spreadsheets/d/19gePTXX8nga8hfOfBgiS94sUC5snXnKOwf8RMSABmPI/pub?amp;single=true&amp;gid=0&amp;output=html
