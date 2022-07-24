---
title: 编译和调试 PHP
date: 2020-04-01 21:00:00
updated: 2020-04-01 21:00:00
tags: 
- PHP
---

## 编译

基本上按照官方的来就行了：

[https://github.com/Microsoft/php-sdk-binary-tools](https://github.com/Microsoft/php-sdk-binary-tools)

<!-- more -->

```bash
git clone https://github.com/Microsoft/php-sdk-binary-tools.git c:\php-sdk
cd c:\php-sdk
git checkout php-sdk-2.2.0
./phpsdk-vc15-x64.bat
phpsdk_buildtree phpmaster
git clone https://github.com/php/php-src.git && cd php-src
phpsdk_deps --update --branch 7.4
buildconf && configure --enable-cli && nmake
```

注意 `phpsdk_deps --update --branch 7.4` 这一个命令。官方例子是 master，但我执行的时候会报：  

```
Fatal error: Uncaught SDK\Exception: Unsupported branch 'master'
```

在工具里面 var_dump 查看支持的分支后发现没有 master，于是选 7.4 。

同样还是这一个命令。由于网络原因，可能会有些 zip 包下载下来后无法解压。

```
Fatal error: Uncaught SDK\Exception: Failed to open 'C:\php-sdk\.tmp\c2bc78629d0b6f3212ff42957cc6fb2a\packs\freetype-2.9.1-1-vc15-x64.zip'. in C:\php-sdk\lib\php\libsdk\SDK\FileOps.php:172
```

我尝试用下载软件下载，下载下来的文件可以正常解压。让工具直接读这个手动下载的文件就行了。

由于工具每次运行的时候，都会生成临时目录，因此把它改成固定的目录。

`php-sdk\lib\php\libsdk\SDK\FileOps.php`   

```php
protected function md(string $name = "", bool $tmp = false) : string
{
    // ...
    				$ret = $pre . DIRECTORY_SEPARATOR . md5(uniqid());
    // ...
}
```

把 `md5(uniqid())` 改成字符串 `"tmp"`。

`php-sdk\lib\php\libsdk\SDK\Build\Dependency\Package.php`

```php
public function retrieve(string $path) : void
{/*{{{*/
    $this->filepath = $path . DIRECTORY_SEPARATOR . $this->name;

    $cont = $this->fetcher->getByUri($this->getUri());

    $fd = fopen($this->filepath, "wb");
    fwrite($fd, $cont);
    fclose($fd);
}/*}}}*/
```

在 getByUri 上一行加入：  

```php
if (file_exists($this->filepath))
{
    return;
}
```

然后把删除文件的代码注释掉：

`php-sdk\lib\php\libsdk\SDK\Build\Dependency\Package.php`

```php
public function cleanup() : void
{/*{{{*/
    // unlink($this->filepath);		
}/*}}}*/
```

然后手动下载压缩包。先获取 URL 。

`php-sdk\lib\php\libsdk\SDK\Build\Dependency\Manager.php`

```php
public function performUpdate(string &$msg = NULL, bool $force = false, bool $backup = true) : void
{
    // ...
		foreach ($series_data as $item) {
			echo "Processing package $item", PHP_EOL;
			$pkg = new Package($item, $this->series, $this->fetcher);

			$pkg->retrieve($tmp_dir_packs);
			$pkg->unpack($tmp_dir_deps);
			$pkg->cleanup();

			unset($pkg);
		}
    // ...
}
```

把循环体的内容改为：  

```php
echo 'https://windows.php.net/downloads/php-sdk/deps/vc15/x64/'  . $item . PHP_EOL;
```

> 这里的 vc15 和 x64 根据情况替换。后面文件名会在执行 `phpsdk_deps --update --branch 7.4` 的时候展示出来。哪个失败就手动下载哪个。

在 foreach 下面加个 `die();` 。

执行一次命令获取所有 URL。然后批量复制到下载软件里面下载。

把压缩包放到 `php-sdk\.tmp\tmp\packs` 底下，再次执行 `phpsdk_deps --update --branch 7.4`。

成功的提示：  

```
Updates performed successfully.
```

接下来执行：  

```
buildconf.bat
```

成功的提示：  

```
Rebuilding configure.js
Now run 'configure --help'
```

接着执行：  

```
configure --disable-all --enable-cli --enable-debug
```

成功的提示：  

```
---------------------------------------
|                   |                 |
---------------------------------------
| Build type        | Debug           |
| Thread Safety     | Yes             |
| Compiler          | Visual C++ 2019 |
| Architecture      | x64             |
| Optimization      | disabled        |
| Native intrinsics | SSE2            |
| Static analyzer   | disabled        |
---------------------------------------

Type 'nmake' to build PHP
```

接着执行：

```
nmake
```

成功的提示：  

```
SAPI sapi\cli build complete
```

编译后的文件在 `php-sdk\phpmaster\vc15\x64\php-src\x64\Debug_TS` 。

进入目录执行：

```
php -v
```

## 调试






