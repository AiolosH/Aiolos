---
title: 变量和基本类型
description: C++
date: 2020-01-02 10:44:00 +08:00
tags: C++
category: C++
---

## C++ 基本内置类型
类型 | 含义 | 最小存储空间
- | - | -
bool | 布尔型 | -
char | 字符型 | 8位
wchar_t | 宽字符型 | 16位
short | 短整型 | 16位
int | 整型 | 16位
long | 长整型 | 32位
float | 单精度浮点型 | 6位有效数字
double | 双精度浮点型 | 10位有效数字
long double | 扩展京都浮点型 | 10为有效数字

## 整型
表示整数 字符和布尔值的算术类型合称为整型。

字符类型 
- char 表示单个机器字节（byte）
- wchar_t 用于扩展字符集 比如汉字、日文 这类字符集中一些字符不能用单个char表示 前面加<font color="red"><b>"L" </b></font>

整型值
- short 类型为半个机器字长（word）
- int   为一个机器字长
- long  为一个或者两个机器字长（32位机器中int和long通常字长是相同）

布尔类型
- bool true false 

带符号与无符号类型
除了bool类型，其他类型既可以又符号也可以是无符号。第一位为符号位，无符号型只能表示大于或等于0的数，带符号的可以表示正数也可以表示负数。

int short long 默认是带符号型，前面加unsigned无符号型, unsigned int 可以简写为unsigned。

## 变量
左值与右值
- 左值：左值可以出现在赋值语句的左边或者右边. 比如：变量 int a = 0; int b = a
- 右值：右值只能出现在赋值的右边，不能出现在赋值语句的左边. 比如 0 = 1 是错的

定义与声明
- 定义：用于为变量分配存储空间，为变量指定初始值。
- 声明：向程序表明变量的类型和名字。 定义也是声明

extern关键字<b><u>是声明变量而不是定义</u></b>

## 引用
对象的另一个名字 是一种<b><u>复合类型</u></b>

const 引用
``` C++
const int a = 1024;
const int &refa = a;  // 合法
int &refb = a;          // 不合法，普通的非const引用
```

## 预处理器 
避免重复包含同文件
``` C++ 
#ifndef TESTDEFINE_H
#define TESTDEFINE_H

#endif
```