---
title: C++ 容器
description: C++
date: 2020-01-02 10:44:00 +08:00
tags: C++
category: C++
---

## 容器

- | 类型
- | -
顺序容器 | -
vector | 支持快速随机访问
list | 支持快速插入/删除
deque | 双端队列
顺序容器适配器 | -
stack | 后进先出（LIFO）栈
queue | 先进先出（FIFO）队列
priority_queue | 有优先级管理的队列

## 迭代器运算

所有容器都可以的运算

运算 | 作用
- | -
*iter | 返回迭代器iter所指向的元素的引用
iter->mem | 对iter进行解引用，获取名为mem的成员。等效于(*iter).mem
++iter iter++ | iter加1，指向容器下一个元素
--iter iter-- | iter减1，指向容器前一个元素
iter1 == iter2 | 比较两个迭代器是否相同
iter1 != iter2 | 比较两个迭代器是否不同

vector 和deque 额外的运算

运算 | 作用
- | -
iter + n | 迭代器上加整数值n，将产生指向容器中前面的第n个元素的迭代器
iter - n | 迭代器上减整数值n，将产生指向容器中后面的第n个元素的迭代器
iter1 += iter2 | 加法复合赋值运算，结果赋值给iter1
iter1 -= iter2 | 减法复合赋值运算，结果赋值给iter1
iter1 - iter2 | 迭代器减法
>, >=, < , <= | 迭代器关系操作符

关系操作符（<、<=、 > 、 >=）只适用于vector 和deque容器，因为这有这两类容器为其元素提供快速、随机访问

## 容器的选用
- 插入删除的代价
- 随机访问的代价


## 容器适配器
对容器的一种再封装,不同的容器适配器提供不同的函数，使容器的功能得到全新的特定的扩展。
- stack 栈
- queue 队列
- priority_queue 优先队列

```C++
vector<int> vc; // vc : 1,2,3,4,5,6
// 顺序输出  1,2,3,4,5,6
stack<int vector<int>> svc(vc); 
// 一个个pop弹出
// 输出 6,5,4,3,2,1
```