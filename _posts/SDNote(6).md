---
title: 软件设计师准备笔记 Note(6)
description: SDNote
date: 2016-05-20 10:32:20 +08:00
tags: SDNote
category: Note
---

#### TCP/IP协议的数据封装过程
数据->数据段->数据包->数据帧->数据流
传输层的数据单元是数据段，网络层的是数据单元是数据包，数据链路层的数据单元是数据帧，物理层的数据单元是数据流。

#### balabala
is a kind of 泛化
is a 继承

#### windows UNIX
windows: 分时，单用户多任务操作系统
UNIX：C编写，实时，多用户多任务操作系统

操作系统五大功能：处理机管理，存储管理，文件管理，作业管理，设备管理

#### 队列
队列空 front = rear   
满 (rear+1)%m = 0   
入 rear = (rear + 1)%maxsize   
出 front = (front + 1)%maxsize   
个数 (rear-front+maxsize)%maxsize  
