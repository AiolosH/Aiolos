---
title: Redis 常用操作
description: Redis
date: 2020-01-01 00:00:00 +08:00
tags: Redis
category: Redis
---

## redis 字符串的基本命令

命令 | 说明 | 备注
- | - | -
set key value | 设置键值对 | 最常用的写入命令
get key | 通过键获取值 | 最常用的读取命令
del key | 通过 key，删除键值对 | 删除命令，返冋删除数，注意，它是个通用的命令，换句话说在其他数据结构中，也可以使用它
strlen key | 求 key 指向字符串的长度 | 返回长度
getset key value | 修改原来 key 的对应值，并将旧值返回 | 如果原来值为空，则返回为空，并设置新值
getrange key start end | 获取子串 | 记字符串的长度为 len，把字符串看作一个数组，而 Redis 是以 0 开始计数的，所以 start 和 end 的取值范围 为 0 到 len-1
append key value | 将新的字符串 value，加入到原来 key 指向的字符串末 | 返回 key 指向新字符串的长度

## redis 整数和浮点型数字

命令 | 说明 | 备注
- | - | -
incr key | 在原字段上加 1 | 只能对整数操作
incrby key increment | 在原字段上加上整数（increment） | 只能对整数操作
decr key | 在原字段上减 1 | 只能对整数操作
decrby key decrement | 在原字段上减去整数（decrement） | 只能对整数操作
incrbyfloat keyincrement | 在原字段上加上浮点数（increment） | 可以操作浮点数或者整数

如果开始把 val 设置为浮点数，那么 incr、decr、incrby、decrby 的命令都会失败。Redis 并不支持减法、乘法、除法操作，功能十分有限，这点需要我们注意。

## Redis hash结构命令

命令 | 说明 | 备注
- | - | -
hdel key field1[field2......] | 删除 hash 结构中的某个（些）字段 | 可以进行多个字段的删除
hexists key field | 判断 hash 结构中是否存在 field 字段 | 存在返回 1，否则返回 0
hgetall key | 获取所有 hash 结构中的键值 | 返回键和值
hincrby key field increment | 指定给 hash 结构中的某一字段加上一个整数 | 要求该字段也是整数字符串
hincrbyfloat key field increment | 指定给 hash 结构中的某一字段加上一个浮点数 | 要求该字段是数字型字符串
hkeys key | 返回 hash 中所有的键 | ——
hlen key | 返回 hash 中键值对的数量 | ——
hmget key field1[field2......] | 返回 hash 中指定的键的值，可以是多个 | 依次返回值
hmset key field1 value1 [field2 field2......] | hash 结构设置多个键值对 | ——
hset key filed value | 在 hash 结构中设置键值对 | 单个设值
hsetnx key field value | 当 hash 结构中不存在对应的键，才设置值 | ——
hvals key | 获取 hash 结构中所有的值 | ——


## Redis链表（linked-list）数据结构和常用命令


### 链表的常用命令

命令 | 说明 | 备注
- | - | -
lpush key node1 [node2.].....  | 把节点 node1 加入到链表最左边 | 如果是 node1、node2 ...noden 这样加入， 那么链表开头从左到右的顺序是 noden...node2、node1
rpush key node1[node2]...... | 把节点 node1 加入到链表的最右边 | 如果是 node1、node2....noden 这样加  入，那么链表结尾从左到右的顺序是 node1、node2,node3...noden
lindex key index | 读取下标为 index 的节点 | 返回节点字符串，从 0 开始算
llen key | 求链表的长度 | 返回链表节点数
lpop key | 删除左边第一个节点，并将其返回 | ——
rpop key | 删除右边第一个节点，并将其返回 | ——
linsert key before|after pivot node | 插入一个节点 node，并且可以指定在值为pivot 的节点的前面（before）或者后面（after) | 如果 list 不存在，则报错；如果没有值为对应 pivot 的，也会插入失败返回 -1
lpushx list node  | 如果存在 key 为 list 的链表，则插入节点 node, 并且作为从左到右的第一个节点 | 如果 list 不存在，则失败
rpushx list node | 如果存在 key 为 list 的链表，则插入节点 node，并且作为从左到右的最后个节点 | 如果 list 不存在，则失败
lrange list start end | 获取链表 list 从 start 下标到 end 下标的节点值 | 包含 start 和 end 下标的值
lrem list count value | 如果 count 为 0，则删除所有值等于 value 的节 点：如果 count 不是 0，则先对 count 取绝对值，假设记为 abs，然后从左到右删除不大于 abs 个等于 value 的节点 | 注意，count 为整数，如果是负数，则 Redis 会先求取其绝对值，然后传递到后台操作
lset key index node | 设置列表下标为 index 的节点的值为 node | ——
ltrim key start stop | 修剪链表，只保留从 start 到 stop 的区间的节点，其余的都删除掉 | 	包含 start 和 end 的下标的节点会保留


### 链表的阻塞命令

命令 | 说明 | 备注
- | - | -
blpop key timeout | 移出并获取列表的第一个元索，如果列表没有元素会阻塞列表直到等待超时或发现可弹出元索为止 | 相对于 lpop 命令，它的操作是进程安全的
brpop key timeout | 移出并获取列表的最后一个元素，如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止 | 相对于 rpop 命令，它的操作是进程安全的
rpoplpush key sre dest | 按从左到右的顺序，将一个链表的最后一个元素移除，并插入到目标链表最左边 | 不能设置超时时间
brpoplpush key src dest timeout | 按从左到右的顺序，将一个链表的最后一个元素移除，并插入到目标链表最左边，并可以设置超时时间 | 	可设置超时时间


## Redis集合数据结构和常用命令

命令 | 说明 | 备注
- | - | -
sadd key member1 [member2 member3......] | 给键为 key 的集合増加成员 | 可以同时増加多个
scard key | 统计键为 key 的集合成员数 | —
sdiffkey1 [key2] | 找出两个集合的差集 | 参数如果是单key，那么 Redis 就返回这个 key 的所有元素
sdiftstore des key1 [key2] | 先按 sdiff 命令的规则，找出 key1 和 key2 两 个集合的差集，然后将其保存到 des 集合中。 | 	—
sinter key1 [key2] | 求 key1 和 key2 两个集合的交集。 | 参数如果是单 key，那么 Redis 就返冋这个 key 的所有元素
sinterstore des key1 key2 | 先按 sinter 命令的规则，找出 key1 和 key2 两个集合的交集，然后保存到 des 中 | —
sismember key member | 判断 member 是否键为 key 的集合的成员 | 如果是返回 1，否则返回 0
smembers key | 返回集合所有成员 | 如果数据量大，需要考虑迭代遍历的问题
smove src des member | 将成员 member 从集合 src 迁移到集合 des 中 | —
spop key | 随机弹出集合的一个元素 | 注意其随机性，因为集合是无序的
srandmember key [count] | 随机返回集合中一个或者多个元素，count 为限制返回总数，如果 count 为负数，则先求其绝对值 | count 为整数，如果不填默认为 1，如果 count 大于等于集合总数，则返回整个集合
srem key member1[member2......] | 移除集合中的元素，可以是多个元素 | 对于很大的集合可以通过它删除部分元素，避免删除大量数据引发 Redis 停顿
sunion key1 [key2] | 求两个集合的并集 | 参数如果是单 key，那么 Redis 就返回这个 key 的所有元素
sunionstore des key1 key2 | 先执行 sunion 命令求出并集，然后保存到键为 des 的集合中 | —

## Redis有序集合（sorted set）串数据结构和常用命令

命令 | 说明 | 备注
- | - | -
zadd key score1 value1 [score2 value2......] | 向有序集合的 key，增加一个或者多个成员 | 如果不存在对应的 key，则创建键为 key 的有序集合
zcard key | 获取有序集合的成员数 | —
zcount key min max  | 根据分数返回对应的成员列表 | min 为最小值，max 为最大值，默认为包含 min 和 max 值，采用数学区间表示的方法，如果需要不包含，则在分数前面加入“(”，注意不支持“[”表示
zincrby key increment member | 给有序集合成员值为 member 的分数增加 increment | —
zinterstore desKey numkeys key1 [key2 key3......] | 求多个有序集合的交集，并且将结果保存到 desKey 中 | numkeys 是一个整数，表示多少个有序集合
zlexcount key min max | 求有序集合 key 成员值在 min 和 max 的范围 | 这里范围为 key 的成员值，Redis 借助数据区间的表示方法，“[”表示包含该值，“(”表示不包含该值
zrange key start stop [withscores] | 按照分值的大小（从小到大）返回成员，加入 start 和 stop 参数可以截取某一段返回。如果输入可选项 withscores，则连同分数一起返回	这里记集合最人长度为 len，则 Redis 会将集合排序后，形成一个从 0 到 len-1 的下标，然后根据 start 和 stop 控制的下标（包含 start 和 stop）返回
zrank key member | 按从小到大求有序集合的排行 | 排名第一的为 0，第二的为 1……
zrangebylex key min max [limit offset count] | 根据值的大小，从小到大排序，min 为最小值，max 为最大值；limit 选项可选，当 Redis 求出范围集合后，会生产下标 0 到 n，然后根据偏移量 offset 和限定返回数 count，返回对应的成员 | 这里范围为 key 的成员值，Redis 借助数学区间的表示方法，“[”表示包含该值，“(”表示不包含该值 
zrangebyscore key min max [withscores] [limit offset count] | 根据分数大小，从小到大求取范围，选项 withscores 和 limit 请参考 zrange 命令和 zrangebylex 说明 | 根据分析求取集合的范围。这里默认包含 min 和 max，如果不想包含，则在参数前加入“(”， 注意不支持“[”表示
zremrangebyscore key start stop | 根据分数区间进行删除 | 按照 socre 进行排序，然后排除 0 到 len-1 的下标，然后根据 start 和 stop 进行删除，Redis 借助数学区间的表示方法，“[”表示包含该值，“(” 表示不包含该值
zremrangebyrank key start stop | 按照分数排行从小到大的排序删除，从 0 开始计算 | —
zremrangebylex key min max | 按照值的分布进行删除 | —
zrevrange key start stop [withscores] | 从大到小的按分数排序，参数请参见 zrange | 与 zrange 相同，只是排序是从大到小
zrevrangebyscore key max min [withscores] | 从大到小的按分数排序，参数请参见 zrangebyscore	与 | zrangebyscore 相同，只是排序是从大到小
zrevrank key member | 按从大到小的顺序，求元素的排行 | 排名第一位 0，第二位 1......
zscore key member | 返回成员的分数值 | 返回成员的分数
zunionstore desKey numKeys key1 [key2 key3 key4......] | 求多个有序集合的并集，其中 numKeys 是有序集合的个数 | ——