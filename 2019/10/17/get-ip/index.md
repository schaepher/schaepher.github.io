# 获取可连接到某个域名的 IP



```sh
#!/bin/sh

function get_ip() {
    host=$1
    ip=$(nc -vz $host 443 2>&1 | grep "Connect" | awk -F ' ' '{print $4}' | awk -F ':' '{print $1}')
    echo $ip $host
}

get_ip registry-1.docker.io
```

