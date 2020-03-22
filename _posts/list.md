---
title: 链表
description: 数据结构
date: 2020-01-01 00:00:00 +08:00
tags: 数据结构
category: 数据结构
---

# 缓存使用

缓存是一种提高数据读取性能的技术，在硬件设计、软件开发中都有着非常广泛的应用，比如常见的 CPU 缓存、数据库缓存、浏览器缓存等等。缓存的大小有限，当缓存被用满时，哪些数据应该被清理出去，哪些数据应该被保留？  
这就需要缓存淘汰策略来决定。常见的策略有三种：先进先出策略 FIFO（First In，First Out）、最少使用策略 LFU（Least Frequently Used）、最近最少使用策略 LRU（Least Recently Used）。

# 链表
单链表 双链表 循环链表

## 单链表

### 判断链表是否有环

采用快慢指针来判定
``` C++
fast = fast.Next.Next;
slow = slow.Next;
```

slow每次向前走一步，fast向前追了两步,遇到环fast会跑到slow后面，这样会出现slow==fast的情况，出现这种情况表示链表中存在环。
## 双链表
## 循环链表
