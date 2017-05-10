---
layout:     post
title:      "Mifare Ultralight C"
date:       2017-05-08 19:40:00
author:     "CreeperSan"
header-img: "img/post/170510mifare-ultralight-c/header.jpg"
tags:
    - 智能卡
    - NXP
    - Mifare
---

## Mifare Ultralight C

![](/img/post/170510mifare-ultralight-c/0.jpg)

偶然接触到了一个NFC标签，使用的是NXP的Mifare Ultralight C，因为第一次接触，就去百度了下，可惜没找到什么资料,这里就自己归纳了下一点个人的看法以及网上的一些资料，仍然有很多东西不懂。

个人理解，感觉Ultralight C就像是Ultralight的升级版。Ultralight C相比于Ultralight有更大的存储空间，并且支持密码认证。简单对比下

+ 相同点
	1. 通讯协议都支持 ISO/IEC 144443-3 协议
	2. UID码长度都为7字节 (UID唯一识别码)
	3. 通讯速度都是106kbps
	4. 均不支持机卡通讯加密类型

+ 不同点
	1. Ultralight数据存储容量为48bytes,而Ultralight C为128bytes
	2. Ultralight无验证密钥种类，Ultralight C支持TDES验证密钥
	3. Ultralight无机卡验证，而Ultralight C支持三重认证

### 关于Ultralight C
可以分为230个区块(page)，相比Ultralight只有16个区块。每个Page由4个区块组成。其中每个区块容量有16Byte(?)，二每个区块的最后一个区块则用来存放2组密钥(keyA,keyB)(?)，以及密钥对应各自的访问权限(?)。

>每张卡片第一区块的第一区块（page0，block0）只能读取无法写入数据，称为制造商代码（Manufacturer Code）, 第1－4byte为UID。第5byte为比特计数检查码（bit count check)，其余的存放卡片制造商的数据。所以每张卡片实际能使用的只有15个区块，即便如此也可用于15个不同的应用。

------------

Android尝试用for循环循环疯狂读取读取扇区
![](/img/post/170510mifare-ultralight-c/0.jpg)

剩下的了解再补充...



