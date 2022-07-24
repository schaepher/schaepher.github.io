# 用 CURL 命令分析请求时间



https://stackoverflow.com/questions/18215389/how-do-i-measure-request-and-response-times-at-once-using-curl

curl-format.txt

```
          域名解析结束时间:  %{time_namelookup}\n
  与远程主机建立连接完成时间:  %{time_connect}\n
      SSL/SSH握手结束时间:  %{time_appconnect}\n
          数据发送开始时间:  %{time_pretransfer}\n
发送结束前所有重定向所需时间:  %{time_redirect}\n
  接收返回的第一个字节的时间:  %{time_starttransfer}\n
                            ----------\n
                    总耗时:  %{time_total}\n
```

`curl -w "@curl-format.txt" -o /dev/null -s "https://www.baidu.com"`
