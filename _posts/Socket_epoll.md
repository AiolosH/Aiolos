---
title: Socket编程_连接
description: Socket TCP/IP
date: 2016-04-11 20:29:32 +08:00
tags: Socket_Epoll
category: Socket编程
---

### socket笔记


非阻塞socket 指调用立即返回

非阻塞调用下
Accept() 没有连接 返回-1 errno 值设置为EAGAINA或者EWOULDBLOKC 宏定义都为11

recv()、recvfrom() 没有数据返回 -1  errno 返回11 socket关闭返回0

send() 对关闭的socket调用send() 引发一个SIGPIPE，进程捕捉这个信号，因为SIGPIPE系统默认处理是关闭进程

fcntl() 判断文件或者socket描述符为阻塞还是非阻塞状态


### epoll调用函数

#### epoll_create()  
  创建一个epoll文件描述符
```
  int epoll_create(int size);  
```
  * 创建一个epoll的句柄  
  * 参数size指定epoll所支持的最大句柄数（类似于池）  
  * 函数会返回一个新的epoll句柄，之后的所有操作将通过这个句柄来进行操作。  
  * 在用完句柄之后，需要用close来关闭创建的句柄。  

  * 当create发生错误
   * EINVAL，参数size不是一个整数
   * ENFILE，系统已经分配了最大限度地文件描述符个数了
   * ENOMEM，无足够内存完成此操作

#### epoll_ctl()  
  用来添加/修改/删除需要的侦听的文件描述符及其事件
```
  int epoll_ctl(int epfd, int op, int fd, struct epoll_event *event);  
```
  * 参数epfd是epoll_create()的返回值  
  * 参数op表示动作，用三个宏表示：  
      1、EPOLL_CTL_ADD:注册新的fd到epfd中  
      2、EPOLL_CTL_MOD:修改已经注册的fd的监听事件  
      3、EPOLL_CTL_DEL:从epfd中删除一个fd  
  * 参数fd是需要监听的socket描述符  
  * 参数event通知内核需要监听什么事件  

<b>struct epoll_event结构</b>

```
  typedef union epoll_data {  
    void \* ptr;  
    int fd;  
    __uint32_t u32;  
    __uint64_t u64;  
  }  epoll_data_t;

  struct epoll_event {
    __uint32_t events; //epoll events  
    epoll_data_t data; //user data variable
  };
```
<b>events的定义</b>
* EPOLLIN : 表示对应的文件描述符可读  
* EPOLLOUT : 表示对应的文件描述符可写  
* EPOLLPRI : 表示对应的文件描述符有紧急的数据可读（这里应该表示有带外数据到来）  
* EPOLLERR : 表示对应的文件描述符发生错误
* EPOLLHUP ：表示对应的文件描述符被挂断  
* EPOLLET : 将EPOLL设为边缘触发（edge triggered）模式， 这是相对于（level triggered）来说的  
* EPOLLONESHOT : 只监听一次时间，当监听完这次事件之后，如果还需要继续监听这个socket的话，需要再次把这个socket加入到EPOLL队列中。

#### epoll_wait()  
  接受发生在被侦听的描述符上的用户感兴趣的IO事件  
```
  -int epoll_wait(int epfd, struct epoll_event *events, int maxevents, int timeout);

```
* 参数 epfd是epoll_create() 的返回值  
* 参数events是一个epoll_event*的指针，当epoll_wait这个函数操作成功之后，epoll_events里面将储存所有的读些事件。  
* 参数maxevents是当前需要监听的所有socket句柄数   
* 参数timeout是epoll_wait的超时，为0的时候表示马上返回，为-1的时候表示一直等下去，直到有事件返回，正整数表示等这么长的时间   
* 一般如果网络主循环是单独的线程的话，可以与用-1来等，这样可以保证一些效率，如果是和侏罗纪在同一个线程的话，则可以用0来保证主循环的效率。
注：epoll_wait范围之后应该是一个循环，遍历所有的事件。  

epoll文件描述符用完后，需要close关闭

每次添加/修改/删除/文件描述符都需要调用epoll_ctl，所以要尽量少的调用epoll_ctl.
