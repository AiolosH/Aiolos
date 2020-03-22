---
title: 类型转换
description: C++
date: 2020-01-06 00:00:00 +08:00
tags: C++
category: C++
---

# 隐式转换和显式转换
- 隐式转换  
    指不需要用户干预，编译器默认进行的类型转换行为  
    低精度向高精度转换  
    1、多种类型计算
    ``` c++
    int nValue = 6;
    double dValue = 10.01;
    double dSum = nValue + dValue; // 16.01 nValue 会转换成double, 在和dValue相加
    ```
    2、不同类型赋值
    ``` c++
    int nValue = 6;
    double dValue = nValue; // 隐式转换成double
    ```
    3、函数传参和返回值
    ``` c++
    void fun(double dValue); //隐式转换成double
    fun(6);


    double Add(int a, int b)
    {
        return a + b;       // 隐式转换成double
    }
    ```

    高精度向低精度转换  出现强制类型转换
    ``` c++
    double dValue = 6.01;
    int nValue = dValue // nValue = 6  有警告 丢失精度
    ```
    ``` c++
    double dValue = 6.01;
    int nValue = (int)dValue; // nValue = 6 无警告 强制转换类型
    ```
- 显示转换  
    强制转换  
    1、 const_cast  
    2、 dynamic_cast  
    3、 reinterpret_cast  
    4、 static_cast  

# 上行转换和下行转换
当进行上行转换，也就是把<b><u>子类</b></u>的指针或引用转换成<b><u>父类</b></u>表示，这种转换是<b><u>安全</b></u>的  
当进行下行转换，也就是把<b><u>父类</b></u>的指针或引用转换成<b><u>子类</b></u>表示，这种转换是<b><u>不安全</b></u>的，也需要程序员来保证  

# C++中四种cast转换

- const_cast   
    强制消除对象的常量性, 用于将const变量转为非const

    ```
    const int n = 5;
    const int *cpn = &n;
    int* pn = const_cast<int*>(cpn);
    ++*pn;  //n的值被修改为了6
    ```

- dynamic_cast  
    特点：可以在<u><b>执行期</b></u>决定真正的类型，可以检测继承关系  
    <u><b>安全</b></u>的向下转型(父类转子类), 用于动态类型转换, 用于类层次间的向上和向下转化。向上转换时只能用于含有<u><b>虚函数</b></u>的类。  
    为什么要有虚函数：就说明它有想要让基类指针或引用指向派生类对象的必要，此时转换才有意义。

    在类层次间进行上行转换时，dynamic_cast和static_cast的效果是一样的  
    在进行下行转换时，dynamic_cast具有类型检查的功能，比static_cast更安全  

    ```
    dynamci_cast<a>(p)
    ```
    只有在指针p指向a或者a的派生类时才不会返回空值，注意是指向，而不是指针的类型
    ``` c++
    class A
    {
    public:
        A() { a = 10; }
        ~A(){}

        void get() { cout << a << endl; }
    private:
        int a;
    };

    class B : public A
    {
    public:
        B() { b = 11; }
        ~B() {}
        void get() { cout << b << endl; }
    private:
        int b;
    };

    // 上行转换没有问题
    B* Bb = new B;
    Bb->get();
    A* Aa = dynamic_cast<A*>(Bb);
    Aa->get();

    // 下行转换 get()不是虚函数，存在问题 Aa "运行时dynmic_cast的操作数必须包含多态类型"
    A* Aa = new A;
    Aa->get();
    B* Bb = dynamic_cast<B*>(Aa);   // 运行时这里报错，Bb = nullptr
    Bb->get();
    ```

    A中的get改成虚函数
    ``` C++
    class A
    {
    public:
        A() { a = 10; }
        ~A(){}

        virtual void get() { cout << a << endl; } // 加上virtual
    private:
        int a;
    };
    ```

- reinterpret_cast  
    几乎什么都可以转，比如将int转指针，很不靠谱，可能会出问题，尽量少用。
    
- static_cast  
    用于各种隐式转换，比如非const转const，void*转指针等, static_cast能用于多态向上转化(子类都父类)，如果向下转(父类到子类)能成功但是不安全，结果未知

    ``` c++
    class Base
    {
    public:
        virtual void f() { cout << "Base::f" << endl; }
        void f1() { cout << "Base::f1" << endl; }
    private:
        double x;
        double y;
    };

    class Derived : public Base
    {
    public:
        virtual void f() { cout << "Derived::f" << endl; }
        virtual void k() { cout << "Derived::k" << endl; }
    private:
        double z;
    };

    //但是如果pB不是真的指向Derived，则用dynamic_cast则返回NULL，能够更早的禁止error的发生，
    //如果用static_cast虽然返回的不为NULL，但是运行时可能抛出exception。
    void test()
    {
        Base* pB = new Base();
        // 基类转子类 向下转换 能成功，结果未知
        Derived* pD3 = static_cast<Derived*>(pB); // 这里转成功，但下面报错
        pD3->f();       // 这里没问题
        pD3->k();       // 这里报错
        pD3->f1();
        // 基类转子类 向下转换 检查类型，返回NULL
        Derived* pD4 = dynamic_cast<Derived*>(pB); // 这里pD4 = nullptr
        pD4->f();       // 这里需要判断if(pD4 == NULL)
        pD4->k();
        pD4->f1();
    }
    ```