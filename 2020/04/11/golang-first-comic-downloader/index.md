# 第一个 Go 语言程序：漫画下载器


原文地址：  

> 第一个 Go 语言程序：漫画下载器：    
> [https://schaepher.github.io/2020/04/11/golang-first-comic-downloader](https://schaepher.github.io/2020/04/11/golang-first-comic-downloader)

之前学了点 Go 语言，但没有写出一个比较有用的工具，基本上算白学。得选一个又简单又比较有有价值的功能来实现。

之前用 PHP + Laravel 写的漫画下载器不好用，这刚好是一个简单又实用的功能，干脆用 Go 语言重新写一个。

所有代码在 GitHub 上：  

> [https://github.com/schaepher/comic-downloader-example](https://github.com/schaepher/comic-downloader-example)

实现的功能和获得对应的实践如下：  

<!-- more -->

1. hello world
    + 程序的结构
    + 包的引用
    + 编译和运行代码
    + 函数/方法的可见性
    + `fmt` 库输出字符串

2. 请求网页和写入文件
    + 变量定义和赋值
    + 字符串
    + if 语句
    + 无返回值的函数
    + `net/http` 库发起请求和接收响应
    + `io/ioutil` 库将网页内容写入文件

3. 漫画标题和下载 ID 的解析
    + 结构体的定义和初始化
    + 结构体的方法
    + 单返回值的函数
    + `fmt` 库格式化输出字符串
    + `regexp` 库正则表达式  
        * 除了用正则，还可以用 `goquery` 来解析 html，但这里不使用。

4. 代码整理，抽取函数
    + 多返回值的函数
    + 自定义错误信息
    + `strconv` 库将字符串转为整数

5. 代码整理，放到类里面
    + 方法内部修改结构体的值（引用）
    + 空白标识符

6. 获取漫画的所有文件名
    + 数组和切片的声明
    + 字符串转 byte 切片
    + `strings` 库替换字符串
    + `encoding/json` 库解析 Json
    + `fmt` 库打印结构体

7. 下载漫画
    + 字符串类型元素的切片的初始化
    + 字符串拼接
    + for range 循环
    + 普通的 for 循环
    + `os` 库获取当前所在工作目录的路径、判断文件或文件夹是否存在、创建文件夹
    + `strconv` 库将整数转为字符串

8. 并发下载漫画
    + Go协程（goroutines）和通道（channel）
    + 引用类型与 make()
    + 匿名函数（闭包）
    + defer
    + `sync` 库等待 goroutines 执行结束
    + 接口类型
    + 类型转换
    
9. 再次执行时避免下载已有页面
    + 判断一个字符串是否存在于字符串切片中
    + 往切片中添加元素
    + `io/ioutil` 库读取文件夹里的文件列表

10. 将配置抽取到配置文件
    + 获取程序所在的目录
    + `io/ioutil` 库读取文件内容

11. 没有全部下载成功时重试
    + 自定义错误类型

> 注，编译和执行环境都是 Windows 10

一开始尝试对每份代码做分析，写了一些后发现很费时间，所以还未写解析的部分主要列出相关资料，并作必要的补充。主要来源是 《The Way To Go》 的中文版：  

> [https://github.com/Unknwon/the-way-to-go_ZH_CN/blob/master/eBook/directory.md](https://github.com/Unknwon/the-way-to-go_ZH_CN/blob/master/eBook/directory.md)

注意，在运行代码前需要确保已安装 Go 环境。

## v1: hello world

先从最简单的开始。

创建项目 comic-downloader ，在目录里面创建 `main.go` 文件。  

以下代码在：  

> [https://github.com/schaepher/comic-downloader-example/blob/master/v01-hello-world/main.go](https://github.com/schaepher/comic-downloader-example/blob/master/v01-hello-world/main.go)

`main.go`

```go
package main

import "fmt"

func main() {
    fmt.Println("hello world")
}
```

需要说明的内容有两点：  

- Go 的代码不需要在代码行结束后加分号 `;` 。
- Go 语言通过函数/方法名的首字母大小写控制访问权限。大写首字母代表 public，小写首字母代表 private。

执行命令：  

```
go run main.go
```

输出：

```
hello world
```

`go run main.go` 会将代码编译为可执行文件，然后执行。

如果要分开，可以这样执行：  

```shell
go build -o main.exe main.go
./main.exe
```

## v2: 请求网页和写入文件

对于下载功能，我最关心的是如何发送 http 请求和如何读取结果。

以下代码在：  

> [https://github.com/schaepher/comic-downloader-example/blob/master/v02-http-get-write-file/main.go](https://github.com/schaepher/comic-downloader-example/blob/master/v02-http-get-write-file/main.go)

`main.go`

```go
package main

import (
    "fmt"
    "io/ioutil"
    "net/http"
)

func check(e error) {
    if e != nil {
        panic(e)
    }
}

func main() {
    var err error
    var url = "https://cn.bing.com"
    res, err := http.Get(url)
    check(err)
    data, err := ioutil.ReadAll(res.Body)
    check(err)

    ioErr := ioutil.WriteFile("cn.bing.com.html", data, 644)
    check(ioErr)

    fmt.Printf("Got:\n%q", string(data))
}
```

这里展示了变量声明和赋值的不同形式。

首先看 `var err error` ，这里用到的语法是 `var 变量名 变量类型`，因此这一句定义了一个类型为 `error` 的变量 `err` 。

> 4.4 变量：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.4.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.4.md)  
> 注意：  
> 当一个变量被声明之后，系统自动赋予它该类型的零值：int 为 0，float 为 0.0，bool 为 false，string 为空字符串，指针为 nil。记住，所有的内存在 Go 中都是经过初始化的。

Go 语言和 C 语言或者 JAVA 把变量类型放在前面的形式不同，Go 语言总是把类型放在后面。这点在下面的例子中都可以看到，无论是变量名、函数参数（例如上面的 check 函数）还是函数返回值，类型都放在后面。

对于有弱类型语言（例如 PHP）编程经验的人来说，这种顺序会舒服很多。因为写代码的时候不需要先想/查清楚返回值的类型再开始写，或者写完后面的函数调用再到前面补类型。

```go
res, err := http.Get(url)
```

这里涉及四个知识点：  

- 变量省略类型声明并赋值  
    > 4.4 变量：  
    > [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.4.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.4.md)  
- 发起一个 HTTP GET 请求  
    > 15.3 访问并读取页面：  
    > [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/15.3.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/15.3.md)
- 函数多个返回值，用逗号隔开  
    > 6.2 函数参数与返回值（第一部分）：
    > [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/06.2.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/06.2.md)
- Go 语言没有“异常”这一设计，通常给函数多加一个返回值表示错误    
    > Why does Go not have exceptions?  
    > [https://golang.org/doc/faq#exceptions](https://golang.org/doc/faq#exceptions)  
    > 13 错误处理与测试：
    > [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/13.0.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/13.0.md)  


下一行的 `check(err)` 用于检查是否有错误：

```go
func check(e error) {
    if e != nil {
        panic(e)
    }
}
```

涉及三个知识点：

- Go 的 if 判断不需要加括号。  
    > 5.1 if-else 结构：  
    > [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/05.1.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/05.1.md)
- 当一个指针被定义后没有分配到任何变量时，它的值为 nil。  
    注意，只有指针才能为 nil。假设有代码：  

    ```go
    var str string = nil
    ```

    编译时会报错：`cannot use nil as type string in assignment`  

    > 4.9 指针：
    > [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.9.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.9.md)
- `panic()` 用于终止程序  
    > 13.2 运行时异常和 panic：
    > [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/13.2.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/13.2.md)

回到主函数，再往下是读取结果：

```go
data, err := ioutil.ReadAll(res.Body)
```

然后是将结果写到文件里面：

```go
ioErr := ioutil.WriteFile("cn.bing.com.html", data, 644)
```

> 12.2 文件读写  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/12.2.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/12.2.md)

```go
fmt.Printf("Got:\n%q", string(data))
```

这里 `string(data)` 将 data 转换为字符串。  

> 7.6.4 修改字符串中的某个字符：   
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/07.6.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/07.6.md)

## v3: 解析标题和下载 ID

这个漫画下载网站漫画的 ID 和下载时 URL 的 ID 不一致，所以要将这个 ID 提取出来。  

以下代码在：

> [https://github.com/schaepher/comic-downloader-example/blob/master/v03-regex-struct-method/main.go](https://github.com/schaepher/comic-downloader-example/blob/master/v03-regex-struct-method/main.go)

`main.go`

```go
package main

import (
    "fmt"
    "io/ioutil"
    "net/http"
    "regexp"
)

func check(e error) {
    if e != nil {
        panic(e)
    }
}

type ComicSite struct {
    MainPageUrl string
}

func (cs ComicSite) GetComicMainPageUrl(comicId int) string {
    return fmt.Sprintf("%s/cn/s/%d/", cs.MainPageUrl, comicId)
}

func main() {
    comicSite := ComicSite{
        MainPageUrl: "https://*****",
    }

    // 获取漫画页
    comicMainPageUrl := comicSite.GetComicMainPageUrl(282526)
    res, err := http.Get(comicMainPageUrl)
    check(err)
    data, err := ioutil.ReadAll(res.Body)
    check(err)
    html := string(data)

    // 匹配标题
    titleR, err := regexp.Compile(`<title>(.+?)</title>`)
    check(err)
    titleMatches := titleR.FindStringSubmatch(html)
    if titleMatches == nil {
        panic("comic title not found")
    }
    title := titleMatches[1]
    fmt.Println(title)

    // 匹配下载 ID
    downloadR, err := regexp.Compile(`cn/(\d+)/1.(jpg|png)`)
    check(err)
    downloadMatches := downloadR.FindStringSubmatch(html)
    if downloadMatches == nil {
        panic("download id not found")
    }
    downloadIdStr := downloadMatches[1]
    fmt.Println(downloadIdStr)
}
```

这里引入了结构体。  

```go
type ComicSite struct {
    MainPageUrl string
}
```

初始化和赋值：  

```go
comicSite := ComicSite{
    MainPageUrl: "https://*****",
}
```

> 10 结构（struct）与方法（method）：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/10.0.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/10.0.md)  
> 10.1 结构体定义：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/10.1.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/10.1.md)  
> 10.6 方法：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/10.6.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/10.6.md)

结构体的方法：  

```go
func (cs ComicSite) GetComicMainPageUrl(comicId int) string {
    return fmt.Sprintf("%s/cn/s/%d/", cs.MainPageUrl, comicId)
}
```

注意与函数做比较：  

```go
func GetComicMainPageUrl(comicId int, mainPageUrl string) string {
    return fmt.Sprintf("%s/cn/s/%d/", mainPageUrl, comicId)
}
```

func 后面多了个 `(cs ComicSite)` 。在 Go 语言中，将其称为接收者（receiver）。由于 Go 里面没有 this 关键字，所以这里也可以写成：

```go
func (this ComicSite) GetComicMainPageUrl(comicId int) string {
    return fmt.Sprintf("%s/cn/s/%d/", this.MainPageUrl, comicId)
}
```

熟悉的味道。

再看看客户端的调用：  

```go
comicSite := ComicSite{
    MainPageUrl: "https://*****",
}
comicSite.GetComicMainPageUrl(282526)
```

正则库的使用：  

```go
titleR, err := regexp.Compile(`<title>(.+?)</title>`)
check(err)
titleMatches := titleR.FindStringSubmatch(html)
if titleMatches == nil {
    panic("comic title not found")
}
title := titleMatches[1]
```

这里在编译正则表达式的时候，用到了反引号，表示这是一个非解释字符串。

> 4.6 字符串：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.6.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.6.md)
> 9.2 regexp 包：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/09.2.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/09.2.md)  
> 正则表达式30分钟入门教程：  
> [https://deerchao.cn/tutorials/regex/regex.htm](https://deerchao.cn/tutorials/regex/regex.htm)

由于只需要获取 `()` 里的内容，因此用 FindStringSubmatch。  

假设 html 的值是 `aaa<title>标题</title>bbb` ，则 titleMatches 的值为：  

```json
[
  "<title>标题</title>",
  "标题"
]
```

## v4-5: 代码整理

分为两部分。

代码整理的第一部分是把匹配的代码放到函数里面。

以下代码在：

> [https://github.com/schaepher/comic-downloader-example/blob/master/v04-function-error/main.go](https://github.com/schaepher/comic-downloader-example/blob/master/v04-function-error/main.go)

`main.go` 部分代码：

```go
func getDownloadId(html string) (int, error) {
    downloadR, err := regexp.Compile(`cn/(\d+)/1.(jpg|png)`)
    if err != nil {
        return 0, err
    }

    downloadMatches := downloadR.FindStringSubmatch(html)
    if downloadMatches == nil {
        err := errors.New("download id not found")
        return 0, err
    }

    downloadId, err := strconv.Atoi(downloadMatches[1])
    if err != nil {
        return 0, err
    }

    return downloadId, nil
}
```

说明三个点：  

- 自定义错误信息内容  

    ```go
    err := errors.New("download id not found")
    ```

    > 13.1 错误处理：
    > [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/13.1.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/13.1.md)
- 函数多返回值  
    > 6.2 函数参数与返回值：
    > [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/06.2.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/06.2.md)
- 字符串转整数  
    > 4.7.12 字符串与其它类型的转换  
    > [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.7.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.7.md)

代码整理的第二部分是把函数转为结构体的方法。  

以下代码在：

> [https://github.com/schaepher/comic-downloader-example/blob/master/v05-reference-param/main.go](https://github.com/schaepher/comic-downloader-example/blob/master/v05-reference-param/main.go)

`main.go` 部分代码：  

```go
type Comic struct {
    Id         int
    Title      string
    DownloadId int
    ComicSite  ComicSite
}

func (comic *Comic) LoadMeta() error {
    var err error
    var mainPageHtml string

    comicMainPageUrl := comic.ComicSite.GetComicMainPageUrl(comic.Id)
    mainPageHtml, err = comic.getComicMainPageHtml(comicMainPageUrl)
    if err != nil {
        return err
    }

    comic.Title, err = comic.findTitle(mainPageHtml)
    if err != nil {
        return err
    }

    comic.DownloadId, err = comic.findDownloadId(mainPageHtml)
    if err != nil {
        return err
    }

    return nil
}

func (_ Comic) findTitle(html string) (string, error) {
    titleR, err := regexp.Compile(`<title>(.+?)</title>`)
    if err != nil {
        return "", err
    }

    titleMatches := titleR.FindStringSubmatch(html)
    if titleMatches == nil {
        err := errors.New("comic title not found")
        return "", err
    }
    title := titleMatches[1]

    return title, nil
}
```

对比以下两段代码：

```go
func (_ Comic) findTitle(html string) (string, error) {
    // ...
}
```

```go
func (cs ComicSite) GetComicMainPageUrl(comicId int) string {
    // ...
}
```

有个不同的地方是这里结构体变量设置为空白标识 `_`。因为 findTitle 这个函数不需要用到 Comic 这个结构体的内容。

再对比：  

```go
func (comic *Comic) LoadMeta() error {
    // ...
    comic.Title, err = comic.findTitle(mainPageHtml)
    // ...
}
```

多了个 `*` ，表示 comic 是一个 Comic 类型的指针，对其内容的修改会影响到外部的变量。  

另外无论是值类型还是指针，其调用方式都是 `obj.method(...)` ，Go 会自动识别。

> 10.6.3 指针或值作为接收者：   
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/10.6.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/10.6.md)

## v6: 获取漫画的所有文件名

接下来要准备下载了。不过在此之前要先获取下载链接。

漫画主页提供的预览图是缩小版的图片，因此不能直接使用。  

漫画主页还提供了页面总数。虽然文件名是按照数字顺序的，但是文件扩展名可能是 jpg 或者 png 或者其他的。  

通过观察，我发现在点击下载的时候，会去请求一个 js 文件。内容格式如下：  

```js
var galleryinfo = [{"lan": "cn","name": "1.jpg"},]
```

把后面的数组匹配出来然后做 json 解码就行了。正好还能学习 `encoding/json` 库和 `strings` 库。

以下代码在：

> [https://github.com/schaepher/comic-downloader-example/blob/master/v06-decode-json-replace-string/main.go](https://github.com/schaepher/comic-downloader-example/blob/master/v06-decode-json-replace-string/main.go)

`main.go` 部分代码：

```go
type ComicFile struct {
    Name string `json:"name"`
}

type Comic struct {
    Id         int
    Title      string
    DownloadId int
    ComicSite  ComicSite
    ComicFiles []ComicFile
}

func (comic *Comic) LoadMeta() error {
    // ...
    comicIndexUrl := comic.ComicSite.GetComicIndexUrl(comic.Id)
    comic.ComicFiles, err = comic.readComicIndexes(comicIndexUrl)
    // ...
}

func (_ Comic) readComicIndexes(comicIndexUrl string) ([]ComicFile, error) {
    res, err := http.Get(comicIndexUrl)
    if err != nil {
        return nil, err
    }
    htmlByte, err := ioutil.ReadAll(res.Body)
    if err != nil {
        return nil, err
    }

    html := string(htmlByte)

    r, err := regexp.Compile("\\[.+]")
    if err != nil {
        return nil, err
    }
    jsonStr := r.FindString(html)
    validJson := strings.Replace(jsonStr, ",]", "]", 1)

    var pages []ComicFile
    err = json.Unmarshal([]byte(validJson), &pages)
    if err != nil {
        return nil, err
    }

    return pages, nil
}
```

说明三个点：

第一：切片的声明  

```go
var pages []ComicFile
```

> 7.2 切片：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/07.2.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/07.2.md)

数组的声明呢？  

```go
var pages [100]ComicFile
```

二维数组呢？

```go
var pages [X][Y]ComicFile
// pages[x][y]
```

把 `[Y]ComicFile` 当成 `COMICFILE` 的话，上述声明就变成了：  

```go
var pages [X]COMICFILE
```

第二：字符串的替换  

```go
validJson := strings.Replace(jsonStr, ",]", "]", 1)
```

1 表示替换一次。

> 4.7.4 字符串替换：
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.7.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.7.md)

第三：Json 解码： 

```go
var pages []ComicFile
err = json.Unmarshal([]byte(validJson), &pages)
```

> 12.9 JSON 数据格式：
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/12.9.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/12.9.md)

由于 Unmarshal 第一个参数指定为 byte 类型的切片，所以要先做一次转换。

第二个参数是传指针， Unmarshal 直接在函数里面修改这个变量。

还可以：  

```go
pages := new([]ComicFile)
err = json.Unmarshal([]byte(validJson), pages)
```

因为 new() 得到的是结构体的指针。  

> 10.2.2 map 和 struct vs new() 和 make()：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/10.2.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/10.2.md)

看一下 json 串和结构体：  

```json
[{"lan": "cn","name": "1.jpg"}]
```

```go
type ComicFile struct {
    Name string `json:"name"`
}
```

ComicFile 这个结构体只定义了一个字段，而且由于字段名称与 json 串里面的大小写不一样，所以后面加一个补充说明 `json:"name"` 。  

解码的时候只会把 name 的值放到 Name 里面，并且忽略掉 lan 。

如果 json 字段本身就是大写，则不需要加后面的补充。

要确保结构体的字段以大写字母开头，否则 Json 解析后该字段为空。

## v7: 下载漫画

终于要下载漫画了。

以下代码在：  

> [https://github.com/schaepher/comic-downloader-example/blob/master/v07-encode-json-log-create-dir-for-range/main.go](https://github.com/schaepher/comic-downloader-example/blob/master/v07-encode-json-log-create-dir-for-range/main.go)

`main.go` 部分代码：

```go
func (comic Comic) GetDirPath() string {
    pwd, _ := os.Getwd()

    return pwd + "/comics/" + strconv.Itoa(comic.Id)
}

func createDirIfNotExist(dir string) error {
    if _, err := os.Stat(dir); os.IsNotExist(err) {
        err = os.MkdirAll(dir, 0755)
        if err != nil {
            return err
        }
    }

    return nil
}

func download(comic Comic) error {
    log.Printf("Downloading: %s\n", comic.Title)

    err := createDirIfNotExist(comic.GetDirPath())
    if err != nil {
        return err
    }

    data, err := json.Marshal(comic)
    if err != nil {
        return err
    }
    err = ioutil.WriteFile(comic.GetMetaFilePath(), data, 0644)
    if err != nil {
        return err
    }
    log.Printf("Meta file saved: %s\n", comic.GetMetaFilePath())

    for _, comicFile := range comic.ComicFiles {
        log.Printf("Start downloading: %s\n", comicFile.Name)

        for i := 0; i < len(comic.ComicSite.DownloadSourceUrls); i++ {
            downloadUrl, err := comic.ComicSite.GetComicDownloadUrl(comic.DownloadId, comicFile.Name, i)
            if err != nil {
                break
            }

            log.Printf("Trying: %s\n", downloadUrl)
            resp, err := http.Get(downloadUrl)
            if err != nil || resp.StatusCode != 200 {
                log.Printf("Failed: %s\n", downloadUrl)
                continue
            }
            data, err := ioutil.ReadAll(resp.Body)

            err = ioutil.WriteFile(comic.GetFilePath(comicFile.Name), data, 0644)
            if err != nil {
                return err
            }

            log.Printf("Saved : %s\n", comic.GetFilePath(comicFile.Name))
        }
    }

    return nil
}

func main() {
    comicSite := ComicSite{
        MainPageUrl: "https://******",
        DownloadSourceUrls: []string{
            "https://******/img/cn",
        },
    }

    comic := &Comic{ComicSite: comicSite, Id: 282526}
    err := comic.LoadMeta()
    check(err)

    err = download(*comic)
    check(err)
}
```

该漫画网站有两种域名用于获取漫画图片：  

- 在线阅读时请求的域名
- 下载时请求的域名

有时候在线阅读请求不到图片，但用于下载的域名可以获取到。有时候反之。所以当下载出错时，要换另一个域名试试。

先看 `download` 函数。

在下载前，要先创建文件夹。首先获取文件夹路径：

```go
func (comic Comic) GetDirPath() string {
    pwd, _ := os.Getwd()

    return pwd + "/comics/" + strconv.Itoa(comic.Id)
}
```

这里获取的是当前的工作目录，不是程序文件所在的目录。获取程序文件所在的目录会在后面给出例子。

整数转字符串：

> 4.7.12 字符串与其它类型的转换  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.7.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.7.md)

字符串拼接：  

```go
pwd + "/comics/"
```

如果要在循环中拼接字符串（例如将数组每个元素用逗号拼接起来），用 `+` 号拼接不是高效的做法。

```go
var strB strings.Builder
strB.WriteString("abc")
strB.WriteString("def")
fmt.Println(strB.String()) // abcdef
```

在 《The Way To Go》 里面还会看到用 `bytes.Buffer` 。区别在于 Go 1.10 才引入的 `strings.Builder` 效率更高。

接下来创建文件夹的 createDirIfNotExist 就不做说明了。

接着是把漫画的基本信息保存到文件里面。

前面介绍过 Json 字符串解码，现在要把结构体编码成字符串：

```go
data, err := json.Marshal(comic)
```

写完基本信息，接下来就是下载漫画图片了。  

下面用了嵌套循环，展示了 for 的两种不同写法。  

首先是遍历漫画所有文件用的 for range：

```go
for _, comicFile := range comic.ComicFiles {
    // ...
}
```

和 PHP 的 foreach 很相似。

这里会返回 index 和 value。 index 被我用 `_` 忽略掉了。

接着是遍历不同的下载域名链接：  

```go
for i := 0; i < len(comic.ComicSite.DownloadSourceUrls); i++ {
    // ...
}
```

> 注：该网站在某个在线阅读方式中用到了 CDN， 图片下载速度快很多。这个 CDN 用的是 HTTP/2 。由于 Go 的 http 库默认开启 HTTP/2 ，所以无需修改代码。  
> Starting with Go 1.6, the http package has transparent support for the HTTP/2 protocol when using HTTPS.  
> [https://golang.org/pkg/net/http/](https://golang.org/pkg/net/http/)

## v8: 并发下载漫画

上面下载的时候，用 for 循环一张张下载，必须得等一张下载结束才能继续。这样效率太低，要下载半天。  

那么就要想办法并发下载。

但是要注意控制并发的数量。如果不做控制，有的漫画两百多页一下子两百多个并发请求，对源站不友好。

并发的代码一开始是参考下面链接中的方案二：  

> 来，控制一下 Goroutine 的并发数量：  
> [https://segmentfault.com/a/1190000017956396](https://segmentfault.com/a/1190000017956396)  
> 这篇写得很好，感谢！

但是我当时没理解过来，写下了有问题的代码。下面我先解析我改正后的代码， 解析完再说说之前我哪里理解错了，以及基于错误理解写的代码。

#### 并发示例

用一个简单的例子来理解这部分内容，然后再将其改造成一个并发库。

上正确版的代码：  

> [https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v1-fix/thread.go](https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v1-fix/thread.go)

`thread.go`

```go
package main

import (
    "log"
    "math/rand"
    "sync"
    "time"
)

var wg sync.WaitGroup

func main() {
    maxTask := 10

    maxThread := 3
    ch := make(chan int, maxThread)
    for i := 0; i < maxThread; i++ {
        threadId := i
        go func() {
            wg.Add(1)
            defer wg.Done()

            log.Printf("Worker [%d] started at %d\n", threadId, time.Now().Unix())

            for taskId := range ch {
                seconds := 1 + rand.Intn(9)
                log.Printf("Task [%d] will sleep %d seconds\n", taskId, seconds)
                time.Sleep(time.Second * time.Duration(seconds))
                log.Printf("Task [%d] finished", taskId)
            }

            log.Printf("Worker [%d] finished at %d\n", threadId, time.Now().Unix())
        }()
    }

    for i := 0; i < maxTask; i++ {
        ch <- i
    }

    close(ch)
    wg.Wait()
}
```

> 14.1 并发、并行和协程（前两部分）  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/14.1.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/14.1.md)   
> 14.2 协程间的信道   
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/14.2.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/14.2.md)  

大致知道五点：  

- `go` 关键字执行函数或方法时，会创建协程。  
- 通道（Channel）是一个先进先出的队列。多个协程可使用同一个通道。通道里的一个数据只会被其中一个协程访问到。
- 当通道满时，发送者无法再发送数据，只能阻塞并等待接收者消费通道的数据。如果通道已经空了，则接收者无法消费，只能阻塞并等待发送者发送数据。
- 通道默认无缓冲，即只能一发一收。可以创建带缓冲的通道，这样可以同时发送多个和接收多个。  
- close() 使得通道无法再接收数据，但剩下的数据可以被消费。用 for-range 消费时会自动检测通道是否关闭且无剩余数据。

回到代码中。

```go
maxThread := 3
ch := make(chan int, maxThread)
```

这里创建了带缓冲的通道，允许通道里存放三个数据。接着启动与通道数量对应的协程：  

```go
for i := 0; i < maxThread; i++ {
        threadId := i
        go func() {
            // ...
        }()
    }
```

> 6.8 闭包：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/06.8.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/06.8.md)

先忽略匿名函数里面的 WaitGroup 。

```go
for taskId := range ch {
    seconds := 1 + rand.Intn(9)
    log.Printf("Task [%d] will sleep %d seconds\n", taskId, seconds)
    time.Sleep(time.Second * time.Duration(seconds))
    log.Printf("Task [%d] finished", taskId)
}
```

协程里面不断读取通道的数据。但是由于刚启动的时候通道里面没有数据，所以这里会阻塞。三个协程都阻塞了。

继续往下走：  

```go
for i := 0; i < maxTask; i++ {
    ch <- i
}
```

这里开始往通道发送数据。由于通道在上面被设置为只能存三个数据，所以这里一开始最多只能放三个。一旦放满又没被消费， for 循环就会被阻塞。  

一旦开始放数据，协程就可以从通道里拿数据了。

示例见：  

> [https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v1-fix/thread.log](https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v1-fix/thread.log)

```log
2020/04/16 01:59:52 Worker [0] started at 1586973592
2020/04/16 01:59:52 Task [0] will sleep 6 seconds
2020/04/16 01:59:52 Worker [1] started at 1586973592
2020/04/16 01:59:52 Task [1] will sleep 7 seconds
2020/04/16 01:59:52 Worker [2] started at 1586973592
2020/04/16 01:59:52 Task [2] will sleep 3 seconds
2020/04/16 01:59:55 Task [2] finished
```

当 maxTask 个任务发送完毕后，for 循环就结束了。

但注意，此时协程里的任务未必结束，但 for 循环后面的代码会继续跑。

```go
close(ch)
```

关闭通道入口，避免协程无限等待。

如果此时直接退出，会导致协程也被中断。

那么我们就要想办法等待协程任务执行结束。这时就要用到 WaitGroup 了。

```go
for i := 0; i < maxThread; i++ {
    // ...
    go func() {
        wg.Add(1)
        defer wg.Done()
        // ...
    }()
}
// ...
wg.Wait()
```

在匿名函数开始执行时，往里面加了个 1。

紧接着用 defer 指定了一个方法调用（wg.Done 就是 `wg.Add(-1)`），这个方法会在匿名函数 return 后执行。  

> 6.4 defer 和追踪：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/06.4.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/06.4.md)

然后在主函数的最后，用了 `wg.Wait()` 等到归零时才继续。

什么时候归零呢？在所有协程 return 后都执行了 `wg.Done()`。而协程要退出，就代表着任务已经执行结束了。

这样就做到了等待所有任务执行完再退出程序。

#### 并发库

为了将上面这个思路应用到漫画下载里面，可以选择将其直接分块写到 `main.go` 里面，或者抽取到一个专门的库。这里选择另外写一个库，可以借此演示引用项目中其他文件的方法。

下面先展示这个库的使用示例，再解释库自身的内容。

以下代码在：  

> [https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v2-fix/test/main.go](https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v2-fix/test/main.go)

`test/main.go`

```go
package main

import (
    "../../thread-v2-fix"
    "log"
    "math/rand"
    "time"
)

func main() {
    tp := Thread.Pool{MaxThread: 3}
    tp.Prepare(func(param interface{}) {
        taskId := param.(int)

        seconds := rand.Intn(9) + 1
        log.Printf("Task [%d] will sleep %d seconds", taskId, seconds)

        time.Sleep(time.Second * time.Duration(seconds))

        log.Printf("Task [%d] finished", taskId)
    })

    tasksCount := 10
    for i := 0; i < tasksCount; i++ {
        tp.RunWith(i)
    }

    tp.Wait()
}
```

总体上与前面的例子一致。我将 `thread-v1-fix` 分为三个部分：

- 存储协程执行的函数（Prepare）
- 发送任务（RunWith）
- 等待任务结束（Wait）

匿名函数的参数是一个接口类型，这样可以接收任何类型的入参。

匿名函数应首先将参数转换为所需的类型，然后再执行下面的操作。例如上例中的 `taskId := param.(int)` 将 param 转换为 int 类型。

甚至可以让传入的参数就是一个匿名函数，然后直接执行。例如：  

```go
func main() {
    tp := Thread.Pool{MaxThread: 3}
    tp.Prepare(func(param interface{}) {
        doSomething := param.(func())
        doSomething()
    })

    tasksCount := 10
    for i := 0; i < tasksCount; i++ {
        taskId := i
        tp.RunWith(func() {
            log.Println(taskId)
        })
    }

    tp.Wait()
}
```

接下来看 `thread-v2-fix` 的具体实现。

以下代码在：  

> [https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v2-fix/thread.go](https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v2-fix/thread.go)

`thread.go`

```go
package Thread

import (
    "log"
    "sync"
    "time"
)

type Pool struct {
    MaxThread int
    chParams  chan interface{}
    waitGroup sync.WaitGroup
    function  func(param interface{})
}

func (tp *Pool) Prepare(function func(item interface{})) {
    tp.chParams = make(chan interface{}, tp.MaxThread)
    tp.waitGroup = sync.WaitGroup{}
    tp.function = function

    for i := 0; i < tp.MaxThread; i++ {
        workerId := i
        go func() {
            tp.waitGroup.Add(1)
            defer tp.waitGroup.Done()

            log.Printf("Worker [%d] started at %d\n", workerId, time.Now().Unix())
            for param := range tp.chParams {
                tp.function(param)
            }
            log.Printf("Worker [%d] finished at %d\n", workerId, time.Now().Unix())
        }()
    }
}

func (tp *Pool) RunWith(param interface{}) {
    tp.chParams <- param
}

func (tp *Pool) Wait() {
    close(tp.chParams)
    tp.waitGroup.Wait()
}
```

在 Prepare 的时候将匿名函数保存起来，然后在协程里面获取到通道数据之后调用。

上面这个库算是一个简化版的实现，因为还有很多内容没有考虑到。例如最明显的是没有考虑到出错的情况。

所以如果为了更实际的使用，应该去参考开源库的实现：

> [https://github.com/go-playground/pool](https://github.com/go-playground/pool)  
> [https://github.com/nozzle/throttler](https://github.com/nozzle/throttler)  
> [https://github.com/Jeffail/tunny](https://github.com/Jeffail/tunny)  
> [https://github.com/panjf2000/ants](https://github.com/panjf2000/ants)

接下来说说我是如何误解下面这篇文章的方案二，并且基于错误的理解写出自己的版本。

> 来，控制一下 Goroutine 的并发数量：  
> [https://segmentfault.com/a/1190000017956396](https://segmentfault.com/a/1190000017956396)

如果不感兴趣，请直接跳过【我是怎么理解错的】和【基于错误的理解写出的版本】这两部分，跳转到 v9 。

#### 我是怎么理解错的

一开始我会先验证这个方案的代码是否可行，于是复制代码并执行。

以下代码来自于：  

> 来，控制一下 Goroutine 的并发数量：  
> [https://segmentfault.com/a/1190000017956396](https://segmentfault.com/a/1190000017956396)

```go
package main

import (
    "fmt"
    "sync"
    "time"
)

var wg sync.WaitGroup

func main() {
    userCount := 10
    ch := make(chan int, 5)
    for i := 0; i < userCount; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            for d := range ch {
                fmt.Printf("go func: %d, time: %d\n", d, time.Now().Unix())
                time.Sleep(time.Second * time.Duration(d))
            }
        }()
    }

    for i := 0; i < 10; i++ {
        ch <- 1
        ch <- 2
        //time.Sleep(time.Second)
    }

    close(ch)
    wg.Wait()
}
```

我认为限制了通道的缓冲区长度为 5，那么应该是控制最多五个任务并发。结果一运行就傻了，居然同时开了十个任务。  

现在当然可以知道是因为开了十个协程。就算一开始通道满了，当被其中五个协程获取后，位置就会空出来。然后 for 循环继续发送，剩下的五个协程也可以获取，直到每个协程都正在执行任务。所以实际上控制任务数的是 userCount。

这时就会奇怪了，限制通道缓冲区长度为 5 的意义是什么？为什么不设置和 userCount 一致？以下是我的看法：

- 限制通道长度，减少内存资源消耗
- 不需要很快执行完 for 循环  
    因为如果通道一直处于满的状态（协程获取到的任务一直没执行完），那么就没法往通道发送数据。而 for 循环必须等到所有数据发送完才结束。  
    如果通道设置得大一些，就能加快 for 循环的结束。例如这里将通道设置为 20 ，就会很快结束 for 循环，因为不会被阻塞。  

#### 基于错误的理解写出的版本

以下代码来自于：

> [https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v1/thread.go](https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v1/thread.go)   

`thread.go`

```go
package main

import (
    "log"
    "math/rand"
    "sync"
    "time"
)

var wg sync.WaitGroup

func main() {
    maxThread := 3
    ch := make(chan int, maxThread)

    taskCount := 10
    for i := 0; i < taskCount; i++ {
        tmpId := i
        go func(taskId int) {
            wg.Add(1)
            defer wg.Done()

            log.Printf("Task id is [%d]\n", taskId)

            workerId := <-ch
            log.Printf("Worker [%d] started at %d, task id is [%d]\n", workerId, time.Now().Unix(), taskId)

            seconds := 1 + rand.Intn(9)
            log.Printf("Task [%d] will sleep %d seconds\n", taskId, seconds)
            time.Sleep(time.Second * time.Duration(seconds))
            log.Printf("Task [%d] finished", taskId)

            log.Printf("Worker [%d] finished at %d\n", workerId, time.Now().Unix())

            ch <- workerId
        }(tmpId)
    }

    for i := 1; i <= maxThread; i++ {
        ch <- i
    }

    wg.Wait()
    close(ch)
}
```

这样的代码仍然可以按照限制的个数执行任务。

这里我为每个任务都开启一个协程，但是只有从通道里获取数据之后才正式执行任务。执行完任务后把数据放回通道，让其他协程获取并执行。  

这种做法有好处也有坏处。

坏处是如果任务量很大，例如一万个，会导致开启了一万个协程。这点从日志中可以看出来。  

好处是如果乱序执行任务比顺序执行任务更符合业务要求的话，能够达到乱序的效果。

当然，好处和坏处都是在一定场景下才能判断的。例如我这里下载漫画的时候就希望它按照顺序来下载，所以显然这种方式不符合我的要求。上面在展示修复后的版本时，就用的是顺序执行的方法。

我也有以这个错误版本为基础写了个顺序的版本。本来是作为版本 11 写的，但后来觉得这个版本没有必要，合并到版本 8 里面了。  

> [https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v2-1/thread.go](https://github.com/schaepher/comic-downloader-example/blob/master/v08-channel-wait-group-go-func-defer/thread-v2-1/thread.go)

这个思路是把任务先存起来，然后循环取出来并启动协程来执行。启动协程之前从通道获取数据，以此控制并发数。

## v9: 再次执行时避免下载已有页面

这个下载站有时候下载一张漫画图的时候会失败，然后再请求几次就能成功了。

（每次都能给我整出新花样）.jpg

但我不想总因为中间的某几张下载不了花太多时间重试，于是就放到整个漫画其他文件下载完之后再执行一次程序进行补充下载（后续改为自动重试）。

这样就带来一个问题，直接重试会导致一些已经下载的漫画页面再次被下载。所以我得列出已经下载的漫画页面，然后只下载那些缺失的页面。

以下代码在：  

> [https://github.com/schaepher/comic-downloader-example/blob/master/v09-list-dir-files/main.go](https://github.com/schaepher/comic-downloader-example/blob/master/v09-list-dir-files/main.go)

`main.go`

```go
type DownloadParam struct {
    Comic     Comic
    ComicFile ComicFile
}

func downloadComic(comic Comic, maxThread int) error {
    // ...
    existFiles, err := ListDirFiles(comic.GetDirPath())
    if err != nil {
        return err
    }

    log.Println("Downloading comic files")
    tp := Thread.Pool{MaxThread: maxThread}
    tp.Prepare(func(param interface{}) {
        downloadParam := param.(DownloadParam)
        downloadImg(downloadParam.Comic, downloadParam.ComicFile)
    })

    for _, comicFile := range comic.ComicFiles {
        if InArray(comicFile.Name, existFiles) {
            continue
        }
        tp.RunWith(DownloadParam{Comic: comic, ComicFile: comicFile})
    }
    // ...
}

func ListDirFiles(root string) ([]string, error) {
    var files []string
    fileInfo, err := ioutil.ReadDir(root)
    if err != nil {
        return files, err
    }
    for _, file := range fileInfo {
        files = append(files, file.Name())
    }
    return files, nil
}

func InArray(item string, items []string) bool {
    for _, tmpItem := range items {
        if tmpItem == item {
            return true
        }
    }
    return false
}
```

ListDirFiles 来自于：  

> List directory in Go：  
> [https://stackoverflow.com/a/49196644](https://stackoverflow.com/a/49196644)

这个函数创建了一个类型为 string 的切片，然后用 append 不断往切片里添加文件名。

> 7.5 切片的复制与追加：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/07.5.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/07.5.md)

InArray 函数是自己实现的判断当前文件名是否在文件列表中。

Go 没有判断元素是否在一个切片中的方法（比如 PHP 中的 in_array），因此每次都需要自己写。

## v10: 将配置抽取到配置文件

该版本的代码在：  

> [https://github.com/schaepher/comic-downloader-example/blob/master/v10-config/main.go](https://github.com/schaepher/comic-downloader-example/blob/master/v10-config/main.go)

到目前为止，网站和要下载的漫画 ID 都是放在代码里面的。这样导致要下载新漫画的时候，都得重新编译。因此要把配置抽取出来。

分析 v9 的代码，可以找到以下配置项：  

- 漫画主页 URL
- 下载地址的域名
- 漫画 ID
- 存储漫画的文件夹位置
- 并发数量

这里打算使用 Json 文件作为配置文件。  

因此定义以下结构体：  

```go
type Config struct {
    MainPageUrl        string   `json:"mainPageUrl"`
    DownloadSourceUrls []string `json:"downloadSourceUrls"`
    MaxThread          int      `json:"maxThread"`
    ComicIds           []int    `json:"comicIds"`
    ComicsRootDir      string   `json:"comicsRootDir"`
}
```

那么从哪里读取这个 Json 配置文件呢？默认跟可执行文件同一个目录吧。

前面使用 `os.Getwd()` 获取的是执行时所在的目录，而这里则是可执行文件所在的目录。

首先用 `os.Args[0]` 获取执行文件时使用的路径。  

> 如果在 Windows 10 上执行，会得到绝对路径。就算使用 `./main.exe`，也会得到完整路径。    
> 如果在 Linux 上执行，会得到执行时的路径。例如使用 `./main` 执行时，会得到 `./main`。  

然后用 `filepath.Dir()` 获取到该文件的文件夹。  

最后用 `filepath.Abs()` 得到绝对路径。上文有提到系统之间的差异，所以用这个函数来确保获取到正确的路径。

接着是读取这个文件，这里用了 `ioutil.ReadFile(filePath)` 。

## v11: 没有全部下载成功时重试

在 `v9: 再次执行时避免下载已有页面` 这一节碰到下载不了的漫画页面时，会先下载其他的，然后手动再次执行程序进行补充下载。

重试这种能交给程序做的事情为什么要手动执行？

如何做？

在一个漫画下载完后，再次获取文件夹内部的文件列表。如果文件数量和漫画数量对不上，则抛出错误。外部获得这个错误后执行重试。

此时有个问题：外部如何判断抛出的错误是漫画没有全部下载的错误？因为还可能出现其他类型的错误。

用错误的文本信息做比较是一种方法，不过容易出问题，而且不优雅。我们更希望能像 try-catch 那样自定义异常类型，然后根据类型做处理。

其实之前在转换变量类型的时候，会返回两个值：

- 转换后的变量
- 转换是否成功（bool 类型的变量）

那么就可以通过自定义错误类型 NotAllComicDownloadedError ，实现 error 接口。然后在外面尝试将错误转换为 NotAllComicDownloadedError 。如果成功，就表示出现这个错误，进入重试。

以下代码在：  

> [https://github.com/schaepher/comic-downloader-example/blob/master/v11-custom-error-retry/main.go](https://github.com/schaepher/comic-downloader-example/blob/master/v11-custom-error-retry/main.go)

`main.go` 部分代码：

```go
for retries := 0; ; {
    err = downloadComic(*comic, config.MaxThread)
    if err == nil {
        break
    }

    if _, ok := err.(NotAllComicDownloadedError); !ok {
        panic(err)
    }

    if retries++; retries > config.MaxRetry {
        break
    }

    log.Printf("Retrying, comic [%d]: %d", comic.Id, retries)
}
```

当 if 有两个表达式的时候，第一个是初始化，第二个才是判断。  

> 5.1 if-else 结构：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/05.1.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/05.1.md)

接下来就是定义错误类型 NotAllComicDownloadedError ，它需要实现 error 接口。

> 11.1 接口是什么：  
> [https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/11.1.md](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/11.1.md)

先看看 error 接口的定义：  

`$GOROOT/src/builtin/builtin.go`

```go
// The error built-in interface type is the conventional interface for
// representing an error condition, with the nil value representing no error.
type error interface {
    Error() string
}
```

实现：

```go
type NotAllComicDownloadedError struct {
    Comic Comic
}

func (err NotAllComicDownloadedError) Error() string {
    return fmt.Sprintf("download error: not all Comic images of [%d] are downloaded", err.Comic.Id)
}
```

至此已经实现了基本够用的功能，等到需要实现更多功能的时候再继续添加。

