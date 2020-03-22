---
title: C++ 11 auto
description: C++
date: 2020-01-05 00:00:00 +08:00
tags: C++
category: C++
---

# auto 类型推导
自动推导类型, <font color="red">必须初始化</font>

使用auto，编译器会在<font color="red">编译期间</font>自动推导出变量的类型，不用我们手动指明变量的数据类型.
```C++
auto name = value;
```
auto 仅仅是一个占位符，在编译器期间它会被真正的类型所替代。

## 高级用法
```C++
int  x = 0;
const  auto n = x;  //n 为 const int ，auto 被推导为 int
auto f = n;      //f 为 const int，auto 被推导为 int（const 属性被抛弃）
const auto &r1 = x;  //r1 为 const int& 类型，auto 被推导为 int
auto &r2 = r1;  //r1 为 const int& 类型，auto 被推导为 const int 类型
```
总结 auto 和 const
- 当类型不为引用时，auto 的推导结果将不保留表达式的 const 属性
- 当类型为引用时，auto 的推导结果将保留表达式的 const 属性。

## auto 的限制
- auto 不能在函数的参数中使用 (参数只是声明，没有定义，无法自动推导类型)
- auto 不能作用于类的非静态成员变量（也就是没有 static 关键字修饰的成员变量）中
- auto 关键字不能定义数组
    ```C++ 
    char str[] = "testauto";
    auto str1[] = str;  //arr 为数组，所以不能使用 auto
    ```
- auto 不能作用于模板参数

## auto 的引用场景
主要用了auto自动推导类型的特点

- auto 定义迭代器 简化复杂迭代器的书写
- 泛型编程 
