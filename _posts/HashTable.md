---
title: 散列表
description: 数据结构
date: 2020-01-01 00:00:00 +08:00
tags: 数据结构
category: 数据结构
---

# 散列表

## 散列函数
三点散列函数设计的基本要求：
- 散列函数计算得到的散列值是一个非负整数；
- 如果 key1 = key2, 那 hash(key1) == hash(key2)；
- 如果 key1 ≠ key2, 那 hash(key1) ≠ hash(key2)。

由于第3点要求, 所以产生了几乎无法避免的散列冲突问题

散列函数的设计, 我们要尽可能让散列后的值随机且均匀分布, 这样会尽可能地减少散列冲突, 即便冲突之后, 分配到每个槽内的数据也比较均匀。

## 装载因子
```
散列表的装载因子=填入表中的元素个数/散列表的长度
```
装载因子越大, 说明散列表中的元素越多, 空闲位置越少, 散列冲突的概率就越大,性能会下降。

装在因子过大, 可以进行动态扩容, 重新申请一个更大的散列表, 并且将原来散列表中的数据重新插入新的散列表中。

装载因子阈值的设置要权衡时间、空间复杂度。如果内存空间不紧张, 对执行效率要求很高, 可以降低负载因子的阈值；相反, 如果内存空间紧张, 对执行效率要求又不高, 可以增加负载因子的值, 甚至可以大于 1。

## 散列冲突(哈希冲突)
在真实的情况下, 要想找到一个不同的 key 对应的散列值都不一样的散列函数, 几乎是不可能的。即便像业界著名的MD5、SHA、CRC等哈希算法, 也无法完全避免这种散列冲突。而且因为数组的存储空间有限, 也会加大散列冲突的概率。

简单描述 ：哈希算法被计算的数据是无限的, 而计算后的结果范围有限, 会存在不同数据计算得到的结果相同。
## 解决散列冲突

开放寻址法（open addressing）和链表法（chaining）

### 开放寻址法 

往散列表中插入数据时, 如果某个数据经过散列函数散列之后, 存储位置已经被<font color="red">占用</font>了, 我们就从当前位置开始, 依次往后查找, 看是否有<font color="red">空闲位置</font>, 直到找到为止。
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/hashtable_findaddress.png)


核心思想：如果出现散列冲突, 就重新探测一个空闲位置, 将其插入。
- 线性探测法（Linear Probing）  
    当散列表中插入的数据越来越多时, 散列冲突发生的可能性就会越来越大, 空闲位置会越来越少, 线性探测的时间就会<font color="red">越来越久。</font>极端情况下, 我们可能需要探测整个散列表。删除和查找也是同理
- 二次探测（Quadratic probing）
跟线性探测很像, 线性探测每次探测的步长是 1, 那它探测的下标序列就是 hash(key)+0, hash(key)+1, hash(key)+2……而二次探测探测的步长就变成了原来的“二次方”, 也就是说, 它探测的下标序列就是 hash(key)+0, hash(key)+1^2, hash(key)+2^2……

- 双重散列（Double hashing）
不止使用一个散列函数, 使用一组散列函数 hash1(key), hash2(key), hash3(key)……先用第一个散列函数, 如果计算得到的存储位置已经被占用, 再用第二个散列函数, 依次类推, 直到找到空闲的存储位置。

### 开放寻址法优点与缺点：
开放寻址法适用于装在因子小于1的情况, 接近1的时候会存在大量的哈希冲突导致大量的探测、再散列等, 性能会下降很多。   
优点：散列表中的数据都存储在数组中, 可以有效地利用 CPU 缓存加快查询速度, 且序列化简单。  
缺点：删除数据的时候比较麻烦, 需要特殊标记已经删除掉的数据。解决哈希冲突代价较高, 开放寻址法解决冲突的散列表, 装载因子的上限不能太大。这也导致这种方法比链表法更浪费内存空间。

### 链表法 （更加常用）

在散列表后跟一个链表, 所有散列值相同的元素我们都放到相同槽位对应的链表中。
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/hashtable_hashlink.png)

### 链表法优点与缺点：
优点：内存利用率比开放寻址法高, 链表节点可以按需申请, 不需要先申请好。对大装载因子的容忍度更高。   
缺点：链表因为要存储指针, 所以对于比较小的对象的存储, 是比较消耗内存的, 还有可能会让内存的消耗翻倍。链表中的结点是零散分布在内存中的, 不是连续的, 所以对 CPU 缓存是不友好的, 这方面对于执行效率也有一定的影响。

### 开放寻址和链表法的比较
基于链表的散列冲突处理方法比较适合存储大对象、大数据量的散列表, 而且, 比起开放寻址法, 它更加灵活, 支持更多的优化策略, 比如用红黑树代替链表

## 如何设计工业级散列表

必要要求：
- 支持快速的查询、插入、删除操作；
- 内存占用合理, 不能浪费过多的内存空间；
- 性能稳定, 极端情况下, 散列表的性能也不会退化到无法接受的情况。

设计思路：
- 设计一个合适的散列函数；
- 定义装载因子阈值, 并且设计动态扩容策略；
- 选择合适的散列冲突解决方法。

并且需要结合具体的业务场景、具体的业务数据来具体分析。

### JDK1.8 红黑树退化成链表阈值 6
Java 中的 HashMap 这样一个工业级的散列表。
HashMap 默认的初始大小是 16, 最大装载因子默认是 0.75, HashMap 底层采用链表法来解决冲突.

#### 计算hash值
``` java
static final int hash(Object key) {
    int hash;
    return (key == null) ? 0 : (hash = key.hashCode()) ^ (hash >>> 16);
}
```
在 JDK1.8 版本中, 为了对 HashMap 做进一步优化, 我们引入了红黑树。而当链表长度太长（默认超过 8）时, 链表就转换为红黑树, 避免散列表时间复杂度退化成O(n)。我们可以利用红黑树快速增删改查的特点, 提高 HashMap 的性能。当红黑树结点个数少于 6 个的时候, 又会将红黑树转化为链表。因为在数据量较小的情况下, 红黑树要维护平衡, 比起链表来, 性能上的优势并不明显。

## 使用场景
### LRU 缓存淘汰算法
LRU 常用操作
- 往缓存中添加一个数据
- 从缓存中删除一个数据
- 在缓存中查找一个数据

### redis有序集合
redis 常用操作
- 添加一个成员对象
- 按照键值来删除一个成员对象
- 按照键值来查找一个成员对象
- 按照分值区间查找数据, 比如查找积分在[100, 356]之间的成员对象
- 按照分值从小到大排序成员变量

### Java LinkedHashMap
与LRU类似, 最近访问过的会被移动到链表尾部。
LinkedHashMap 是通过双向链表和散列表这两种数据结构组合实现的。LinkedHashMap 中的“Linked”实际上是指的是双向链表, 并非指用链表法解决散列冲突。