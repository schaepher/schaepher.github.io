# 轻量对象存储服务——minio


# minio

Minio是一个非常轻量的对象存储服务。

Github： [minio](https://github.com/minio/minio/blob/master/README_zh_CN.md)

它本身不支持文件的版本管理。如果有这个需求，可以用 s3git 搭配使用。

Github： [s3git](https://github.com/s3git/s3git)

## 安装

minio 文档有列出各平台的安装方式。这里只说 docker 的方式。

docker-compose.yml

```
version: "3"

services:
  minio:
    image: minio/minio
    volumes:
      - minio-data:/data
    ports:
      - "9080:9000"
    environment:
      MINIO_ACCESS_KEY: minio
      MINIO_SECRET_KEY: minio123
    command: server /data

volumes:
  minio-data:
```

将上面内容保存为 docker-compose.yml 文件。然后在这个文件所在的文件夹内执行 `docker-compose up -d`。minio 服务就启动了。

## minio 界面

服务启动后，访问 http://127.0.0.1:9080 进入登录界面：  

![](https://img2018.cnblogs.com/blog/809218/201903/809218-20190305220912631-56248210.png)

输入上面设置的 access key：minio 和 secret key：minio123，登录。

![](https://img2018.cnblogs.com/blog/809218/201903/809218-20190305221158232-74858637.png)

图中 1 是上传一个文件；图中 2 是创建一个 bucket （储存区）。  

文件必须上传到某一个存储区里面，因此必须先创建一个 bucket。

文件上传后，一旦选择文件，就会在顶部出现删除和下载的操作按钮。

# 在 Laravel 里使用

## 配置

1. 引入包  
    `composer require league/flysystem-aws-s3-v3`
1. 修改 config/filesystems.php   

    ```
    ...
    'cloud' => env('FILESYSTEM_CLOUD', 'minio'),
    ...
    'disks' => [
        ...
        'minio' => [
            'driver' => 's3',
            'endpoint' => env('MINIO_ENDPOINT'),
            'use_path_style_endpoint' => true,
            'key' => env('MINIO_ACCESS_KEY_ID'),
            'secret' => env('MINIO_SECRET_ACCESS_KEY'),
            'region' => env('MINIO_DEFAULT_REGION'),
            'bucket' => env('MINIO_BUCKET'),
        ],
        ...
    ]
    ```

1. 修改 .env  

    ```
    FILESYSTEM_CLOUD=minio
    MINIO_ENDPOINT="http://127.0.0.1:9080"
    MINIO_ACCESS_KEY_ID=minio
    MINIO_SECRET_ACCESS_KEY=minio123
    MINIO_DEFAULT_REGION=cn-north-1
    MINIO_BUCKET=刚创建的bucket名称
    ```

## 尝试

1. 打开 tinker  
    `php artisan tinker`
1. 存储  
    `Storage::cloud()->put('hello.json', '{"hello": "world"}');`    
    结果：true
1. 取出  
    `Storage::cloud()->get('hello.json');`  
    结果：{"hello": "world"}
