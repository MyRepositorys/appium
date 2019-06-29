# 九 appium 中的一些定位方式

* 

  ```python
  ID 定位，使用的是元素ID 属性值，需要注意的是页面中存在<frame>类似的子页面，ID 可能有多个，或者是上传图片的时候，图片ID 值也是一致的
  ```

*  

  ```python
  CLASS NAME 定位，这个在页面中可能存在多个的，一般情况配合层级定位/相对定位使用
  ```

* 

  ```python
  XPATH 定位 这个是使用元素的绝对路径和相关属性来进行定位的，但是定位效率低，而且PATH字符串太长
  ```

  | 表达式     |                                                           |
  | ---------- | --------------------------------------------------------- |
  | /          | 从根节点开始匹配                                          |
  | //selector | 从匹配selector 的节点开始匹配接下来的表达式               |
  | NodeName   | 就是选取此节点的所有子节点                                |
  | .          | 选取当前节点                                              |
  | ...        | 选取当前节点的父节点                                      |
  | @          | 选取属性;如[@text="value"] 表示匹配属性text="value"的节点 |

  | 通配符 | 描述               |
  | ------ | ------------------ |
  | *      | 匹配任何元素       |
  | @*     | 匹配任何属性节点   |
  | node() | 匹配任何类型的节点 |

  

* 

  ```python
  LIST 定位，这个定位就是WebDriver中的find_elements_by_xxx() 获取的是一组选组
  应用场景如下：
  	当在APP 中上传图像的时候，打开本地相册的时候，会发现所有的图像的ID 是一致的，这个时候就可以使用list定位，然后使用索引下标的方式指定[index] 第几张图片,
      或者是下拉菜单的选项，ID值也都可能是一致的
  ```



* ```pyt
  UiAutomator 定位是安卓系统原生的定位方式，且支持元素的全部属性定位，定位原理是通过android的android uiatumator的类库与查找元素，Appium 元素定位是基于UiAutomator 定位再次封装的
  使用的方法：
  	find_element_by_android_uiautomator('new UiSelector().resourceId("ID")')
  	find_element_by_android_uiautomator('new UiSelector().className("CLASS NAME")')
  	find_element_by_android_uiautomator('new UiSelector().text("textValue")')
  	
  ```

  

