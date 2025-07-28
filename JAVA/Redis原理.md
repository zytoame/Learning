## 数据结构
### 简单动态字符串SDS
header：len（字符串长度），alloc（buf申请的长度/字节数，不包含结束标示/0），flags（不同头类型用来控制SDS头的大小）
	![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728144100176.png)

**内存预分配**：追加字符串会首先申请新内存空间：新字符串小于1M，则新空间 为 扩展后字符串长度的两倍+1；大于1M，新空间：字符串长度+1M+1
申请内存的时候需要和linux的内核交互，这个操作非常消耗资源
- 优点
	- 获取字符串长度的时间复杂度为O（1）
	- 支持动态扩容
	- 减少内存分配次数
	- 二进制安全
### IntSet
Redis中set集合 的一种实现方式，基于整数数组来实现，具备长度可变，有序等特征 
数组本身是一个指针，指向起始元素的地址 ，是连续内存空间。contents指向数组第一个元素的地址
**set值必须是2^n**
- **支持动态升级**：添加的数字超出int16_t范围，insert会自动升级编码方式，为int32，每个整数占4个字节。按照心电编码方式及元素个数扩容数组；**倒序**依次将数组中的元素拷贝到扩容后的正确位置（防止覆盖）；encouding属性改变，length属性改变
- 底层采用二分查找来查询
- 元素唯一有序
- ![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728150505702.png)
### Dict
键和值的映射关系通过dict来实现
组成：哈希表，哈希节点，字典
类似java 的HashTable，底层是数组加链表来解决哈希冲突
Dict包含两个哈希表，ht[ 0 ]平常用，ht[1]用来rehash
添加键值对：**头插法**，**与运算**
	在链表头部插入新节点。新节点总是成为头节点；插入的时间复杂度为O（1）
		头插法的实现
			![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728151903809.png)

字典结构：
	![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728151632288.png)

扩容：dict在每次新增键值对时都会检查负载因子（LoadFactor = used/size）
	触发的两种情况：1. 负载因子≥1，且服务器没有执行bgsave或者bgrewriteaof等后台进程；2. 负载子>5
	![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728153203914.png)
收缩：删除元素时对负载因子做检查，小于0.1做收缩

渐进式rehash  
	rehash过程：
	![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728154445169.png)
	渐进式rehash流程：
	![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728154215016.png)

### ZipList
特殊的“双端链表”，有一系列特殊编码的**连续**内存块组成。
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728161222170.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728161241761.png)


![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728160743040.png)
	![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728161334985.png)
	![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728161802624.png)

连锁更新问题

### QuickList
双端链表，每个节点都是一个ZipList
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728163341877.png)
### SkipList
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728165040147.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728165109938.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728165129205.png)
### RedisObject
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728165928164.png)
### String
最好使用整数，或者小于44字节，因为raw需要申请两次内存
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728171236470.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728171330417.png)

![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728171315186.png)

### List
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728172407690.png)

### Set
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728192626160.png)
### ZSet
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728193132155.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728195318216.png)




## 网络模型
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728201432402.png)
阻塞IO
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728205804905.png)


非阻塞IO
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728205727122.png)
**==IO多路复用==**
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728210936003.png)

![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728210649115.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728210800128.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728211854876.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728212334857.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728214253802.png)


![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728214112232.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728215223611.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728215758345.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728220023229.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728220141878.png)
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728220342815.png)
	核心业务是单线程，命令处理是单线程
	删除bigKey可能会导致主线程阻塞，耗时久，因此采用一种异步删除的方法，通过后台另一个线程去删除
	集群会引入其他问题，搭建复杂
	![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728221216146.png)

![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250728220817847.png)

## 通信协议
## 内存策略