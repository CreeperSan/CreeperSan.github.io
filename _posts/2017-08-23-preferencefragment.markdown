---
layout:     post
title:      "Android中的设置界面 - PreferenceFragment"
date:       2017-08-23 18:54:00
author:     "CreeperSan"
header-img: "img/post/170507about/header.jpg"
tags:
    - Android
    - 界面
    - PreferenceFramgnet
---

## 前言
今天在写播放器的设置界面的时候，PreferenceFragment是个很不错的选择（FragmentActivity已经不建议使用），但是用法又忘记了，遂再次记下一些基础用法，以免日后忘记了查的麻烦

## 介绍
用于写设置界面比较方便

## 使用方法
1. 首先得准备一个Activity和一个容器用于展示这个Fragment
2. 重写一个类继承自PreferenceFragment
3. 在重写的类之中的`onCreate()`方法中调用`addPreferencesFromResource()`方法即可把界面导入进来
4. 在Activity中通过`FragmentManager`可以把`PreferenceFragment`加进来

## 注意
1. 默认保存的Preference是保存在手机的 data/data/包名/shared_prefs/下面，文件名是 包名_preference.xml
2. 如果我们想修改他的文件名可以在这样子写
	```JAVA
    getPreferenceManager().setSharePreferenceName("名字");
    ```
3. 注意，上面这个要在添加视图进来之前调用才能看到效果（其实放在后面也是有效果的，只是会看不出来）
4. 要检测每一项的点击事件可以重写`preferenceFragment`的`onPreferenceTreeClick()`方法

## 参考链接
+ [PreferenceFragment | Android Developer](https://developer.android.google.cn/reference/android/preference/PreferenceFragment.html)
