---
title: linux 常用监控命令
description: linux 监控命令
date: 2016-06-23 11:05:14 +08:00
tags: linux
category: linux
---

### linux 常用监控命令

#### vmstat命令用于显示虚拟内存、内核线程、磁盘、系统进程、I/O 块、中断、CPU 活动 等的统计信息。
r  ：表示运行队列，如果运行队列过大，表示你的CPU很繁忙，一般会造成CPU使用率很高

b  ：表示阻塞的进程数

swpd ：虚拟内存已使用的大小，如果大于0，表示你的机器物理内存不足了，如果不是程序内存泄露的原因，那么你该升级内存了或者把耗内存的任务迁移到其他机器

free  ：空闲的物理内存的大小

buff  ： 系统占用的缓存大小

cache ：直接用来记忆我们打开的文件,给文件做缓冲

si  ：每秒从磁盘读入虚拟内存的大小，如果这个值大于0，表示物理内存不够用或者内存泄露了

us ：用户CPU时间

sy ：系统CPU时间

so ： 每秒虚拟内存写入磁盘的大小，如果这个值大于0，同上。

sy ： 系统CPU时间，如果太高，表示系统调用时间长，例如是IO操作频繁。
id  ： 空闲 CPU时间，一般来说，id + us + sy = 100

wt ： 等待IO CPU时间。

#### netstat是一个用于监控进出网络的包和网络接口统计的命令行工具。它是一个非常有用的工具，系统管理员可以用来监控网络性能，定位并解决网络相关问题。

#### iostat是一个用于收集显示系统存储设备输入和输出状态统计的简单工具。这个工具常常用来追踪存储设备的性能问题，其中存储设备包括设备、本地磁盘，以及诸如使用NFS等的远端磁盘。
```
$ sudo apt-get install sysstat
$ iostat
```
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/linux_iostat.png)   
<b>avg-cpu</b>   
%user: 在用户级别运行所使用的CPU的百分比.
%nice:优先进程消耗的CPU时间，占所有CPU的百分比.
%system: 在系统级别(kernel)运行所使用CPU的百分比.
%iowait: CPU等待硬件I/O时,所占用CPU百分比.
%steal: 管理程序维护另一个虚拟处理器时，虚拟CPU的无意识等待时间百分比.
%idle: CPU空闲时间的百分比.   
<b>Device</b>   
tps: 每秒钟发送到的I/O请求数.
KB_read /s: 每秒读取的block数.
KB_wrtn/s: 每秒写入的block数.
KB_read:  启动到现在 读入的block总数.
KB_wrtn:  启动到现在写入的block总数.
