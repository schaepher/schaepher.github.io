---
title: nginx-multiple-domain
date: 2019-08-24 17:52:41
updated: 2019-08-24 17:52:41
tags:
---

问题：Laravel 的配置里面域名只能配置一个，但是现实要求多个域名能够访问。

因此使用 Nginx 做转发。

```nginx
server {
    listen 80;
    server_name another-api.mydomain.com;

    location / {
      proxy_read_timeout 600s;
      fastcgi_read_timeout 600s;
      proxy_set_header        Host api.mydomain.com;
      proxy_set_header        X-Real-IP $remote_addr;
      proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header        X-Forwarded-Proto $scheme;
      proxy_pass http://api.mydomain.com;
    }
}
```

注意 header 里面的 Host 要设置为代理的域名