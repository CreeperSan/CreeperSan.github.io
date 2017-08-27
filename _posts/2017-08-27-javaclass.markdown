---
layout:     post
title:      "关于Java中的get方法"
date:       2017-08-27 11:21:00
author:     "CreeperSan"
header-img: "img/post/170507about/header.jpg"
tags:
    - Java
---

## 说正事
在JAVA中，不需要设置一个值的情况下,我们写类中的一个属性，通常会这样子写
```Java
class A {
	private int a = 0;
    
    private int getA(){
    	return a;
    }
}
```

但是我们也可以这样写
```JAVA
class A {
	public final a = 0;
}
```
其实这样子写也没有违反JAVA的编程安全性原则，因为编程者可以任意的使用A中的a对象，但是由于final声明他们却无法对a做出任何修改，所以采用以上的形式是个更安全的做法。


