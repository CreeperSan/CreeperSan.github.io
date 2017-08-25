---
layout:     post
title:      "Html中让div铺满全屏"
date:       2017-08-24 16:18:00
author:     "CreeperSan"
header-img: "img/post/170507about/header.jpg"
tags:
    - Html
    - 全屏
---

## 前言
突然有想法，想给自己写一个Html5的工具类桌面导入给WallpaperEngine中作为自己的桌面，但是一开头就卡在了背景图片全屏上，现在解决了记一下。



## 使用方法
1. 首选确保`html`和`body`的标签是`height:100%;`
2. 让`html`和`body`设定成`padding:0;margin:0;`用于消除四周围的百变
3. 我是在`body`标签下面放了一个占满所有空间`div`，然后在这个`div`中设置的背景图片
4. 给`div`设定的CSS如下
	```CSS
    .BackgroundDiv{
    	background:url(res/default.jpg) no-repeat;
        background-size:cover;
        min-height:100%;
        background-position:center center;
    }
    ```


## 技巧
1. 设定CSS时这样写
	```CSS
    *{
    	样式
    }
    ```
	则代表对所有标签都适用里面的属性
2. 设定已经存在的样式时不需要加. 而创建一个新的Class的时候就要记得加.
	```CSS
    html{
    	样式
    }
    .newClass{
    	样式
    }
    ```

