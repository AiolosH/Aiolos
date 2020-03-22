---
title: 初识Socket
description: Socket TCP/IP
date: 2016-03-15 18:37:51 +08:00
update: 2016-03-17 20:29:20 +08:00
tags: Socket TCP/IP
category: Socket编程
---

## TCP/IP 与 Socket编程

### TCP/IP协议


### Socket编程

Socket是网络通信的基本单元，应用层到传输层的接口，可以将套接字看作不同个主机间的进程，进行双向通信的端点。  
套接字之间的连接过程可以分为3个步骤：1、服务器监听；2、客户端请求；3、连接确认。

socket有三个属性： 协议、 端口号、 IP地址。


#### Socket服务端

sockaddr结构
```
struct sockaddr
{
  unsigned short sa_family;
  char sa_data[14];
}
```
sa_family 表示2个字节的地址族，通常使用AF_INET


sockaddr_in结构
```
struct sockaddr_in  
{  
short sin_family;  
unsigned short sin_port;  
struct in_addr sin_addr;  
unsigned char sin_zero[8];  
};
```
sin_family 表示地址族   
sin_port 表示按网络顺序的16位端口号   
sin_addr in_addr结构体，表示按网络顺序的32位的因特网地址  
sin_zero 是为了让sockaddr与sockaddr_in两个数据结构保持大小相同而保留的空字节  

in_addr用来表示32位的IPv4地址

in_addr结构
```
struct in_addr
{
  in_addr_t s_addr;
}
```
sockaddr 和 sockaddr_in的区别
![妈蛋为什么显示不出来](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/1.png)

两者的占用的内存大小是一致的，因此可以相互转化，从这个意义上说，他们并无区别。sockaddr 通常用在bind,connect,recvfrom,sendto等函数的参数，指明地址信息，是一种通用的套接字。sockaddr_in是internet环境下套接字的地址形式。所以在网络编程中我们会对sockaddr_in结构体进行操作。先使用sockaddr_in来建立所需的信息，最后使用类型转化就可以了。

```
#include <stdio.h>
#include <stdlib.h>
#include <sys/socket.h>
#include <netinet/in.h>


int main(int argc,char **argv)
{
int socket;
struct sockaddr_in mysock;

socket = socket(AF_INET,SOCK_STREAM,0);  //获得socket

memset((void *)&mysock, 0, sizeof(mysock));//windows 下使用memset赋值，初始化结构体
(bzero(&mysock,sizeof(mysock));  //linux下初始化结构体)


mysock.sin_family = AF_INET;  //设置地址家族
mysock.sin_port = htons(800);  //设置端口800
mysock.sin_addr.s_addr = inet_addr("192.168.1.0");  //设置地址
bind(sockfd,(struct sockaddr *)&mysock,sizeof(struct sockaddr); /* bind的时候进行转化 */

//... ...

return 0;

}
```
我在测试的时候，如果inet_addr()传入参数不是127.0.0.1，就无法执行bind()函数将套接口和本地地址绑定，是bind返回值为-1
