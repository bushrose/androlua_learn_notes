## 一、前言

上一篇我们完成了软件的基本功能，如果想在用户使用我们的app时，自动检测新版本并让自动完成安装，这样岂不是更好？本篇我们就来探究一下远程更新的过程，并完成实际的功能。另外在使用过程中发现，登录之后重启app，会发现需要再次登录，使用很不方便，我们也在第三部分解决这个问题。

## 二、fusion app远程更新

- **远程更新的本质**

远程更新的本质，就是通过接口获取数据并做处理。主要分为以下三步：

1. 开发后台服务接口，接口提供版本号、更新内容、下载链接等信息
2. 获取本地安装的app的版本信息
3. 本地发起http请求，获取远程的数据，比较本地版本和远程的版本，如果远程的版本大于本地版本，则需要更新

- **远程更新的代码实现**

首先我们准备服务接口，已经有应用准备好了相关接口，我们只需下载做好配置即可。这里后台采用水仙app，app界面如下：

![Screenshot_2023-02-10-20-17-46-567_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-10-20-17-46-567_com.jpg)


【水仙app】

下载链接:https://wwp.lanzoup.com/iB9Y10n62t0b  

提取码 : hgsc


使用qq登录注册后，在app主界面，点击我的后台-->右上角三个点-->修改配置，按照如下配置，这个key我们记录下来，会用于后面接口请求。

![mmexport1676032242416](https://gitee.com/teisyogun/images/raw/master/mmexport1676032242416.png)


在app首页，点击对接文档-->更新系统-->点链接，可以看到接口需要传输的参数和返回的参数，接下来我们按照接口文档来编写代码。

![Screenshot_2023-02-10-20-34-34-639_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-10-20-34-34-639_com.jpg)


以下是代码实现：

```lua
-- 将以下代码粘贴到程序启动事件中或者侧滑栏增加一个检查更新的栏目，放置在点击事件中。
function 检查更新(url,admin,key)
  packinfo=this.getPackageManager().getPackageInfo(this.getPackageName(),((1552294270/8/2-8392)/32/1250-25.25)/8-236)
  version=tostring(packinfo.versionName)
  --print(version)

  local url=url.."?admin="..admin.."&key="..key
  Http.get(url,nil,"utf-8",nil,function(code,content)
    if code==200 and content then
      local cjson=require("cjson")
      local JSON=cjson.decode(content)
      ver=JSON.data.ver
      link=JSON.data.link
      if ver>version then
        对话框()
        .设置标题("版本更新")
        .设置消息(JSON.data.content)
        .设置积极按钮("立即下载",function()
          弹出消息("应用正在下载，请关注通知栏")
          下载文件(link)
          安装程序("/storage/emulated/0/Download/"..取文件名(link))
        end)
        .设置消极按钮("暂时不考虑")
        .显示()
      end
    else
      弹出消息("网络错误或参数错误，请检查")
    end
  end)
end

function 安装程序(路径)
  import "android.net.*"
  import "android.content.*"
  intent = Intent(Intent.ACTION_VIEW)
  intent.setDataAndType(Uri.parse("file://"..路径),"application/vnd.android.package-archive")
  intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
  activity.startActivity(intent)
end

function 取文件名(path)
  return path:match(".+/(.+)$")
end


url="http://shuixian.ltd/main/api/new/new.php"
admin="1213212313"           -- 管理员账号就是注册登录水仙的qq号
key="123123123"              -- 采用自己的key
检查更新(url,admin,key)
```

- **fusion app配置及水仙后台配置**

修改版本名为1.1，再点击右上角三个点，再点打包安装

![mmexport1676033340648](https://gitee.com/teisyogun/images/raw/master/mmexport1676033340648.png)

打包完成后，可以看到打包后的apk路径，记录下这个路径。

![mmexport1676033344347](https://gitee.com/teisyogun/images/raw/master/mmexport1676033344347.png)

打开水仙app，依次点击我的后台-->更新系统，上传上一步路径下的app，在进行如下配置：

```
版本号：填1.1
更新内容：随便填写
下载链接：点击下方上传安装包后会自动生成，不做更改
```

配置完成后，再点击发布更新。

![Screenshot_2023-02-10-20-54-12-448_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-10-20-54-12-448_com.jpg)

水仙app配置完成后，返回我们的工程文件，再把app的版本名更改为1.0，点击打包安装，打开安装后的app看到如下界面，就说明完成了远程更新的功能。

![Screenshot_2023-02-10-21-01-14-272_com](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-10-21-01-14-272_com.jpg)


## 三、fusion app免登录

重启app出现再次登录的原因是因为webview加载网页，没有记录cookie，在配置页-网页加载完毕事件中增加如下代码：

```lua
import "android.webkit.CookieManager"
local cookieManager = CookieManager.getInstance()
cookieManager.flush()
```

配置好后再次打包安装即可。


如果还不清楚怎么操作，可以下载我的工程文件，导入到自己的FA中查看。

链接:https://pan.baidu.com/s/1JXUdL3OZaOSNtVaeZy9H7w 

提取码:9d92

## 四、总结

本文完成了远程更新的功能和免登录的功能，这样一个简单的应用就完成了。当然FA还提供一些其他功能，后面的文章再介绍自带的一些函数和组件。


