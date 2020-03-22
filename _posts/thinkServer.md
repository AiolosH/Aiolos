---
title: 服务器架构思考
description: 服务器
date: 2016-05-30 22:40:32 +08:00
tags: 服务器
category: 服务器
---

#### 线程池 threadPool
线程池中的线程在初始化之后进入等待状态，即跑一个等待线程，pthread_cond_wait(条件变量,互斥变量)
在这个函数中进行阻塞，然后再有需要线程调用的时候使用pthread_cond_signal(条件变量)，然后可以执行pthread_cond_wait后面的语句，这样线程就可以成功分配了。
