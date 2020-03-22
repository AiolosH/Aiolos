---
title: C++ 复制控制
description: C++
date: 2020-01-05 00:00:00 +08:00
tags: C++
category: C++
---

## 复制构造函数

### 用途
- 根据一个同类型的对象显式或隐式初始化一个对象
- 复制一个对象，将他作为实参传给一个函数
- 从函数返回时复制一个对象
- 初始化顺序容器中的元素
- 根据元素初始化列表初始化数组元素

### 禁止复制  
有些类需要完全禁止复制，可以将默认构造函数声明为private, 但是类的友元和成员仍可以进行复制，如果连友元和成员中的复制也禁止，可以声明一个private复制构造函数且不对其定义。