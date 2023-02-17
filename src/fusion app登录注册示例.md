## 一、前言
在常见的app中，需要用户登录后才能使用app，本节我们使用fusion app制作一个登录页面，登录成功之后再跳转到app主页。

## 二、准备工作

下载水仙app和fusion app重制版，在后台回复【水仙】和【fa】即可获取下载链接。

## 二、工程配置

### 2.1.fusion app配置

- **新建工程**

在主页点击加号新建工程-->选择空白模板，再点击创建，创建完成按如下配置：

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-12-10-38-05-478_com.jpg)

- **增加子页面**

在子页面，点击+号，选择底栏模板，页面名称“哔哩哔哩”。注意这里的页面名称需要和代码中`进入子页面("哔哩哔哩")`中的文字匹配，这也是fa实现子页面跳转的关键。

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-12-11-10-42-056_com.jpg)

再点击刚建好的子页面，在程序启动事件中增加如下代码：

```lua
加载网页("https://m.bilibili.com/index.html")
```

![](https://gitee.com/teisyogun/images/raw/master/IMG_20230212_111745.jpg)


- **增加程序启动事件**

在主页面（左上角显示为工程编辑的是主页面）自定义事件-->程序启动中，增加如下代码：
```lua
layout={
  LinearLayout;
  layout_height="fill";
  layout_width="fill";
  orientation="vertical";
  {
    LinearLayout;
    layout_height="30%h";
    layout_width="match_parent";
    {
      RelativeLayout;
      layout_height="match_parent";
      layout_width="match_parent";
      {
        TextView;
        layout_height="wrap_content";
        textSize="20sp";
        text=[==[Hello,
欢迎来到 我的视频站]==];
        layout_marginLeft="20dp";
        textColor="0xFF000000";
        layout_marginTop="70dp";
        layout_width="wrap_content";
      };

    };
  };
  {
    LinearLayout;
    layout_height="45%h";
    layout_width="match_parent";
    orientation="vertical";
    {
      CardView;
      layout_height="match_parent";
      id="登录页面";
      layout_width="match_parent";
      {
        RelativeLayout;
        layout_height="match_parent";
        padding="20dp";
        layout_width="match_parent";
        {
          CardView;
          layout_height="45dp";
          id="卡片1";
          radius="10dp";
          backgroundColor="#DCDCDC";
          layout_width="match_parent";
          {
            EditText;
            textColor="0xFF000000";
            hintTextColor="0xFF585858";
            backgroundColor="0x00ffffff";
            InputType='number';
            hint="请输入账号";
            id="user";
            layout_width="match_parent";
          };
        };
        {
          CardView;
          layout_height="45dp";
          id="卡片2";
          layout_below="卡片1";
          layout_marginTop="20dp";
          radius="10dp";
          backgroundColor="#DCDCDC";
          layout_width="match_parent";
          {
            EditText;
            textColor="0xFF000000";
            hintTextColor="0xFF585858";
            backgroundColor="0x00ffffff";
            id="pass";
            hint="请输入密码";
            password="true";
            layout_width="match_parent";
          };
        };
        {
          CardView;
          layout_height="45dp";
          id="卡片3";
          layout_below="卡片2";
          layout_marginTop="20dp";
          radius="10dp";
          backgroundColor="0xFF000000";
          layout_width="match_parent";
          {
            TextView;
            layout_height="match_parent";
            textColor="0xFFFFFFFF";
            id="logod";
            text="登录";
            gravity="center";
            layout_width="match_parent";
          };
        };
        {
          TextView;
          layout_alignParentRight="true";
          textColor="#ff757575";
          text="还没有账号?立刻注册";
          onClick=function()
            注册页面.setVisibility(View.VISIBLE)
            登录页面.setVisibility(View.GONE)
          end;
          layout_marginTop="20dp";
          layout_below="卡片3";
        };
      };
    };
    {
      CardView;
      layout_height="match_parent";
      id="注册页面";
      layout_width="match_parent";
      {
        RelativeLayout;
        layout_height="match_parent";
        padding="20dp";
        layout_width="match_parent";
        {
          CardView;
          layout_height="45dp";
          id="卡片4";
          radius="10dp";
          backgroundColor="#DCDCDC";
          layout_width="match_parent";
          {
            EditText;
            textColor="0xFF000000";
            hintTextColor="0xFF585858";
            backgroundColor="0x00ffffff";
            id="user1";
            hint="请输入账号(5到12位数字)";
            InputType='number';
            layout_width="match_parent";
          };
        };
        {
          CardView;
          layout_height="45dp";
          id="卡片5";
          layout_below="卡片4";
          layout_marginTop="20dp";
          radius="10dp";
          backgroundColor="#DCDCDC";
          layout_width="match_parent";
          {
            EditText;
            textColor="0xFF000000";
            hintTextColor="0xFF585858";
            backgroundColor="0x00ffffff";
            id="pass1";
            hint="请输入密码";
            layout_width="match_parent";
          };
        };
        {
          CardView;
          layout_height="45dp";
          id="卡片6";
          layout_below="卡片5";
          layout_marginTop="20dp";
          radius="10dp";
          backgroundColor="#DCDCDC";
          layout_width="match_parent";
          {
            EditText;
            textColor="0xFF000000";
            hintTextColor="0xFF585858";
            backgroundColor="0x00ffffff";
            hint="请输入用户名";
            id="name1";
            layout_width="match_parent";
          };
        };
        {
          CardView;
          layout_height="45dp";
          id="卡片7";
          layout_below="卡片6";
          layout_marginTop="20dp";
          radius="10dp";
          backgroundColor="0xFF000000";
          layout_width="match_parent";
          {
            TextView;
            layout_height="match_parent";
            textColor="0xFFFFFFFF";
            text="注册";
            id="注册ID";
            gravity="center";
            layout_width="match_parent";
          };
        };
        {
          TextView;
          layout_alignParentRight="true";
          textColor="#ff757575";
          text="已有账号?立刻登录";
          onClick=function()
            登录页面.setVisibility(View.VISIBLE)
            注册页面.setVisibility(View.GONE)
          end;
          layout_marginTop="20dp";
          layout_below="卡片7";
        };
      };
    };
  };
  {
    LinearLayout;
    layout_height="match_parent";
    layout_width="match_parent";
  };
};

activity.setContentView(loadlayout(layout))




-- 上面为布局代码，以下为登录注册的核心代码
local cjson=import "cjson"

admin="512357657"   -- 替换为自己水仙后台的账号，也就是qq号
key="9a712a0c17d598d38bdc"     -- 替换为自己水仙后台的key,水仙app主页，点击我的后台-->右上角三个点-->修改配置
-- 注册
注册ID.onClick=function()
  local url="http://shuixian.ltd/main/api/user/register.php"
  -- 请将下面admin和key等于号的内容替换成自己的水仙后台
  data="admin="..admin.."&user="..tostring(user1.getText()).."&password="..tostring(pass1.getText()).."&name="..tostring(name1.getText()).."&key="..key

  网络模块.提交(url,data,nil,"utf-8",nil,function(code,content,cookie,header)
    if code==200 and content then--成功
      local JSON=cjson.decode(content)
      if JSON.code==1 then
        print("注册成功,请在登录页面登录")
        登录页面.setVisibility(View.VISIBLE)
        注册页面.setVisibility(View.GONE)
      else
        print("注册失败"..JSON.msg)
      end
    else
      print('网络错误或参数错误')
    end
  end)
end

-- 登录
logod.onClick=function()
  local url="http://shuixian.ltd/main/api/user/login.php"
  local data="admin="..admin.."&user="..tostring(user.getText()).."&password="..tostring(pass.getText()).."&key="..key
  网络模块.提交(url,data,nil,"utf-8",nil,function(code,content,cookie,header)
    if code==200 and content then--成功
      local JSON=cjson.decode(content)
      if JSON.code==1 then
        进入子页面("哔哩哔哩")
      else
        print("登录失败"..JSON.msg)
      end
    else
      print('网络错误或参数错误')
    end
  end)
end

```

### 2.2. 水仙app配置

- **打开登录开关和注册开关**

水仙app主页，点击我的后台-->用户系统-->右上键三个点-->修改配置。

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-12-10-59-12-908_com.jpg)


-- **获取管理员账号和key**

管理员账号就是注册水仙app的qq号，在我的页面可以查看，如下图：

![](https://gitee.com/teisyogun/images/raw/master/IMG_20230212_110302.jpg)



key获取方式：水仙app主页，点击我的后台-->右上角三个点-->修改配置。请将2.1代码中admin和key替换为自己的水仙后台账号和key，替换后再运行。


![](https://gitee.com/teisyogun/images/raw/master/mmexport1676032242416.png)



## 三、成果展示

- **注册页面**

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-12-11-26-26-535_com.jpg)

- **登录页面**

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-12-11-26-22-255_com.jpg)

- **登录后的首页**

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-02-12-11-28-45-590_com.jpg)


如果还不知道怎么操作，可以下在我的工程文件，下载完导入即可：

下载链接：

链接:https://pan.baidu.com/s/1dF06LxuySdBYjs45Qodejw 

提取码:okhz



## 四、总结

本文主要使用了fa的子页面跳转，及自定义页面功能，需要一点编程基础，可以先学习下lua的基础课程。欢迎大家点赞加关注，将持续更新fa的相关内容。