---
title: STL模版
description: STL模版
date: 2016-09-12 10:24:14 +08:00
tags: C++
category: C++
---

#### STL模版

目录结构
```
<algorithm>、<deque>、<functional>、<iterator>、<vector>、<list>    
<map>、<memory>、<numeric>、<queue>、<set>、<stack>、<utility>
```

容器
```
向量(vector)   连续存储的元素<vector>

列表(list)     由节点组成的双向链表，每个结点包含着一个元素<list>

双队列(deque)  连续存储的指向不同元素的指针所组成的数组<deque>

集合(set)      由节点组成的红黑树，每个节点都包含着一个元素，节点之间以某种作用于元素对的谓词排列，没有两个不同的元素能够拥有相同的次序 <set>

多重集合(multiset) 允许存在两个次序相等的元素的集合 <set>

栈(stack)   后进先出的值的排列 <stack>

队列(queue)   先进先出的执的排列 <queue>

优先队列(priority_queue)   元素的次序是由作用于所存储的值对上的某种谓词决定的的一种队列 <queue>

映射(map)   由{键，值}对组成的集合，以某种作用于键对上的谓词排列 <map>

多重映射(multimap)   允许键对有相等的次序的映射 <map>
```

迭代器
