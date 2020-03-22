---
title: 红黑树
description: 数据结构
date: 2020-01-01 00:00:00 +08:00
tags: 数据结构
category: 数据结构
---

## 平衡二叉查找树的初衷
解决普通二叉查找树在频繁的插入、删除等动态更新的情况下, 出现时间复杂度<font color="red">退化</font>的问题。

## 平衡二叉树(AVL树)
平衡因子：平衡二叉树中每个节点有一个平衡因子, 每个节点的平衡因子是该节点左子树的高度减去右子树的高度, 平衡因子的绝对值小于等于1, 所以平衡因子取值为(-1, 0, 1)


## 红黑树
- 根节点是黑色的 
- 每个叶子节点都是黑色的空节点（NIL）, 也就是说, 叶子节点不存储数据
- 任何相邻的节点都不能同时为红色, 也就是说, 红色节点是被黑色节点隔开的
- 每个节点, 从该节点到达其可达叶子节点的所有路径, 都包含相同数目的黑色节点
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/RBtree_1.png)