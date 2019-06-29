# 十一：Toast 元素

> ### Toast 简介

```pyth
Android 中的Toast是一种简易的消息提示框，当视图显示给用户，在应用程序中显示为浮动，不会获得焦点，无法被点击，
Toast的意义就是尽可能的不引人注意，同时还向用户提示信息，希望用户看到；
Toast 显示的时间有限，一般3s左右就消失了，因此传统的元素定位是无法定位到的
如下图中的"验证失败过多，请15分钟后再次验证"
```

<img height='330' src='C:\Users\Administrator.MS-201605312249\Desktop\image\Toast.png'>



> ### 获取Toast提示信息的前提条件

```pyt
需要安装appium-uiautomator2-driver
	nmp install appium-uiautomator2-driver
python 中下载了selenium 模块
	pip install selenium
使用管理员身份执行appium-desktop，因为appium server会从"C:\Program Files\Appium\resources\app\node_modules\appium\node_modules\appium-uiautomator2-server\apks" 读取已经安装的了appium-uiautomato2-deriver，否则容易抛异常，没有权限读取该apk	
手机安装 io.appium.uiautomator2.server，这个上一步骤读取apk 就是为了在手机中安装该server的
```



> ### 代码如下

```python
#coding=UTF-8

from selenium.webdriver.support.select import By
from appium import webdriver
from time import sleep
capabilities={
  "platformName": "Android",
  "platformVersion": "8.0.0",
  "deviceName": "SJE0217427004743",
  'noReset':True,
  "automationName":'uiautomator2',
  "appPackage": "com.tal.kaoyan",
  'appActivity':'com.tal.kaoyan.ui.activity.SplashActivity'
}

driver=webdriver.Remote('http://localhost:4723/wd/hub',capabilities)



#输入UserName
userName=driver.find_element(By.ID,"com.tal.kaoyan:id/login_email_edittext")
userName.clear()
userName.send_keys('aaaa')

#输入Pwd
pwd=driver.find_element(By.ID,"com.tal.kaoyan:id/login_password_edittext")
pwd.clear()
pwd.send_keys('aaaaa')

#点击登录
login_btn=driver.find_element(By.ID,'com.tal.kaoyan:id/login_login_btn')
login_btn.click()

print('-------开始登录-------')

# times=5
# while times>0:
#   login_btn.click()
#   sleep(1)
#   times=times-1

error_info="验证失败次数过多，请15分钟后再试"
errorInfo_path="//*[@text=\'{}\']".format(error_info)
errorInfo=driver.find_element(By.XPATH,errorInfo_path)
print(errorInfo.text)

print('---------执行到这---------------')
```







> ### 测试视频如下



<img src='D:\Program Files(x86)\typora\gif\Toast.gif'>

