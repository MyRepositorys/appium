# 四：启动模拟器上的app



> ## 连接模拟器

```python
当前使用的模拟器是夜神
    首先将夜神安装目录下的adb.exe 拷贝覆盖SDK 中的adb.exe
启动夜神模拟器,然后cmd 执行adb devices
    获取devices,也就是127.0.0.1:62001 (因为模拟器是运行在本地的所以只要指定URL:PORT)就可以了

获取要运行的app 的包名和类名
    在模拟器中打开一个app
    执行adb shell 
    键入dumpsys window | grep mCurrentFocus    获取当前运行的app包名和类名
        mCurrentFocus=Window{be59e94 u0 cn.com.open.mooc/cn.com.open.mooc.ui.loading.MCLoadingActivity}
       其中appPackage=cn.com.open.mooc    appActivity=cn.com.open.mooc.ui.loading.MCLoadingActivity
```





> ##  使用appium desktop 启动模拟器app:

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

