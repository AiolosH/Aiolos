---
title: 侵入式和非侵入式
description: 设计模式
date: 2020-01-02 00:00:00 +08:00
tags: 设计模式
category: 设计模式
---

### 非侵入式设计

客户端的代码可能包含框架功能和客户端自己的功能。

非侵入式设计则表现为客户端实现框架提供的接口。

非侵入式设计则不然，之前写过的代码仍有价值。 

### 侵入式设计

设计者将框架功能“推”给客户端，而非侵入式设计，则是设计者将客户端的功能“拿”到框架中用。

侵入式设计有时候表现为客户端需要继承框架中的类

侵入式设计带来的最大缺陷是，当你决定重构你的代码时，发现之前写过的代码只能扔掉。