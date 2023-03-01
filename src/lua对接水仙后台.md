
### 前言

水仙后台提供了丰富的api，由于官方只提供了iapp对接示例，文章将使用lua对接水仙后台。适用于FA、FA2、AndLua+、AIDE lua、Simple lua等，只要软件支持网络请求，文章中的方法都适用。


### api封装

```lua
shuixian={
    api=function(moduleName,method,postdata,call)
        local url="http://shuixian.ltd/main/api/"
        Http.post(url..moduleName.."/"..method..".php",postdata,function(code,content,cookie,header)
            call(code,content,cookie,header)
        end)
    end   
}
```

### 食用方法

- 导入模块 或将上面代码复制到自己的代码中，复制代码就不需要导入

```import "shuixian"```

- 调用方法

shuixian.api(模块名,方法名,提交参数(可为表或字符串),返回参数)

例子：以用户系统-用户注册为例


```lua
shuixian.api("user","register",postdata,function(code,content,cookie,header))


--[[

在水仙后台找到对应系统对应方法的提交接口，如注册接口：
http://shuixian.ltd/main/api/user/register.php

则上面方法的模块名和方法名如下：
http://shuixian.ltd/main/api/{模块名}/{方法名}.php



postdata说明：

以用户系统注册接口为例，官方示例如下：
提交参数{
    admin=管理员账号
    user=注册账号
    password=账户密码
    name=注册昵称
    mail=邮箱(未开启验证码注册不需要填)
    code=验证码(未开启验证码注册不需要填)
    key=后台的key(未开启key则不需要填)
}

postdata={
    admin="管理员账号",
    user="注册账号",
    password="",
    name="注册昵称",
    mail="邮箱(未开启验证码注册不需要填)",
    code="验证码(未开启验证码注册不需要填)",
    key="后台的key(未开启key则不需要填)"
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
import "shuixian"
import "cjson"

postdata={
    admin="自己在水仙的管理员账号，就是个人中心的qq号",
    -- 管理员账号
    user="1234567",
    -- 注册用户的账号
    password="dx12345",
    -- 注册用户的密码
    name="张三"
}
-- mail,code,key 看是否在个人后台开启，如开启在postdata中添加参数即可



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

shuixian.api("user","register",postdata,function(code,content,cookie,header)
    if(code==200) then
        local result=cjson.decode(content)
        if(result.code==1) then
            print("注册成功")  -- 编写自己的业务处理代码
        elseif(result.code==0) then
            print("注册失败-"..result.msg) -- 编写自己的业务处理代码
        else
            print("程序错误-"..result.msg) -- 编写自己的业务处理代码
        end
    else

    end
end)


```


### 总结

对接返回json格式数据的api，就是一个json解析的操作，通过软件自带的网络请求模块即可完成我们的需求。

---