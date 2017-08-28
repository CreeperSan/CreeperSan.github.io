---
layout:     post
title:      "Android Studio中开启Java8支持"
date:       2017-08-28 10:37:00
author:     "CreeperSan"
header-img: "img/post/170507about/header.jpg"
tags:
    - Android Studio
    - Java
---

### 前沿
来晚了来晚了，应该很多人都知道了，但是刚刚用到反射时，用到了 `Method.isAnnotationPresent(Class)`方法，编译器提示需要Java8.0，上网查了下把方法记录下来

### 方法
找到所在Module的buil.gradle，如下面增加就好了
```gradle
android {
  ...
  defaultConfig {
    ...
    jackOptions {									//增加
      enabled true									//增加
    }												//增加
  }
  compileOptions {									//增加
    sourceCompatibility JavaVersion.VERSION_1_8		//增加
    targetCompatibility JavaVersion.VERSION_1_8		//增加
  }													//增加
}
```

### 只需要支持Lambda表达式
```gradle
android {
    //设置JDK1.8
    compileOptions {
            sourceCompatibility JavaVersion.VERSION_1_8
            targetCompatibility JavaVersion.VERSION_1_8
        }
}
buildscript {
    repositories {
        mavenCentral()
    }

    dependencies {
        classpath 'me.tatarka:gradle-retrolambda:3.2.5'
    }
}

repositories {
    mavenCentral()
}

//添加插件
apply plugin: 'me.tatarka.retrolambda'
```

### 尾巴
Lambda表达式真爽啊
