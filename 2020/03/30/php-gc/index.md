# PHP 垃圾回收


1. 每个值容器（zend_value）里面都会有引用计数结构体 zend_rrefcounted
2. 引用计数减少到 0 时进行清除
3. unset() 将值的引用减少 1
4. 值容器引用在减少 1 后如果不为 0 ，则加入回收池
5. 回收池满后，开始执行回收
    1. 第一次遍历回收池所有值容器。对所有值容器的引用减 1 。如果是嵌套对象（如数组和对象），则遍历其元素，元素值容器的引用减 1 。  
        - 这是一个深度遍历的过程。
        - 这里是模拟减 1，减到 0 时不触发回收
    2. 第二次遍历回收池所有值容器。对引用计数不为 0 的值容器引用加 1 （恢复到之前的样子），并将其从回收池中移出。
    3. 回收池中引用计数为 0 的值容器被作为垃圾清除。

<!-- more -->

如：

```php
<?php

$arr = [];

$arr[0] = 'gc';
xdebug_debug_zval('arr');
// 输出：
// arr: (refcount=1, is_ref=0)=array (0 => (interned, is_ref=0)='gc')

$arr[1] = &$arr;
xdebug_debug_zval('arr');
// 输出：
// arr: (refcount=2, is_ref=1)=array (0 => (interned, is_ref=0)='gc', 1 => (refcount=2, is_ref=1)=...)

$arr[2] = &$arr;
xdebug_debug_zval('arr');
// 输出：
// arr: (refcount=3, is_ref=1)=array (0 => (interned, is_ref=0)='gc', 1 => (refcount=3, is_ref=1)=..., 2 => (refcount=3, is_ref=1)=...)

$arr[3] = $arr;
xdebug_debug_zval('arr');
// 输出：
// arr: (refcount=5, is_ref=1)=array (0 => (interned, is_ref=0)='gc', 1 => (refcount=5, is_ref=1)=..., 2 => (refcount=5, is_ref=1)=..., 3 => (refcount=1, is_ref=0)=array (0 => (interned, is_ref=0)='gc', 1 => (refcount=5, is_ref=1)=..., 2 => (refcount=5, is_ref=1)=...))

unset($arr);
xdebug_debug_zval('arr');
// 输出：
// arr: no such symbol
```

unset 前，$arr 引用计数为 5 。

unset 将 $arr 引用计数减 1 ，得到 $arr 引用计数 4。

遍历 $arr 。

将 $arr[0] 值容器引用计数减 1，不影响 $arr 。

将 $arr[1] 值容器引用计数减 1，得到 $arr 引用计数 3 。

将 $arr[2] 值容器引用计数减 1，得到 $arr 引用计数 2 。

将 $arr[3] 值容器引用计数减 1。  

遍历 $arr[3] 。

将 $arr[3][1] 引用计数减 1，得到 $arr 引用计数 1 。
将 $arr[3][2] 引用计数减 1，得到 $arr 引用计数 0 。

回收 $arr 。

