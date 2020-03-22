---
title: windows静态库和动态库
description: C++
date: 2020-01-02 14:30:00 +08:00
tags: C++
category: C++
---

# 动态链接库
动态链接库通常都不能直接运行，也不能接受消息。是一些独立的文件，其中包含能被可执行程序或者其他DLL调用来完成某项工作的函数。只有在其他模块调用动态链接库中的函数时，它才发挥作用。

windows API中的所有函数都包含在DLL中。其中有3个最重要的DLL，
- Kernel32.dll 包含用于管理内存、进程和线程的各个函数；
- User32.dll 包含用于执行用户界面任务的各个函数（比如窗口创建和消息传递）
- GDI32.dll 包含用于画图和显示文本的各个函数

静态库
函数和数据被编译进一个二进制文件（lib）。在使用静态库的情况下，在编译链接可执行文件时，链接器从库中复制这些函数和数据并把它们和应用程序的其他模块组合起来创建最终的可执行文件（exe）

在使用动态库的时候，往往提供两个文件，一个引入库（lib）和一个dll。引入库包含被DLL导出的函数和变量的符号名，DLL包含实际的函数和数据。在编译链接可执行文件时，只需要链接引入库，DLL中的函数代码和数据并不复制到可执行文件中，在运行的时候，再去加载DLL,访问DLL中导出的函数。

## 使用好处

- 可以采用多种变成语言编写
- 增强产品功能
- 二次开发
- 简化项目
- 节省磁盘空间内存
- 有助于资源共享
- 有助于实现应用程序本地化

## 加载方式
- 隐式连接
- 显示加载

## dumpbin
看dll文件中定义的函数

## 隐式连接

### extern 和 _declspec(dllimport) 导入函数的区别
告诉编译器我们从动态链接库上加载的 运行效率更高
``` C++

// extern int add(int a, int b);
// extern int subtract(int a, int b);

_declspec(dllimport) int add(int a, int b);
_declspec(dllimport) int subtract(int a, int b);
```

### 导出动态库函数
``` C++
_declspec(dllexport) int add(int a, int b);
_declspec(dllexport) int subtract(int a, int b);
```
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/libdll_1.png)

### extern "C" 的作用
兼容C的风格, 导出函数名与原函数名相同, 不加这个会被编译器修改

``` C++
// extern int add(int a, int b);
// extern int subtract(int a, int b);

extern "C" _declspec(dllexport) int add(int a, int b);
extern "C" _declspec(dllexport) int subtract(int a, int b);
```

![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/libdll_2.png)


加_stdcall 又会导致导出函数名不同
``` C++
// extern int add(int a, int b);
// extern int subtract(int a, int b);

extern "C" _declspec(dllexport) int _stdcall add(int a, int b);
extern "C" _declspec(dllexport) int _stdcall subtract(int a, int b);
```

![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/libdll_3.png)

## 动态加载

### LoadLibrary

用于导入动态链接库
``` C++
HINSTANCE hInst;
hInst = LoadLibrary(_T("Dlltest.dll"));
```

### FreeLibrary
释放动态链接库
``` C++
HINSTANCE hInst;
hInst = LoadLibrary(_T("Dlltest.dll"));
FreeLibrary(hInst);
```

### def文件
此文件可以修改到处函数名字
需要在DLL编译前，添加到 "链接器->输入->模块定义文件" 中.

### MAKEINTRESOURCE()

## 加载过多动态库会导致浪费