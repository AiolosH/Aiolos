---
title: 标准库String
description: C++
date: 2020-01-02 10:44:00 +08:00
tags: C++
category: C++
---

## 标准库 string 
string 类型支持长度可变的字符串，C++标准库负责管理与存储字符串相关的内存，及提供各种有用的操作。

### string 对象初始化
string初始化 | 作用
- | - 
string s1; | 默认构造函数 s1为空串
string s2; | 将s2初始化为s1的副本
string s3("value"); | 将s3初始化为一个字符串
string s4(n,'c'); | 将s4初始化为字符'c'的n个副本

### string对象操作
string操作 | 作用
- | - 
s.empty() | 判断s是否为空
s.size() | s的字符数
s[n] | 返回s中位置为n的字符
s1 + s2 | 连接两个字符串，返回新串
s1 = s2 | s2赋值给s1
s1 == s2 | 比较两个字符串内容
!=, <, <=, >, >= | 与 == 类似的操作
