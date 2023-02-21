
### 前言

文章主要说明在FA中的中文函数的代码实现，不仅要知道用法，更要知其实现的原理。前面的用法为FA中的用法，仅支持在FA中使用，源码可以在其它app中使用。


### 进入子页面

```进入子页面("页面名称")```

- lua源码：

```lua
function 进入子页面(name,param)
  if(param~=nil)then
    activity.newActivity(name,param)
   else
    activity.newActivity(name)
  end
end
```

### 加载JS

```加载Js([[JavaScript代码]])```

- lua源码

```lua
function 加载Js(str,callback)
  if not pcall(function()
      获取浏览器().evaluateJavascript(str,callback or function() end)
    end) then
    获取浏览器().loadUrl("javascript:"..str)
  end
end
```

### 获取浏览页

```获取浏览页(1)```

lua源码：

```lua
function 获取浏览页(n)
  if n then
    return activity.uiManager.getPage(n)
   else
    return activity.uiManager.currentPage
  end
end
```

### 获取浏览器

```lua
function 获取浏览器()
  return 获取浏览页().webView
end
```

### 加载网页

```加载网页("链接")```

- lua源码：

```lua
function 加载网页(url)
  获取浏览器().loadUrl(url)
end
```

### 停止加载

```停止加载()```

- lua源码

```lua
function 停止加载()
  获取浏览器().stopLoading()
end
```

### 刷新网页

```刷新网页()```

- lua源码

```lua
function 刷新网页()
  获取浏览器().reload()
end
```

### 网页前进

```网页前进()```

- lua源码

```lua
function 网页前进()
  获取浏览器().goForward()
end
```

### 网页后退

```网页后退()```

- lua源码

```lua
function 网页后退()
  获取浏览器().goBack()
end
```

### 返回网页顶部

```返回网页顶部()```

- lua源码

```lua
function 返回网页顶部()
  获取浏览器().scrollTo(0,0)
end
```

### 弹出消息

```
弹出消息("消息内容")
```

- lua源码

```lua
print("消息内容")
```

### 退出程序

```
退出程序()
```

- lua源码

```lua
function 退出程序()
  if activity.packageName == "net.fusionapp" then
    activity.finish()
  else
    System.exit(0)
  end
end
```

### 退出页面

```
退出页面()
```

- lua源码

```lua
function 退出页面()
  activity.finish()
end
```

### 复制文本

```复制文本("文本内容")```

- lua源码

```lua
function 复制文本(a)
  if(Context==nil)then
    import "android.content.Context"
  end
  activity.getSystemService(Context.CLIPBOARD_SERVICE).setText(a)
end
```

### 分享文本

```分享文本("文本内容")```

- lua源码

```lua
function 分享文本(text)
  local ShareCompat=luajava.bindClass "androidx.core.app.ShareCompat"
  ShareCompat.IntentBuilder
  .from(activity)
  .setText(text)
  .setType("text/plain")
  .startChooser()
end
```
