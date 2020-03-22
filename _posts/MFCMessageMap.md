---
title: MFC 消息映射
description: MFC
date: 2019-12-01 00:00:00 +08:00
tags: MFC
category: MFC
---

# Message Mapping(消息映射)

### CCmdTarget 
MFC 中消息映射体系的积累，是MFC处理命令消息的基础、核心

``` C++
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

```C++
typedef void (AFX_MSG_CALL CCmdTarget::*AFX_PMSG)(void);

struct AFX_MSGMAP_ENTRY
{
	UINT nMessage;   // windows message
	UINT nCode;      // control code or WM_NOTIFY code
	UINT nID;        // control ID (or 0 for windows messages)
	UINT nLastID;    // used for entries specifying a range of control id's
	UINT_PTR nSig;   // signature type (action) or pointer to message #
	AFX_PMSG pfn;    // routine to call (or special value)
};
```

```C++
struct AFX_MSGMAP
{
	const AFX_MSGMAP* (PASCAL* pfnGetBaseMap)();
	const AFX_MSGMAP_ENTRY* lpEntries;
};
```

```C++
#define DECLARE_MESSAGE_MAP() \
protected: \
	static const AFX_MSGMAP* PASCAL GetThisMessageMap(); \
	virtual const AFX_MSGMAP* GetMessageMap() const; \
```

DECLARE_MESSAGE_MAP 相当于声明一个如下结构
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/mfcmessagemap.png)   

```C++
#define BEGIN_MESSAGE_MAP(theClass, baseClass) \
	const AFX_MSGMAP* theClass::GetMessageMap() const \
		{ return GetThisMessageMap(); } \
	const AFX_MSGMAP* PASCAL theClass::GetThisMessageMap() \
	{ \
		typedef theClass ThisClass;						   \
		typedef baseClass TheBaseClass;					   \
		static const AFX_MSGMAP_ENTRY _messageEntries[] =  \
		{
```
theClass指定消息映射所属的类的名字。baseClass指定theClass的基类的名字。


```C++
#define END_MESSAGE_MAP() \
		{0, 0, 0, 0, AfxSig_end, (AFX_PMSG)0 } \
	}; \
		__pragma(warning(pop))	\
		static const AFX_MSGMAP messageMap = \
		{ &TheBaseClass::GetThisMessageMap, &_messageEntries[0] }; \
		return &messageMap; \
	}		
```

在源文件中，用BEGIN_MESSAGE_MAP宏开始消息映射，然后为每个消息处理函数加入一个入口，最后用END_MESSAGE_MAP宏结束消息映射。


### 命令传递

MFC的消息循环的规定
- 如果是一般的WINDOWS的消息（WM_XXX）,一定是由派生类流向基类，没有旁流的可能
- 如果是命令消息WM_COMMAND, 就会有奇怪的路线


### 程序进入点
``` C++ 
extern "C" int WINAPI
_tWinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance,
	_In_ LPTSTR lpCmdLine, int nCmdShow)
#pragma warning(suppress: 4985)
{
	// call shared/exported WinMain
	return AfxWinMain(hInstance, hPrevInstance, lpCmdLine, nCmdShow);
}
```