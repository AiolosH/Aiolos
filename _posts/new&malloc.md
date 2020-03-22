---
title: new和malloc的区别
description: C++
date: 2020-01-04 00:00:00 +08:00
tags: C++
category: C++
---

# new 和 malloc的区别
区别 | new | malloc 
- | - | - 
- | 运算符 | 库函数 
内存申请位置 | 自由存储区动态分配(包括堆) | 堆上动态分配内存 |
返回类型安全性 | 返回对象类型的指针(类型安全)| void*(需要通过类型转换成对应类型) d
分配失败返回值 | 抛出bad_alloc异常 | 返回NULL
指定内存大小 | 不需要 | 需要
调用构造和析构 | 调用, 初始化变量 | 不调用, 不初始化变量
处理数组 | int* a = new int[10] | int* a = (int*)malloc(sizeof(int) * 10);
已分配内存的扩充 | 无法直接分配 | 调用realloc<u><b>重新分配</b></u>内存, 需要判断是否还有连续内存
函数重载 |  可以 | 不可以

- 内存申请位置
new申请的内存位置取决于operate new

- 返回类型安全性 

    new 返回的是对应类型指针, 类型严格与对象匹配, 无须进行类型转换 
    
    malloc内存分配成功则是返回void*, 需要通过类型转换成对应类型  
    
    类型安全很大程度上可以等价于内存安全, 类型安全的代码不会试图方法自己没被授权的内存区域
- 分配失败返回值

    new 会抛出bad_alloc异常, malloc 则会返回NULL;
- 指定内存大小

    new的对象或者数组的内存大小编译器会自行计算得到, malloc 需要传入需要分配空间的大小
- 调用构造和析构

    构造(new) 1、先分配内存, 2、调用构造函数, 对象初始化
    析构(delete) 1、调用析构函数, 2、释放内存

    并不是都会调用构造函数, 对于简单类型(如int)
- 处理数组 / 函数重载

    new 支持数组的处理
    ![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/cplusplus_new.png)
    ![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/vcruntime_new.png)
- 已分配内存的扩充

    realloc 重新分配需要的内存
    ![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/realloc.png)

## 为啥有了malloc/free 还要new/delete ?
对于复杂的数据类型，malloc 只能动态分配内存，未对分配的内存进行初始化，new分配内存并初始化复杂的数据类型，在delete中销毁并释放内存。
 