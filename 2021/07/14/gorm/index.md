# GORM 底层实现


## 查询原理

1. 执行查询  
   `gorm.io/gorm/callbacks/query.go::Query(db *gorm.DB)`
2. 扫描结果集  
   `gorm.io/gorm/scan.go::Scan(rows *sql.Rows, db *DB, initialized bool)`  

扫描结果集的过程

1. 取出结果集的所有字段
2. 根据 Find() 时传入的引用判断存放的容器。比如用 `map[string]interface{}`，或者结构体切片 `[]User`，其他类型不一一列出。以下描述的是结构体切片的流程。
3. 根据结果集字段的个数，生成与其长度相等的 `interface{}` 类型的 values 切片，以及长度相等的 Field 类型的 fields 切片。
   - values 切片将会被重复使用
4. 找出结构体内与结果集列字段匹配的字段，并且在 fields 切片与列字段相同下标的槽里面放入结构体字段的信息。
5. 生成结构体变量
6. 在 values 切片的每个槽都设置与 fields 切片相同位置上的字段类型。  
   - values 的每个 item 是 `interface{}`，如果不在每次扫描之前都重新赋值，就会影响到已赋值的数据。
7. 调用原生库扫描数据行到 value 切片
8. 取出 fields 里有效的 field，在 values 里面取出相同位置的数据，并使用 field 将得到的数据赋值到结构体变量里面。
9. 结构体变量加入 ReflectValue
10. 回到 5 继续扫描下一行

## Eager Load

1. 执行驱动（driving）表的查询，将结果按照 foreignKey 的值分组
2. 取所有 foreignKey ，到被驱动（driven）表查询
3. 对于 driven 表的查询结果，逐个根据 referenceKey 找到 driving 表的结果分组，给分组里每个对象的相应 field 赋值

## 给结构体变量和结构体指针赋值有区别么？

如果是结构体指针，那么当 foreignKey 存在相同的数据时，同一个结构体指针会赋值给不同的 driving 表结果。一旦其中一个修改，另一个也会被修改。

## 可以在同一个 gorm.DB 指针并发查询么？

每次调用条件或者 Find 都会获取新的数据库实例，因此不会出现共用一个数据库实例的情况。




