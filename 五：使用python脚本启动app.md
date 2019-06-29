# 五：使用python脚本启动app

> ## 代码部分

```python
from appium import webdriver

capabilities={
  "platformName": "Android",
  "platformVersion": "5.1.1",
  "deviceName": "127.0.0.1:62001",
  "appPackage": "cn.com.open.mooc",
  "appActivity": "cn.com.open.mooc.ui.loading.MCLoadingActivity"
}

driver=webdriver.Remote('http://localhost:4723/wd/hub',capabilities)
```



> ## 需要注意的是

```python
一：首先需要手动启动appium server
二：web.Remote() 里面的url 中的端口号4723 是在appium desktop 中的日志获取的，还有/wd/hub 是固定的
三：每次运行脚本要确保 adb devices 能获取到设备信息 模拟器获取的就是"127.0.0.1:62001", 真机获取到的是uuid
```



> ## 测试视频如下

<video src="D:\Program Files(x86)\typora\vedio\appium_1 脚本启动app.mp4"></video>





> ## 使用本地APK 安装到模拟器并启动APP

```python
首先下载apk 到本地计算机
在capabilities 中添加一个key
    'app':r'绝对地址'
    'app':r'D:\chrome download\imooc7.2.010102001android.apk'
    'appActivity':'com.imooc.component.imoocmain.splash.GuideActivity'
需要注意的是apk 版本不一样启动类不一样

capabilities={
  "platformName": "Android",
  "platformVersion": "5.1.1",
  "deviceName": "127.0.0.1:62001",
  'app':r'D:\chrome download\imooc7.2.010102001android.apk',
  "appPackage": "cn.com.open.mooc",
  'appActivity':'com.imooc.component.imoocmain.splash.GuideActivity'
}
```





> ### 测试视频如下

<video src="D:\Program Files(x86)\typora\vedio\appium_2 安装并启动app.mp4">

