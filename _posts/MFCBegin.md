---
title: MFC start
description: MFC
date: 2019-12-01 00:00:00 +08:00
tags: MFC
category: MFC
---
# Windows 程序
## 消息基础，事件驱动

``` C++
WinMain(hInst, hPrev, ...)
{
    MSG msg;
    RegisterClass(...);
    CreateWindow(...);
    ShowWindows(...);
    UpdateWindow(...);
    while(GetMessage(&msg, ...))
    {
        TranslateMessage(&msg); // 转换键盘消息
        DispatchMessage(&msg);  // 消息分发
    }

    return msg.wParam;
}


WndProc(hwnd, msg, wParam, lParam)
{
    switch(msg)
    {
        case WM_CREATE:...
        case WM_COMMAND:...
        case WM_LBUTTONDOWN:...
        case WM_PAINT:...
        case WM_CLOSE:...
        case WM_DESTORY:...
        default: return DefWindowProc(...);
    }

    ...
}
```

### windows 内设消息数据格式
``` C++
typedef struct tagMSG
{
    HWND        hwnd;
    UINT        message; // WM_XXX 消息 如WM_MOUSEMOVE etc.
    WPARAM      wParam;
    LPARAM      lParam;
    DWORD       time;
    POINT       pt;
}MSG;
```

### 消息处理
``` C++
MSG msg;

while (GerMessage(&msg, NULL, NULL, NULL))
{
    TranslateMessage(&msg); // 转换键盘消息
    DispatchMessage(&msg);  // 消息分发
}
```


### 窗口函数
```C++
LRESULT CALLBACK WndProc(HWND hwnd, UNIT message, WPARAM wParam, LPARAM lParam)
{
    ...

    switch(msg)
    {
        case WM_CREATE:...
        case WM_COMMAND:...
        case WM_LBUTTONDOWN:...
        case WM_PAINT:...
        case WM_CLOSE:...
        case WM_DESTORY:...
        default: return DefWindowProc(...);
    }

    ...
}
```
不论什么消息，都必须处理，所以switch/case中的default中调用 DefWindowProc，它是windows 内部默认的消息处理函数.

#### wParam lParam 意义
不同操作环境有变化


### 消息映射（Message Map）

```C++
struct MSGMAP_ENTRY
{
    UINT nMessage;
    LONG (*pfn)(HWND, UINT, WPARAM, LPARAM);
};

#define dim(x) (sizeof(x) / sizeof(x[0]))
```

pfn是函数指针

### 对话框
- 模态对话框: 父窗口无效，直到对话框结束
- 非模态对话框：父窗口和对话框同时运行


### PeekMessage 和 GetMessage
相同点都是从消息队列中抓消息，

- GetMessage
- PeekMessage

### 动态创建

 需要下面三个
- DECLARE_DYNCREATE
- IMPLEMENT_DYNCREATE
- class CRuntimeClass

#### DECLARE_DYNCREATE
``` C++
// DECLARE_DYNCREATE
#define DECLARE_DYNCREATE(class_name) \ 
public: \
    static CRuntimeClass class##class_name; \
    virtual CRuntimeClass* GetRuntimeClass() const;
```

宏定义中出现## 表示连接符，告诉编译器把两个字符串连在一起


#### IMPLEMENT_DYNCREATE

``` C++
// IMPLEMENT_DYNCREATE
#define IMPLEMENT_DYNCREATE(class_name, base_class_name) \
        _IMPLEMENT_RUNTIMECLASS(class_name, base_class_name, 0xFFFF, NULL)
```

其中 _IMPLEMENT_RUNTIMECLASS 定义如下

``` C++
#define _IMPLEMENT_RUNTIMECLASS(class_name, base_class_name, wSchema, pFnNew) \ 
        static char _lpsz##class_name[] = #class_name; \
        CRuntimeClass class_name::class##class_name = { \
            _lpsz##class_name, sizeof(class_name), wSchema, pfnNew, \
                RUNTIME_CLASS(base_class_name), NULL}; \
    
    static AFX_CLASSINIT _init##class_name(&class_name::class##class_name); \ 
        CRuntimeClass* class_name::GetRuntimeClass() const \
            { return &class_name::class##class_name' } 
```

其中 RUNTIME_CLASS 定义如下
``` C++
#define RUNTIME_CLASS(class_name) \ 
        (&class_name::class##class_name)
```

其中 AFX_CLASSINIT 定义如下
``` C++
struct AFX_CLASSINIT
{ 
    AFX_CLASSINIT(CRuntimeClass* pNewClass); 
};

AFX_CLASSINIT::AFX_CLASSINIT(CRuntimeClass* pNewClass)
{
    pNewClass->m_pNextClass = CRuntimeClass::pFirstClass;
    CRuntimeClass::pFirstClass = pNewClass;
}
```

用 DECLARE_DYNCREATE(Cxxx) 和 IMPLEMENT_DYNCREATE(Cxxx, CxxxBase) 完成构建数据和加入链表的操作

#### CView demo
``` C++
// 在头文件中 
class CView::public CWnd
{
    DECLARE_DYNAMIC(CView)
    ...
};

// 在源文件中
IMPLEMENT_DYNCREATE(CView, CWnd)
```

宏进行展开得到如下
``` C++
// 头文件中
class CView : public CWnd
{
public:
    static CRuntimeClass classCView;
    virtual CRuntimeClass* GetRuntimeClass() const;
};

/// 源文件中
static char _lpszCView[] = "CView";
CRuntimeClass CView::classCView = {
    _lpszCView, sizeof(CView), 0xFFFF, NULL，
        &CWnd::classCWnd, NULL};

static AFX_CLASSINIT _init_CView(&CView::classCView);
CRuntimeClass* CView::GetRuntimeClass() const
    { return &CView::classView; }
```

### 类型识别 (IsKindOf)
```C++
// 头文件
class CObject
{
public:
    ...
    BOOL IsKindOf(const CRuntimeClass* pClass) const;
};

// 源文件
BOOL CObject::IsKindOf(const CRuntimeClass* pClass) const
{
    CRuntimeClass* pClassThis = GetRunTimeClass();
    while (pClassThis != NULL)
    {
        if (pClassThis == pClass)
            return TRUE;
        
        pClassThis = pClass->m_pBaseClass; //  向上找
    }

    return FALSE;
}
```
