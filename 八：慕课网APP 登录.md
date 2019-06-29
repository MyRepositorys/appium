# 八：慕课网APP 登录



> ### 流程分析

```python
APP的使用分为首次使用和非首次使用，APP页面是不一样的
首次使用,有 海报，个人标签，618广告
非首次使用 只有APP广告然后直接进入主页
登录，分两种情况
	1. 未登陆过，首先出现的是主页页面，在注册页面跳转到登录页面
    2.登陆过，直接跳转到登录页面
执行流程图如下：
```

<img src="D:\Program Files(x86)\typora\image\imooc_app_login.PNG">



> ### 代码如下

```python
from appium import webdriver
from selenium.common.exceptions import NoSuchElementException
from selenium.webdriver.support.select import By
from selenium.webdriver.common.action_chains import ActionChains
import time
class RebuilderLogin():

 capabilities = {
         "platformName": "Android",
         "platformVersion": "8.0.0",
         "deviceName": "SJE0217427004743",
         'noReset': True,
         "appPackage": "cn.com.open.mooc",
         'appActivity': 'com.imooc.component.imoocmain.splash.MCSplashActivity'
    }


 def __init__(self):
     self.driver = webdriver.Remote('http://localhost:4723/wd/hub', self.capabilities)
     self.driver.implicitly_wait(5)

 def __call__(self):
    return self.driver

    #验证页面是否有指定元素
 def findElement(self,str, path):
    if str == 'id':
            attr = By.ID
    elif str == "class":
            attr = By.CLASS_NAME
    elif str == "text":
            attr = By.LINK_TEXT
    elif str == "XPATH":
            attr = By.XPATH
    elif str == "CSS_SELECTOR":
            attr = By.CSS_SELECTOR
    try:
        ele = self.driver.find_element(attr, path)
    except NoSuchElementException:
        return [False, None]
    return [True,ele]

 def login(self):
    userName = self.findElement('id', 'cn.com.open.mooc:id/accountEdit')
    if userName[0] == True:
        userName[1].clear()
        time.sleep(1)
        userName[1].send_keys('17621973097')

    pwd = self.findElement('id', 'cn.com.open.mooc:id/passwordEdit')
    if pwd[0] == True:
        pwd[1].clear()
        time.sleep(1)
        pwd[1].send_keys('Qiuqwe@!&^')

    login_btn = self.findElement('id', 'cn.com.open.mooc:id/login')
    if login_btn[0] == True:
        login_btn[1].click()

 def afterFirstUseApp(self):

    # 点击广告页面的'跳过按钮'
    try:
        jump_over = self.driver.find_element(By.CLASS_NAME, "android.widget.TextView")
    except NoSuchElementException:
        print("没找到jump_over")
    jump_over.click()



 def firstLoginOrRepeatlyLogin(self,isFirstUseApp=None):

    if isFirstUseApp!=True:
        self.afterFirstUseApp()

    # 点击底部栏的登录按钮
    try:
        account = self.driver.find_element(By.ID, "账号")
        account.click()
    except NoSuchElementException:
        print("suck it")

    # 点击账号页面'点击登录'
    self.driver.find_element(By.CLASS_NAME, "android.widget.TextView").click()

    # 验证当前页面是否是注册页面
    isRegister = self.findElement('id', 'cn.com.open.mooc:id/tv_register_tips')
    if isRegister[0] == False:
        self.login()
    else:
        # 点击注册页面"登录按钮"
        self.driver.find_element(By.ID, "cn.com.open.mooc:id/right_text").click()
        self.login()
    print("--------process down------------------")


rl=RebuilderLogin()
driver=rl()
rl.firstLoginOrRepeatlyLogin()
```





```python
from appium import webdriver
from appium_test.reBuildLogin import RebuilderLogin
import time

#初始化driver
rl=RebuilderLogin()
driver=rl()

#验证是否是第一次使用APP,结果返回[True/False, WebElement/None]
def isFirstOpenApp():
  return rl.findElement('class','android.widget.ImageView')

def swipePageLeftOrRight(derection,times):
  size = driver.get_window_size()
  width = size['width']
  height = size['height']
  if derection=='left':
    start_x=width * 0.9
    end_x=width *0.1
  else:
    start_x=width * 0.1
    end_x=width *0.9
  while (times>0):
    driver.swipe(start_x, height * 0.5, end_x, height * 0.5)
    times=times-1

if isFirstOpenApp()[0]==True:
  swipePageLeftOrRight('left',3)

#点击立即体验
rl.findElement('class','android.widget.ImageView')[1].click()

#点击属性标签页的跳过
rl.findElement('id','cn.com.open.mooc:id/tvSkip')[1].click()
time.sleep(3)
#取消首次使用app的广告
driver.swipe(530,1400,530,1400,50)
print('-------------process execute there----------')
time.sleep(3)
print('-------------before login----------')
rl.firstLoginOrRepeatlyLogin(True)
```



```python
RebuilderLogin类中的方法：
__init__():	初始化方法使用capabilities={} 初始化self.driver，需要注意的是self.driver是初始化实例中变量的driver，如果不加self. RebuilderLogin 是获取不到driver的
__call__: 这个是实例方法 install() 获取driver 用的
findElement(): 该方法是对find_element(By,selector)的再一次封装，因为find_element有可能定位不到元素，所以使用try except 进行封装，将结果以列表[True/False,WebElement/None] 返回
login(): 将登陆操作封装起来，方便复用，其中首次登陆，非首次登陆，用户名框有无默认值的情况，所以需要先clear()，然后再send_keys()
afterFirstUseApp(): 用于非首次使用APP，跳过广告
firstLoginOrRepeatlyLogin():登录前的操作，登录，需要点击底部菜单栏'账号'-->'点击登录'--'注册/登录页面'，对这些动作进行封装
swipePageLeftOrRight():这个方法是针对于首次使用APP，页面出现海报，封装的，需要左右滑动
```







> ### 遇到的问题

```python
首先 UiAutomator 定位是不准确的
其次，当遇到定位不准确的时候可以使用坐标进行点击在上面代码中swipe(500,1400,500,1400)就是使用(x,y)坐标进行点击
如何是的APP 像第一次使用，在应用里 找到对应APP 把APP data 清除即可
```





> ### 测试视频如下

 1. case_1 首次使用APP 进行登录

    <img src="D:\Program Files(x86)\typora\vedio\慕课网登录case_1.gif">



2.  case 2 非首次使用APP，首次登录

   <img src="D:\Program Files(x86)\typora\vedio\慕课网登录case_2.gif">



3. case 3 非首次使用APP 非首次登录

   <img src="D:\Program Files(x86)\typora\vedio\慕课网登录case_3.gif">

