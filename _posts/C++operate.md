---
title: C++ 操作符
description: C++
date: 2020-01-02 10:44:00 +08:00
tags: C++
category: C++
---

## 一元操作符
作用在一个操作数上的操作符 取地址操作符（&）和解引用操作符（*）

## 二元操作符
作用在两个操作数上的操作符 加法操作符（+）和减法操作符（-）

## 三元操作符
作用在三个操作数上的操作符

## 操作符的优先级

## 位操作

操作符 | 功能 | 用法
- | - | - 
~ | 位求反 | ~expr
<< | 左移 | expr1 << expr2
>> | 右移 | expr1 >> expr2
& | 位与 | expr1 & expr2
^ | 位异或 | expr1 ^ expr2
\| | 位或 | expr1 | expr2

后置操作符 前置操作符


## 类型转换

### 隐式转换

- 指针转换
    ```C++
    int na[10];
    int* pi = na;
    ```
    - 任意数据类型的指针都可以转换为void* 类型
    - 整型数值常量0可以转换为任意指针类型
- 转换为bool类型

- 算术类型与bool类型的转换
    ```C++
    bool b = true;
    int nval = b;  // nval = 1

    double dbval = 3.14;
    bool b2 = pi; // b2 = true;
    dbval = false // dbval = 0
    ```
- 转换与枚举类型
- 转换为const对象
    ```C++
    int i;
    const int ni = 0;
    const int &j = i;
    const int *p = &ni;
    ```
- 由标准库类型定义的转换

### 显式转换

- dynamic_cast
- const_cast
转换掉表达式的const性质
```C++
const char* pc_str;
char* pc = string_copy(const_cast<char*>(pc_str));
```
- static_cast
编译器隐式执行的任何类型转换都可以有static_cast显式完成
```C++
double d = 100.0;
char ch = static_cast<char>(d);
```
- reinterpret_cast

### 四个调试时有用常量
``` C++
__FILE__    //  文件名
__LINE__    //  当前行号
__TIME__    //  文件被编译的时间
__DATE__    //  文件被编译的日期
```