# MySQL Row Count


legend:  
InnoDB中为何不像MyISAM那样维护一个row_count变量呢？


Schaepher:  
变量的修改需要加锁

legend:  
不= =

legend:  
那MyISAM就不用加锁了？

Schaepher:  
要啊，这不所以才要干掉嘛

legend:  
不。。。

legend:  
这个开销应该还好

legend:  
你想想

legend:  
而且每次新增，删除本身就是要加锁的啊，这里锁的开销其实可以忽略

legend:  
我的理解是因为mvcc

legend:  
因为你并没法知道开启事务那一刻，实际的行数是多少

legend:  
必须通过undolog算出来

legend:  
发哥，来反驳我

legend:  
尼玛，来啊

legend:  
battle

legend:  
搞我

Schaepher:  
那事务开启的时候，读取那个行数值不就好了

legend:  
哈？

legend:  
怎么读取

Schaepher:  
就是像 myisam 那样弄一个变量存储，然后读取这个值

legend:  
你什么时候更新呢

Schaepher:  
提交事务的时候

legend:  
那你这个事务提交了

legend:  
你这个事务之前的事务呢

