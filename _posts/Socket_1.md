---
title: Socket编程
description: Socket TCP/IP
date: 2016-03-18 20:29:20 +08:00
tags: Socket TCP/IP
category: Socket编程
---


## socket编程函数参数及用法

<a href = "http://baike.baidu.com/view/573408.htm">WSAStartup()</a>   
```
int WSAStartup (
  WORD wVersionRequested,
  LPWSADATA lpWsaData
  );
```
使用socket的程序在使用Socket之前必须使用的函数，初始化作用。

<a href = "http://baike.baidu.com/view/569225.htm">socket()</a>   
```
int socket(
  int af,
  int type,
  int protocol
  );
```
af：表示一个地址描述，AF_INET  
type：指定socket类型。TCP(SOCK_STREAM)和UDP(SOCK_DGRAM)等等   
protocol：套接口所用的协议，不想指定用0，常用的有TCP(IPPROTO_TCP)、UDP(IPPROTO_UDP)等等。   
分配套接口的描述字及其所用资源，打开socket。

<a href = "http://baike.baidu.com/view/569184.htm">bind()</a>
```
int bind(
  SOCKET s,
  const struct socketaddr FAR* name,
  int namelen
  );
```
s：表示一个未捆绑的套接口的描述字   
name：赋予套接口的地址，sockaddr结构请看<a href = "http://huobingli.github.io/2016/03/15/Socket/">上一篇</a>   
namelen：name名字的长度
在调用该函数时，将TCP/IP类型的sockaddr_in结构的指针指向通用的地址结构sockaddr，绑定本地地址和套接口。

bind成功返回0，不成功返回SOCKET_ERROR。当bind()函数调用失败，WSAGetLastError()函数所返回的最常见的错误是WSAEADDRINUSE(100048)。发生这个错误是该程序和其他应用程序绑定了同名的socket(同一个端口号和同一本地IP地址的组合)

<a href = "http://baike.baidu.com/view/569204.htm">listen()</a>
```
int listen (
  SOCKET s,
  int backlog
  );
```
s：用于标识一个已经捆绑但未连接的套接口的描述字   
backlog：等待连接队列的最大长度

创建一个套接口并监听申请的连接

<a href = "http://baike.baidu.com/view/569214.htm">send()</a>
```
int send (
  SOCKET s,
  const char FAR* buf,
  int len,
  int flags
  );
```

s：用于标识一个已经捆绑但未连接的套接口的描述字   
buf：包含待发送数据的缓冲区   
len：缓冲区中数据的长度
flags：调用执行方式

用于已连接的数据包或了流式套接口发送数据。对于数据报类套接口，必须注意发送数据长度不超过通讯子网的IP包的最大长度。  

成功完成send()调用并不以为这数据传送到达，如果传送系统的缓冲区空间不够保存需传送的数据，除非套接口处于非阻塞I/O方式，否则send()将阻塞。对于非阻塞的SOCK_STREAM类型的套接口，实际写的数据数目可能在1到所需大小之间，其值取决于本地和远端主机的缓冲区大小，可以通过select()调用来确定合适能够进一步发送数据。

<a href = "http://baike.baidu.com/view/569210.htm">recv()</a>
```
int recv (
  SOCKET s,
  char* buf,
  int len,
  int flags
  );

```
s：用于标识一个已经捆绑但未连接的套接口的描述字   
buf：接受缓冲区，存放接收到的数据
len：缓冲区中数据的长度
flags：调用执行方式

当应用程序调用recv函数时，recv先等待s的发送缓冲 中的数据被协议传送完毕，如果协议在传送s的发送缓冲中的数据时出现网络错误，那么recv函数返回SOCKET_ERROR，如果s的发送缓冲中没有数 据或者数据被协议成功发送完毕后，recv先检查套接字s的接收缓冲区，如果s接收缓冲区中没有数据或者协议正在接收数据，那么recv就一直等待，只到 协议把数据接收完毕。当协议把数据接收完毕，recv函数就把s的接收缓冲中的数据copy到buf中（注意协议接收到的数据可能大于buf的长度，所以 在这种情况下要调用几次recv函数才能把s的接收缓冲中的数据copy完。recv函数仅仅是copy数据，真正的接收数据是协议来完成的），recv函数返回其实际copy的字节数。如果recv在copy时出错，那么它返回SOCKET_ERROR；如果recv函数在等待协议接收数据时网络中断了，那么它返回0。

<a href = "http://baike.baidu.com/view/569190.htm">connect()</a>
```
int connect (
  SOCKET s,
  const struct sockaddr name,
  int namelen
  );
```
s：标识一个未连接socket
name：指向要连接套接字的sockaddr结构体的指针(对TCP/IP总是采用sockaddr_in 结构)
namelen：sockaddr结构体的字节长度

建立于指定socket的连接。   
connect()成功返回0，不成功返回SOCKET_ERROR。对于TCP socket，connect()调用失败后，WSAGetLastError() 函数返回的最常见的错误信息是WSAECONNREFUSED（10061）。引起此错误的只有这样几种情况：服务器没有运行、你在客户端（或服务端）对sin_port的初始化不正确或者IP地址不正确。在UDP socket上调用connect()并不对网络进行访问，对于UDP socket，最常见的错误是WSAEADDRINUSE(10048)，如果在同一个本地socket上，调用一次以上connect()函数，并且引用同一个远程socket名称时，就会产生这个错误。
