---
title: 二叉树
description: 数据结构
date: 2020-01-01 00:00:00 +08:00
tags: 数据结构
category: 数据结构
---

# 树
- 高度：节点到叶子节点的最长路径（边数）
- 深度：根节点到这个节点所经历的边数
- 层：节点高度 + 1
- 树的高度：根节点高度

# 二叉树

## 完全二叉树

最后一层子节点都靠左

## 满二叉树
叶子节点全都在最底层，除了叶子节点之外，每个节点都有左右两个子节点
## 存储方式
### 链式存储法
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/binarytree_linked.png)

### 基于数组的<b>顺序存储法</b>
数组顺序存储的方式比较适合<u><b>完全二叉树</b></u>，
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/binarytree_array_2.png)

其他类型的二叉树用数组存储会比较浪费存储空间
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/binarytree_array_1.png)
## 二叉树遍历

每个节点最多会被访问两次，所以遍历操作的时间复杂度，跟节点的个数 n 成正比，也就是说二叉树遍历的时间复杂度是 O(n)。

### 前序遍历 （中左右）
#### 前序递归算法
递归退出 当pNode为叶节点
``` C++
void PreOrder(TNode* pNode)
{
    if (pNode != NULL)  // 递归退出条件
    {
        printf("%c", pNode->data);  // 访问根节点
        PreOrder(pNode->lChild);    // 访问左子树
        PreOrder(pNode->rChild);    // 访问右子树
    }
}
```

### 中序遍历 （左中右）
#### 中序递归算法
``` C++
void InOrder(TNode* pNode)
{
    if (pNode != NULL)  // 递归退出条件
    {
        InOrder(pNode->lChild);     // 访问左子树
        printf("%c", pNode->data);  // 访问根节点
        InOrder(pNode->rChild);     // 访问右子树
    }
}
```

### 后序遍历 （左右中）
#### 后序递归算法
``` C++
void PostOrder(TNode* pNode)
{
    if (pNode != NULL)  // 递归退出条件
    {
        PostOrder(pNode->lChild);   // 访问左子树
        PostOrder(pNode->rChild);   // 访问右子树
        printf("%c", pNode->data);  // 访问根节点
    }
}
```


### 层序遍历 （BFS 广度优先算法）

