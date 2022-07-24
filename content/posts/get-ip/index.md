---
title: 获取可连接到某个域名的 IP
date: 2019-10-17 12:04:23
updated: 2019-10-17 12:04:23
categories:
 - Scripts
tags:
 - Scripts
 - hosts
 - nc
---


```sh
#!/bin/sh

function get_ip() {
    host=$1
    ip=$(nc -vz $host 443 2>&1 | grep "Connect" | awk -F ' ' '{print $4}' | awk -F ':' '{print $1}')
    echo $ip $host
}

get_ip registry-1.docker.io
```
