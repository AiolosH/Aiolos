---
title: 堆
description: 数据结构
date: 2020-01-01 00:00:00 +08:00
tags: 数据结构
category: 数据结构
---

# 堆
是一种特殊的树，满足一下两个条件
- 堆是一个完全二叉树
- 堆中每一个节点的值都必须大于等于（或小于等于）其子树中每个节点的值   
大顶堆：每个节点的值都大于等于子树中每个节点值的堆   
小顶堆：每个节点的值都小于等于子树中每个节点值的堆   

### 堆的存储
堆的数组存储方式

![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/heap_array.png)

<b>数组头需要加入一个空节点</b>，数组中下标为 i 的节点的左子节点，就是下标为 i∗2 的节点，右子节点就是下标为 i∗2+1 的节点，父节点就是下标为 i / 2​ 的节点。  
``` c++
        i/2     // 父节点
     /    
    i           // 当前节点
  /    \    
2i      2i+1    // 当前节点的左右子节点
```

- 完全二叉树来说，下标从 n/2+1 到 n 的节点都是叶子节点。

### 堆化

插入或者删除元素后，使堆继续满足其的特性的过程  
分为 <u><b>从上向下</u></b> 和 <u><b>从下向上</u></b>  

### 堆的操作

#### 插入元素
插入到数组的末尾，然后进行自下往上堆化操作

![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/heap_insert.png)
``` C++
// 参数 堆数组  插入的元素 数组个数 
void insert(int a[], int data, int& count) {
	if (count >= maxCount) return; // 堆满了就不插入了
	++count;
	a[count] = data;
	int i = count;
    // 插入节点与对应的父节点比较，如果插入的节点比父节点大交换位置
    // 直到比较到根节点或者小于某个父节点
	while (i / 2 > 0 && a[i] > a[i / 2])  
    {  
        auto tmp = a[i];
        a[i] = a[i / 2];
        a[i / 2] = tmp;
		i = i / 2;
	}
}
```

#### 删除元素
删除的元素与最后一个元素换位，删除最后一个元素后使堆恢复其特性，即将删除位置的元素复位。  

以删除堆顶元素举例
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/heap_delete.png)

堆顶元素与最后一个元素交换，然后恢复堆特性，

当前的堆顶节点肯定会下沉，所以候选的堆顶节点会从其左右子节点产生。

``` C++
```


### 堆排序
堆排序每趟产生的有序区一定是全局有序区，也就是说每趟产生的有序区中所铀元素都归位了

``` C++
// 堆化操作
void sift(int R[], int low, int high)
{
	int i = low, j = 2 * i;
	auto tmp = R[i];
	while (j <= high)
	{
		if (j < high && R[j] < R[j + 1]) 
			j++;
		if (tmp < R[j])
		{
			R[i] = R[j];
			i = j;
			j = 2 * i;
		}
		else break;
	}

	R[i] = tmp;
}
void HeapSort(int R[], int n)
{
	int i;
	auto tmp = 0;
    // 只需要对半个数组进行堆化，其余半个数组为叶子节点
	for (i = n / 2; i >= 1; i--)
		sift(R, i, n);

    // 建堆完成，每次取堆顶元素（每次的最大值），对剩余数组在进行堆化
	for (i = n; i >= 2; i--)
	{
		tmp = R[1];
		R[1] = R[i];
		R[i] = tmp;
		sift(R, 1, i - 1);
	}
}
```