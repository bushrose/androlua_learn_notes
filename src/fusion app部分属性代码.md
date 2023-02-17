
> **声明：代码收集于网络**

- 手机方向

```lua
-- 垂直方向 
 orientation="vertical",--垂直方向 

-- 水平方向 
 orientation="horizontal",--水平方向 
```


- 权重值分配

```lua
 layout_weight="1",--权重值分配 
```

- 控件设置ID

```lua
 id="button",--控件ID 
```

- 单击事件

```lua
 onClick=function()--单击事件
end,--单击事件 结束
```

- 布局

```lua
-- 布局背景
 background="#ffffffff",--布局背景

-- 布局宽度 
 layout_width="fill",--布局宽度

-- 布局高度 
 layout_height="fill",--布局高度 

-- ↹布局边距 
 layout_margin="8dp",--布局边距

-- ∧布局顶距 
 layout_marginTop="15dp",--布局顶距

-- ＜布局左距
 layout_marginLeft="4%w",--布局左距

-- ＞布局右距
 layout_marginRight="4%w",--布局右距

-- ∨布局底距
 layout_marginBottom="15dp",--布局底距

-- 布局填充
 padding="2dp",--布局填充 
```


- gravity属性

```lua
gravity="center",--顶：top｜中：center｜左：left｜右：right｜底：bottom 

-- 重力居顶↑置中
 gravity="top|center",--重力居顶｜置中 

-- 重力居底↓置中
 gravity="bottom|center",--重力居底｜置中 

-- 重力居顶置左 
 gravity="top|left",--重力居顶｜置左 

-- 重力居顶置右 
 gravity="top|right",--重力居顶｜置右 

--重力居左←置中
 gravity="left|center",--重力居左｜置中

-- 重力居右→置中 
 gravity="right|center",--重力居右｜置中

-- 重力居左置底 
 gravity="left|bottom",--重力居左｜置底

-- 重力居右置底 
 gravity="right|bottom",--重力居右｜置底
```

- 视图路径

```lua
 src="drawable/icon.png",--视图路径
```

- 图片颜色

```lua 
 colorFilter="#ffffff",--图片颜色 
```

- 图片显示类型 

```lua
 scaleType="fitXY",--图片显示类型：centerCrop 
```

- 文本内容 

```lua
 text="文本内容",--文本内容
``` 

- 文本大小

```lua
 textSize="16sp",--文本大小 
```

- 文本颜色 

```lua
 textColor="#ffffff",--文本颜色
``` 

- 文本显示类型

```lua
 typeface=Typeface.DEFAULT_BOLD,--文本显示类型
``` 

- 文本可选复制

```lua
 textIsSelectable=true,--内容可选复制
``` 

- 圆角半径

```lua
 radius="10dp",--圆角半径
```

- 卡片提升 

```lua
 cardElevation="12dp",--卡片提升
```

- 阴影层次

```lua
 elevation="4dp",--阴影层次
``` 

- 卡片背景色

```lua
 cardBackgroundColor="#ffffff",--卡片背景色
```

- 纽扣背景色

```lua
 backgroundColor="#8EC0E4",--背景色
``` 

- 控件显示/隐藏/不可视

```lua
 visibility=8,--不可视4--隐藏8--显示0
``` 

- 控件透明度

```lua
 alpha=0.6,--控件透明度
```

- 开关控件颜色 

```lua
 填写控件ID.ThumbDrawable.setColorFilter(PorterDuffColorFilter(0xffff0000,PorterDuff.Mode.SRC_ATOP))--开关控件颜色
```

- 进度条颜色 

```lua
 填写控件ID.IndeterminateDrawable.setColorFilter(PorterDuffColorFilter(0xffff0000,PorterDuff.Mode.SRC_ATOP))--进度条颜色 
```

- 隐藏光标

```lua
 cursorVisible=false,--false隐藏,true则为显示
```

- 隐藏圆弧阴影 

```lua
 overScrollMode=View.OVER_SCROLL_NEVER,--隐藏圆弧阴影 
```

- 输入法｜Enter键

```lua
 imeOptions="actionSearch",--输入法Enter键
```

- 编辑框属性

```lua
--编辑框｜限制最多输入 
 maxLength="10",--限制最多输入文字
 

--编辑框｜只可输入数字 
 inputType="number",--设置只可输入数字

--编辑框｜禁止换行输入 
 singleLine=true,--禁止换行输入


--编辑框｜隐藏为*号 
 password=true,--自动隐藏为*号 

--编辑框｜文字过长隐藏 
 ellipsize="end",--文字过长自动隐藏

--编辑框｜气泡提示 
 error="请输入",--气泡提示 

--编辑框｜为空时显示 
 hint=" 请输入"--内容为空时显示

--禁用编辑框 
focusable=false,--禁用编辑框
```

- 禁止弹出输入法 

```lua
 focusableInTouchMode=true,--禁止弹出输入法
```


- 滚动条

```lua
--隐藏纵向滑条 
 verticalScrollBarEnabled=false,--隐藏纵向滑条

--隐藏横向滑条 
 horizontalScrollBarEnabled=false,--隐藏横向滑条
```

- 控件属性

```lua
--控件是否可使用 
 enabled=false,--是否可使用

--控件是否可点击 
 focusable=true,--是否可点击
```

- 调用系统窗口 

```lua
 fitsSystemWindows=true,--调用系统窗口 
```
