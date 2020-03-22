---
title: 字符串匹配算法
description: 数据结构
date: 2020-01-01 00:00:00 +08:00
tags: 数据结构
category: 数据结构
---

# BF 算法（暴力匹配算法，朴素匹配算法）
我们在主串中，检查起始位置分别是 0、1、2…n-m 且长度为 m 的 n-m+1 个子串，看有没有跟模式串匹配的

``` C++
int BF(string strMain, string strTarget)
{
	int i = 0, j = 0;
	while (i < strMain.length() && j < strTarget.length())
	{
		if (strMain[i] == strTarget[j])
		{
			i++; j++;	// 正常匹配
		}
		else
		{
			i = i - j + 1;
			j = 0;		// 子串重新开始
		}
	}

	if (j >= strTarget.length())
	{
		return (i - strTarget.length());	// 匹配成功，返回第一个字符下标
	}
	else
	{
		return -1;	// 表示未匹配成功
	}
}
```

# RK 算法
redis的布隆过滤器 RK算法
# BM 算法

grep

# KMP 算法