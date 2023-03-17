
### 实现效果

- 使用wifi

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-03-13-21-27-50-689_com.jpg)


- 使用流量

![](https://gitee.com/teisyogun/images/raw/master/Screenshot_2023-03-13-21-25-38-510_com.jpg)


### 源码

```lua
--程序启动时会执行的事件
--程序启动事件
--网络检测
manager = activity.getSystemService(Context.CONNECTIVITY_SERVICE); 
gprs = manager.getNetworkInfo(ConnectivityManager.TYPE_MOBILE).getState(); 
if tostring(gprs)== "CONNECTED" then
  --连接
  print("你娃儿流量真多")
  --上面括号内容可任意修改或者删除print打印事件
else
  connManager = activity.getSystemService(Context.CONNECTIVITY_SERVICE)
  mWifi = connManager.getNetworkInfo(ConnectivityManager.TYPE_WIFI);
  if tostring(mWifi):find("none") then
    --未连接
    print("网络未连接")
    --上面括号内容可任意修改(不建议删除)
  else
    --连接
    print("正在使用WIFI网络")
    --上面括号内容可任意修改或者删除print打印事件
  end
end
```

### 总结

网络检测为常见功能，判断app是否处于正常环境，或处于wifi网络时再进行下载等相关操作。

