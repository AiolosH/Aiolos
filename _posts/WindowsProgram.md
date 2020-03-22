---
title: Windows编程
description: program
date: 2016-10-11 10:22:51 +08:00
tags: program
category: program
---

####
hWnd h表示句柄，Wnd表示窗口，所以是窗口句柄
DWORD Double Word  每个word2个字节 DWORD是4个字节， 每个字节8位，共32位，设备驱动程序和服务的许多参数都是此类型


#### 可变参数 ...
C语言中有一种长度不确定的参数，形如："…"，它主要用在参数个数不确定的函数中，我们最容易想到的例子是printf函数。
```C++
函数原型
int printf( const char *format [, argument]... );
```

在标准C语言中定义了一个头文件专门用来对付可变参数列表，它包含了一组宏，和一个va_list的typedef声明。还要用到下面三个宏定义

```C++
typedef char* va_list;
#define va_start(list) list = (char*)&va_alist
#define va_end(list)
#define va_arg(list, mode)\
((mode*) (list += sizeof(mode)))[-1]

```

```C++
void va_start( va_list arg_ptr, prev_param );
type va_arg( va_list arg_ptr, type );
void va_end( va_list arg_ptr );
```
va表示variable-argument(可变参数)   
需要包含头文件stdarg.h

使用步骤：   
1、使用需要在函数中首先定义一个va_list类型变量，如上为arg_ptr，这个变量是存储参数地址的指针.因为得到参数的地址之后，再结合参数的类型，才能得到参数的值。

2、然后用va_start宏初始化⑵中定义的变量arg_ptr,这个宏的第二个参数是可变参数列表的前一个参数,即最后一个固定参数。

3、然后依次用va_arg宏使arg_ptr返回可变参数的地址,得到这个地址之后，结合参数的类型，就可以得到参数的值。

4、设定结束条件，这里的条件就是判断参数值是否为-1。注意被调的函数在调用时是不知道可变参数的正确数目的，程序员必须自己在代码中指明结束条件。至于为什么它不会知道参数的数目，在看完这几个宏的内部实现机制后，自然就会明白。
