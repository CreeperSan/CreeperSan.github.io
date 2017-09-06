---
layout:     post
title:      "Adaptive Icons - Android O 自适应图标简单用法"
date:       2017-09-09 16:33:00
author:     "CreeperSan"
header-img: "img/post/170507about/header.jpg"
tags:
    - Android
---

# Adaptive Icons - Android O 自适应图标简单用法

### 说点废话

Android 8.0 终于都来啦，等了我好久，手机一看到推送马上就升级了上去，个人感觉Android 8.0还是挺好的，虽说界面改动除了下拉通知和设置之外改动不大，没有4.4升级5.0那么激动吧~

---

### 个人理解
Adaptive Icons可以让我们的应用程序支持不同风格的启动器，能够根据启动器来自动适应应用图标的裁剪风格。要是所有都能适配的话，桌面就不会一个圆形图标，一个正方形图标，一个圆角矩形图标，一个不规则图标其他的乱七八糟的图标裁剪啦~就都可以统一风格了~
<img src="https://developer.android.google.cn/guide/practices/ui_guidelines/images/NB_Icon_Mask_Shapes_Ext_02.gif" width="300">
个人理解其实就是把原本1层的图标分成了2层，其中一层是背景层，一层是前景层。

应用程序的图标 = 背景层 + 前景层（盖在背景层上面）

然后，启动器会有一个Mask (这个不知道怎么翻译……遮罩层吗？就暂时把它当作遮罩层吧...) ，启动器如果要不同风格的图标，就可以用自己的遮罩层裁剪应用程序图标从而生成不同的应用程序图标啦~
<img src="https://developer.android.google.cn/guide/practices/ui_guidelines/images/NB_Icon_Layers_3D_03_ext.gif" width="300">

为什么要2层呢？其实，这样子做出来的图标是支持动画效果的！从预览图中我们可以看出前景层和背景层同一时间段的滑动速度是不一样的，所以才会有2层吧？？不知道有没有理解错。
<img src="https://developer.android.google.cn/guide/practices/ui_guidelines/images/Single_Icon_Parallax_Demo_01_2x_ext.gif" width="300" >
好...好强，向Google大佬低头...
<img src="https://imgsa.baidu.com/forum/w%3D580/sign=5db4f713dc3f8794d3ff4826e2190ead/22f9a8ec8a136327ad21d698998fa0ec09fac777.jpg">

---

### How to use?
1. 首先准备3张图片，一张默认（为了兼容）的一张前景一张背景，前景最好是透明背景的图片，咱就准备了这3张
    ![为了兼容](http://img.blog.csdn.net/20170909160031512?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ3JlZXBlcl9zYW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)&nbsp;&nbsp;&nbsp;![前景图](http://img.blog.csdn.net/20170909155045005?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ3JlZXBlcl9zYW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)&nbsp;&nbsp;&nbsp; ![背景图](http://img.blog.csdn.net/20170909155121357?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ3JlZXBlcl9zYW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
    前景图不知道能不能看到。。透明+白色。。。
    这里要注意的是，我们准备的前景图和背景图要比默认的图要大点，比方说默认的建议是 48*48 dp ，那么前景图和背景图建议是 108*108 dp，其中的 72*72 dp将会出现在遮罩层里面，其余的作为动画出现的部分。这里谷歌说前景图和背景图是`must be sized at 108 x 108 dp.`我试了下好像不是也可以显示，不过还是按照规矩来吧。

2. 添加图片到工程里面
    按道理说放哪里都可以，只要你能引用到就行。我是放在了这里，然后替换了默认的ic_launcher
    ![图片](http://img.blog.csdn.net/20170909161304324?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ3JlZXBlcl9zYW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


3. 在mipmap下新建图标的配置文件
    剪完之后如图所示，应该都能看懂吧，就不说了
    ![在mipmap下新建图标的配置文件](http://img.blog.csdn.net/20170909160809900?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ3JlZXBlcl9zYW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
    我顺便把工程默认的ic_launcher也覆盖掉吧，如果不需要，就随便啦

4. 编辑配置文件
	见名知意啦，就不做解释了
	```
	<adaptive-icon xmlns:android="http://schemas.android.com/apk/res/android">
	    <background android:drawable="@drawable/ic_icon_background"/>
	    <foreground android:drawable="@drawable/ic_icon_foreground"/>
	</adaptive-icon>
	```

5. 确认manifest.xml
	确认`application`标签下`icon`对应着我们刚刚放进去的图标的配置文件名就好了
	```
	<application
			...
	        android:icon="@mipmap/ic_launcher"
	        android:roundIcon="@mipmap/ic_launcher"
	        ...>
	</application>
```

### 大功告成
运行起来看~简直有趣~

下面是在Android 8.0下的表现，桌面是Pixel Launcher，在设置里面更改了遮罩层的样式

![Default](http://img.blog.csdn.net/20170909162935733?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ3JlZXBlcl9zYW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![Tear Drop](http://img.blog.csdn.net/20170909162955658?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ3JlZXBlcl9zYW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![Square](http://img.blog.csdn.net/20170909163015850?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ3JlZXBlcl9zYW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

下面是在Android 5.1下的表现，用的是默认的图标了

![5.1](http://img.blog.csdn.net/20170909163049133?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ3JlZXBlcl9zYW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)