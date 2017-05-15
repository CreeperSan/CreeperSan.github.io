---
layout:     post
title:      "关于Candence与PADS的一点点归纳"
date:       2017-05-08 19:40:00
author:     "CreeperSan"
header-img: "img/post/170508about-orcad-and-pads/header.jpg"
tags:
    - OrCAD
    - PADS
    - Canence
    - PCB
---



[TOC]

一点点归纳

## 基础知识

#### 设计PCB前要知道的几个概念
+ 库(library)管理原件的综合工具
+ 层(layer)成对出现,为偶数(所以也就不会有5层板，7层板诸如此类的)
+ 线和孔(Trace and Via)线宽，孔径

#### PCB设计的步骤
1. 元件建库(原理图封装、PCB封装)
2. 绘制原理图(元件连线、导出网表)
3. 布局布线(元件布局布置，连线，铺铜)
4. 导出制造文件(整理丝印，导出光绘文件)

[表格显示有问题，点击这里跳转→](https://github.com/CreeperSan/creepersan.github.io/blob/master/_posts/2017-05-08-about-orcad-and-pads.markdown)

#### 常用原理图元件
|元件名称|对应名称|
|------|--------|
|二极管|diobe|
|蜂鸣器|piezo buzzer|
|普通电阻|R|
|滑动变阻|RESISTOR VAR|
|电解电容|CAP|
|陶瓷电容|CAP NP||
|电感|INDUCTOR|
|有源晶振|CRYSTAL|
|无源晶振|OSC|
|按键|SW PUSHBUTTON|
|磁珠|CHOKE|

#### OrCad自带元件库说明
|库文件名|内容|元件数量|比如|
|------|----|-------|---|
|AMPLIFIER.OLB|模拟放大器IC|182|CA3280 , TL027C , EL4093|
|ARITHMETIC.OLB|逻辑运算IC|182|TC4032B , 74LS85|
|ATOD.OLB|AD转换IC|618|ADC0804 , TC7109|
|BUS DRIVERTRANSCEIVER.OLB|汇流排驱动IC|632|74LS244 , TC7109|
|CAPSYM.OLB|电源，地，输入输出口，标题栏等|35|-|
|CONNECTOR.OLB|连接器|816|4 HEADER，CON AT62，RCA JACK|
|COUNTER.OLB|计数器IC|182|74LS90，CD4040B|
|DISCRETE.OLB|分立式元件，常用零件|872|电阻，电容，电感，开关，变压器|
|DRAM.OLB|动态存储器|623|TMS44C256，MN41100-10|
|ELECTRO MECHANICAL.OLB|电机类元件|6|马达，断路器|
|FILTRE.OLB|滤波器类元件|80|MAX270，LTC1065|
|FPGA.OLB|可编程逻辑器件|-|XC6216/LCC|
|GATE.OLB|逻辑门(CMOS,TTL)|691|-|
|LATCH.OLB|锁存器|305|4013，74LS73，74LS76|
|LINE DRIVER RECEIVER.OLB|线控驱动与接收器|380|SN75125，DS275|
|MECHANICAL.OLB|机构图件|110|M HOLE 2，PGASOC-15-F|
|MICROCONTROLLER.OLB|单晶片微处理器|523|68HC11，AT89C51|
|MICRO PROCESSOR.OLB|微处理器|288|如80386，Z80180|
|MISC.OLB|杂项图件|1567|未分类的零件|
|MISC2.OLB|杂项图件|772|未分类零件|
|MISCLINEAR.OLB|线性杂项图件|365|14573，4127，VFC32|
|MISCMEMORY.OLB|记忆体杂项图件|278|28F020，X76F041|
|MISCPOWER.OLB|高功率杂项图件|222|REF-01，PWR505，TPS67341|
|MUXDECODER.OLB|解码器|449|4511，4555，74AC157|
|OPAMP.OLB|运放|610|101，1458，UA741|
|PASSIVEFILTER.OLB|被动式滤波器|14|DIGNSFILTER，RS1517T，LINE FILTER|
|PLD.OLB|可编程逻辑器件|355|22V10，10H8|
|PROM.OLB|只读记忆体运算放大器|811|18SA46，XL93C46|
|REGULATOR.OLB|稳压IC|549|7805，7912|
|SHIFTREGISTER.OLB|移位寄存器|610|4006，SNLS91|
|SRAM.OLB|静态存储器|691|MCM6164，P4C116|
|TRANSISTOR.OLB|晶体管|210|2N2222A，2N2905|

## 入门项目1 - 按键LED
1. 修改光标类型，Tools - Options - Global/General - Cursor - style - Full Screen
2. 修改默认规则线宽setup - Design Rules - Default - Clearance - Trace width这里，从左到右分别对应最小线宽，默认线宽，最大线宽

## 入门项目2 - TDA7052功放电路

+ 为什么要铺铜
	1. 减少底线阻抗，提高抗干扰能力
	2. 降低压降，提高电源效率
	3. 与地线相连，减少环路面积
	4. 提高电源效率，减少高频干扰
	5. ~~为了好看~~

+ 任意角度旋转元器件(PADS Layout)
	选中元器件，右键 - spin

+ 元器件对齐
	选中对个元器件，右键 - Align

## 进阶项目1
+ 检查电路图
	tools - verify... ，其中，第一个为安全距离检查，第二个为连通性检查

+ 关于覆铜
	同一层的连线会阻隔附着铜箔，覆铜时要注意这点
