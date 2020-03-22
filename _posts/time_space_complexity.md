---
title: 算法时间复杂度和空间复杂度
description: Algorithm
date: 2020-01-03 00:00:00 +08:00
tags: Algorithm
category: Algorithm
---

算法的好坏主要还是从算法所占用的「时间」和「空间」两个维度去考量。

- 时间维度：是指执行当前算法所消耗的时间，我们通常用「时间复杂度」来描述。

- 空间维度：是指执行当前算法需要占用多少内存空间，我们通常用「空间复杂度」来描述。

# 时间复杂度

通常使用「大O表示法」，T(n) = O(f(n))

#### 常见数量级
常见的时间复杂度量级有：

- 常数阶O(1)
``` c++
int a = 0; 
int b = 1;

int c = a + b;
```
即没有循环，消耗的时间不随某个变量增长而增长，所以为O(1)

- 对数阶O(logN)
``` c++
int i = 1;
while(i<n)
{
    i = i * 2;
}
```

while循环里每次都是i * 2，i的值就为2^n 所以执行次数就为log2N(2要下标)，所以为O(logN)

- 线性阶O(n)
``` c++
//while循环
int a = 0;
int i = 0;
int n = 10;
while(i < n)
{
    a++;
}

//for循环
int a = 0;
int i = 0;
for(; i < n; i++)
{
    a++;
}
```

for 循环和while循环里的代码会执行N边，消耗的时间即为N，所以为O(n)

- 线性对数阶O(nlogN)
``` c++
int i = 0;
int m = 0;
int n = 10;
for(; m < n; m++)
{
    i = 1;
    while(i < n)
    {
        i = i * 2;
    }
}
```

好理解，就是两层循环，一层是O(n)，一层是O(logN)，总的复杂度就是O(nlogN)

- 平方阶O(n^2) / O(m * n)
``` c++
int i, j, a;
i = j = a = 0;
int m, n;
m = n = 10;
for(; i <= m; i++)
{
   for(; j <= n; j++)
    {
        a++;
    }
}
```
更好理解 m * n，当m == n 时就为O(n^2)

- 立方阶O(n³)

- K次方阶O(n^k)

- 指数阶(2^n)

# 空间复杂度

是对一个算法在运行过程中临时占用存储空间大小的量度。

一个算法在计算机存储器上所占用的存储空间，包括<b>存储算法本身所占用的存储空间</b>，算法的<b>输入输出数据所占用的存储空间</b>和算法在<b>运行过程中临时占用的存储空间</b>这三个方面

- O(1)

算法的空间复杂度为一个常量，即不随被处理数据量n的大小而改变时，可表示为O(1)
``` c++
int a;
int b;
int c;
printf("%d %d %d \n",a,b,c);
```

- O(n)

算法的空间复杂度与n成线性比例关系时，可表示为0(n)
``` c++
int fun(int n)
{
    int k=10;
    if（n==k)
        return n;
    else
        return fun(++n);
}
```

- O(1og2N) (2 下标)

算法的空间复杂度与以2为底的n的对数成正比时，可表示为0(10g2n)

# 排序算法的空间复杂度和时间复杂度
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/suanfaxingneng.png)