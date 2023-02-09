## 一、前言

在上一节，我们新建了工程，做好了准备。本节在工程中加入B站网页，屏蔽页面广告。

## 二、工程配置

### 2.1、基础配置

1. **配置**

![Screenshot_2023-02-09-18-45-07-629_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-09-18-45-07-629_com.jpg)

-  程序启动事件，填入以下代码

```lua
加载网页("https://m.bilibili.com/index.html")

-- 加载网页 为软件自带的函数，后面做函数介绍
-- 链接地址 百度搜索bilibili，把浏览器地址栏的链接复制过来
```

点击右上角三角符号，我们可以看到页面如下:
![Screenshot_2023-02-09-18-54-51-842_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-09-18-54-51-842_com.jpg)

-   网页控制

网页控制如下图填写，
域名或URL我们填写B站的域名，`m.bilibili.com`，
域名
`https://www.baidu.com/xxx.html`，去除https://和后面斜杠之后的就是域名，其它网站类似。

删除元素，我们去除顶部和浮动框。这里填写`m-home-float-openapp,suspension`，多个类名用逗号隔开，或者用@ID(123)删除元素。类名和id获取如第二张图。
 

![Screenshot_2023-02-09-19-14-42-433_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-09-19-14-42-433_com.jpg)


![Screenshot_2023-02-09-19-08-54-317_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-09-19-08-54-317_com.jpg)



2. **组件**

