---
title: C++ 模板与泛型
description: C++
date: 2020-01-05 00:00:00 +08:00
tags: C++
category: C++
---

## 模板
``` C++
template<Typename T>
```

模板定义从template开始，后面接模板形参表，模板形参表使用尖括号括住的一个或多个模板形参的列表，中间用逗号分隔。

泛型代码重要原则
- 模板的形参是const引用
- 函数体重的测试之用 < 比较

### 模板特化
一个或多个模板形参的实际类型或实际值是指定的


## Template Functions
实现一个数值幂次方的函数

对于整数型
``` C++
int Power(int base, int exponent)
{
    int result = base;
    if (exponent == 0) return (int)1;
    if (exponent < 0) return (int)0;
    while (--exponent) return *= base;
    return result;
}
```

对于长整型
``` C++
long Power(long base, long exponent)
{
    long result = base;
    if (exponent == 0) return (long)1;
    if (exponent < 0) return (long)0;
    while (--exponent) return *= base;
    return result;
}
```

两个函数除了类型不同，实现过程都是一样, 可以把 <font color="red">数据类型也变成参数</font>

``` C++
templage <class T> 
T Power(T base, T exponent)
{
    T result = base;
    if (exponent == 0) return (T)1;
    if (exponent < 0) return (T)0;
    while (--exponent) result *= base;
    return result;
}
```

## Template Class

``` C++
template <class T>
class CThree
{
public:
    CThree(T t1, T t2, T t3);
    T Min();
    T Max();

private:
    T a, b, c;
}

templte <class T>
CThree<T>::CThree(T t1, T t2, T t3)
    a(t1), b(t2), c(t3)
{
}

templte <class T>
T CThree<T>::Min()
{
    T min = a < b ? a : b;
    return min < c ? min : c;
}

templte <class T>
T CThree<T>::Max()
{
    T max = a > b ? a : b;
    return max > c ? max : c;
}
```

每个成员函数都要加上<B> templte \<class T></B>


