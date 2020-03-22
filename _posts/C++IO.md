---
title: C++ IO库
description: C++
date: 2020-01-02 10:44:00 +08:00
tags: C++
category: C++
---

## C++ IO库
- | 作用
- | - 
istream 输入流类型 | 提供输入操作
ostream 输出流类型 | 提供输出操作
cin | 读入标准输入的istream对象
cout | 写到标准输出的ostream对象 
cerr | 输出标准错误的ostream对象，常用于程序错误信息
\>>操作符 | 用于从istream对象中读入输入
<<操作符 | 用于吧输出写到ostream对象中
getline | 需要分别去istream类型和string类型的两个引用形参从istream中读取一个单词写入stream对象

### IO类型
头文件 | 读取类型 | -
- | - | -
iostream | 读写控制窗口的类型 | istream 从流中读取
- | - | ostream 写到流中去
- | - | iostream对流进行读取；从istream和ostream派生而来
fstream | 读写一直命令文件的类型 |  ifstream从文件中读取；istream派生而来
- | - | ofstream写到文件中去；由ostream派生而来
- | - | fstream 读写文件；由iostream派生而来 
sstream | 读写存储在内存中的string对象 | istringstream从string对象中读取；由istream派生而来
- | - | ostringstream写到string对象中读取；由istream派生而来
- | - | stringstream对string对象进行读写；由iostream派生而来
