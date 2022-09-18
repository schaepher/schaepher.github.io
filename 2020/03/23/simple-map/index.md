# 简单的 map 实现


> In computer science, an associative array, map, symbol table, or dictionary is an abstract data type composed of a collection of (key, value) pairs, such that each possible key appears at most once in the collection. —— wikipedia  
> 在计算机科学中，关联数组、映射、符号表或者字典是一种由一系列(键、值)对组成的集合，且集合中的每个键最多出现一次。

由于写代码经常会用到 Map 的结构，经常会很好奇 Map 是怎么实现的。特别是如果只用到 C 语言，它应该怎么实现。

在去看 PHP 数组的源码之前，我自己设想了一下最简单的实现方式。

## 最简单的 map

由两个数组组成，一个存储 key，另一个存储 value。

<!-- more -->

类似于下面这种：

```c
注意：这里画图的时候把 key 数组的值和下标做了个翻转

                  +-----+-----+-----+-----+-----+-----+-----+-----+
                  |     |     |     |     |     |     |     |     |
            value | 100 | 250 | 233 | 333 | 123 | 345 | 678 | 111 |
                  |     |     |     |     |     |     |     |     |
  key array       +-----------------------------------------------+
                  |     |     |     |     |     |     |     |     |
            index |  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |
                  |     |     |     |     |     |     |     |     |
                  +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
                     |     |     |     |     |     |     |     |
                     v     v     v     v     v     v     v     v
                  +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
                  |     |     |     |     |     |     |     |     |
            index |  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |
                  |     |     |     |     |     |     |     |     |
value array       +-----------------------------------------------+
                  |     |     |     |     |     |     |     |     |
            value | 20  | 50  | 12  | 32  | 17  | 55  | 77  | 99  |
                  |     |     |     |     |     |     |     |     |
                  +-----+-----+-----+-----+-----+-----+-----+-----+
```

每次要获取一个 key 对应的值的时候，先遍历 key 数组，找到 key 的下标。然后再用该下标去 value 数组获取下标对应的值，就得到了 value。

例如要获取 key 为 250 对应的值 `map_get(map, 250)`：

遍历 key array，下标为 0 的值是 100，下标为 1 的值是 250，这个就是想要找的。把下标 1 记到小本本上。  

用下标 1 去 value array 找，得到 50 这个值。于是 `map_get(map, 250)` 的值是 50。

## 改进的方向

- 降低时间复杂度
- key 和 value 对于其他类型的支持
- 扩容
- 顺序遍历

### 降低时间复杂度

我们可以知道的是，普遍用于减低时间复杂度的方式是使用 hash 来查找，时间复杂度为 O(1) 。

而使用 hash 的方式又会有 hash 冲突。hash 冲突主要有四种解决方式：

- 链地址法（常用）
- 开放定址法
- 再哈希法  
  不要和扩容时的 rehash 搞混
- 建立公共溢出区

### 扩容

通常采取双倍扩容。扩容会涉及到两个方面：

- 扩容条件  
  它主要根据负载因子来确定是否扩容。
- rehash  
  扩容后需要对 key 重新做一次 hash，使得数据区分散在更多的 hash 桶内