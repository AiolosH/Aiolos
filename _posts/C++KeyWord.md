---
title: explicit 关键字
description: C++
date: 2020-01-05 00:00:00 +08:00
tags: C++
category: C++
---

## explicit 关键字
``` C++
class Test1
{
public:
    Test1(int n)
    {
        num=n;
    }//普通构造函数
private:
    int num;
};
class Test2
{
public:
    explicit Test2(int n)
    {
        num=n;
    }//explicit(显式)构造函数
private:
    int num;
};
int main()
{
    Test1 t1=12;//隐式调用其构造函数,成功
    Test2 t2=12;//编译错误,不能隐式调用其构造函数
    Test2 t2(12);//显式调用成功
    return 0;
}
```
Test1的构造函数带了一个int型的参数

```C++
Test1 t1 = 12;  // 调用成功
```


Test2的构造函数被声明为explicit(显式), 表示不能通过隐式转换来调用这个构造函数
```C++
Test2 t2 = 12;  //调用失败
```
