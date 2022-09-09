# logstash


### 多个 Filebeat 源

根据文件名区分

### 多个源的解决方案

加一层 MQ，通过 MQ 不同的队列来获取


### 多个配置文件

https://stackoverflow.com/questions/27146032/make-logstash-add-different-inputs-to-different-indices

Logstash 的事件会被分发到 pipeline 所有配置文件里的 input  

要区分多个的时候，要在 input 里面设置 type ，并通过条件语句区分。

```
input {
  udp {
    ...
    type => "foo"
  }
  file {
    ...
    type => "bar"
  }
}

output {
  if [type] == "foo" {
    elasticsearch {
      ...
      index => "foo-index"
    }
  } else {
    elasticsearch {
      ...
      index => "bar-index"
    }
  }
}
```

### 解析 HTML

https://stackoverflow.com/questions/1600526/how-do-i-encode-decode-html-entities-in-ruby

https://stackoverflow.com/questions/51412579/logstash-not-producing-output-although-pipeline-main-starts

### 错误

https://discuss.elastic.co/t/invalid-frame-type-received-69-84/130234

https://stackoverflow.com/questions/50693683/filebeat-to-logstash-invalidframeprotocolexception



