---
title: C++ 泛型
description: C++
date: 2020-01-02 10:44:00 +08:00
tags: C++
category: C++
---

## 泛型算法

标准库操作不同容器的函数算法
``` C++
#include <algorithm>
#include <numeric>
```

算法直接修改容器大小，需要增加或删除元素必须使用容器操作

### 排序算法
全部排序
局部排序

## 迭代器
- 插入迭代器: 与容器绑定，实现容器插入元素操作
- iostream迭代器: 与输入输出流绑定，用于迭代便利所关联的IO流
- 反向迭代器: 反向遍历

插入迭代器

back_inserter 创建爱你使用push_back实现插入的迭代器  
front_inserter 使用push_front实现插入  
inserter 使用insert实现插入操作

iostream迭代器


反向迭代器
一种反向遍历容器的迭代器，也就是从最后一个元素到第一个元素遍历容器。对于反向迭代器，++操作访问前一个元素，--访问下一个元素

