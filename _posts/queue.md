---
title: 队列
description: 数据结构
date: 2020-01-01 00:00:00 +08:00
tags: 数据结构
category: 数据结构
---

# 队列
具有先进先出的特性，支持在队尾插入元素，在队头删除元素。两个基本的操作：入队 enqueue()，放一个数据到队列尾部；出队 dequeue()，从队列头部取一个元素。

## 顺序队列
用数组实现的队列，需要记录队头和队尾的两个节点

<b>存在问题：</b>
随着不停地进行入队、出队操作，head 和 tail 都会持续往后移动。当 tail 移动到最右边(即顺序队列分配空间的结尾)，即使数组中还有空闲空间，也无法继续往队列中添加数据了。


## 链式队列
用链表实现的队列，需要记录队头和队尾的两个节点

## 环形队列

## 阻塞队列
阻塞队列其实就是在队列基础上增加了阻塞操作

## 并发队列
线程安全的队列

## 队列应用
队列可以应用在任何有限资源池中，用于排队请求

消息队列  Kafka、ActiveMQ、RabbitMQ