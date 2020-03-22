---
title: 进程间通讯 —— 共享内存
description: 进程间通讯
date: 2017-01-01 17:00:00 +08:00
tags: 进程间通讯
category: 进程间通讯
---


共享内存就是允许两个不相关的进程访问同一个逻辑内存。共享内存是在两个正在运行的进程之间共享和传递数据的一种非常有效的方式。不同进程之间共享的内存通常安排为同一段物理内存。进程可以将同一段共享内存连接到它们自己的地址空间中，所有进程都可以访问共享内存中的地址，就好像它们是由用C语言函数malloc分配的内存一样。而如果某个进程向共享内存写入数据，所做的改动将立即影响到可以访问同一段共享内存的任何其他进程。

所以共享内存相当于一个公共空间，如果多个线程需要访问同一块共享内存，可以使用信号量对共享内存进行同步处理。


创建共享内存函数   
1、共享内存标识符（非负整数）  
2、共享内存容量
3、共享内存权限
```c++
int shmget(key_t key, size_t size, int shmflg);  
```

将创建的共享内存连接到当前进程的地址空间
1、由shmget函数返回的共享内存标识。
2、指定共享内存连接到当前进程中的地址位置，通常为空，表示让系统来选择共享内存的地址。
3、一组标志位，通常为0。
```c++
void *shmat(int shm_id, const void *shm_addr, int shmflg);  
```