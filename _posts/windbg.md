---
title: windbg dump 分析
description: C++
date: 2020-01-02 00:00:00 +08:00
tags: C++
category: C++
---

# windbg 分析

## windbg dump 分析

重新加载symbol文件
```
.reload /f  
```

显示加载的模块列表
```
lm 
```

命令定位当前异常的上下文信息，并显示指定记录中的重要寄存器
```
.ecxr 
```

使用断点
```
bl (Breakpoint List)命令列出当前存在的断点和他们的状态。
bp (Set Breakpoint) 命令设置新断点。
bu (Set Unresolved Breakpoint) 命令设置新断点。使用bu设置的断点和bp设置的断点特点不同，详细信息查看后面的内容。
bm (Set Symbol Breakpoint) 在匹配指定格式的符号上设置断点。
ba (Break on Access) 命令设置数据断点。这种断点在指定内存被访问时触发。(可以在写入、读取、执行或发生内核I/O时触发，但不是所有处理器都支持所有的内存访问断点。更多信息，查看ba (Break on Access)。)
bc (Breakpoint Clear) 命令移除一个或多个断点。
bd (Breakpoint Disable) 命令暂时禁用一个或多个断点。
be (Breakpoint Enable) 命令重新启用一个或多个断点。
br (Breakpoint Renumber) 命令修改一个已存在的断点的ID。
bs (Update Breakpoint Command) 命令用于更改已存在的断点所关联的命令。
bsc (Update Conditional Breakpoint) 命令用于更改已存在的断点的触发条件。
```


扩展显示某个模块的详细信息
```
lmi 

lmvm ntdll
``` 

## windbg 