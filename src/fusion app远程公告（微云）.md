
### 前言

在app中经常会有发送公告的需求，告知用户一些重大的事情。本文将使用FA重置版和qq收藏的笔记功能完成远程公告的功能。

### 远程公告的思路

1. 在qq收藏新建笔记，设置好公告内容
2. 分享笔记给好友，拿到外部链接地址
3. FA发送http请求，解析出公告内容

### 在qq收藏新建笔记，设置好公告内容

- 点击头像，在点击收藏

![](https://gitee.com/teisyogun/images/raw/master/IMG_20230216_213805.jpg)

- 点击右上角加号

![](https://gitee.com/teisyogun/images/raw/master/IMG_20230216_213856.jpg)

- 按照以下格式输入以下内容。

```
【公告标题】这是FA的公告标题【公告标题】
【公告内容】这是公告内容【公告内容】
【公告显示】开【公告显示】
【按钮标题】关闭【按钮标题】
【公告返回】关【公告返回】
【暗主题】关【暗主题】

```

每一块控制不同的显示效果

![](https://gitee.com/teisyogun/images/raw/master/mmexport1676556511549.png)

在笔记中录入：
![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-16-21-35-35-414_com.jpg)


### 分享笔记给好友，拿到外部链接地址

点击分享的链接，再点击右上角三个点，再点击复制链接。保存好这个链接，下一步需要用。
![](https://gitee.com/teisyogun/images/raw/master/IMG_20230216_215127.jpg)


### FA发送http请求，解析出公告内容

在FA新建工程，如何新建项目，不再赘述，可以前面的文章。把以下代码粘贴到程序启动事件中，将第一行的链接替换为上一步拿到的链接。

```lua

-- 代码来源于网络

url="https://sharechain.qq.com/c2282a70cb92e88f3ebae5c767543a4f"  -- 替换为自己的
local headers={["User-Agent"]="Mozilla/5.0 (Linux; Android 9; STF-AL00 Build/HUAWEISTF-AL00; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/71.0.3578.99 Mobile Safari/537.36"}
Http.get(url.."#t="..os.time(),nil,"UTF-8",headers,function(code,content,cookie,header)
  if(code==200 and content)then
    --这一堆是识别替换QQ远程的乱码
    local content=content:match('<div class="note%-content">(.-)</div>%s+</article>')
    local content=content:gsub("</p ><p>","") or content;
    local content=content:gsub("<%/?p>","") or content;
    local content=content:gsub("</div><div>","") or content;
    local content=content:gsub("<%/?div>","") or content;
    local content=content:gsub("<%/?span>","") or content;
    local content=content:gsub("<br%s+/>","\n") or content;
    local content=content:gsub("&nbsp;"," ") or content;
    local content=content:gsub("</div><div>","") or content;
    local content=content:gsub("！","\n") or content;
    --替换结束
    公告标题=content:match("【公告标题】(.-)【公告标题】")
    公告内容=content:match("【公告内容】(.-)【公告内容】")
    按钮标题=content:match("【按钮标题】(.-)【按钮标题】")
    公告显示=content:match("【公告显示】(.-)【公告显示】")
    公告返回=content:match("【公告返回】(.-)【公告返回】")
    暗主题=content:match("【暗主题】(.-)【暗主题】")
    --暗主图=="开"    --这里手动开暗主题调试
    if(暗主题=="开")then--判断远程明暗主题切换
      UIColor="#222222"
      btColor="#ffffff"
      nrColor="#dfffffff"
     else
      UIColor="#ffffff"
      btColor="#000000"
      nrColor="#98000000"
    end
    公告布局=
    {
      LinearLayout;
      orientation='vertical';
      layout_width='fill';
      layout_height='fill';

      {
        CardView;
        layout_gravity='center';
        layout_width='80%w';
        layout_height='36%h';
        cardBackgroundColor=UIColor;
        layout_margin='0dp';
        cardElevation='2dp';
        radius='15dp';
        {
          LinearLayout;
          orientation='vertical';
          layout_width='fill';
          layout_height='75dp';
          background=UIColor;
          {
            TextView;
            id='bt';
            layout_width='fill';
            layout_height='fill';
            text=公告标题;
            textSize='25sp';
            textColor=btColor;
            gravity='bottom|center';
          };
        };
        {
          LinearLayout;
          orientation='vertical';
          layout_width='fill';
          layout_height='145dp';
          layout_marginTop='75dp';
          background=UIColor;
          {
            TextView;
            id='nr';
            layout_width='fill';
            layout_height='fill';
            layout_margin='35dp';
            text=公告内容;
            textSize='15sp';
            textColor=nrColor;
            gravity='left';
          };
        };
        {
          CardView;
          layout_gravity='bottom|center';
          layout_width='75dp';
          layout_height='35dp';
          layout_marginBottom='15dp';
          cardBackgroundColor='#FF0055FF';
          layout_margin='0dp';
          cardElevation='3dp';
          alpha=0.85;
          radius='15dp';
          {
            TextView;
            id='nn1';
            layout_width='fill';
            layout_height='fill';
            text=按钮标题;
            textSize='16sp';
            textColor='#ffffff';
            gravity='center';
            onClick=function(v)
              tc.dismiss()
            end;
          };
        };
      };
    };
    tc=AlertDialog.Builder(this).show()

    if(公告返回=="开")then
      tc.setCancelable(true)
     else
      tc.setCancelable(false)
    end
    tc.getWindow().setContentView(loadlayout(公告布局));
    import"android.graphics.drawable.ColorDrawable"
    tc.getWindow().setBackgroundDrawable(ColorDrawable(0x00000000));
    tc.getWindow().clearFlags(WindowManager.LayoutParams.FLAG_ALT_FOCUSABLE_IM);
    bt.getPaint().setFakeBoldText(true)
    nr.getPaint().setFakeBoldText(true)
    nn1.getPaint().setFakeBoldText(true)
    if(公告显示=="关")then
      tc.dismiss()
     else
      tc.show()
    end

   else
    print("获取公告失败 "..code)
  end
end)
```

### 最终效果

粘贴保存后运行，看到如下效果，就说明已经完成了。

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-16-21-55-08-434_com.jpg)


### 总结

通过qq收藏和fa，完成了简单的公告功能。除此之外，还可以通过水仙app或蓝奏云等完成类似的功能，等待大家去探索。