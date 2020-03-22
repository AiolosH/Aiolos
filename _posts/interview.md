---
title: Interview Skill
description: Interview
date: 2017-01-01 00:00:00 +08:00
tags: Interview
category: Interview
toc: true
---


##### 数组指针和指针数组
##### 回调函数
##### sizeof()函数
```
char a[100]在当作函数参数的时候退化成一个指针，只占四个字节
```
##### 常见的ASCII值转换
```
a -> 97 A -> 65
```
##### 内存分配方式
```
堆区 : 按需分配，动态分配 ，new/delete、malloc/free 的内存块，如果程序员没有释放掉，程序结束就会释放
栈区 : 执行时自动分配 ， <b>局部变量</b> 和 <b>函数参数</b>
全局/静态存储区 : 执行时自动分配 ， 存放静态变量，全局变量，一般不允许修改（当然可以通过非正常手段修改，方法也很多）
```
