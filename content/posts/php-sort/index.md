---
title: PHP sort 源码
date: 2020-03-30 23:25:00
updated: 2020-03-30 23:25:00
tags: 
- PHP
- 源码
---



`ext/standard/array.c`

<!-- more -->

```c
/* {{{ proto bool sort(array &array_arg [, int sort_flags])
   Sort an array */
PHP_FUNCTION(sort)
{
	zval *array;
	zend_long sort_type = PHP_SORT_REGULAR;
	compare_func_t cmp;

	ZEND_PARSE_PARAMETERS_START(1, 2)
		Z_PARAM_ARRAY_EX(array, 0, 1)
		Z_PARAM_OPTIONAL
		Z_PARAM_LONG(sort_type)
	ZEND_PARSE_PARAMETERS_END_EX(RETURN_FALSE);

	cmp = php_get_data_compare_func(sort_type, 0);  // 根据 sort_flags 选择比较函数

	if (zend_hash_sort(Z_ARRVAL_P(array), cmp, 1) == FAILURE) {
		RETURN_FALSE;
	}
	RETURN_TRUE;
}
```

接下来找 zend_hash_sort 。

`Zend/zend_hash.h`

```c
#define zend_hash_sort(ht, compare_func, renumber) \
	zend_hash_sort_ex(ht, zend_sort, compare_func, renumber)
```

用于排序的算法是 zend_sort 。

`Zend/zend_sort.c`

```c
ZEND_API void zend_sort(void *base, size_t nmemb, size_t siz, compare_func_t cmp, swap_func_t swp)
```

该排序算法来自于 LLVM 项目的 libc++ 实现。  

> [https://github.com/llvm/llvm-project/blob/master/libcxx/include/algorithm](https://github.com/llvm/llvm-project/blob/master/libcxx/include/algorithm)

```c++
template <class _Compare, class _RandomAccessIterator>
void
__sort(_RandomAccessIterator __first, _RandomAccessIterator __last, _Compare __comp)
```

## 快排

快排是实践中最快的已知排序算法。平均时间复杂度是 O(N log N)，平均空间复杂度是 O(log N)。

> 空间复杂度主要是递归使用的栈空间。最优递归深度是 log N 。

思路：  

在数组中选一个元素作为中心元素，把数组元素划分为小于中心元素的集合以及大于中心元素的集合，两个集合放到中心元素的两边。然后再对两个集合分别划分，一直划分到元素个数为 1 或 0 的时候才停下。

优化：

- 小数组  
    元素较少（N <= 20）时，快排不如插入排序。使用插入排序可以节约大约 15% 的运行时间。  
    > 就算有很多元素，经过不断的划分，总会有元素个数小于等于 20 的时候。
- 中心元素的选取  
    1. 选最左边或者最右边是最简单的，但是很容易导致花费很多时间。例如数组已经有序的情况下。  
    2. 随机选取会更好一些，但随机数的生成也比较耗时。  
    3. 三数中值。取左、中、右位置的三个值，取中数作为中心元素。这是最好的选择，节约快排大约 5% 的运行时间。

zend_sort 是怎么做的？  

- 元素小于等于 16 个的时候，使用插入排序  
    ```c
    if (nmemb <= 16) {
        zend_insert_sort(base, nmemb, siz, cmp, swp);
        return;
    }
    ```

- 元素大于 16 个的时候，使用快排的指针交换法  
	左右两个指针分别往中间移动，直到左边指针指向大于中心元素，右边指针小于中心元素，然后左右指针值互换，再继续移动。  
    还有一种是挖坑法。

- 中心元素的选取根据元素个数分为两种情况：  
	1. 个数小于 1024 时，将数组做一次平分，取中间数和两边缘数，如 `|...|...|` 的竖线部分，然后取三数中值。
	2. 个数大于等于 1024 时，将数组做两次平分，取三个中间数和两边缘数，如 `|...|...|...|...|` 的竖线部分，然后取五数中值。  

	> 个数非常大时，可能会因为划分后元素个数仍大于 1024 而再取五数中值。


