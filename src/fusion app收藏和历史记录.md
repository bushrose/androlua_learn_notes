
### 实现效果

- 添加收藏

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-03-06-21-04-57-227_com.jpg)

- 查看收藏

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-03-06-21-05-20-020_com.jpg)

- 查看历史记录

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-03-06-21-05-27-208_com.jpg)


- 清除缓存

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-03-06-21-05-37-780_com.jpg)


### 工程文件下载

在公众号后台回复【fa收藏】即可获取下载链接。



### 第一部分 程序启动时会执行的事件

#### 程序启动时会执行的事件

```lua
--清除缓存
function clr()
  --导入File类
  import "java.io.File"
  --显示多选框
  items={"浏览记录","缓存文件"}
  多选对话框=AlertDialog.Builder(this)
  .setTitle("清除记录")
  --勾选后执行
  .setPositiveButton("确定",function()
    if clearhistory==1 and clearall==1 then
      File(lstads).delete()
      File(lstwebads).delete()
      lst={}
      lstweb={}
      os.execute("pm clear "..activity.getPackageName())
    elseif clearhistory==0 and clearall==1 then
      os.execute("pm clear "..activity.getPackageName())
    elseif clearhistory==1 and clearall==0 then
      File(lstads).delete()
      File(lstwebads).delete()
      lst={}
      lstweb={}
    else return nil
    end
  end)
  --选择事件
  .setMultiChoiceItems(items, nil,{ onClick=function(v,p)
      --清除历史
      if p==0 then clearhistory=1
      end
      --清除缓存
      if p==1 then clearall=1
      end
    end})
  多选对话框.show();
  clearhistory=0
  clearall=0
end


--1.地址
favads="/data/data/"..activity.getPackageName().."/fav.lua"
favwebads="/data/data/"..activity.getPackageName().."/favweb.lua"

--2.序列化
function slz(obj) 
  local lua = "" 
  local t = type(obj) 
  if t == "number" then 
    lua = lua .. obj 
  elseif t == "boolean" then 
    lua = lua .. tostring(obj) 
  elseif t == "string" then 
    lua = lua .. string.format("%q", obj) 
  elseif t == "table" then 
    lua = lua .. "{\n" 
    for k, v in pairs(obj) do 
      lua = lua .. "[" .. slz(k) .. "]=" .. slz(v) .. ",\n" 
    end 
    local metatable = getmetatable(obj) 
    if metatable ~= nil and type(metatable.__index) == "table" then 
      for k, v in pairs(metatable.__index) do 
        lua = lua .. "[" .. slz(k) .. "]=" .. slz(v) .. ",\n" 
      end 
    end 
    lua = lua .. "}" 
  elseif t == "nil" then 
    return nil 
  else 
    error("can not serialize a " .. t .. " type.") 
  end 
  return lua 
end 
function rslz(lua) 
  local t = type(lua) 
  if t == "nil" or lua == "" then 
    return {}
  elseif t == "number" or t == "string" or t == "boolean" then 
    lua = tostring(lua) 
  else 
    error("can not unserialize a " .. t .. " type.") 
  end 
  lua = "return " .. lua 
  local func = loadstring(lua) 
  if func == nil then 
    return nil 
  end 
  return func() 
end

--3.读取收藏文件
function read_fav()
  import "java.io.File"
  File(favads).createNewFile()
  sfav=io.open(favads):read("*a")
  File(favwebads).createNewFile()
  sfavweb=io.open(favwebads):read("*a")
  --转换成table
  fav=rslz(sfav)
  favweb=rslz(sfavweb)
end

--4.存储收藏文件
function save_fav()
  --转换成string
  sfav=slz(fav)
  sfavweb=slz(favweb)
  --保存
  file=io.open(favads,"w+")
  io.output(file)
  io.write(sfav)
  io.flush()
  io.close(file)
  file=io.open(favwebads,"w+")
  io.output(file)
  io.write(sfavweb)
  io.flush()
  io.close(file)
end

--5.收藏夹布局
function favshow()
  favlayout={
    LinearLayout,
    orientation="1",
    gravity="center",
    layout_width="wrap_content",
    layout_height="wrap_content",
    {
      TextView,
      text="",
      gravity="center",
      layout_width="wrap_content",
      textSize="0sp",
      background="#000000",
      layout_height="15dp",},
    {
      TextView,
      text="收藏夹",
      gravity="center",
      layout_width="wrap_content",
      textSize="30sp",
      textStyle="bold",
      layout_height="50dp",},
    {
      ListView,
      id="favlv",
      items=fav,
      layout_width="fill",
      layout_height="wrap_content",
    },
  }
end

--6.收藏夹显示
function show_fav() 
  read_fav()
  favshow()
  fl=AlertDialog.Builder(activity)
  .setView(loadlayout(favlayout))
  .setNegativeButton("取消",DialogInterface.OnClickListener{
    onClick=function()
    end
  })
  .create()
  fl.show()
  favlv.onItemClick=function(l,v,c,b)
    加载网页(favweb[b])
    fl.dismiss()
  end
  favlv.onItemLongClick=function(l,v,c,b)
    od=b
    popwin(od)
    return true
  end
end
--7.收藏夹编辑框布局
function efavshow(e1,e2)
  efavlayout={
    LinearLayout,
    orientation="1",
    Focusable=true,
    FocusableInTouchMode=true,
    {
      EditText,
      id="efav",
      text=e1,
      layout_marginTop="5dp",
      layout_width="80%w",
      layout_gravity="center",
    },
    {
      EditText,
      id="efavweb",
      text=e2,
      layout_margiTop="5dp",
      layout_width="80%w",
      layout_gravity="center",
    },
  }
end

--8.显示编辑框
function show_efav(b)
  read_fav()
  local e1=fav[b]
  local e2=favweb[b]
  efavshow(e1,e2)
  efl=AlertDialog.Builder(activity)
  .setTitle("编辑收藏")
  .setView(loadlayout(efavlayout))
  .setPositiveButton("确认",DialogInterface.OnClickListener{
    onClick=function()
      if (efav.text=="" or efavweb.text=="") then 
        print("请填写完整")
      else
        fav[b]=efav.text
        favweb[b]=efavweb.text
        save_fav()
        print("修改成功")
        efl.dismiss()
        show_fav()
      end
    end})
  .setNegativeButton("取消",DialogInterface.OnClickListener{
    onClick=function() 
      show_fav()
    end})
  .setNeutralButton("删除",DialogInterface.OnClickListener{
    onClick=function()
      对话框()
      .设置消息("确定要删除吗？")
      .设置积极按钮("确定",function()
        table.remove(fav,b)
        table.remove(favweb,b)
        save_fav()
        print("删除成功")
        efl.dismiss()
        show_fav()
      end)
      .设置消极按钮("取消",function()
        show_fav()
      end)
      .显示()
    end})
  .create()
  efl.show()
end

--9.添加收藏
function add_fav()
  read_fav()
  e1=webView.getTitle()
  e2=webView.getUrl()
  local rpt=0
  local nfav=#fav
  for i=1,nfav do
    if favweb[i]==webView.getUrl() then
      rpt=1
      break
    end
  end
  if rpt==1 then 
    print("该网页已在收藏夹")
  else 
    efavshow(e1,e2)
    afl=AlertDialog.Builder(activity)
    .setTitle("添加收藏")
    .setView(loadlayout(efavlayout))
    .setPositiveButton("添加",DialogInterface.OnClickListener{
      onClick=function()
        if (efav.text=="" or efavweb.text=="") then
          print("请填写完整")
        else
          table.insert(fav,1,efav.text)
          table.insert(favweb,1,efavweb.text)
          save_fav()
          print("收藏成功")
          rpt=nil
        end
      end})
    .setNegativeButton("取消",DialogInterface.OnClickListener{
      onClick=function() end})
    .create()
    afl.show()
  end
end

--10.收藏排序
function upfav(b)
  if b~=1 then
    ufav=fav[b]
    ufavweb=favweb[b]
    table.remove(fav,b)
    table.remove(favweb,b)
    table.insert(fav,b-1,ufav)
    table.insert(favweb,b-1,ufavweb)
  end
  save_fav()
  show_fav()
end  
--11.长按弹窗
function popwin(od)
  local win1="向上移动"
  local win2="编辑"
  local win3="向下移动"
  local wina={win1,win2,win3}
  local winb={win2,win3}
  local winc={win1,win2}
  if od==1 then
    win=winb
  elseif od==#fav then
    win=winc
  else
    win=wina
  end
  winlayout={
    LinearLayout,
    orientation="vertical",
    {ListView,
      id="winlv",
      items=win,
      layout_width="fill_parent",
      layout_height="wrap_content",},
  }
  winl=AlertDialog.Builder(activity)
  .setView(loadlayout(winlayout))
  .create()
  winl.show()
  winlv.onItemClick=function(l,v,c,b)
    if win[b]==win1 then
      fl.dismiss()
      upfav(od)
    elseif win[b]==win2 then
      fl.dismiss()
      show_efav(od)
    elseif win[b]==win3 then
      fl.dismiss()
      downfav(od)
    end
    winl.dismiss()
  end
end
function downfav(b)
  if b~=#fav then
    dfav=fav[b]
    dfavweb=favweb[b]
    table.remove(fav,b)
    table.remove(favweb,b)
    table.insert(fav,b+1,dfav)
    table.insert(favweb,b+1,dfavweb)
  end
  save_fav()
  show_fav()
end
```

#### 历史记录
```lua
--1.历史记录
lstads="/data/data/"..activity.getPackageName().."/lst.lua"
lstwebads="/data/data/"..activity.getPackageName().."/lstweb.lua"
--2.序列化
function slz(obj) 
  local lua = "" 
  local t = type(obj) 
  if t == "number" then 
    lua = lua .. obj 
  elseif t == "boolean" then 
    lua = lua .. tostring(obj) 
  elseif t == "string" then 
    lua = lua .. string.format("%q", obj) 
  elseif t == "table" then 
    lua = lua .. "{\n" 
    for k, v in pairs(obj) do 
      lua = lua .. "[" .. slz(k) .. "]=" .. slz(v) .. ",\n" 
    end 
    local metatable = getmetatable(obj) 
    if metatable ~= nil and type(metatable.__index) == "table" then 
      for k, v in pairs(metatable.__index) do 
        lua = lua .. "[" .. slz(k) .. "]=" .. slz(v) .. ",\n" 
      end 
    end 
    lua = lua .. "}" 
  elseif t == "nil" then 
    return nil 
  else 
    error("can not serialize a " .. t .. " type.") 
  end 
  return lua 
end 
function rslz(lua) 
  local t = type(lua) 
  if t == "nil" or lua == "" then 
    return {}
  elseif t == "number" or t == "string" or t == "boolean" then 
    lua = tostring(lua) 
  else 
    error("can not unserialize a " .. t .. " type.") 
  end 
  lua = "return " .. lua 
  local func = loadstring(lua) 
  if func == nil then 
    return nil 
  end 
  return func() 
end

--3.历史记录框布局
function hstshow()
  hstlayout={
    LinearLayout,
    orientation="1",
    gravity="center",
    layout_width="wrap_content",
    layout_height="wrap_content",
    {
      TextView,
      text="",
      gravity="center",
      layout_width="wrap_content",
      textSize="0sp",
      background="#000000",
      layout_height="15dp",},
    {
      TextView,
      text="历史记录",
      gravity="center",
      layout_width="wrap_content",
      textSize="30sp",
      textStyle="bold",
      layout_height="50dp",},
    {
      ListView,
      id="hlst",
      items=lst,
      layout_width="fill",
      layout_height="wrap_content",
    },
  }
end

--4.读取历史文件
function read_hst()
  import "java.io.File"
  File(lstads).createNewFile()
  slst=io.open(lstads):read("*a")
  File(lstwebads).createNewFile()
  slstweb=io.open(lstwebads):read("*a")
  --转换成table
  lst=rslz(slst)
  lstweb=rslz(slstweb)
end

--5.新网页加入历史记录
function add_hst()
  if string.len(webView.getTitle())<=300 then--粗略过掉无效标题
    newtitle=webView.getTitle()
    newurl=webView.getUrl()
    table.insert(lst,1,newtitle) --标题表添加新标题
    table.insert(lstweb,1,newurl) --网址表添加新网址
  end
end

--6.存储历史文件
function save_hst()
  --转换成string
  slst=slz(lst)
  slstweb=slz(lstweb)
  --保存
  file=io.open(lstads,"w+")
  io.output(file)
  io.write(slst)
  io.flush()
  io.close(file)
  file=io.open(lstwebads,"w+")
  io.output(file)
  io.write(slstweb)
  io.flush()
  io.close(file)
end

--7.显示历史记录框
function show_hst() 
  hstshow()
  local hl=AlertDialog.Builder(activity)
  .setView(loadlayout(hstlayout))
  .setNegativeButton("好",DialogInterface.OnClickListener{
    onClick=function()
    end
  })
  .create()
  hl.show()
  hlst.onItemClick=function(l,v,c,b)
    加载网页(lstweb[b])
    hl.dismiss()
  end
  hlst.onItemLongClick=function(l,v,c,b)
    hl.dismiss()
    对话框()
    .设置消息("是否删除记录？")
    .设置消极按钮("否",function()
      show_hst()
    end)
    .设置积极按钮("是",function()
      table.remove(lst,b)
      table.remove(lstweb,b)
      save_hst()
      show_hst()
    end )
    .显示()
    return true
  end
end
```





### 第二部分 浏览器加载新页面并获得新标题时执行的事件

```lua
--读取历史记录
read_hst()
--加入历史记录
add_hst()
--存储历史记录
save_hst()
```




### 第三部分 可分别填入到点击事件

```lua
--打开历史记录
show_hst()
--加入收藏
add_fav()
--打开收藏
show_fav()
```




