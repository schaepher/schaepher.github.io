# Camunda 流程图配置


## 结果
收到结果后，有三种方式设置结果变量到变量仓库。

1. Input/Output 每个变量一个 Output
2. Input/Output 一个变量内同时设置多个变量
3. Listener 里面设置 end 类型，并同时设置多个变量

Response 是 Json，用 JavaScript 处理。

### Input/Output 每个变量一个 Output

Script 内容为：

```
S(response).prop('字段名').boolValue()
```

### Input/Output 一个变量内同时设置多个变量

Script 内容为：

```
resp = S(response)
var1 = resp.prop('字段名').boolValue()
execution.setVariable('字段名', var1)
```

### Listener 里面设置 end 类型，并同时设置多个变量

Script 内容为：

```
resp = S(response)
var1 = resp.prop('字段名').boolValue()
execution.setVariable('字段名', var1)
```
