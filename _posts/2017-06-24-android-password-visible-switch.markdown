
---
layout:     post
title:      "Android切换密码是否可见"
date:       2017-07-26 11:43:00
author:     "CreeperSan"
header-img: "img/post/170507about/header.jpg"
tags:
    - Android
    - EditText
    - Kotlin
---

> 本来还以为Android切换EditText的可见与否只需要简单的改一改inputType就行的，没想到其中门道也没那么简单，就简单记录下
> 语言采用 Kotlin 开发

## 步骤



1. 修改EditText的inputType
	+ 显示密码的inputType `InputType.TYPE_TEXT_VARIATION_VISIBLE_PASSWORD`
	+ 隐藏密码的inputType `InputType.TYPE_CLASS_TEXT or InputType.TYPE_TEXT_VARIATION_PASSWORD`
2. 将光标重新放到行首
	+ `Selection.setSelection((passwordEditText.text as Spannable),passwordEditText.text.length)`

## 程序
所以整体部分的程序为以下
``` Kotlin
passwordVisibleButton.setOnClickListener {
            if (isPasswordVisible){
                isPasswordVisible = false //标志位
                passwordEditText.inputType = InputType.TYPE_TEXT_VARIATION_VISIBLE_PASSWORD //设置密码可见情况
                passwordVisibleButton.setImageResource(R.drawable.ic_visibility_off_black) //修改按钮图标样式
            }else{
                isPasswordVisible = true
                passwordEditText.inputType = InputType.TYPE_CLASS_TEXT or InputType.TYPE_TEXT_VARIATION_PASSWORD
                passwordVisibleButton.setImageResource(R.drawable.ic_visibility_black)
            }
            Selection.setSelection((passwordEditText.text as Spannable),passwordEditText.text.length)//光标回到行末
        }
```

## 参考
+ [Android中EditText显示明文与密码的两种方式](http://www.jb51.net/article/90004.htm)
+ [Android edittext 属性inputtype详解](http://blog.csdn.net/qq_16064871/article/details/44701727)
+ [Android中密码输入内容可见性切换](http://blog.csdn.net/dawanganban/article/details/23374187)