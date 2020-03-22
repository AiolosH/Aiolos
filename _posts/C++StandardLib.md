---
title: C++ 标准库算法整理
description: C++
date: 2020-01-05 00:00:00 +08:00
tags: C++
category: C++
---

## C++ 标准库算法整理
### 查找对象算法
#### 1、简单查找算法

函数 | 用法
- | -
find(beg, end, val) | 查找特定元素，返回引用第一个匹配元素的迭代器，不存在返回end
count(beg, end, val) | 返回元素出现次数
find_if(beg, end, unaryPred) | 在beg到end中找满足unaryPred(参数)为真的第一个元素
count_if(beg, end, unaryPred) | 在beg到end中找满足unaryPred(参数)为真的所有元素个数

unaryPred 为函数适配器，

#### 2、查找许多值中的一个算法

要求beg1 end1和 beg2 end2 的类型完全匹配，不要求beg1 和beg2类型完全匹配

函数 | 用法
- | - 
find_first_of(beg1, end1, beg2, end2) | 在(beg1,end1)中找(beg2,end2)中的任意元素，未找到返回end1
find_first_of(beg1, end1, beg2, end2, binaryPred) | 在(beg1,end1)中找(beg2,end2)中的任意元素，未找到返回end1
find_end(beg1, end1, beg2, end2) | 在(beg1,end1)中查找最后一个和(beg2,end2)中匹配的匹配项
find_end(beg1, end1, beg2, end2, binaryPred) | 

#### 3、查找子序列的算法

函数 | 用法
- | - 
adjacent_find(beg, end) | 搜索序列中两个连续相等的元素
adjacent_find(beg, end, binaryPred) | 搜索序列中两个连续相等的元素，满足binaryPred条件
search(beg1, end1, beg2, end2) | 找第一个序列中第二个子序列
search(beg1, end1, beg2, end2, binaryPred) | 找第一个序列中第二个子序列, 满足binaryPred条件
search_n(beg, end, count, val) | 找序列中找给定val的出现次数，返回第一个匹配项
search_n(beg, end, count, val, binaryPred) | 找序列中找给定val的出现次数，返回第一个匹配项, 满足binaryPred条件

### 其他只读算法

函数 | 用法
- | - 
for_each(beg, end, f) | 
mismatch(beg1, end1, beg2) | 返回不匹配的迭代器 全部匹配返回end1
mismatch(beg1, end1, beg2, binaryPred) | 返回不满足binaryPred条件的迭代器 全部匹配返回end1
equal(beg1, end1, beg2) | 判断两个序列是否相等，相等返回true
equal(beg1, end1, beg2, binaryPred) | 判断两个序列是否满足binaryPred条件，相等返回true

### 二分查找

序列有序

函数 | 用法
- | - 
lower_bound(beg, end, val) | 在(beg,end)中查找不小于val的第一个元素
lower_bound(beg, end, val, comp) | 在(beg,end)中查找不小于val的第一个元素，comp用于指定序列排序所使用的比较。
upper_bound(beg, end, val) | 在(beg,end)中查找大于val的第一个元素
upper_bound(beg, end, val, comp) | 在(beg,end)中查找大于val的第一个元素，comp用于指定序列排序所使用的比较
equal_range(beg, end, val) | 找出有序序列中所有和val相等的元素
equal_range(beg, end, val, comp) | 找出有序序列中所有和val相等的元素，comp用于指定序列排序所使用的比较
binary_search(beg, end, val) | 序列是否包含与val相等的元素
binary_search(beg, end, val, comp) | 序列是否包含与val相等的元素，comp用于指定序列排序所使用的比较

### 容器元素的算法
#### 1、只写元素不读元素算法

函数 | 用法
- | - 
fill_n(dest, cnt, val) | 以给定的迭代器为起始位置，为cnt个数的元素设置值val
generate_n(dest, cnt, Gen) | 以给定的迭代器为起始位置，为cnt个数的元素设置由Gen函数的返回值

#### 2、使用输入迭代器写入元素的算法

函数 | 用法
- | - 
copy(beg, end, dest) | (beg,end) 复制到迭代器dest开始的序列
transfrom(beg, end, dest, unaryOp) | (beg,end) 通过unaryOp操作后，输入到迭代器dest开始的序列
transfrom(beg, end, beg2, dest, unaryOp) | (beg,end) 通过unaryOp操作后，输入到迭代器dest开始的序列
replace_copy(beg, end, dest, old_val, new_val) | (beg,end) 输入到迭代器dest开始的序列,oldval替换为new_val
replace_copy_if(beg, end, dest, unaryPred, new_val) | (beg,end) 输入到迭代器dest开始的序列,符合unaryPred条件的元素替换为new_val
merge(beg1, end1, beg2, end2, dest) |  合并两个有序序列后写入到dest
merge(beg1, end1, beg2, end2, dest, comp) | 合并两个有序序列后写入到dest，comp用于指定序列排序所使用的比较

#### 3、使用前