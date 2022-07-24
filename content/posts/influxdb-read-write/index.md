---
title: InfluxDB 存储结构、读、写
date: 2021-03-06 00:00:00
updated: 2021-07-31 17:35:00
categories:
 - Database
 - InfluxDB
tags:
 - InfluxDB
---

> 这篇最早是 2021 年 3 月写的，最近又拿出来复习一遍，也补充了一些新的内容。上一篇博客发表过后已经 3 个月没有发表新的博客，就把这篇拿出来了。内容没有完全梳理完毕，算是笔记。先发出来，后续再逐渐完善。

InfluxDB 是开源的时序数据库，采用列式存储。原先有开源集群版本，但在 0.11 版本之后，集群版本仅在商业版中提供。

<!-- more -->

在一些场景中，需要用到集群，但又不需要完整的集群功能，只需要简单地实现分片存储和查询或者副本集就行了。可以在开源的基础上添加这些简单的功能。

添加功能的方式可以分为通过顶层的 HTTP API 操作和参考 InfluxDB 源码写相应扩展。

例如通过 HTTP API 写入数据时可以通过 Nginx 的一致性 hash 将数据转发到不同的 InfluxDB 实例，用 HTTP API 把请求发送到所有 InfluxDB 然后手动合并，或者写个中间层合并。但是资源消耗比较大，而且不够灵活。因此很有必要了解 InfluxDB 的源码。

一个系统的发展通常是越来越复杂，并且这个过程中的代码会受到其发展过程中的影响。选择一个合适的版本就行了。这里选择的是 0.11.1 版本的代码。按照惯例，省略的代码用 `// ...` 代替。

## 基础概念

InfluxDB 的 measurement 类似关系数据库的 table，Point 类似关系数据库的行，存储着某一时刻的数据。Point 的接口定义如下：

```go
type Point interface {
	// Measurement 部分
    Name() string
	SetName(string)

    // Tag 部分
	Tags() Tags
	AddTag(key, value string)
	SetTags(tags Tags)

    // Field 部分
	Fields() Fields

    // Timestamp 部分
	Time() time.Time
	SetTime(t time.Time)
	UnixNano() int64

    // Measurement + Tags
	Key() []byte

    // ...
}
```

Point 有四大块：

- Measurement：类似于表。
- Tag：起到索引的作用。标签可以有多个，每个标签是一个 `key,value` 映射。
- Field：字段，具体的值。
- Timestamp：时间点。

这四块中，Measurement 和 Tag 组成了 Series，类似于一个集合。由于 Series 没有 Timestamp 维度，因此一个 Series 底下有多个时间点的数据，也就意味着有多个 Point。

Series 的 key 由一个 measurement 名称、 多个 `tag_key=tag_value` 组成，例如 `series.Key = "cpu,host=A"`。

## influxDB 是怎么读取一行数据的？

- 从查询语句中解析出所有 field
- 找到这些 field 的类型对应的 iterator
- 根据查询语句对 field 的要求（例如聚合），用装饰模式创建对应的 iterator，包裹底层的 iterator。
- 由 Emitter 来调用 iterator 读取数据  
    - 遍历所有 iterator，读取每个字段的下一个数据，放到 buffer 里面。buffer 是一个数组，按照顺序存放每个 iterator 的结果。
    - 这次读取时的【时间、measurement、tags】会发生变化，作为 row 的 key。
    - 如果读取后在 buffer 里面找不到这个 key，则创建一个 row；如果存在，则加入这次读的数据。

集群在查询时，用了一层 remoteIteratorCreator，来读取远程 shard 的数据。

底层的 iterator 在 `tsdb/engine/tsm1/engine.go` 里面。

```go
// buildIntegerCursor creates a cursor for an integer field.
func (e *Engine) buildIntegerCursor(measurement, seriesKey, field string, opt influxql.IteratorOptions) integerCursor {
	cacheValues := e.Cache.Values(SeriesFieldKey(seriesKey, field))
	keyCursor := e.KeyCursor(SeriesFieldKey(seriesKey, field), opt.SeekTime(), opt.Ascending)
	return newIntegerCursor(opt.SeekTime(), opt.Ascending, cacheValues, keyCursor)
}
```

### Iterator 是如何工作的？

举一个 sum 的例子。

sum 是函数，在 `influxql/call_iterator.go` 里面由 `NewCallIterator` 创建 `integerReduceIntegerIterator` 或者 `floatReduceFloatIterator`。  

> 由于 InfluxDB 的数据类型只有四种：浮点数、整数、字符串和布尔值，所以仅需要支持浮点数和整数。

以 `integerReduceIntegerIterator` 为例。

对于要合并的数据，两者的 field_key 和 tags 是一致的，这样可以生成一个唯一 key。对于每个 key，生成一个对应的 `integerReduceIntegerPoint`。

`integerReduceIntegerPoint` 保存了一个 value，放在 prev 结构体里面。每次得到一个相同 key 的时候，获取 `integerReduceIntegerPoint`，并将当前值与 prev 的值相加，并保存到 prev 里面。在对上一个阶段的结果集做一遍这个合并后，得到一批 IntegerPoint，并从大到小排序。每次 Next() 从中取最后一个。

### 嵌套的 Iterator 是如何配合的？

假设有 IteratorB(IteratorA) 这样的嵌套。

每次 IteratorB 执行 Next() 的时候，会先执行一次 reduce()，目的是合并或过滤掉符合条件的相邻的数据。它会去找 IteratorA 获取一个时间段的所有数据，然后将这些数据转换为只剩下一条。

### 一行的数据是如何合并的？

【时间、measurement、tags】 每次读取的时候都有可能发生变化。这是因为每个字段虽然是按照时间顺序读取，但某一时刻，不一定所有的字段都有值，此时读取的是指定时刻之后的数据。

这样一个 buffer 中，各个字段的时间可能不一致。如果查询语句是按时间增序，则取时间最小的那个字段。以这个字段的 【时间、measurement、tags】 去 buffer 中找相匹配的 field。以此组合成 row。

字段的顺序怎么办？字段的顺序在一开始创建 iterator 集合的时候就固定了。每次读取的时候都是按照 iterator 的顺序读取。在组合 row 的时候，如果一个 iterator 的数据不能满足 【时间、measurement、tags】，则其对应的下标的值为 nil。

### 集群应该如何处理？

集群使用 remoteIteratorCreator，它会创建 ReaderIterator，从 `io.Reader` 里读取数据。这个 `io.Reader` 是一个 TCP 连接。

根据 select 指定的时间范围，找到时间范围内的所有 shard 及其所在的集群节点。然后对每个节点都建立一个连接。

## influxDB 是怎么存储数据的？

> 存储格式：  
> http://blog.fatedier.com/2016/08/05/detailed-in-influxdb-tsm-storage-engine-one

在启动后，会定期检查是否应该将缓存中的数据刷入到磁盘中。

数据文件是 tsm 类型。整个文件包含四个部分：

```
┌────────┬────────────────────────────────────┬─────────────┬──────────────┐
│ Header │               Blocks               │    Index    │    Footer    │
│5 bytes │              N bytes               │   N bytes   │   4 bytes    │
└────────┴────────────────────────────────────┴─────────────┴──────────────┘
```

Blocks 存储着实际数据。每个 Block 表示一批 series + field 相同且经过压缩后的数据。

```

┌────────┬────────────────────────────────────┬─────────────┬──────────────┐
│ Header │               Blocks               │    Index    │    Footer    │
│5 bytes │              N bytes               │   N bytes   │   4 bytes    │
└────────┴────────────────────────────────────┴─────────────┴──────────────┘
                            ↑ 取这个部分得到下图

┌───────────────────────────────────────────────────────────┐
│                          Blocks                           │
└───────────────────────────────────────────────────────────┘
                              ↓ 切割
┌───────────────────┬───────────────────┬───────────────────┐
│      Block 1      │      Block 2      │      Block N      │
└───────────────────┴───────────────────┴───────────────────┘
                              ↓ 切割
┌─────────┬─────────┬───────────────────┬─────────┬─────────┐
│  CRC    │  Data   │  CRC    │  Data   │  CRC    │  Data   │
│ 4 bytes │ N bytes │ 4 bytes │ N bytes │ 4 bytes │ N bytes │
└─────────┴─────────┴─────────┴─────────┴─────────┴─────────┘
```

在向 InfluxDB insert 多条数据的时候， InfluxDB 会将每条数据转换成一个 Point，并按照 Point 的 series + field 分组。

```go
func (e *Engine) WritePoints(points []models.Point, measurementFieldsToSave map[string]*tsdb.MeasurementFields, seriesToCreate []*tsdb.SeriesCreate) error {
    // ...
    key := string(p.Key()) + keyFieldSeparator + k
    values[key] = append(values[key], NewValue(p.Time().UnixNano(), v))
    // ...
}
```

> 这里的 `p` 是 point，`p.Key()` 是 measurement + series，`k` 是 field key。`values` 的类型是 `map[string][]Value`

每个分组的数据会分别加入到缓存里面。接着写一份到 WAL（Write Ahead Log，写日志） 文件里面，便于程序重启或崩溃后恢复内存数据。

> 缓存里面包括原先存储在磁盘上的数据，这些数据会和后续新增的数据合并并且排序。

然后对缓存中每个分组的数据执行压缩，压缩的结果是一个 Block。每个分组保存的是一个 Field 的数据，因此一个 Block 对应一个 Field。

```go
block, err := values.Encode(nil)
```

这里的 `values` 的类型是 `[]Value`，即上面的那个 values 取其中一个 field 的分组。说明每个 block 存储的是一个 field 的数据。

```
┌─────────┬─────────┐
│  CRC    │  Data   │
│ 4 bytes │ N bytes │
└─────────┴─────────┘
```

其中的 Data 部分有三个内容：

```
┌───────────────────┬───────────────────┬───────────────────┐
│  first timestamp  │   all timestamp   │     all value     │
└───────────────────┴───────────────────┴───────────────────┘
```

1. Data 部分第一个数据的时间戳
2. 所有数据的时间戳
3. 所有数据的值

这里的时间戳和它对应的值是分成两部分存储的。

接着计算这个 Block 的 CRC 校验码：

```go
func (t *tsmWriter) WriteBlock(key string, minTime, maxTime int64, block []byte) error {
    // ...
    var checksum [crc32.Size]byte
	binary.BigEndian.PutUint32(checksum[:], crc32.ChecksumIEEE(block))
    // ...
}
```

先写 CRC 校验码再写 Data。

写入 CRC 校验码之前会判断文件是否已经有内容，如果没有，则写入 Header。

```
    ↓ 这个部分
┌────────┬────────────────────────────────────┬─────────────┬──────────────┐
│ Header │               Blocks               │    Index    │    Footer    │
│5 bytes │              N bytes               │   N bytes   │   4 bytes    │
└────────┴────────────────────────────────────┴─────────────┴──────────────┘
```

之后把这个 Block 的 【key（即 series + field）、field 的数据类型、时间段、该 Block 在文件的偏移量、该 Block 的长度】 添加到内存中的索引。

```go
t.index.Add(key, blockType, values[0].UnixNano(), values[len(values)-1].UnixNano(), t.n, uint32(n))
```

写完所有 Block 之后，再把索引写入到文件。之后把原先的 tsm 文件删掉。

```
                                                     ↓ 索引是这个部分
┌────────┬────────────────────────────────────┬─────────────┬──────────────┐
│ Header │               Blocks               │    Index    │    Footer    │
│5 bytes │              N bytes               │   N bytes   │   4 bytes    │
└────────┴────────────────────────────────────┴─────────────┴──────────────┘
```


## 连续查询（Continues Query）

连续查询是由 InfluxDB 按照一定时间间隔执行查询，并将结果插入到指定表中。

连续查询分为基础语法和高级语法。它们的区别在于对查询时间范围和两次查询的间隔的配置。

首先是基础语法：

```
CREATE CONTINUOUS QUERY <cq_name> ON <database_name>
BEGIN
  SELECT <function[s]> INTO <destination_measurement> FROM <measurement> [WHERE <stuff>] GROUP BY time(<interval>)[,<tag_key[s]>]
END
```

基础语法的查询间隔为：`GROUP BY time()` 的 interval。即如果 interval 为 1m，则一分钟执行一次。

基础语法的查询时间范围为：执行查询的时间点 `now()` 减去 `GROUP BY time()` 的 interval。即 `WHERE time >= (now() - interval) AND time < now()`。

高级语法：

```
CREATE CONTINUOUS QUERY <cq_name> ON <database_name>
RESAMPLE EVERY <interval> FOR <interval>
BEGIN
  SELECT <function[s]> INTO <destination_measurement> FROM <measurement> [WHERE <stuff>] GROUP BY time(<interval>)[,<tag_key[s]>]
END
```

高级语法比基础语法多了一行：`RESAMPLE EVERY <interval> FOR <interval>`

其中 EVERY 确定查询间隔，FOR 确定查询时间范围。其中一个可以不填，例如：

`RESAMPLE EVERY <interval>` 或者 `RESAMPLE FOR <interval>`。

其中一个不填时，相当于自动把它的 interval 设置为 `GROUP BY time()` 的 interval。

当数据输入有延迟时，需要使用高级语法的 `FOR` 扩大查询范围。

例如聚合一分钟的数据需要延迟半分钟，那么将 `FOR` 设置为 2 分钟。这样就能在第三分钟开始的时候，查询第一和第二分钟的数据。由于第二分钟的数据需要再等半分钟才有，所以相当于是获取第一分钟的数据。

## 写入

https://docs.influxdata.com/influxdb/v1.8/guides/hardware_sizing/

单机写入的极限是每秒 75 万个字段。估算方法是一秒的 point 数量乘以一条数据的字段数量。point 数量可以从 `_internal` 库的 write 表的 pointReq 获取。字段数量可以执行 `show field keys` 获取。

在某些场景下，不是每一秒钟都有 75 万个字段，而是在每分钟内的某一秒会同时收到超过 75 万个字段的数据。这种情况要取这些数据在一分钟每秒的平均值。如果平均值不超过 75 万个字段，那么单机可以承受住。

也就是 InfluxDB 最多一分钟可以写 4500 万个字段，实际值可能会比这个小一些，可以通过业务数据测试实际负载。

## 写入的优化

https://docs.influxdata.com/influxdb/v2.0/write-data/best-practices/optimize-writes/

1. 使用 gzip 压缩
2. 批量写，最理想的是一次 5000 行
3. 转换为行的时候，按字典顺序排序 tag 的字段
4. 设置最合适的时间精度。例如同一个 tag 不会有两条同一秒的数据，那么就把时间精度设置为秒级

## Series File

https://www.jianshu.com/p/4e6fda6d6b63

