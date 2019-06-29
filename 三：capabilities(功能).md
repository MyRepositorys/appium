# 三：capabilities(功能)



> ##  什么是capabilities



```python
- desired capability 作用是配置appium 回话,用于告诉appium 服务器的平台和应用程序，类似于一种协议,desired capability 是一个map 或者说字典
- session的本意是回话的意思，session的起源是因为http协议是无状态的协议，如何保持客户端与服务器的链接(也就是说在一次会话中服务器如何识别客户端)中持续的回话

- 客户端在发起通讯的时候首先发送一个desired capabilities的JSON对象给服务器(其实说JSON对象也不合适,因为http里面都是文不能,应该说多层嵌套的字典),服务器收到后会创建一个session(这个过程类似于B/S结构中服务器在内存中新建一个session对象返回并把对象存到MAP中ID作为KEY 返回给客户端，客户端下次访问的时候带着ID,服务器会尝试使用ID到MAP<session>中获取session,如果能获取到，则使用session中封装的客户端的信息,像capabilities中的内容会被封装到session中)所以说session 指的是持续通话的一种手段

- session的存活时间(有的可以自定义,有的是浏览器实例生命周期有关,打开浏览器---接着关闭浏览器,这个session 就死了,在B/S 结构中无法侦测到浏览器实例的生命周期,在C/S结构中应该能检测到浏览器的生命周期)

- 类似于cookie 应该是细粒度的东西 cookie 是保存在客户端的东西,绑定的是用户而不是浏览器,比如BAIDU在浏览器管理的文件中中写入cookie,当某用户再次访问BAIDU的时候会带上这些COOKIE.在B/S架构中sessionid 往往放在COOKIE中
```







> ## capabilities 参数



```python
首先打开appium desktop
启动appium server
    log日志上有一下信息输出
        [Appium] Welcome to Appium v1.13.0
        [Appium] Appium REST http interface listener started on 0.0.0.0:4723
打开Automatic Server 配置
    配置一下capabilities:
        platformName       Android
        platformVersion    5.1.1
        deviceName         127.0.0.1:62001
        appPackage         cn.com.open.mooc
        appActivity        cn.com.open.mooc.ui.loading.MCLoadingActivity

然后点击start session 并检查模拟器上是否运行我们指定的app
```



> ### capabilities 参数——官网





<img src="D:\Program Files(x86)\typora\image\General capabilities.png">





> ### capabilities 中需要注意的参数

```python
{'noReset':True,"fullReset":True} 
下面图片是appium 的官方解释，我觉得没说清除，下面是我找到的解释
noReset 默认值是False 不会在session回话前clear app data
fullReset 默认值False，fullReset=True 会在session开始前卸载已经存在的APK和test执行后卸载刚安装的APK
关于设置noResrt=False 后 app启动后还是像首次启动那样，是因为appActivity 参数设置的类启动,启动的是app的引导界面
```

<img src="D:\Program Files(x86)\typora\image\options_reset.PNG">

