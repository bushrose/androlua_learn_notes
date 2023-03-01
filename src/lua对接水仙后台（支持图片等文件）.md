
### 前言

上一篇文章中写了lua对接水仙后台，不过发现不能支持图片上传，比如修改头像等，支持修改头像。


### api封装

```lua
require "import"
import "http"
shuixian={
    post=function(moduleName,method,postdata,filedata,call)
        local url="http://shuixian.ltd/main/api/"
        if(filedata==nil) then
            content,cookie,code,header=http.post(url..moduleName.."/"..method..".php",postdata)
            call(code,content,cookie,header)
        else
           content,cookie,code,header=http.upload(url..moduleName.."/"..method..".php",postdata,filedata)
           call(code,content,cookie,header) 
        end
    end   
}
```

### 食用方法

- 导入模块 或将上面代码复制到自己的代码中，复制代码就不需要导入

```import "shuixian"```

- 调用方法

shuixian.api(模块名,方法名,提交参数(可为表或字符串),文件参数(可为表或字符串),返回参数)

例子：以用户系统-用户注册为例


```lua
shuixian.api("user","register",postdata,function(code,content,cookie,header))

--[[
在水仙后台找到对应系统对应方法的提交接口，如用户修改接口：
http://shuixian.ltd/main/api/user/user_set.php

则上面方法的模块名和方法名如下：
http://shuixian.ltd/main/api/{模块名}/{方法名}.php


postdata说明：

以用户系统-用户修改接口为例，官方示例如下：
提交参数{
admin=管理员账号
user=用户账号
password=用户密码
project=要修改的信息(例:name、signatrue、password、head、wallet)
例如:
  project=name(修改昵称)
  name=要修改的昵称
  
  project=signatrue(修改签名)
  signatrue=要修改的签名
  
  project=password(修改密码)
  new_password=要修改的新密码
  
  project=head(修改头像)
  
  project=wallet(扣除用户积分)
  num=扣除的数量
  
  project=mail(修改邮箱)
  mail=新邮箱
  code=验证码
}

-- 以修改头像为例
postdata={
    admin="管理员账号",
    user="注册账号",
    password="用户密码",
    project="head"
}

filedata={
    head="/storage/emulated/0/Pictures/Image.jpg"   -- 头像图片的路径
}


返回参数说明：
code：响应代码，2xx表示成功，4xx表示请求错误，5xx表示服务器错误，-1表示出错
content：内容，如果code为-1，则为出错信息
cookie：服务器返回的用户身份识别信息
header：服务器返回的头信息


解析返回内容：

使用cjson等json包解析
result=cjson.decode(content)
if(result.code==1) then
    print("注册成功")
elseif(result.code==0) then
    print("注册失败-"..result.msg)
else
    print("程序错误-"..result.msg)
end

]]
```

- 测试案例

```lua
import "cjson"
import "http"

shuixian={
    post=function(moduleName,method,postdata,filedata,call)
        local url="http://shuixian.ltd/main/api/"
        if(filedata==nil) then
            content,cookie,code,header=http.post(url..moduleName.."/"..method..".php",postdata)
            call(code,content,cookie,header)
        else
           content,cookie,code,header=http.upload(url..moduleName.."/"..method..".php",postdata,filedata)
           call(code,content,cookie,header) 
        end
    end   
}

postdata={
    admin="自己在水仙后台的管理员账号，也就是qq号",
    user="注册账号",
    password="",
    project="head",
    key="在后台修改配置的key"
}
-- key 看是否在个人后台开启，如开启在postdata中添加参数即可

-- 无文件上传的接口，filedata参数传nil即可
filedata={
    head="/storage/emulated/0/Pictures/Image.jpg"   -- 头像图片的路径
}

shuixian.api("user","user_set",postdata,filedata,function(code,content,cookie,header)
    if(code==200) then
        local result=cjson.decode(content)
        if(result.code==1) then
            print("修改成功")  -- 编写自己的业务处理代码
        elseif(result.code==0) then
            print("修改失败-"..result.msg) -- 编写自己的业务处理代码
        else
            print("程序错误-"..result.msg) -- 编写自己的业务处理代码
        end
    else

    end
end)

--[[

返回参数的多层级的json，如举报记录接口，查看文档返回如下参数：

返回参数{
code=响应码(0失败，1成功，-1程序错误)
msg=响应信息
data{
 id=id
 user=举报用户
 name=用户昵称
 head=用户头像
 content=举报内容
 time=举报时间
 state=受理状态
 result=受理内容
 }
}

如：
获取举报用户，result.data.user即可
]]

```


### 总结

对接返回json格式数据的api，就是一个json解析的操作，通过软件自带的网络请求模块即可完成我们的需求。

---