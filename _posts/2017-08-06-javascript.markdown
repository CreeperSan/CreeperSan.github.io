---
layout:     post
title:      "一些关于JS"
date:       2017-08-06 9:45:00
author:     "CreeperSan"
header-img: "img/post/170507about/header.jpg"
tags:
    - Javascript
    - 网页
---
## Javascript

> 图片来自[慕课网](https//www.imooc.com)，内容为慕课网和自己总结

### 入门
+ 在html中插入javascript，使用标签
	```
    <script type="text/javascript">
    	这里是代码
    </script>
    ```
+ 在html中插入外部js文件,值得注意的是在JS文件中不需要script标签，直接编写就好了，如下
	```
    //index.xml
    <script src="script.js"></script>
    //script.js
    alert("代码")
    ```
+ 关于JS应该放置的位置，我们可以在xml文档的任意位置放置JavaScript代码，但是我们一般放置在网页的head和body部分。javascript作为一种脚本语言可以放在html页面中任何位置，但是浏览器解释html时是按先后顺序的，所以前面的script就先被执行。比如进行页面显示初始化的js必须放在head里面，因为初始化都要求提前进行（如给页面body设置css等）；而如果是通过事件调用执行的function那么对位置没什么要求的。
+ 其语句规范与Java类似，以分号 ; 作为一条语句的结束。其实分号也可以不写...
+ 注释，和Java一毛一样
+ 变量的定义，使用关键字 var ，变量名字必须以字母，下划线，或者美元符号开始命名一个变量。其他的都大同小异。还有，变量需要先声明再赋值，而且变量可以声明就马上使用，但是这样不符合规范，建议还是先声明再使用。变量区分大小写。
JavaScript保留的关键字
![](/img/post/170806javascript/6.jpg)
+ if..else..语句跟Java一毛一样
+ 函数的定义,使用function作为关键字，参考以下例子
	```javascript
    function makeAlert(){
    	alert("函数调用了")
    }
    ```
    一个点击按钮调用函数的例子可以写成这样子
    ```javascript
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>函数调用</title>
    	<script type="text/javascript">
        	context(){
            	alert("函数调用了");
            }
        </script>
    </head>
    <body>
    	<form>
        	<input type="button" value="戳我" onClick="context()">
        </form>
    </body>
    </html>
    ```

### 常用互动方法
+ JS输出内容 ```document.write(内容)``` 可以直接向HTML输出流写内容
	+ 可以直接写值，可以写变量，可以写标识符，也可以写用+连接的字符串啊什么的
	+ 关于输出空格，用这个```&nbsp;```代替空格，参考[链接](http://www.imooc.com/wiki/view?pid=167)
+ JS警告弹窗(alert消息对话框)
	+ ```alert(内容)```
	+ 在对话框关闭前，不能执行其他操作。~~阻塞线程~~
+ JS带确定和取消的对话弹窗 (comfirm对话框)
	+ ```confirm(内容)```，返回值为Boolean，~~也是阻塞的~~
	+ 如下例子所示
		```javascript
        var mymessage = confirm("你是人吗?")
        if(mymessage){
        	//点击了确定
        }else{
        	//点击了取消
        }
        ```
+ JS提问 (prompt对话框)
	+ ``` prompt(str1,str2) ``` ，参数分别为消息对话框中的文字（不可修改），与文本框中的文字（可修改）
	+ 点击确定则返回输入框的内容，反则返回null
+ JS打开新窗口
	+ ```window.open(URL,窗口名称，参数字符串)```，返回值为打开的窗口对象
	+ URL为可选参数，在窗口中要显示网页的网址或路径。如果省略这个参数，或者它的值是空字符串，那么窗口就不显示任何文档。
	+ 窗口名称为可选参数，为被打开的窗口的名称
		+ 由字母，数字和下划线字符组成
		+  _blank：在新窗口显示目标网页
		+  _self：在当前窗口显示目标网页
		+  _top：框架网页中在上部窗口中显示目标网页
		+  相同 name 的窗口只能创建一个，要想创建多个窗口则 name 不能相同。
		+  name 不能包含有空格。
	+ 参数字符串，可选参数，设置窗口参数，各参数用逗号隔开。参数如下图，要注意的是设置参数时要考虑浏览器的兼容性
	![1](/img/post/170806javascript/1.jpg)
	+ 例子
	```javascript
    window.open('http://www.imooc.com','_blank','width=600,height=300,top=100,left=0')
    ```
+ JS关闭窗口
	+ window.close();
	+ 窗口对象.close();

### DOM（文档对象模型）操作
关于DOM(文档对象模型)，我们先看这样一段代码。
![](/img/post/170806javascript/2.jpg)
将其标签节点分解为DOM节点层次图，如下图所示
![](/img/post/170806javascript/3.jpg)
HTML文档可以说是由不同节点构成的一个集合。三种常见的节点如下
1. 元素节点，比如```<html>```,```<body>```,```<p>```，也就是标签
2. 文本节点，内容，比如```<li>这里面就是文本节点</li>```
3. 属性节点，属性，比如```<a hert="这个是就是属性节点">Hello</a>```

+ 通过ID获取元素
	+ ```document.getElementBuId("ID")```，通过标签指定的唯一的ID来找到元素
	+ 如果找到了，则返回HTMLParagraphElement
	+ 如果找不到，则返回null
	+ 此时我们获取到的是一个完整的对象，如果我们相对其进行操作，则需要通过他的属性和方法
+ innerHTML属性
	+ 用于获取或者替换HTML元素的文本节点内容
	+ ```对象.innerHtml``` 其中对象为获取到的元素对象，比如通过上面的方法获取到的元素对象
+ 改变HTML样式
	+ ```对象.style.属性 = 新样式```
	+ 例子
	```javascript
    document.getElementById("con").style.color = "#66ccff"
    ```
	+ 属性对照表，此表只是一小部分的属性表
	![](/img/post/170806javascript/4.jpg)
+ 显示和隐藏 ( display属性 )
	+ ```对象.style.display = 值```
	+ 值的取值有以下
	![](/img/post/170806javascript/5.jpg)
+ 控制类名
	+ className属性设置或返回元素的class属性。
	+ ```对象.classNmae = classname```
	+ 作用
		1. 获取元素的class属性
		2. 为网页内的某个元素指定一个css样式来更改元素的外观
		3. 改变当前标签的内容，比如```<p>```这样的标签，我可以通过这个方法改变成```<h1>```类型。

### JS中数组的一些东西
+ ```var myArray = new Array();``` 创建一个长度不固定的新的空数组，如果输出，则为undefined
+ 可以直接赋值myArray[0] = 20;
+ JS中的数组都是变长的，即使指定了长度，仍然可以把元素存储在规定长度意外
+ 对比一下Java
> 在java（的字符串容器）里，先指定长度可以节省内存空间。因为你不预先指定长度，电脑会默认分配一个32字节的长度，但正常情况下并不需要这么多。虽然这节省的并没有多少，但节省的地方多了你就感觉到了
+ 创建数组时赋值
	1. ```var array = new Array(0,2,5,8,3,6,9)```
	2. ```var array = [0,1,4,7,2,5,8,3,6,9]```
+ 数组.length获得数组长度，length可以赋值来改变数组的长度
+ 数组的方法
	![](11.jpg)
+ 关于数组的排序分几步走
	1. 创建排序方法
		```javascript
        function sortNum(a,b){
        	return a-b//此处为升序,降序为b-a
        }
        ```
    1. 数组调用sort方法
    	```javascript
        myarray.sort(sortNum)
        ```

### 条件判断语句
+ 和JAVA类似
+ 字符串内容比较可以直接用 ==

### 函数
+ 举一个简单的例子
	```javascript
    function sum(a,b){
    	alert(a+b)
    }
    //调用
    sum(100,20)
    ```
+ 函数的的调用
	+ 可以直接在script标签的内容节点中调用
	+ 可以写在input的属性中，为onclick属性，值为要调用的函数的名字()
+ 带返回值的函数
	```javascript
    function add(x,y){
    	return x+y
    }
    ```
+ JS中的三目运算符跟JAVA也一毛一样

### javascript事件响应机制
JavaScript 创建动态页面。事件是可以被 JavaScript 侦测到的行为。 网页中的每个元素都可以产生某些可以触发 JavaScript 函数或程序的事件。比如说，当用户单击按钮或者提交表单数据时，就发生一个鼠标单击（onclick）事件，需要浏览器做出处理，返回给用户一个结果。
+ 主要事件列表
	![](/img/post/170806javascript/7.jpg)
+ onfocus()弹出函数，后无限弹窗的解决办法
	```javascript
    function focus(){
    	alert("233")
        document.getElementById("对象的ID").blur();
    }
    ```
+ onselect需要双击鼠标才能触发
+ onchange 文本框内容改变事件 , 只有当改变了文本框内容，并且焦点消失了以后才会触发这个事件
+ onload 在页面加载完成后才会被调用
+ onunload貌似对chrome浏览器,firefox浏览器没作用
+ 获取input组件的值
	```javascript
    document.getElementById( id名 ).value
    ```

### 对象
+ Date日期对象
	+ 通过new方法创建一个日期对象，如果不传入参数，则日期为当前系统时间
	+ 可以通过传入参数来指定时间
		```javascript
        new Date(2017,6,21)
        new Date('Jun 21, 2017')
        ```
	+ 获取设置日期的方法
		![](/img/post/170806javascript/8.jpg)
   	+ getTime() setTime()拿到的传入的都是时间戳

### 字符串
+ .toUpperCase()，把表写字母变成大写字母
+ .toLowerCase()，把字符串中的字母全部变成小写
+ .length 为字符串长度
+ 其他像charAt,indexOf这些跟Java就一毛一样了
+ subString()与substr貌似是一样的

### Math
Math的对象属性，是静态的
![](/img/post/170806javascript/9.jpg)
Math的对象方法
![](/img/post/170806javascript/10.jpg)
+ 向上取整 Math.ceil(num)
+ 向下取整 .floor(num)
+ 四舍五入取整 .round(num)
+ 随机数.random()，随机的0-1的double

### 浏览器对象
+ window对象
	+ 对象方法如下
	![](/img/post/170806javascript/12.jpg)
+ JS定时器
	+ 分为一次性定时器和间隔性触发定时器
	+ 方法如下
	![](/img/post/170806javascript/13.jpg)
     setInterval(代码,交互时间（ms作为单位）)，返回一个可以传递给 clearInterval() 从而取消对"代码"的周期性执行的值。
    ```javascript
    setInterval("clock()",1000)
    var timer = setInterval(clock,1000)
    clearInterval(timer)//取消定时器
    ```
+ History对象
his对象位于window对象中
```window.history.属性或者方法```
history对象记录了用户曾经浏览过的页面(URL)，并可以实现浏览器前进与后退相似导航的功能。
注意:从窗口被打开的那一刻开始记录，每个浏览器窗口、每个标签页乃至每个框架，都有自己的history对象与特定的window对象关联。
	+ History对象的属性和方法
	![](/img/post/170806javascript/14.jpg)
    ![](/img/post/170806javascript/15.jpg)
	+ .go方法传一个有符号的整数
	+ .go(-1)与.back()方法相同效果
	+ .forward()与.go(1)方法相同效果
+ location对象
	+ location用于获取或设置窗体的URL，并且可以用于解析URL。
	+ ```location.属性/方法``
	+ location对象图示
	![](/img/post/170806javascript/16.jpg)
    + location对象属性
    ![](/img/post/170806javascript/17.jpg)
    + location对象方法
   	![](/img/post/170806javascript/18.jpg)
+ Navigator对象
	+ Navigator对象包含有关浏览器的信息，通常用于检测浏览器与操作系用的版本
	+ 属性
	![](/img/post/170806javascript/19.jpg)
+ userAgent对象 (在Navigatior对象之中)
	+ navigator.userA0gent
    + 几种userAgent
    ![](/img/post/170806javascript/20.jpg)
+ screen对象，用于获取屏幕信息
	+ ![](/img/post/170806javascript/21.jpg)

>未完待续


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>