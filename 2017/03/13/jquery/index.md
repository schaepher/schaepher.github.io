# jQuery简单笔记


jQuery 是一个 JavaScript 库，简化了 JavaScript 的编程。

语法：$(selector).action()

selector 是字符串，表示HTML元素。

|对象|符号|例子|效果|
|:--|:--|:--|:--|
|当前整个HTML|this|this|选择整个HTML|
|标签|标签名|"p"|选择所有\<p\>元素|
|id|#|"#test"|选择所有 id = "test"的元素|
|class|.|".test"|选择所有 class = "test"的元素|
|链接|[]|[href="test"]|选择所有 href 等于 "test"的元素|
|||[href!="test"]|选择所有 href 不等于 "test"的元素|
|||[href$="test"]|选择所有 href 以 "test" 结尾的元素|
|表格|ul li:|"ul li:first"|选择每个 \<ul\> 的第一个 \<li\> 元素|
|||||

以上三者可以合起来用：$("p#test.test")

action()列表：  

|隶属|名称|功能|
|:--|:--|:--|
|document|ready(function)|HTML文档加载完毕时执行function|
|window||浏览器视口|
|所有元素|hide()|隐藏所选元素|
||show()|显示所选元素|
||toggle()|以上两者切换|
||fadeIn()|渐渐隐藏|
||fadeOut()|渐渐显示|
||fadeToggle()|以上两者切换|
||slideUp()|向上滑动隐藏元素|
||slideDown()|向下滑动显示元素|
||slideToggle()|以上两者切换|
||addClass()|添加一个或多个类|
||removeClass()|删除一个或多个类|
||toggleClass()|以上两者切换|
||mouseover(function)|鼠标悬停在元素上时执行function|
||focus(function)|元素获得焦点时执行function|
||click(function)|点击元素时执行function|
||dblclick(function)|双击元素时执行function|
||attr()|改变元素的属性|
||css()|改变或返回元素的css属性|
||animate({dict参数})|执行动画以使元素符合参数指定内容（属性名用骆驼命名法）|
||stop(bool,bool)|停止动画|
||text()|设置或返回所选元素的文本内容|
||html()|设置或返回所选元素带 HTML 标记的内容|
||val()|设置或返回表单字段的值|
||append(string)|元素内容结尾添加|
||after(string)|元素结束之后添加|
||remove()|删除整个元素|
||empty()|删除子元素|
||width()|不包括 padding 和 border|
||height()|不包括 padding 和 border|
||innerWidth()|包括 padding|
||innerHeight()|包括 padding|
||outerWidth()|包括 padding 和 border|
||outerHeight()|包括 padding 和 border|
||||

当出现动画动作时，可以传入两个参数：  

- 毫秒表示动作过渡时长。
- 回调，在动画完成后执行

可在数值前使用 += 和 -= 表示相对值。

在不重载整个网页的情况下，AJAX 通过后台加载数据，并在网页上进行显示。

AJAX:  
load()  
get()  
post()
