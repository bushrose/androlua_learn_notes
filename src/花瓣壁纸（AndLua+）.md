
### 最终效果

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-03-01-20-58-57-925_com.jpg)

### 顶部及软件设置

```lua
require "import"
import "android.app.*"
import "android.os.*"
import "android.widget.*"
import "android.view.*"
import "layout"

activity.setTheme(R.Theme_Blue)
activity.setTitle("花瓣壁纸")
activity.setContentView(loadlayout(layout))



主题标题颜色=tonumber(0xFFAA7174)--黑色
文本背景颜色=tonumber(0xFF3C5087)
activity.setTheme(android.R.style.Theme_DeviceDefault_Light)--设置md主题
--标题栏阴影
activity.ActionBar.setElevation(0)
--设置ActionBar背景颜色
import "android.graphics.drawable.ColorDrawable"
--标题栏
activity.ActionBar.setBackgroundDrawable(ColorDrawable(主题标题颜色))--颜色0xFF4C8DAD
--沉浸栏
activity.getWindow().addFlags(WindowManager.LayoutParams.FLAG_DRAWS_SYSTEM_BAR_BACKGROUNDS).setStatusBarColor(主题标题颜色);----颜色0xFF4C8DAD
--底部导航栏
import "android.graphics.Color"
activity.getWindow().setNavigationBarColor(主题标题颜色)
--弹出消息
function print(文本)
  Toast.makeText(activity,文本,Toast.LENGTH_SHORT).show()
end
```


### 布局代码

```lua
import "android.graphics.Typeface"

设置布局=
{
  LinearLayout,--线性布局
  orientation='vertical',--方向
  layout_width='fill',--宽度
  layout_height='fill',--高度
  --  background='#00FFFFFF',--背景颜色或图片路径


  {
    LinearLayout,--线性布局
    orientation='horizontal',--方向
    layout_width='fill',--宽度
    layout_height='fill',--高度

    {
      ImageView;--图片控件
      layout_gravity='center';--卡片重力
      src='https://www.268608.com/imgs/2022/01/b6ccf4406dc638f7.png';--图片路径
      ColorFilter='#FFEDEDED';--图片着色
      layout_width='40dp',--宽度
      layout_height='40dp';--高度
      --layout_weight='1';--剩余属性
      padding="4dp",--往内部元素的填充一定边距
      id="fanhui_yi";
      onClick=function()--点击事件
        activity.finish()--退出页面
      end
    };

    {
      --Button;--文本控件
      TextView;--文本控件
      layout_gravity='center';--卡片重力
      textColor='#FFFFFFFF';--文字颜色
      -- layout_width='140dp',--宽度
      style = "?android:attr/windowTitleStyle",
      text='花瓣壁纸';--显示文字
      layout_marginLeft='18dp';--左距
      typeface=Typeface.DEFAULT_BOLD,--文本显示类型
      id="shapig";
    };


    {
      LinearLayout,--线性布局
      orientation='vertical',--方向
      layout_width='fill',--宽度
      layout_height='fill',--高度
      gravity='center|right';--重力属性
      --左:left 右:right 中:center 顶:top 底:bottom


      {
        ImageView;--图片控件
        src='https://www.268608.com/imgs/2022/01/63dfd5f60693870f.png';--图片路径
        layout_width='40dp';--宽度
        layout_height='40dp';--高度
        ColorFilter='#FFEDEDED';--图片着色
        padding="6dp",--往内部元素的填充一定边距
        id="caidan"
      };
    }
  };
};

activity.ActionBar.setDisplayShowCustomEnabled(true)
activity.ActionBar.setCustomView(loadlayout(设置布局))


--text=activity.getTitle();
function 波纹(id,颜色)--波纹特效
  import "android.content.res.ColorStateList"
  local attrsArray={android.R.attr.selectableItemBackgroundBorderless}
  local typedArray=activity.obtainStyledAttributes(attrsArray)
  Pretend = activity.Resources.getDrawable(typedArray.getResourceId(0,0))
  Pretend.setColor(ColorStateList(int[0].class{int{}},int{颜色}))
  id.setBackground(Pretend.setColor(ColorStateList(int[0].class{int{}},int{颜色})))
end
波纹(fanhui_yi,0xffffffff)
波纹(caidan,0xffffffff)

caidan.onClick=function()--点击事件

  --简单对话框
  AlertDialog.Builder(this).setTitle("关于")
  .setMessage("①使用软件免费！")
  .setPositiveButton("联系作者",{onClick=function()
      function 联系QQ(账号)
        import "android.content.Intent"
        import "android.net.Uri"
        activity.startActivity(Intent(Intent.ACTION_VIEW,Uri.parse("mqqwpa://im/chat?chat_type=wpa&uin="..账号)))
      end
      --调用方法
      联系QQ(xxxxxxxx)

    end})
  --设置积极按钮
  .setNegativeButton("取消",nil)--设置否认按钮
  .show();
end;


import "android.graphics.Typeface"

layout=
{
  LinearLayout,--线性布局
  orientation='vertical',--方向
  layout_width='fill',--宽度
  layout_height='wrap',--高度
  background='#FFF1F2F3',--背景颜色或图片路径



  {
    PullingLayout;--Pulling刷新
    PullUpEnabled=true;--上拉刷新
    --PullDownEnabled=true;--下拉刷新
    layout_width='fill';--布局宽度
    --layout_height='';--布局高度
    --   layout_margin='2%w';--边距
    id="刷新";

    {
      GridView,--网格视图
      numColumns=2,--单排显示数
      layout_width="fill",--宽度
      layout_height="wrap",--高度
      VerticalScrollBarEnabled=false,
      -- OverScrollMode=2,--线条
      id="list"
    };
  };
};
activity.setContentView(loadlayout(layout))--布局视图



item=

{
  LinearLayout,--线性布局
  orientation='vertical',--方向
  layout_width='fill',--宽度
  layout_height='wrap',--高度
  --  background='#00FFFFFF',--背景颜色或图片路径

  {
    CardView;--卡片控件
    layout_margin='5dp';--边距
    layout_gravity='center';--重力
    --左:left 右:right 中:center 顶:top 底:bottom
    elevation='0dp';--阴影
    layout_width='fill';--宽度
    layout_height='wrap';--高度
    --CardBackgroundColor='#FFB2B2B2';--颜色
    radius='8dp';--圆角

    {
      LinearLayout,--线性布局
      orientation='vertical',--方向
      layout_width='fill',--宽度
      padding="8dp",--填充边距
      {
        CardView;--卡片控件
        layout_margin='5dp';--边距
        layout_gravity='center';--重力
        --左:left 右:right 中:center 顶:top 底:bottom
        elevation='0dp';--阴影
        layout_width='fill';--宽度
        layout_height='70%w';--高度
        -- CardBackgroundColor='#ffffffff';--颜色
        radius='8dp';--圆角


        {
          ImageView;--图片控件
          src='';--图片路径
          layout_width='fill';--宽度
          layout_height='fill';--高度
          scaleType='fitXY';--图片显示类型
          id="tup";
        };

      };

      {
        LinearLayout,--线性布局
        orientation='vertical',--方向
        layout_width='fill',--宽度
        layout_height='wrap',--高度
        padding="6dp",--填充边距
        {
          TextView;--文本控件
          --    gravity='center';--重力属性
          --左:left 右:right 中:center 顶:top 底:bottom
          --layout_width='50dp',--宽度
          layout_height='35dp',--高度
          textColor='#eb000000';--文字颜色
          text='名称';--显示文字
          textSize='14dp';--文字大小
          id="mingc"

        };

        {
          TextView;--文本控件
          text='图片链接';--显示文字
          visibility=8,--不可视4--隐藏8--显示0
          id="tp"
        };
      };
    };
  };
};
```

### 复制及下载图片

```lua
adp=LuaAdapter(activity,item)
list.Adapter=adp
--列表项目被单击
list.onItemClick=function(l,v,p,i)
  local 下载链接=(v.Tag.tp.text)
  local 名称链接=(v.Tag.mingc.text)
  --普通对话框
  AlertDialog.Builder(this)
  .setTitle("提示?")
  .setMessage(名称链接)
  .setPositiveButton("下载",{onClick=function(v)
      --导入包
      import "android.net.Uri"
      import "android.content.Context"
      -- import "android.app.DownloadManager"
      --调用系统下载
      downloadManager=activity.getSystemService(Context.DOWNLOAD_SERVICE);
      url=Uri.parse(下载链接);
      request=DownloadManager.Request(url);
      request.setAllowedNetworkTypes(DownloadManager.Request.NETWORK_MOBILE|DownloadManager.Request.NETWORK_WIFI);
      request.setDestinationInExternalPublicDir("保存图片",名称链接..".png");
      request.setNotificationVisibility(DownloadManager.Request.VISIBILITY_VISIBLE_NOTIFY_COMPLETED);
      downloadManager.enqueue(request);
      print("/storage/emulated/0/保存图片")

    end})
  .setNeutralButton("取消",nil)
  .setNegativeButton("复制",{onClick=function()--长按事件
      import "android.content.Context"
      activity.getSystemService(Context.CLIPBOARD_SERVICE).setText(下载链接)
      print("已复制链接")

    end; })
  .show()
end
```


### 爬取代码

```lua
页数=1
function 爬取图片(页数)
  --黄鸟抓包链接
  链接url="https://huaban.com/search/?q=%E5%A3%81%E7%BA%B8&category=beauty&page="..页数.."&per_page=20&wfl=1"
  Http.get(链接url,nil,function(a,b)
    if a==200 then
      数据=b:match('<div class="waterfall">(.-)<div class="label">')
      for v,k,in 数据:gmatch('<a class="main%-img"(.-)</div>') do
        名称=v:match('alt="(.-)"')
        图片=v:match('src="(.-)"')
        adp.add({
          tup="https:"..图片,
          tp="https:"..图片,
          mingc=名称,

        })
      end
    end
  end)
end

爬取图片(页数)
刷新.onLoadMore=function(v)
  页数=页数+1
  爬取图片(页数)
  v.loadmoreFinish(0)
end

```