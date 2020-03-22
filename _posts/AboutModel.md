---
title: 各种模式分析
description: 设计模式
date: 2016-05-11 15:22:51 +08:00
tags: SDNote
category: Note
---

### 设计模型笔记

瀑布模型

传统瀑布模型本质上是一种线性顺序模型，各阶段之间存在着严格的顺序性和依赖性，他属于整体开发模型，规定在开始下一个阶段的工作之前，必须完成前一个阶段的所有细节。

优点：它是规范的文档驱动方法
缺点：最终开发的软件可能并不是用户真正需要的


增量模型   
特点：不需要等到所有需求都出来，可以适应客户需求进行更改，可以快速构造核心产品

优点：系统可维护型极大提高，因为系统是由各个构建集成在一起，需求变更只需要变更部分部件，无需影响整个系统
缺点：要求软件

快速原型化模型
特点：快速构建一个可以在计算机上运行的原型系统，让用户使用，并收集用户反馈意见，获取用户真实需求


螺旋模型
特点：使用与内部开发的大型软件项目，但是只有在开发人员具有风险分析和排除风险的经验以及专门知识时，使用这个模型才会获得成功。


喷泉模型
较好的体现了面向对象软件开发过程无缝迭代的特性，迭代意味着模型中的开发活动常常需要重复多次，在迭代过程中不断完善软件系统，是典型的面向对象的软件过程模型之一。

### 软件测试笔记

单元测试：主要是发现程序代码中的问题，针对详细设计和软件实现阶段的工作进行的

集成测试：验证系统模块是否能够根据系统和程序设计规格说明的描述进行工作，即模块以及模块之间的接口的测试

系统测试：则是验证系统是否确实执行需求规格说明中描述的功能和非功能要求，因此测试目标在需求分析阶段就已经定义

### UML基本知识
UML的词汇表包含三种构造块：事物、关系和图。

事物是对模型中最具有代表性的成分的抽象；  
关系把事物结合在一起；   
图聚集了相关的事物。   

#### UML中有4种事物：结构事物、行为事物、分组事物和注释事物。  

结构事物是UML 模型中的名词，它们通常是模型的静态部分，描述概念或物理元素。结构事物包括类 (class)、接口（interface)、协作（collaboration)、用例（usecase)、主动类（activeclass)、构件（component)、制品（artifact)和结点（node)。   

行为事物是UML模型的动态部分，它们是模型中的动词，描述了跨越时间和空间的行为。行为事物包括：交互（interaction)、 状态机（state machine)和活动（activity)。   

分组事物是UML模型的组织部分，是一些由模型分解成的“盒子”。在所有的分组事物中最主要的分组事物是包（package)。   
注释事物是UML模型的解释部分。这些注释事物用来描述、说明和标注模型的任何元素。   

注解（note)是一种主要的注释事物。注解是一个依附于一个元素或者一组元素之上，对它进行约束或解释的简单符号。

#### 图：UML中提供了多种建模系统的图，体现系统的静态方面和动态方面。

对象图（object diagram)展现了某一时刻一组对象以及它们之间的关系。对象图描述了在类图中所建立的事物的实例的静态快照，给出系统的静态设计视图或静态进程视图。   

序列图（sequence diagram)是场景（scenario)的图形化表示，描述了以时间顺序组织的对象之间的交互活动。    

通信图（communication diagram)强调收发消息的对象的结构组织。   

时序图（Timing Diagram)关注沿着线性时间轴、生命线内部和生命线之间的条件改变，描述对象状态随着时间改变的情况，很像示波器，适合分析周期和非周期性任务。   

交互概览图（Interaction Overview Diagram)是UML 2.0新增的交互图之一，它是活动图的变体，描述业务过程中的控制流概览，软件过程中的详细逻辑概览，以及将多个图进行连接，抽象掉了消息和生命线。序列图、通信图、交互概览图和时序图均被称为交互图。

### 设计模式知识

下面四种都是行为设计模式，大多注重封装变化

解释器（Interpreter)设计模式是给定一个语言，定义它的文法的一种表示，并定义一个解释器，这个解释器使用该表示来解释语言中的句子。   

策略（Strategy)设计模式定义一系列算法，把它们一个个封装起来，并且使它们可相互替换。这一模式使得算法可独立于它的客户而变化。   

中介者（Mediator)用一个中介对象来封装一系列的对象交互。中介者使各对象不需要显式地相互引用，从而使其耦合松散，而且可以独立地改变它们之间的交互。   

观察者（Observer)模式定义对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被自动更新。

四个之间的关系：一个Strategy对象封装一个算法，一个Mediator对象封装对象间的协议。Mediator和 Observer是相互竞争的模式，之间的差别是：Observer通过引入Observer和Subject对象来分布通信，而Mediator对象则封装了其他对象间的通信。