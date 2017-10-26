---
title: java中数组的使用
tags: [java]
date: 2017-10-26 09:17:40
categories: java
description:
thumbnail: 
keywords:
---
### java中操作数组需要四步
#### 1.声明数组
> 语法：   
    **数据类型[] 数组名**  
    **数据类型 数组名[]**  
```
int[] score; //存储学生成绩 类型为整型
double height[]; //存储学生身高 类型为浮点型
String[] names; //存储学生姓名 类型为字符串
```
<!-- more -->
#### 2.分配空间
简单的说就是指定数组中最多可存储多少个元素
> 语法 **数组名 = new 数据类型[数组长度]**
```
scores = new int[5];//长度为5的整数数组
height = new double[5];
names = new String[5];
```
> 上面俩步可以合并为一个步骤：
```
int[] scores = new int[5]
```
#### 3.赋值
分配空间后就可以向数组中放数据了，数组中元素都是通过下标来访问的，例如向 scores 数组中存放学生成绩
```
scores[0] = 89;
scores[1] = 79;
```
#### 4.处理数组中的数据
我们可以对赋值后的数组进行操作和处理，如获取并输出数组中元素的值
```
System.out.println("scores数组中的第一个元素的值："+ scores[0]);
```
在 Java 中还提供了另外一种直接创建数组的方式，它将声明数组、分配空间和赋值合并完成，如:
```
int[] scores = {78,91,84,68};
```
等价于：
```
int[] scores = new int[]{78,91,84,68};//new int[]后为空不能指定长度
```
注意：
1.`int[] score = new int[5];`声明方式需要指定数组长度  
2.`int[] score = new int[5];`声明方式 int后面的中括号`[]`不能丢  
3.`int[] score = new int[]{1,2,3,4,5}`声明方式`int[]`中括号里不能写数字
