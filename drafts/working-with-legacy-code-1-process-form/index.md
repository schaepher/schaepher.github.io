# 与旧代码相处之一：流程表单数据


这个项目是流程系统，有三百条左右的流程。其中一部分流程会共用一些操作，即流程中某几个节点的功能和其他流程一样。但各个流程的原始数据不同，以至于不能完全共用，必须将不同流程的数据转换成功能所需入参。

原来的开发方式让人难以接受，于是我尝试了几种方式。这个过程仿佛是从原始社会到现代社会按顺序走了一遍。（哭了）

#### 原来的开发方式

这个系统的每个节点都有对应的唯一标识。执行某个节点时，会根据这个节点找到对应的代码块执行。其实就是一大堆 if else。例如：  

```php
if ( $nodeCode === 'code_a' ) {
    // do_something
} else if ( $nodeCode === 'code_b' ) {
    // do_something
} // ....
```

把它们看成一个个 function 也是没问题的。

由于流程都有一个唯一 ID，在写业务代码的时候，就用这个 ID 来区分获取数据的方式。例如：  

```php
if ( $processCode === 'proc_code_a' ) {
    $data1 = get_data('proc_a_data_name1');
    $data2 = get_data('proc_a_data_name1');
} else if ( $processCode === 'proc_code_b' ) {
    $data1 = get_data('proc_b_data_name1');
    $data2 = get_data('proc_b_data_name2');
}
```

这种方式写时一时爽，维护起来可就难受了。业务代码里面混入一大堆获取数据的代码。  

在上一篇工作一年的记录中，我开了一个面向对象的入口。在这个路口里面的 Controller 获取数据时，不再是用 if-else 判断，而是利用反射创建对应流程的 DataContainer。  

DataContainer 获取数据有两种方法，下面详细说明。

#### 法一：工厂模式 + 场景方法(18年07月)

```php
/** $container \App\Process\Container\Interface\GetAllDataWhenDoingXXX **/
$container = ProcessInstanceDataContainer::rebuildFrom('proc_inst_id');
$data = $container->getAllDataWhenDoingXXX();

$data1 = $data['data1'];
$data2 = $data['data2'];
```

如果一个流程有上百个节点（确实有），则该流程对应的 DataContainer 将会有对应数量的方法。并且这些方法需要把数据组装成业务代码调用时所需的格式，因此会很复杂。

鉴于以上问题，该方式用了一阵子就没用了。后面改成法二。

#### 法二：工厂模式 + 获取基本数据 + Controller 根据需要获取和组装

不再组装成业务代码所需的格式，仅提供最基础通用的数据。分为两种情况：

1. 表单的数据
2. 根据表单数据获取的基础数据

每次从 Container 获取基础数据：  

```php
/** $container \App\Process\Container\Interface\GetXXXData **/
$container = ProcessInstanceDataContainer::rebuildFrom('proc_inst_id');
$data1 = $container->getData1();
$data2 = $container->getData2();
```

所有需要使用相同方法的流程，都实现同一个接口。在 Controller 层根据这些基础数据拼接成最终所需数据。这样就能将 DataContainer 方法的数量减少很多。

业务层调用的时候，可能不同的流程的表单数据不一样。例如流程 A 有 Data1 但没有 Data2，但可以通过其他数据计算出 Data2，流程 B 反之。这时候接口不变，在实现的时候做转换。

