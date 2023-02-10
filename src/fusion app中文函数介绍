
> **声明：文章来源于代码手册，如有侵权，请联系删除**

FA很贴心的封装了中文函数：
### 1. 进入子页面

```
用法：进入子页面("子页面名称")
高级用法：进入子页面("子页面名称",{链接=url})
从这里传给子页面的链接，在子页面会直接访问链接并触发网页加载事件
```

### 2. 加载JS

```
用法：加载Js([[JavaScript代码]])
列举一些常用的JS代码：
加载Js([[var para = document.createElement("p");]])--代码是用于创建 <p> 元素
加载Js([[var node = document.createTextNode("这是一个新的段落。");]])--为 <p> 元素添加文本节点
加载Js([[para.appendChild(node);]])--将文本节点添加到 <p> 元素中
加载Js([[var element = document.getElementById("div1");]])--查找已存在的元素
加载Js([[element.appendChild(para);]])--添加到已存在的元素中
```


--上面代码可以简写成：
```
[[
加载Js([[
var para = document.createElement("p");
var node = document.createTextNode("这是一个新的段落。");
para.appendChild(node);
var element = document.getElementById("div1");
element.appendChild(para);
]])
]]
JS对于网页的增删改查(以下代码起作用的只有<script>框内的代码，前面的是h5网页代码，用做示例)：
增：
--[[
使用了 appendChild() 方法，用于添加新元素到尾部。
需要将新元素添加到开始位置，可以使用 insertBefore() 方法。
<div id="div1">
<p id="p1">这是一个段落。</p >
<p id="p2">这是另外一个段落。</p >
</div>

<script>
var para = document.createElement("p");--创建标签
var node = document.createTextNode("这是一个新的段落。");--创建文本节点
para.appendChild(node);--将文本节点添加至标签

var element = document.getElementById("div1");--寻找网页中id为div1的元素
var child = document.getElementById("p1");--寻找网页中id为p1的元素
element.insertBefore(para, child);--将创建的标签添加至div1下的p1的前面
</script>
]]

删：
--[[
要移除一个元素，你需要知道该元素的父元素。
因为早期的 Internet Explorer 浏览器不支持 node.remove() 方法。
不在意兼容性可以直接用remove()
<div id="div1">
<p id="p1">这是一个段落。</p >
<p id="p2">这是另外一个段落。</p >
</div>

<script>
var parent = document.getElementById("div1");--寻找id为div1的元素
var child = document.getElementById("p1");--寻找id为p1的元素
parent.removeChild(child);--将div1下的p1删除
</script>
]]

改：
--[[
使用 replaceChild() 方法来替换 HTML DOM 中的元素。
<div id="div1">
<p id="p1">这是一个段落。</p >
<p id="p2">这是另外一个段落。</p >
</div>

<script>
var para = document.createElement("p");--创建一个p标签
var node = document.createTextNode("这是一个新的段落。");--创建一个文本节点
para.appendChild(node);--将文本节点添加至p标签

var parent = document.getElementById("div1");--寻找id为div1的标签
var child = document.getElementById("p1");--寻找id为p1的标签
parent.replaceChild(para, child);--将div1下的p1替换成新建的p标签
</script>
]]

查：
--[[
这里不做代码演示，将js的常用获取api一一列举
document.activeElement --返回当前获取焦点元素
document.anchors --返回对文档中所有 Anchor 对象的引用。
document.baseURI --返回文档的绝对基础 URI
document.body --返回文档的body元素
document.cookie --设置或返回与当前文档有关的所有 cookie。
document.doctype --返回与文档相关的文档类型声明 (DTD)。
document.documentElement --返回文档的根节点
document.documentMode --返回用于通过浏览器渲染文档的模式
document.documentURI --设置或返回文档的位置
document.domain --返回当前文档的域名。
document.embeds --返回文档中所有嵌入的内容（embed）集合
document.forms --返回对文档中所有 Form 对象引用
document.getElementsByClassName() --返回文档中所有指定类名的元素集合，作为 NodeList 对象。
document.getElementById() --返回对拥有指定 id 的第一个对象的引用。
document.getElementsByName() --返回带有指定名称的对象集合。
document.getElementsByTagName() --返回带有指定标签名的对象集合。
document.images --返回对文档中所有 Image 对象引用。
ocument.implementation --返回处理该文档的 DOMImplementation 对象。
document.inputEncoding --返回用于文档的编码方式（在解析时）。
document.lastModified --返回文档被最后修改的日期和时间。
document.links --返回对文档中所有 Area 和 Link 对象引用。
document.readyState --返回文档状态 (载入中……)
document.referrer --返回载入当前文档的文档的 URL。
document.scripts --返回页面中所有脚本的集合。
document.title --返回当前文档的标题。
document.URL --返回文档完整的URL
]]
这些都是原生JS语句，使用起来比较繁琐，JS有一个十分强大的库：jQuery
这个用起来就十分的简单，但不是每个网页都加载了这个库，所以使用前需要在网页中注入JS：
加载JS([[
var hm = document.createElement("script");
hm.src = "http://libs.baidu.com/jquery/2.0.0/jquery.min.js";
var s = document.getElementsByTagName("title")[0]; 
s.parentNode.insertBefore(hm, s);
]])
然后就可以使用jQuery库的语句了，下面简单说下它的增删改查API
增：
append和prepend方法：
$("p").append("追加文本"); --在p标签结尾处插入文本
$("p").prepend("在开头追加文本"); --在p标签开头处插入文本
$("body").append(txt1,txt2,txt3); --可以一次性添加多个文本
after和before方法：
$("img").after("在后面添加文本");
$("img").before("在前面添加文本");
$("img").after(txt1,txt2,txt3); 

删：
$("#div1").remove(); --删除ID为div1的元素
$("#div1").empty(); --删除ID为div1的子元素
$("p").remove(".italic"); --删除类名为italic下的所有p元素

改：
$("#test1").text("Hello world!"); --将id为test1的元素文本设置为Hello world!
$("#test2").html("<b>Hello world!</b>"); --将id为test2的元素html设置为<b>Hello world!</b>
$("#test3").attr("href","http://www.baidu.com/"); --将id为test3的元素的href属性值设置为http://www.baidu.com/
$("#test4").attr({
"href" : "http://www.baidu.com/",
"title" : "百度"
}); --可以用json形式赋予多次属性值

查：
$("*") --所有元素
$("#lastname") --id="lastname" 的元素
$(".intro") --class="intro" 的所有元素
$(".intro,.demo") --class 为 "intro" 或 "demo" 的所有元素
$("p") --所有 <p> 元素
$("h1,div,p") --所有 <h1>、<div> 和 <p> 元素
$("p:first") --第一个 <p> 元素
$("p:last") --最后一个 <p> 元素
$("tr:even") --所有偶数 <tr> 元素，索引值从 0 开始，第一个元素是偶数 (0)，第二个元素是奇数 (1)，以此类推。
$("tr:odd") --所有奇数 <tr> 元素，索引值从 0 开始，第一个元素是偶数 (0)，第二个元素是奇数 (1)，以此类推。
$("p:first-child") --属于其父元素的第一个子元素的所有 <p> 元素
$("p:first-of-type") --属于其父元素的第一个 <p> 元素的所有 <p> 元素
$("p:last-child") --属于其父元素的最后一个子元素的所有 <p> 元素
$("p:last-of-type") --属于其父元素的最后一个 <p> 元素的所有 <p> 元素
$("p:nth-child(2)") --属于其父元素的第二个子元素的所有 <p> 元素
$("p:nth-last-child(2)") --属于其父元素的第二个子元素的所有 <p> 元素，从最后一个子元素开始计数
$("p:nth-of-type(2)") --属于其父元素的第二个 <p> 元素的所有 <p> 元素
$("p:nth-last-of-type(2)") --属于其父元素的第二个 <p> 元素的所有 <p> 元素，从最后一个子元素开始计数
$("p:only-child") --属于其父元素的唯一子元素的所有 <p> 元素
$("p:only-of-type") --属于其父元素的特定类型的唯一子元素的所有 <p> 元素
$("div > p") --<div> 元素的直接子元素的所有 <p> 元素
$("div p") --<div> 元素的后代的所有 <p> 元素
$("div + p") --每个 <div> 元素相邻的下一个 <p> 元素
$("div ~ p") --<div> 元素同级的所有 <p> 元素
$("ul li:eq(3)") --列表中的第四个元素（index 值从 0 开始）
$("ul li:gt(3)") --列举 index 大于 3 的元素
$("ul li:lt(3)") --列举 index 小于 3 的元素
$("input:not(:empty)") --所有不为空的输入元素
$(":header") --所有标题元素 <h1>, <h2> ...
$(":animated") --所有动画元素
$(":focus") --当前具有焦点的元素
$(":contains('Hello')") --所有包含文本 "Hello" 的元素
$("div:has(p)") --所有包含有 <p> 元素在其内的 <div> 元素
$(":empty") --所有空元素
$(":parent") --匹配所有含有子元素或者文本的父元素。
$("p:hidden") --所有隐藏的 <p> 元素
$("table:visible") --所有可见的表格
$(":root") --文档的根元素
$("p:lang(de)") --所有 lang 属性值为 "de" 的 <p> 元素
$("[href]") --所有带有 href 属性的元素
$("[href='default.htm']") --所有带有 href 属性且值等于 "default.htm" 的元素
$("[href!='default.htm']") --所有带有 href 属性且值不等于 "default.htm" 的元素
$("[href$='.jpg']") --所有带有 href 属性且值以 ".jpg" 结尾的元素
$("[title|='Tomorrow']") --所有带有 title 属性且值等于 'Tomorrow' 或者以'Tomorrow' 后跟连接符作为开头的字符串
$("[title^='Tom']") --所有带有 title 属性且值以 "Tom" 开头的元素
$("[title~='hello']") --所有带有 title 属性且值包含单词 "hello" 的元素
$("[title*='hello']") --所有带有 title 属性且值包含字符串 "hello" 的元素
$( "input[id][name$='man']" ) --带有 id 属性，并且 name 属性以 man 结尾的输入框
$(":input") --所有 input 元素
$(":text") --所有带有 type="text" 的 input 元素
$(":password") --所有带有 type="password" 的 input 元素
$(":radio") --所有带有 type="radio" 的 input 元素
$(":checkbox") --所有带有 type="checkbox" 的 input 元素
$(":submit") --所有带有 type="submit" 的 input 元素
$(":reset") --所有带有 type="reset" 的 input 元素
$(":button") --所有带有 type="button" 的 input 元素
$(":image") --所有带有 type="image" 的 input 元素
$(":file") --所有带有 type="file" 的 input 元素
$(":enabled") --所有启用的元素
$(":disabled") --所有禁用的元素
$(":selected") --所有选定的下拉列表元素
$(":checked") --所有选中的复选框选项
$( "p:target" ) --选择器将选中ID和URI中一个格式化的标识符相匹配的<p>元素
```

### 3. 加载网页
```
加载网页("url")
会在当前界面访问url链接
```

### 4. 停止加载
```
停止加载()
注意加括号，FA里少写了，不加括号会报错。
```

### 5. 刷新网页
```
刷新网页()
刷新当前网页访问状态
会触发网页加载事件
```

### 6. 网页前进
```
网页前进()
加载使用网页后退方法时的网页
单独使用没有效果，需要配合网页后退使用
```

### 7. 网页后退
```
网页后退()
访问前一次的访问链接
会触发网页加载事件
```

### 8. 返回网页顶部
```
返回网页顶部()
通过JS实现的滚动滚轮至网页最顶部
```

### 9. 阅读模式
```
阅读模式()
通过JS实现，更改网页排版等，使其便于阅读
```

### 10. 显示对话框
```
对话框()
.设置标题("对话框标题")
.设置消息("对话框消息")
.设置积极按钮("确定",function()
显示消息("点击了确定")--这里是确定按钮点击事件
end)
.设置消极按钮("取消")--这后面也可以设置取消按钮点击事件，仿照确实按钮点击事件
.显示()--显示对话框
```

### 11. 泡沫对话框
```
泡沫对话框(301)
.设置标题("标题")
.设置消息([[消息]])
.设置积极按钮("确定",function()
显示消息("点击了确定")
end)
.设置消极按钮("取消")
.显示()
--方法类似对话框，但泡沫对话框只会在初次进入软件时显示
```

### 12. 弹出消息
```
弹出消息("消息内容")
在屏幕中显示一段内容，非print，是用Toast实现的，所以参数有限制。
```

### 13. 退出程序
```
退出程序()
顾名思义，即退出软件
```

### 14. 退出页面
```
退出页面()
退出当前页面，返回上一次的页面，如已在首页，则退出软件。
```

### 15. 复制文本
```
复制文本("文本内容")
将文本复制至手机剪切板
```

### 16. 分享文本
```
分享文本("文本内容")
弹出手机分享窗口，将文本分享
```

### 17. 分享链接
```
分享文本(webView.getUrl())
即分享文本功能，文本为当前网页链接而已
```

### 18. 发生邮件
```
发送邮件("邮箱")
顾名思义(我也没用过)
```

### 19. 联系QQ
```
联系QQ(QQ号)
弹出QQ咨询窗口，可直接聊天
```

### 20. 加QQ群
```
加QQ群(QQ群号)
弹出加群界面
```

### 21. 页内查找
```
页内查找("词")
在当前网页寻找关键字，并将其高亮显示
通过JS实现，即寻找匹配关键字并将焦点转移
```

### 22. 点击元素
```
点击元素("元素类名")
--即使是被网页控制屏蔽的元素，也可以使用该代码点击
模拟点击网页事件，如网页中的分类按钮，将其屏蔽后，可以自己设置按钮点击显示它
```

### 23. 下载文件
```
下载文件("文件链接")
顾名思义
通过http.download方法实现
```

### 24. 执行Shell
```
执行Shell("shell命令")
Shell为linux命令行语句，安卓本身也是linux系统，所以支持调用
比如：
执行Shell("rm-r 路径") --删除文件
```