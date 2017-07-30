---
layout:     post
title:      "Kotlin中匿名内部类的写法"
date:       2017-07-30 21:56:00
author:     "CreeperSan"
header-img: "img/post/170507about/header.jpg"
tags:
    - Kotlin
    - 语法
---

## Kotlin中匿名内部类的写法
某次需要写的时候忘记了，这里先把他记下来。

分两种情况(其实区别也不大)
1. 匿名内部类继承自接口
假如我们继承自Runnable这个接口类，可以这样写
```Kotlin
val runnable = object : Runnable{
	override fun run(){
    	//内容
    }
}
```

2. 匿名内部类继承自类
```Kotlin
val thread = object : Thread(){
	override fun run(){
    	//内容
    }
}
```

哈哈，其实区别就在于接口不能有实例，所以为Runnable，而类的话就要先实例，所以为Thread()，这样解释应该是错的把 （逃）