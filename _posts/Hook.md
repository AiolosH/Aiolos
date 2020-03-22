---
title: Hook 钩子
description: C++
date: 2020-01-02 14:30:00 +08:00
tags: C++
category: C++
---

# HOOK 钩子技术
Windows系统建立在事件驱动机制上的，说白了就是整个系统都是通过消息传递实现的。hook（钩子）是一种特殊的消息处理机制，它可以监视系统或者进程中的各种事件消息，截获发往目标窗口的消息并进行处理。

## 劫持鼠标和键盘消息
``` C++
HHOOK g_hMouse = NULL;
/*
nCode  hook code
wParam message identifer
lParam mouse coordinates
*/
LRESULT CALLBACK MouseProc(int nCode, WPARAM wParam, LPARAM lParam)
{
	return 1;  // 返回非0 鼠标消息不再进行传递，达到屏蔽鼠标消息的效果
	
    // 若要继续执行
	//return CallNextHookEx(g_hMouse, nCode, wParam, lParam);
}

HHOOK g_hKeyboard = NULL;

/*
nCode  hook code
wParam virtual-key code
lParam keystroke-message information
*/
LRESULT CALLBACK KeyboardProc(int nCode, WPARAM wParam, LPARAM lParam)
{
    // 屏蔽了空格键和回车键
	if (VK_SPACE == wParam || VK_RETURN == wParam)
		return 1;  // 返回非0 屏蔽按键
	else
    {
        // 若要继续执行
        return CallNextHookEx(g_hKeyboard, nCode, wParam, lParam);         
    }	
}

g_hMouse = SetWindowsHookEx(WH_MOUSE, MouseProc, NULL, GetCurrentThreadId());
g_hKeyboard = SetWindowsHookEx(WH_KEYBOARD, KeyboardProc, NULL, GetCurrentThreadId());
```

可以拦截消息，也可以hook特定函数来执行其他的函数。

## detour 