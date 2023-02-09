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

组件整体配置如下图：

![Screenshot_2023-02-09-21-05-16-897_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-09-21-05-16-897_com.jpg)

- 底栏项目

点击加号可以新增底栏，栏目可以根据自己喜好新增，url链接由浏览器打开网站对应页面，在浏览器地址栏复制过来即可。这里我们新增四个栏目

```
首页
https://m.bilibili.com/


国创
https://m.bilibili.com/channel/v/guochuang/chinese

宅舞
https://m.bilibili.com/channel/v/dance/otaku


登录
https://passport.bilibili.com/login
```

- **顶栏 菜单项目**

长按，删除掉模板配置的退出


- **顶栏搜索功能**

开启启用搜索功能，顶部会多一个放大镜的索索按钮
开启输入框模式，没得搜索图标，会多个输入框
搜索url，在B站中随意搜索一个视频，比如我们搜索“九转大肠”，复制出来的链接`https://m.bilibili.com/search?keyword=%E4%B9%9D%E8%BD%AC%E5%A4%A7%E8%82%A0`,把这个链接修改为`https://m.bilibili.com/search?keyword=%s`，其他网站的搜索链接也是类似的操作。


- **顶栏 图标按钮**

新增一个关闭app的功能。在图标仓库选择一个关闭的图标，项目点击事件中选择事件`退出程序()`，再保存退出。


- **侧滑栏配置**

开启侧滑栏，选择一张图片



- **侧滑栏 列表项目**

点击+号新增，项目名称 ：哔哩哔哩，设置项目点击事件中填写`加载网页("https://m.bilibili.com/")`，这句代码就是点击侧滑栏这个列表项时，会请求加载哔哩哔哩的首页。

完成以上配置后，点击右上角三角符号，可以预览app，此时页面如下：

![Screenshot_2023-02-09-21-29-38-217_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-09-21-29-38-217_com.jpg)


### 2.2、app优化

- 页面优化

预览时可以看到国创和宅舞页面顶部有空白，还是通过删除元素的方式来去除，在配置-网页控制中，新增需要删除的元素名称`sub-channel-menu`，这时完整的配置为`m-home-float-openapp,suspension,sub-channel-menu`。

![mmexport1675949976693](https://gitee.com/teisyogun/images/raw/master/mmexport1675949976693.png)


- 增加二次确认操作

点击搜索栏x时，会直接关闭app，体验不好。这里增加一个二次确认的操作。

在组件->顶栏图标按钮，点击图标->设置项目点击事件，将2.1中的的事件修改为以下代码，再保存：

``` lua
对话框()
.设置标题("退出app")
.设置消息("您确定关闭该应用?")
.设置积极按钮("确定",function()
  退出程序()
end)
.设置消极按钮("取消")
.显示()

-- 这些事件都是点击+号，可以选择事件。如何配置需要学习下lua代码的基础知识
```

配置完成后，点击x关闭时，就会弹出对话框让用户确认，如下：

![Screenshot_2023-02-09-21-50-06-754_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-09-21-50-06-754_com.jpg)


- 侧滑栏增加退出按钮

在组件->侧滑栏中，新增退出，选择图标，设置的点击事件与上一步关闭图标的一致，预览时，点开侧滑栏就可以看到新增的退出功能。

![Screenshot_2023-02-09-21-57-10-859_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-09-21-57-10-859_com.jpg)


3. **属性**

在前面2步完成，app已经初步成型，为了让应用更好看，我们调整一下配色，可以根据自己喜好调整，这里以bilibili粉红的颜色来配置。

```
 底栏             #FFF97192
 底栏图标选中      #FF415159
 顶栏             #FFF97192
 导航栏           #FFF97192
 侧滑栏背景        #FFE1EEF6
 -- 只修改这些，其余不动，可以自行研究配色
```

这是我们的界面如下：
![Screenshot_2023-02-09-22-12-26-157_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-09-22-12-26-157_com.jpg)



到此完成了app的雏形，在工程界面点击右上角三个点，可以打包安装。（注意打包路径不要包含中文，可能会出错）

![mmexport1675952295101](https://gitee.com/teisyogun/images/raw/master/mmexport1675952295101.png)




## 三、总结

本章我们完成了app的初步雏形，完成页面常见元素去除，修改应用配色等。目前应用还存在一些问题，下节我们完成app版本检测及免登录。

本文的工程文件下载链接：

链接:`https://pan.baidu.com/s/1N9vo58KYfCWzM9rlOaC11Q `

提取码:8ch4

