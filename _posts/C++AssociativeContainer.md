---
title: C++ 关联容器
description: C++
date: 2020-01-02 10:44:00 +08:00
tags: C++
category: C++
---

## pair类型
定义在utility头文件中

类型 | 操作
- | -
pair<T1, T2> p1 | 创建一个空的pair对象, 元素为T1和T2的类型
pair<T1, T2> p1(v1, v2) | 创建一个pair对象, 元素为T1和T2的类型, first初始化v1, second初始化v2
make_pair(v1, v2) | v1 v2值创建一个新的pair对象
p1 < p2 | pair对象小于运算
p1 == p2 | pair对象的first second 成员都相等
p.first | 返回first
p.second | 返回second

## 关联容器
根据键排列元素

## map 
key-value集合
- key 为const

构造 | 说明
- | -
map<k, v> m; | 创建一个空map对象m, 键为k 值为v
map<k, v> m(m2); | 创建副本m2, m2和m键和值类型必须相同
map<k, v> m(b, e); | b,e 为迭代器， 创建的m存储迭代器b到e的所有元素


### 下标访问vector和map的区别
访问map中不存在的元素会导致map容器中增加一个新元素。

查询操作 | 说明
- | -
map.count(k) | 返回m中k出现的次数, 0或者1, 只表示是否存在
map.find(k) | 存在k索引的元素，返回对应的迭代器，否则返回end

想要读取但不增加元素, 可以先find再读取

删除操作 | 说明
map.erase(k) | 删除键为k的元素
map.erase(p) | 删除迭代器p指向的元素，p必须是map中存在的元素，且不为end
map.erase(b,e) | 删除一段范围元素


## set
key的集合

- 不支持下标操作
- set容器存储的键唯一，且不能修改
- key为const

和map一样的find、count 操作

## multimap multiset
支持一个键对应多个实例

- <B>multimap 因为对应多个相同的键, 不支持下标操作</B>

find count

更多操作 | 说明
- | -
m.lower_bound(k) | 返回一个迭代器, 指向键不小于k的第一个元素
m.upper_bound(k) | 返回一个迭代器, 指向键大于k的第一个元素
m.equal_range(k) | 返回一个迭代器的pair对象 ，first等价于m.lower_bound(k), second等价于m.upper_bound(k)