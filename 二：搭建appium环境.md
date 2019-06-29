# 二：搭建appium环境



> ### 如何搭建appium 工作环境



```python
前面说过appium 的工作流程 
    脚本-->Appium Server -->UiAutomator-->手机app 执行
在这里脚本使用python 编写
Appium Server 由Appium 提供
UiAutomator 是由AndroidSDK 提供
手机执行 是由谷歌提供的手记模拟器

Appium 是使用Node.js 安装的
AndroidSDK 依赖于JDK

Python脚本是如何与Appium链接呢?
Python 使用 Appium 提供的 Appium-python-Client(API)进行链接的
```





> ### 安装基本的环境



```pyth
先安装JDK 和Node.js
JDK 安装之后使用 java-version 检测
安装androidSDK：
    下载SDK
    配置环境变量ANDROID_HOME    Path->%ANDROID_HOME%\tools;    Path-.%ANDROID_HOME%\platform-tools;

SDK 安装之后使用:adb
    命令行出现Android Debug Bridge version 1.0.31 说明安装成功
Node.js 下载之后安装,然后配置环境变量
    执行node --version 查看是否安装完成

安装appium-python-client
    前面说过这个client 只是python 编写的第三方API,所以使用PIP 安装即可
pip install Appium-Python-Client

安装appium：
    下载当前系统所对应的appium 该appium 是个exe可执行文件 点击执行即可这个appium 其实是个appium dektop 桌面应用里面封装了appium server
我们平常所说的appium 是指appium server,appium 是用node.js 写的,要安装appium可以使用
npm install -g appium 即可
安装之后执行 where appium 查看安装路径
执行appium -v 可以查看appium 版本
```





> ### 手机与电脑连接



```python
我的手机是HUAWEI 手机与电脑连接 电脑-->管理--设备管理器-->Android Phone 属性中看到
```

<img src="D:\Program Files(x86)\typora\image\android_adb_interface.png">

```python
但是我们需要使用adb devices 命令去获取手机ID
在cmd 中键入 adb devices 只出现List of devices attached 说明没有成功的获取Phone Id, 这个原因是手机连接电脑后没有启动USB调试模式
对于华为手机要启动USB 调试模式 在手机设置中开发模式开关是隐藏的, 在关于手机-->手机版本  连续点击7次手机版本才会出现开发模式,在里面启动USB 调试,结果如下：
```

<img src="D:\Program Files(x86)\typora\image\adb_hdb.png">

```python
只有出现了ADB Interface 才能在命令行使用adb devices 命令去获取PhoneID
```

<img src="D:\Program Files(x86)\typora\image\adb_devices.png">



> ### 遇到的问题



``` python
手机截图不了?一直提示错误,
解决思路 更新SDK-TOOLS    如何更新?    使用SDK manager 更新
还是截图不了,查看手机安卓版本,若是8.0以上的,SDK 是不支持的,我的手机是HUWEI 9 借助华为手机助手将版本降到8.0 截图成功
```

