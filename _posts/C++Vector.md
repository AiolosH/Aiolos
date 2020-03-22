---
title: 标准库Vector
description: C++
date: 2020-01-02 10:44:00 +08:00
tags: C++
category: C++
---

### vector 对象初始化
vector初始化 | 作用
- | - 
vector<T> v1; | vector保存类型T的对象
vector<T> v2(v1); | v2是v1的副本
vector<T> v3<n, i>; | v3包含n个值为i的元素
vector<T> v4(n); | v4含有值初始化的元素的n个副本

#### vector 动态增长
vector内容和数组一样，是连续分配内存空间的，不同的是，在给vector分配内存时，会比实际需要的多一些，预留出以后插入的空间。当容器中没有空间容纳新元素时，会<b><u>重新分配内存</u></b>，并将老内存空间里的数据拷贝到新的空间中，并撤销原来申请的空间。

### vector 对象初始化
vector操作 | 作用
- | - 
v.empyt(); | 判断v是否为空
v.size(); | v中元素个数
v.push_back(); | v中尾部插入元素
v[n]; | 返回第n个元素
v1 = v2 | v1 换成v2
v1 == v2 | 比较两个vector元素
!=, <, <=, >, >= | 与 == 类似的操作