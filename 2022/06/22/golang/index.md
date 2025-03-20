# golang 编程笔记


# getter 和 setter 在 Golang 中的应用

如果只是读取数据库的信息，不参与写，那么直接用字段，不另外添加 Getter 和 Setter。

> https://softwareengineering.stackexchange.com/a/419316

这样能使代码尽可能地简洁，只是需要程序员去判断什么时候该使用哪种方式。

由于 Golang 自身属于强类型，当需要将 Public Field 改为 Setter 时，可以方便地用工具来完成大量的修改。所以无需担心。

> https://stackoverflow.com/a/11842484


## import

当前包内所有文件所依赖的其他包的 init 执行完后，才能按顺序执行当前包的 init。

## 是否使用 make

如果 slice 或者 map 的元素数量已知，或者可以估计，则使用 make 并传入 size。否则可以使用通常的初始化。

map 也可以传 size。如果不传，则默认为一个较小的值。

chan 则必须使用 make。

## exec: "gcc": executable file not found in %PATH% when trying go build

```
cgo_enabled=0 go build
```

## 结构体比较

如果字段是基本类型，则比较其值。如果字段是结构体，则比较结构体内的字段的值。如果字段是接口类型，则仅比较其指针，不比较接口的指向的值。

