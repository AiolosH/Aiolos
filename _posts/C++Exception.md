---
title: C++ 异常机制分析
description: C++
date: 2020-02-01 00:00:00 +08:00
tags: C++
category: C++
---

## C++异常机制概述

## throw 关键字
throw是个关键字，与抛出表达式构成了throw语句。其语法为：
```C++
throw 表达式;
```
throw语句<font color="red">必须包含在try块中</font>

## 异常对象

C++标准库定义了一组类，用户报告标准库函数遇到的问题
  
标准异常类 | 描述 | 头文件 
- | - | -
exception | 最通用的异常类，只报告异常的发生而不提供任何额外的信息 | exception
runtime_error | 只有在运行时才能检测出的错误 | stdexcept
rang_error |运行时错误：产生了超出有意义值域范围的结果 | stdexcept
overflow_error | 运行时错误：计算上溢 | stdexcept
underflow_error | 运行时错误：计算上溢 | stdexcept
logic_error | 程序逻辑错误 | stdexcept
domain_error | 逻辑错误：参数对应的结果值不存在 | stdexcept
invalid_argument | 逻辑错误：无效参数 | stdexcept
length_error | 逻辑错误：试图创建一个超出该类型最大长度的对象 | stdexcept
out_of_range | 逻辑错误：使用一个超出有效范围的值 | 
bad_alloc | 内存动态分配错误 | new
bad_cast | dynamic_cast类型转换出错 | type_info




## catch 关键字

## 栈展开、RAII
- 栈展开   
就是从异常抛出点一路向外层函数寻找匹配的catch语句的过程，寻找结束于某个匹配的catch语句或标准库函数terminate

- RAII（Resource acquisition is initialization，资源获取即初始化）

## noexcept修饰符与noexcept操作符