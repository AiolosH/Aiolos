---
title: Go 命令
description: Go
date: 2020-01-05 00:00:00 +08:00
tags: Go
category: Go
---

## go build
1、go build 无参数   
生成包名文件
``` go
go build
```

2、go build +文件列表  
``` go
go build main.go lib1.go
``` 
使用"go build+文件列表"方式编译时，可执行文件默认选择文件列表中第一个源码文件作为可执行文件名输出。

3、go build+包

在设置 GOPATH 后，可以直接根据包名进行编译，即便包内文件被增（加）删（除）也不影响编译指令。

go build 编译参数

参数 | 效果
- | -
-v | 编译时显示包名
-p n | 开启并发编译，默认情况下该值为 CPU 逻辑核数
-a | 强制重新构建
-n | 打印编译时会用到的所有命令，但不真正执行
-x | 打印编译时会用到的所有命令
-race | 开启竞态检测

## go clean
会清除掉编译过程中产生的一些文件。在 Java 中通常是 .class 文件，而在Go语言中通常是上面我们所列举的那些文件。
