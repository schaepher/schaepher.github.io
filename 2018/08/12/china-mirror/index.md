# 一些国内镜像源设置


## NPM

`npm config set registry https://registry.npm.taobao.org`

换回来：  

`npm config set registry https://registry.npmjs.org`

如果只想生效一次：

`npm --registry=https://registry.npm.taobao.org install xxxxx`

## Docker

编辑文件： `C:\Users\chensf1\.docker\daemon.json`

在 `registry-mirrors` 里添加 `https://registry.docker-cn.com`，如下：  

```
{"registry-mirrors":["https://registry.docker-cn.com"],"insecure-registries":[], "debug":true, "experimental": false}
```

## alpine

`sed -i 's/http:\/\/dl-cdn.alpinelinux.org/https:\/\/mirror.tuna.tsinghua.edu.cn/' /etc/apk/repositories`

