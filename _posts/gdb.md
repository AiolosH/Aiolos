---
title: gdb调试
description: linux
date: 2016-12-07 10:22:51 +08:00
tags: linux
category: linux
---

# gdb调试

调试准备，生成.o文件
```
g++ -g test.cpp -o test
```

启动gdb调试
```
gdb test
```

命令              | 描述
- | -
list（或l）	     |列出源代码，接着上次的位置往下列，每次列10行
backtrace（或bt） | 查看各级函数调用及参数 ， 函数堆栈
finish        	 | 连续运行到当前函数返回为止，然后停下来等待命令  
frame（或f）      | 帧编号	选择栈帧
info（或i）       |locals	查看当前栈帧局部变量的值
list 行号	        |列出从第几行开始的源代码
list 函数名	     |列出某个函数的源代码
next（或n）	     |执行下一行语句
print（或p）+ 变量|打印表达式的值，通过表达式可以修改变量的值或者调用函数
quit（或q）       |退出gdb调试环境
set var	         |修改变量的值
start	           |开始执行程序，停在main函数第一行语句前面等待命令
step（或s）	     |执行下一行语句，如果有函数调用则进入到函数中
continue(或c)     |继续运行程序
break + 行号      | 在某一行设置断点
回车键            |表示重复上一次命令
