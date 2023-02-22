
###  安装apk

```安装APK(filePath)```

- lua源码

```lua
function 安装APK(filePath)
  local intent = Intent(Intent.ACTION_VIEW);
  intent.addCategory("android.intent.category.DEFAULT");
  intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
  local uri = nil
  if (Build.VERSION.SDK_INT >=  24) then--24是N
    uri = xFileProvider.getUriForFile(activity, activity.getPackageName()..".FileProvider", File(filePath))
    intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
   else
    uri = Uri.fromFile(File(filePath))
  end
  intent.setDataAndType(uri, "application/vnd.android.package-archive");
  activity.startActivity(intent);
end
```

### 联系QQ(qqNUM)

```联系QQ(qqNUM)```

- lua源码

```lua
function 联系QQ(qqNUM)
  local s = "mqqwpa://im/chat?chat_type=wpa&uin=" .. qqNUM
  activity.startActivity(Intent(Intent.ACTION_VIEW, Uri.parse(s)))
end
```

### 加QQ群

```加QQ群```

- lua源码

```lua
function 加QQ群(qqNUM)
  local s = "mqqapi://card/show_pslcard?src_type=internal&version=1&uin=" .. qqNUM .. "&card_type=group&source=qrcode"
  activity.startActivity(Intent(Intent.ACTION_VIEW, Uri.parse(s)))
end
```

### 发送邮件

```发送邮件(email,subject,content) ```

- lua源码

```lua
function 发送邮件(email,subject,content)
  import "android.content.Intent"
  i = Intent(Intent.ACTION_SEND)
  i.setType("message/rfc822")
  i.putExtra(Intent.EXTRA_EMAIL, {email})
  i.putExtra(Intent.EXTRA_SUBJECT,subject)
  i.putExtra(Intent.EXTRA_TEXT,content)
  activity.startActivity(Intent.createChooser(i, "Choice"))
end
```

### 获取剪切板

```获取剪切板()```

- lua源码

```lua
function 获取剪切板()
  if(Context==nil)then
    import "android.content.Context"
  end
  return activity.getSystemService(Context.CLIPBOARD_SERVICE).getText()
end
```

### 复制文本

```复制文本(a)```

- lua源码

```lua
function 复制文本(a)
  if(Context==nil)then
    import "android.content.Context"
  end
  activity.getSystemService(Context.CLIPBOARD_SERVICE).setText(a)
end
```

### 分享链接

```分享链接()```

- lua源码

```lua
function 分享链接()
  分享文本(获取浏览器().url)
end
```



### 对话框

```泡沫对话框```

- lua源码

```lua
local bindClass=luajava.bindClass
local AlertDialog=bindClass("android.app.AlertDialog")
local Builder=AlertDialog.Builder
local indexBuilderPool={}
function 对话框(ctx)
  local index=#indexBuilderPool+1
  local dialog=AlertDialog.Builder(ctx or activity or this)
  indexBuilderPool[index]=dialog
  local _M
  _M= {
    ["设置标题"]=function(...) dialog.setTitle(...) return _M end;
    ["设置消息"]=function(...) dialog.setMessage(...) return _M end;
    ["设置积极按钮"]=function(...)
      local args={...}
      if (#args==1) then
        dialog.setPositiveButton(args[1],nil)
       else
        dialog.setPositiveButton(...)
      end
      return _M end;
    ["设置消极按钮"]=function(...)
      local args={...}
      if (#args==1) then
        dialog.setNegativeButton(args[1],nil)
       else
        dialog.setNegativeButton(...)
      end
      return _M end;
    ["设置中立按钮"]=function(...)
      local args={...}
      if (#args==1) then
        dialog.setNeutralButton(args[1],nil)
       else
        dialog.setNeutralButton(...)
      end
      return _M end;
    ["显示"]=function(...)
      dialog=dialog.show(...)
      indexBuilderPool[index]=dialog
      return _M end;
    ["创建"]=function(...)
      dialog=dialog.create(...)
      indexBuilderPool[index]=dialog
      return _M end;
    ["取消"]=function(...) dialog.cancel(...) return _M end;
    ["关闭"]=function(...)
      dialog.dismiss(...)
      luajava.clear(indexBuilderPool[index])
      indexBuilderPool[index]=true
      return _M end;
    ["dismiss"]=function(...)
      dialog.dismiss(...)
      luajava.clear(indexBuilderPool[index])
      indexBuilderPool[index]=true
      return _M end;
    ["隐藏"]=function(...) dialog.hide(...) return _M end;
    ["设置按钮"]=function(...) dialog.setButton(...) return _M end;
    ["设置按钮1"]=function(...) dialog.setButton(...) return _M end;
    ["设置按钮2"]=function(...) dialog.setButton(...) return _M end;
    ["设置按钮3"]=function(...) dialog.setButton(...) return _M end;
    ["设置视图"]=function(...) dialog.setView(...) return _M end;
    ["设置图标"]=function(...) dialog.setIcon(...) return _M end;
    ["设置是否可以取消"]=function(...) dialog.setCancelable(...) return _M end;
    ["设置项目"]=function(...) dialog.setItems(...) return _M end;
    ["设置多选项目"]=function(...) dialog.setMultiChoiceItems(...) return _M end;
    ["设置取消监听器"]=function(...) dialog.setOnCancelListener(...) return _M end;
    ["设置关闭监听器"]=function(...) dialog.setOnDismissListener(...) return _M end;
    ["设置按键监听器"]=function(...) dialog.setOnKeyListener(...) return _M end;
    ["设置项目选择监听器"]=function(...) dialog.setOnItemSelectedListener(...) return _M end;
    ["启用测量时设置回收"]=function(...) dialog.setRecycleOnMeasureEnabled(...) return _M end;
    ["设置简单选择项目"]=function(...) dialog.setSingleChoiceItems(...) return _M end;
    ["设置自定义标题"]=function(...) dialog.setCustomTitle(...) return _M end;
    ["设置适配器"]=function(...) dialog.setAdapter(...) return _M end;
    ["设置光标"]=function(...) dialog.setCursor(...) return _M end;
    ["设置图标属性"]=function(...) dialog.setIconAttribute(...) return _M end;
    ["设置背景强制反向"]=function(...) dialog.setInverseBackgroundForced(...) return _M end;
    ["获得按钮"]=function(...) dialog.getButton(...) return _M end;
    ["获得列表视图"]=function(...) dialog.getListView(...) return _M end;
    ["当键按下时"]=function(...) dialog.onKeyDown(...) return _M end;
    ["当键抬起时"]=function(...) dialog.onKeyUp(...) return _M end;
    ["添加内容视图"]=function(...) dialog.addContentView(...) return _M end;
    ["设置内容视图"]=function(...) dialog.setContentView(...) return _M end;
    ["关闭选项菜单"]=function(...) dialog.closeOptionsMenu(...) return _M end;
    ["是否正在显示"]=function(...) dialog.isShowing(...) return _M end;
    ["获得窗口"]=function(...) dialog.getWindow(...) return _M end;
    ["设置能否在点击外部后取消"]=function(...) dialog.setCanceledOnTouchOutside(...) return _M end;
    ["设置取消消息"]=function(...) dialog.setCancelMessage(...) return _M end;
    ["getThisDialogObject"]=function()return dialog end,
    ["获得对话框实例"]=function()return dialog end,
  }
  local transC2E={
    ["标题"]="Title",
    ["消息"]="Message",
  }
  setmetatable(_M,{
    ["__newindex"]=function(_M,k,v)
      k=transC2E[k] or k
      dialog[k]=v
    end,
    ["__index"]=function(_M,method,...)
      if method=="标题" or method=="Title" or method=="title" or method=="getTitle" then
        return dialog.findViewById(android.R.id.icon).parent.getChildAt(1).text
      end
      if method=="消息" or method=="Message" or method=="message" or method=="getMessage" then
        return dialog.findViewById(android.R.id.message).text
      end
      _M[method]=function(...)
        local a=dialog[method]
        if type(a)=="function" then
          a(...)
         else
          return a
        end
        return _M
      end
      return _M[method]
    end
  })
  return _M
end
function 泡沫对话框(ctxOrnum,num)
  if num==nil then
    num=ctxOrnum
    ctxOrnum=nil
  end
  local token="|"..tostring(tointeger(num))
  local OneTimeDialogMark=activity.getSharedData("ONE-TIME-DIALOG-MARK")
  if OneTimeDialogMark==nil then
    OneTimeDialogMark="|"
    activity.setSharedData("ONE-TIME-DIALOG-MARK",OneTimeDialogMark)
  end
  if OneTimeDialogMark:find(token,0,true) then
    local _M={}
    setmetatable(_M,{
      ["__index"]=function(_M,method,...)
        _M[method]=function(...) return _M end
        return _M[method]
      end
    })
    return _M
  end
  OneTimeDialogMark=OneTimeDialogMark..token
  local basedialog=对话框(ctxOrnum)
  local func1=basedialog["显示"]
  local func2=basedialog["show"]
  basedialog["显示"]=function(...)
    func1(...)
    activity.setSharedData("ONE-TIME-DIALOG-MARK",OneTimeDialogMark)
  end
  basedialog["show"]=function(...)
    func2(...)
    activity.setSharedData("ONE-TIME-DIALOG-MARK",OneTimeDialogMark)
  end
  return basedialog
end
```