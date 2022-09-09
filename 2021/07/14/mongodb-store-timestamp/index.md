# MongoDB存储时间点数据


## 比较通用的一种方式

```json
{
    "date" : "2020-11-05 00:00:00.000",
    "domain": "test.com",
    "data": {
        "00:00" : {
            "ts": 1604505600,
            "bandwidth": 111.222,
            "cost": 333.444
        },
        "00:01" : {
            "ts": 1604505660,
            "bandwidth": 555.666,
            "cost": 777.888
        }
    }
}
```

查询支持按五分钟合并：  

```js
db.oc_domain.aggregate([
    {
        "$match": {
            "domain": "test.com"
        }
    },
    {
        $project: {
            "domain": 1,
            "data": {
                $objectToArray: "$data"
            }
        }
    },
    {
        $unwind: "$data"
    },
    {
        $group: {
            "_id": {
                "domain": "$domain",
                "timestamp": {
                    "$subtract": [
                        "$data.v.time",
                        {
                            "$mod": [
                                "$data.v.time",
                                5 * 60
                            ]
                        }
                    ]
                }
            },
            "bandwidth": {
                $sum: "$data.v.bandwidth"
            }
        }
    },
    {
        $project: {
            "_id": 0,
            "timestamp": "$_id.timestamp",
            "domain": "$_id.domain",
            "bandwidth": "$bandwidth"
        }
    }
])
```

## 不需要直观地看某个时间点的数据

```json
{
    "date" : "2020-11-05 00:00:00.000",
    "domain": "test.com",
    "data": [
        {
            "ts": 1604505600,
            "bandwidth": 111.222,
            "cost": 333.444
        },
        {
            "ts": 1604505660,
            "bandwidth": 555.666,
            "cost": 777.888
        }
    ]
}
```


查询支持按五分钟合并：  

```js
db.oc_domain.aggregate([
    {
        "$match": {
            "domain": "test.com"
        }
    },
    {
        $unwind: "$data"
    },
    {
        $group: {
            "_id": {
                "domain": "$domain",
                "timestamp": {
                    "$subtract": [
                        "$time",
                        {
                            "$mod": [
                                "$time",
                                5 * 60
                            ]
                        }
                    ]
                }
            },
            "bandwidth": {
                $sum: "$bandwidth"
            }
        }
    },
    {
        $project: {
            "_id": 0,
            "timestamp": "$_id.timestamp",
            "domain": "$_id.domain",
            "bandwidth": "$bandwidth"
        }
    }
])
```

## 不使用时间戳

```json
{
    "date" : "2020-11-05 00:00:00.000",
    "domain": "test.com",
    "data": {
        "00:00" : {
            "time": "2020-11-05 00:00:00.000",
            "bandwidth": 111.222
        },
        "00:01" : {
            "time": "2020-11-05 00:01:00.000",
            "bandwidth": 333.444
        }
    }
}
```

查询支持按五分钟合并：  

```js
db.oc_domain.aggregate([
    {
        "$match": {
            "domain": "test.com"
        }
    },
    {
        $project: {
            "domain": 1,
            "data": {
                $objectToArray: "$data"
            }
        }
    },
    {
        $unwind: "$data"
    },
    {
        $group: {
            "_id": {
                "domain": "$domain",
                "date": {
                    "$subtract": [
                        {
                            "$subtract": ["$data.v.time", new Date("1970-01-01")]
                        },
                        {
                            "$mod": [
                                {
                                    "$subtract": ["$data.v.time", new Date("1970-01-01")]
                                },
                                5 * 60 * 1000
                            ]
                        }
                    ]
                }
            },
            "bandwidth": {
                $sum: "$data.v.bandwidth"
            }
        }
    },
    {
        $project: {
            "_id": 0,
            "date": {
                $toDate: "$_id.date"
            },
            "domain": "$_id.domain",
            "bandwidth": "$bandwidth"
        }
    }
])
```

如果不合并：

```js
db.oc_domain.aggregate([
    {
        "$match": {
            "domain": "v29-dy.ixigua.com"
        }
    },
    {
        $project: {
            "domain": 1,
            "data": {
                $objectToArray: "$data"
            }
        }
    },
    {
        $unwind: "$data"
    },
    {
        $group: {
            "_id": {
                "domain": "$domain",
                "date": "$data.v.time"
            },
            "bandwidth": {
                $sum: "$data.v.bandwidth"
            }
        }
    },
    {
        $project: {
            "_id": 0,
            "date": "$_id.date",
            "domain": "$_id.domain",
            "bandwidth": "$bandwidth"
        }
    }
])
```

## 完全不需要合并的结构

```json
{
    "date" : "2020-11-05 00:00:00.000",
    "domain": "test.com",
    "bandwidth": {
        "00:00" : 111.222,
        "00:05" : 333.444
    }
}
```

```js
{
    $project: {
        "datetime": {
            "$dateFromString": {
                dateString: {
                    "$dateToString": {
                        "date": "$date",
                        "format": "%Y-%m-%dT%H:%M:%S"
                    }
                },
                format: "%Y-%m-%dT%H:%M:%S",
                timezone: {
                    $concat: ["-", "$data.k"]
                }
            }
        }
    }
}
```
