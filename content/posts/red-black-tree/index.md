---
title: 红黑树
date: 2022-06-11 12:26:00
updated: 2022-06-11 12:26:00
tags:
- 树
- 平衡树
- 数据结构
---

2-3 树和 2-3-4 树统称为 B-树（Balanced Tree）。

### 为什么不直接使用 B-树？

既然以 2-3 树和 2-3-4 树都可以用来转换成红黑树，为什么最终使用 2-3-4 树的转换呢？

> [https://stackoverflow.com/questions/8765558/why-dont-we-use-2-3-or-2-3-4-5-trees](https://stackoverflow.com/questions/8765558/why-dont-we-use-2-3-or-2-3-4-5-trees)

> Implementation of 2-3-4 trees typically requires either multiple classes (2NODE, 3NODE, 4NODE) or you have just NODE that has an array of items. In the case of multiple classes you waste lots of time constructing and destructing node instances and reparenting them is cumbersome. If you use a single class with arrays to hold items and children then you are either resizing arrays constantly which is similarly wasteful or you wind up wasting over half your memory on unused array elements. It's just not very efficient compared to Red-Black trees.

> Red-Black trees have only one type of node structure. Since Red-Black trees have a duality with 2-3-4 trees, RB trees can use the exact same algorithms as 2-3-4 trees (no need for the stupidly confusing/complex implementations described in Cormen, Leiserson and Rivest that led to AA trees which are not less complex than the 2-3-4 algorithm.)

> So, Red-Black trees for their ease of implementation plus their memory/CPU efficiency. (AVL trees are nice too. They produce more well balanced trees and are stupid simply to code but they tend to be less efficient due to working too often to maintain only a slightly more compact tree.)

> Oh, and 2-3-4-5-6... etc aren't done because nothing is gained. 2-3-4 has a net-gain over 2-3 trees because they can be done without recursion easily (recursion tends to be less efficient, especially when it cannot be coded tail-recursively). However, B-Trees and Bplus-Trees are pretty much 2-3-4-5-6-7-8-9-etc trees where the max size of the nodes, n, is chosen so that n records can be stored in a single disk sector. (i.e. each disk sector is a node in the tree and the size of the sector is equivalent to the number of items stored in the node.) This is because the time to search through 512 records linearly in memory is still MUCH faster than traversing down a level in the tree which requires another disk seek/fetch. and O(512) is still O(1) and thus maintains O(lg n) for the tree.

> [https://read.seas.harvard.edu/~kohler/notes/llrb.html](https://read.seas.harvard.edu/~kohler/notes/llrb.html)

下一篇将会详细展开红黑树的内容。
