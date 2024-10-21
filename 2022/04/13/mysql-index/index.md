# MySQL Index


Schaepher:  
那索引开始

legend:  
1,2,5

legend:  
1,2,6

legend:  
先回答

Schaepher:  
锁粒度涉及到的是意向锁

Schaepher:  
mvcc 实现原理是快照读。用 undo log 的回滚段存储旧版本数据。

Schaepher:  
事务特性：ACID，原子性，一致性，隔离性，持久性。

Schaepher:  
=。=隔离性我刚没想到

legend:  
隔离性= =

legend:  
我就记得ACID

Schaepher:  
四个隔离级别：
读未提交、读已提交、可重复读、序列化

Schaepher:  
mvcc 在读已提交和可重复读生效。

Schaepher:  
读已提交解决脏读问题

Schaepher:  
可重复读解决两次读数据值不一致的问题

Schaepher:  
mvcc + 可重复读，解决幻读问题

Schaepher:  
next-key lock 解决幻写问题

Schaepher:  
next-key lock 是 gap lock + record lock 结合使用

Schaepher:  
MySQL 默认使用 next-key lock。
当能确定边缘值的时候，用 next-key lock，否则用 gap lock。

Schaepher:  
next

Schaepher:  
![](./img/1.png)

Schaepher:  
淦，我之前理解错索引建立时机的意思了

Schaepher:  
建立时机不是指MySQL本身的建立，而是业务上什么时候给字段加索引

legend:  
哦？？？？

legend:  
我也理解是mysql本身

legend:  
他要问的是怎么建立索引

legend:  
什么场景下需要建立？

Schaepher:  
对

Schaepher:  
建立索引有一个重要指标：cardinality

Schaepher:  
太小没必要索引，因为加了索引 MySQL 也不会去用

Schaepher:  
如果是过程，那就是我发的那篇

Schaepher:  
https://schaepher.github.io/2020/04/30/mysql-index-creation/

Schaepher:  
除了主键，其他都是辅助索引

Schaepher:  
myisam 和 innodb 的索引有什么区别

legend:  
没卷过 myisam的缩影

Schaepher:  
为什么 innodb 的主键的大小不能设置过大？

legend:  
因为查询效率吧

legend:  
太长了，索引就没啥用了= =

legend:  
嗯，我决定去研究下官方说法

Schaepher:  
这个跟 innodb 的索引特性有关

Schaepher:  
结合 myisam 的不同之处

Schaepher:  
结合辅助索引回答

legend:  
哦，和我想的差不多

legend:  
就是太长了会导致树层级变多

legend:  
磁盘io次数变多

Schaepher:  
？

legend:  
嗯？？？？？？

Schaepher:  
资料我看看？

legend:  
https://www.jianshu.com/p/31bfd4ac3e61

Schaepher:  
是其中一点

legend:  
尼玛

Schaepher:  
还有一点是辅助索引存储的 value 不是磁盘位置，而是主键

legend:  
嗯

legend:  
哦= =

legend:  
懂了

legend:  
会导致辅助索引变大

legend:  
内存消耗过大

Schaepher:  
嗯，主键的长度不仅影响了主键索引本身，也影响了辅助索引

legend:  
索引什么时候需要回表

Schaepher:  
啥回表

legend:  
就是什么时候需要去磁盘

Schaepher:  
反过来是不是问，什么时候不需要读磁盘

legend:  
嗯

Schaepher:  
覆盖索引

legend:  
不一定哦

Schaepher:  
查询的字段都在索引里

legend:  
主键的情况呢

Schaepher:  
啥主键

legend:  
主键是不是包含所有子弹

Schaepher:  
哪个情况？

legend:  
字段

Schaepher:  
主键就只有主键

legend:  
主键是需要一次磁盘io是吧

Schaepher:  
不一定，还可能有两次或者三次

Schaepher:  
看查询的主键在 b+ 树的哪个层次

legend:  
嗯？

Schaepher:  
哦不对

legend:  
你想清楚

Schaepher:  
想到数据页去了

legend:  
我一下被你高蒙蔽了

Schaepher:  
不对啊。innodb 是聚集索引

legend:  
嗯

Schaepher:  
主键索引指向数据

legend:  
是的

Schaepher:  
那就是了

Schaepher:  
如果数据量大，那就得每个层次查一次索引

