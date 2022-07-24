---
title: PHP 语言使用细节
date: 2020-04-29 12:41:00
updated: 2020-04-29 12:41:00
tags:
- PHP
---

1. `array_merge()` 、`array_combine()` 和 `+` 处理 key 冲突的区别    

    |操作|数字 key|字符串 key|
    |:--|:--|:--|
    |array_merge|自增|覆盖已存在值|
    |+|使用已存在值|使用已存在值|
    |array_combine|覆盖已存在值|覆盖已存在值|  

    通常使用 array_merge 比 `+` 多。`+` 的使用场景例如以数字 ID 为 key 做深度遍历的时候，由于数组会加上子节点。如果用 array_merge，则会使 key 重制，并从 0 递增。

<!-- more -->

2. 函数式编程相关函数： `array_map()`、 `array_filter()`、 `array_reduce()`    
    - 只有 array_map 把匿名函数放在第一个参数位置  
    - 如果使用 Laravel 的 Collection，其 map 实现会传入 key，导致不能直接使用单参数的 trim 函数。

3. list() 如果使用数组，则 PHP 5 和 PHP 7 的顺序不同  
    ```php
    $a = 1;
    $b = 2;
    $arr = [];
    list($arr[0], $arr[1]) = [$a, $b];

    // $arr == [ 2, 1 ]; // PHP 5
    // $arr == [ 1, 2 ]; // PHP 7
    ```

4. 关联数组元素为空的情况下， json_encode() 会将其解释为 `[]`，而不是 `{}`  
    三种解决方法：  
    - 使用 JSON_FORCE_OBJECT 选项  
    - 不使用关联数组，而是对象 `[ 'a' => new \stdClass() ]`
    - 对有可能为空的关联数组都加上强制转换 `(object)$arr`

5. Json 包含过大的整数时，json_decode() 会将其转换为浮点数  
    解决方法：  
    - 使用 JSON_BIGINT_AS_STRING

6. 善用 filter_var() 函数  
    可用于做以下判断：  
    - 是否为整数
    - 是否为浮点数  
    - 是否为有效的 IP
    - 是否为有效的 IPv4
    - 是否为有效的 IPv6
    - 是否为内网 IP
    - 是否为有效的 Email 地址

7. 魔术方法 `__call()` 和 `__callStatic()` 仅在目标方法不可访问时调用  
    例如方法不为 public 或者方法不存在  

8. 魔术方法 `__get()` 、 `__set()` 、 `__isset()` 、 `__unset()` 仅在目标属性不可访问时调用  
    例如属性不为 public 或者属性不存在  

9. 数组在使用等于号比较的时候，会用 (key, value) 一起验证。  
    这意味着索引数组如果顺序不一致，则不相等。  
    也意味着关联数组即使顺序不同，只要 (key, value) 对的上就相等。  

10. strpos 在第二个参数 needle 非字符串的时候，会将其转换为十六进制字符串  
    例如 `strpos("1", 1)` 结果为 false，而 `strpos("\x1", 1)` 结果为 0

11. 关联数组中的整数字符串在会被当成数字处理  
    例如：  
    ```php
    foreach (['0' => 'a'] as $key => $value) {
        var_dump(is_int($key)); // true
        var_dump(is_string($key)); // false
    }
    ```  
    结合 strpos 的特点，要注意。

12. `isset($arr['a'])` 比 `array_key_exists('a', $arr)` 快  

13. `isset()` 判断变量是否存在，或者是否为 NULL， `empty()` 判断更多  

14. 变量和数组以值传递，对象以引用传递  
    如果要让方法返回的数组是用以用传递，则需要在方法名前面加上 `&`

15. `array_filter()` 会保留索引数组的索引，导致其变成关联数组  
    在 json_encode 的时候，会变成对象。因此要先用 `array_values()` 处理  

16. `array_reduce()` 匿名函数第一个参数是结果值，第二个是遍历到的值

17. `__sleep()` 和 `__wakeup()` 用于 `serialize()` 和 `unserialize()`  
    `__sleep()` 返回 public 字段名数组。`__wakeup()` 是在反序列化后做初始化。  
    `__wakeup()` 之前会先设置字段的值，并且不调用构造函数。  
    
    Serializable 接口需要实现 `serialize()` 方法和 `unserialize($serialized)` 方法。  
    `serialize()` 方法获取值（把私有变量放到数组），然后返回调用 `serialize()` 的结果。  
    `unserialize($serialized)` 方法需要先将 `$serialized` 反序列化，然后手动恢复属性值。  

18. `__clone()` 用于 clone 后修改对象。  
    由于属性值是对象时， clone 会复制引用（浅拷贝），所以要在 `__clone()` 里修改属性，再次执行 clone 。以此达到深拷贝的效果。  


## 其他  

> [十个 PHP 开发者最容易犯的错误](https://mp.weixin.qq.com/s?__biz=MzUyNDg1Nzg1OA==&mid=2247484939&amp;idx=1&amp;sn=8cba4a294e8f48186b5a182bf6f58489&source=41#wechat_redirect)
