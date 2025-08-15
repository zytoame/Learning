# 基本语法
1. 大小写敏感：**类名、接口名**首字母大写，**方法名**首字母小写。
2. **源文件名**必须和**类名**相同
3. 所有程序都是从public static void main(String[ ], args);开始
4. 标识符：类名、变量名、方法名、包名、常量名等。以字母、$、_ 、 开头。
5. Java 中基本数据类型（如 `int`）的参数传递是**值传递**，方法内修改不会影响原始变量。
    若需修改原始数据，需通过引用类型（如数组、对象）间接实现。
    ```java
    //不改变原始变量，输出a = 10， b=20
    public class RunoobTest { 
	    public static void main(String[] args) { 
		    int a = 10, b = 20; 
		    swap(a, b); // 调用swap方法 
		    System.out.println("a = " + a + ", b = " + b); // 输出a和b的值
		 } 
		public static void swap(int x, int y) { 
			int temp = x; x = y; y = temp; 
		}
	}
	//真正交换两个变量：使用数组或对象包装
	//输出 a = 20, b = 10
	public class RunoobTest {
		public static void main(String[] args){
			int[] arr = {10, 20};
			swap(arr,0,1);
			System.out.println("a = " + a + ", b = " + b);
		}
		public static void swap(int[] arr, int i, int j){
			int temp = arr[i]; arr[i] = arr[j]; arr[j] = temp;
		}
	}
	```
6.  Character方法

| 序号  | 方法与描述                              |
| --- | ---------------------------------- |
| 1   | isLetter() <br>是否是一个字母             |
| 2   | isDigit()<br>是否是一个数字字符             |
| 3   | isWhitespace()<br>是否是一个空白字符        |
| 4   | isUpperCase()<br>是否是大写字母           |
| 5   | isLowerCase()<br>是否是小写字母           |
| 6   | toUpperCase()<br>指定字母的大写形式         |
| 7   | toLowerCase()<br>指定字母的小写形式         |
| 8   | toString()<br>返回字符的字符串形式，字符串的长度仅为1 |

# Java常用容器的底层实现

## Map接口的实现类

### 1. HashMap
- **底层结构**：==数组+链表+红黑树（JDK8+）==
- **实现原理**：
  - 初始容量默认为16，负载因子0.75
  - 通过key的hashCode()计算哈希值，确定数组下标
  - 哈希冲突时使用链表解决（拉链法）
  - 当链表长度超过8且数组长度≥64时，链表转为红黑树
  - 当红黑树节点数小于6时，退化为链表
- **特点**：
  - ==非线程安全==
  - ==允许null键和null值==
  - 迭代顺序不保证

### 2. LinkedHashMap
- **底层结构**：继承HashMap，增加==双向链表==维护插入==顺序==
- **实现原理**：
  - 在HashMap基础上维护了一个双向链表
  - 可以保持插入顺序或访问顺序（LRU实现基础）
- **特点**：
  - 保持插入顺序或访问顺序
  - 性能略低于HashMap

### 3. TreeMap
- **底层结构**：红黑树
- **实现原理**：
  - 基于红黑树（==自平衡二叉查找树==）实现
  - ==按键的自然顺序或Comparator排序==
- **特点**：
  - ==按键有序==
  - 查询、插入、删除==时间复杂度O(log n)==

### 4. ConcurrentHashMap
- **底层结构**：JDK8+采用数组+链表+红黑树，类似HashMap但线程安全
- **实现原理**：
  - ==JDK7使用分段锁==
  - ==JDK8+使用CAS+synchronized锁单个桶==
  - ==读操作通常无锁==
- **特点**：
  - ==线程安全==
  - ==高并发性能优于Hashtable==

### 5. Hashtable
- **底层结构**：==数组+链表==
- **实现原理**：
  - 类似HashMap但==方法使用synchronized修饰==
- **特点**：
  - ==线程安全==但性能较差
  - ==不允许null键和null值==

## Set接口的实现类

Set的实现基本都是基于对应的Map实现：

### 1. HashSet
- **底层结构**：==基于HashMap==
- **实现原理**：
  - 使用HashMap存储元素，==值统一为PRESENT对象==
- **特点**：
  - ==无序==
  - 允许null元素
  
|特性|说明|
|---|---|
|**自动去重**|重复元素无法插入，直接避免重复解。|
|**O(1) 时间复杂度**|插入和查询操作平均时间复杂度为 `O(1)`，高效。|
|**代码简洁**|无需手动写循环判断是否重复，直接依赖 `HashSet` 的特性。|

### 2. LinkedHashSet
- **底层结构**：基于LinkedHashMap
- **实现原理**：
  - 继承HashSet，使用LinkedHashMap存储
- **特点**：
  - 保持插入顺序

### 3. TreeSet
- **底层结构**：基于TreeMap
- **实现原理**：
  - 使用TreeMap存储元素
- **特点**：
  - 元素有序
  - ==不允许null元素（取决于Comparator）==
## List接口的实现类

### 1. ArrayList
- **底层结构**：==动态数组==
- **实现原理**：
  - 初始容量10，==扩容时增加50%==（newCapacity = oldCapacity + (oldCapacity >> 1)）
  - ==使用System.arraycopy()进行数组拷贝==
- **特点**：
  - ==随机访问快(O(1))==
  - ==插入删除慢（需要移动元素）==

### 2. LinkedList
- **底层结构**：==双向链表==
- **实现原理**：
  - ==每个元素(Node)包含前后指针==
- **特点**：
  - ==插入删除快(O(1))==
  - ==随机访问慢(O(n))==

### 3. Vector
- **底层结构**：类似ArrayList但==线程安全==
- **实现原理**：
  - 方法==使用synchronized修饰==
  - ==扩容默认增加一倍==
- **特点**：
  - ==线程安全==但性能较差

## Queue/Deque接口的实现类

### 1. PriorityQueue
- **底层结构**：二叉堆（数组实现）
- **实现原理**：
  - 默认小顶堆
  - 通过Comparator可自定义排序
- **特点**：
  - 出队顺序按优先级

### 2. ArrayDeque
- **底层结构**：循环数组
- **实现原理**：
  - 头尾指针实现双端操作
  - 扩容时加倍
- **特点**：
  - 比LinkedList更高效（数组局部性原理）

## 性能分析要点

1. **时间复杂度**：
   - HashMap：理想情况下O(1)，最坏O(log n)（红黑树）
   - TreeMap：O(log n)
   - ArrayList：随机访问O(1)，插入删除O(n)
   - LinkedList：插入删除O(1)，随机访问O(n)

2. **空间考虑**：
   - 链表结构比数组占用更多内存（需要存储指针）
   - 负载因子影响HashMap空间利用率

3. **并发场景**：
   - ConcurrentHashMap优于Hashtable
   - CopyOnWriteArrayList适合读多写少场景

理解这些底层实现可以帮助你在不同场景下选择合适的容器，并能够准确分析代码性能。


# `synchronized`关键字详解

`synchronized`是Java中用于==实现线程同步==的关键字，它提供了一种简单的机制来确保线程安全，防止多个线程同时访问共享资源导致的数据不一致问题。

## 基本概念

`synchronized`可以理解为一种"锁"机制，它有以下特性：
- ==**互斥性**==：同一时刻只有一个线程可以获取锁
- ==**可见性**==：锁释放前对共享变量的修改对其他线程可见
- ==**可重入性**==：同一个线程可以重复获取已经持有的锁

## 三种使用方式

### 1. 同步实例方法

```java
public synchronized void method() {
    // 同步代码
}
```

**特点**：
- **锁对象**是**当前实例对象(this)**
- 同一实例的多个同步方法互斥
- 不同实例的方法不互斥

### 2. 同步静态方法

```java
public static synchronized void staticMethod() {
    // 同步代码
}
```

**特点**：
- 锁对象是**当前类的Class对象(类名.class)**
- 所有调用该静态方法的线程都会互斥
- 与实例方法的锁不同，不会互斥

### 3. 同步代码块

```java
public void method() {
    // 非同步代码
    
    synchronized(lockObject) {
        // 同步代码
    }
    
    // 非同步代码
}
```

**特点**：
- **可以灵活指定锁对象**
- 锁对象可以是任意对象实例(**通常使用专门的对象作为锁**)
- 比同步方法更细粒度的控制

## 底层实现原理

### 1. JVM层面的实现

`synchronized`在JVM中的实现基于**Monitor**(监视器)机制：
- 每个Java对象都有一个关联的Monitor
- Monitor包含以下几个关键部分：
  - _ owner：持有锁的线程
  - _ EntryList：等待获取锁的线程队列
  - _ WaitSet：调用wait()后等待的线程队列

### 2. 字节码层面

同步代码块在字节码中表现为：
- `monitorenter`：进入同步块
- `monitorexit`：退出同步块
- 编译器会自动插入异常处理确保锁释放

### 3. 锁升级过程(JDK6+优化)

现代JVM中，`synchronized`经历了锁升级优化：
1. **无锁状态**：初始状态
2. **偏向锁**：只有一个线程访问时，记录线程ID
3. **轻量级锁(自旋锁)**：有少量竞争时，通过CAS获取锁
4. **重量级锁**：竞争激烈时，升级为操作系统级别的互斥锁

## 使用注意事项

1. **锁对象选择**：
   - 不要使用String常量等可能被共享的对象作为锁
   - 推荐==使用专门创建的Object作为私有锁==

2. **性能考虑**：
   - 同步范围应尽可能小
   - 避免在同步块中执行耗时操作
   - 考虑使用更高性能的并发工具(如ReentrantLock)

3. **死锁风险**：
   - 避免嵌套获取多个锁
   - 如果需要获取多个锁，应确定固定顺序

## 与Lock接口的对比

| 特性                | synchronized | Lock接口实现类 |
|---------------------|-------------|---------------|
| 获取锁方式           | 自动获取释放 | 需要手动lock/unlock |
| 可中断性             | 不支持       | 支持            |
| 公平锁               | 非公平       | 可配置公平/非公平 |
| 尝试获取锁           | 不支持       | 支持tryLock     |
| 条件变量             | 单一wait/notify | 支持多个Condition |
| 性能                 | JDK6+优化后较好 | 通常更优        |

`synchronized`是Java中最基础的同步机制，虽然功能不如`java.util.concurrent.locks`包中的锁丰富，但在大多数情况下已经足够，且使用更简单。

## 继承
```java
class SuperClass { 
	private int n; 
	// 无参数构造器 
	public SuperClass() { 
		System.out.println("SuperClass()"); 
	} 
	// 带参数构造器 
	public SuperClass(int n) { 
		System.out.println("SuperClass(int n)"); 
		this.n = n; 
	} 
} 
// SubClass 类继承 
class SubClass extends SuperClass { 
	private int n; 
	// 无参数构造器，自动调用父类的无参数构造器 
	public SubClass() { 
		System.out.println("SubClass()"); 
	} 
	// 带参数构造器，调用父类中带有参数的构造器 
	public SubClass(int n) { 
		super(300); 
		System.out.println("SubClass(int n): " + n); 
		this.n = n; 
	} 
}
```

## JVM
JVM（Java Virtual Machine）是Java程序运行的核心组件，负责将Java字节码转换为机器码并执行。它提供了内存管理、垃圾回收（GC）、线程管理等关键功能，确保Java程序跨平台运行（"Write Once, Run Anywhere"）。
### **Q1: OOM（OutOfMemoryError）怎么处理？**

- **堆内存不足**：调整 `-Xmx`，检查内存泄漏。
- **元空间不足**：调整 `-XX:MetaspaceSize`。
- **线程栈溢出**：减少 `-Xss`（默认1MB）。
    
### **Q2: 如何排查CPU 100%？**

1. `top` 找到高CPU的Java进程。
2. `jstack <pid>` 分析线程栈，定位耗时方法。
    

### **Q3: G1 和 CMS 的区别？**

|**对比项**|**G1**|**CMS**|
|---|---|---|
|**算法**|分Region标记-整理|并发标记-清除|
|**延迟**|可控（`MaxGCPauseMillis`）|不可控（可能并发失败）|
|**内存**|无碎片|有碎片（需Full GC整理）|

## StringBuilder

| 特性        | 说明                                |
| --------- | --------------------------------- |
| **可变性**   | 内容可以修改，不会创建新对象                    |
| **非线程安全** | 不适合多线程环境（多线程用 `StringBuffer`）     |
| **高性能**   | 比 `String` 的拼接（`+` 或 `concat`）快很多 |
| **自动扩容**  | 初始容量不够时自动增加缓冲区大小                  |

| 方法                       | 说明           | 示例                                      |
| ------------------------ | ------------ | --------------------------------------- |
| **`append(x)`**          | 追加内容（支持各种类型） | `sb.append(" World")` → `"Hello World"` |
| **`insert(index, x)`**   | 在指定位置插入      | `sb.insert(5, ",")` → `"Hello, World"`  |
| **`delete(start, end)`** | 删除子串         | `sb.delete(5, 6)` → `"Hello World"`     |
| **`reverse()`**          | 反转字符串        | `sb.reverse()` → `"dlroW olleH"`        |
| **`toString()`**         | 转为 `String`  | `String s = sb.toString()`              |
| **`length()`**           | 返回当前长度       | `int len = sb.length()`                 |
| **`setLength(n)`**       | 设置长度（截断或填充）  | `sb.setLength(5)` → `"Hello"`           |

## s.length 和  s.length() 的区别

|情况|语法|适用对象|示例|
|---|---|---|---|
|**数组**|`s.length`|数组（`int[]`, `String[]` 等）|`int[] arr = {1, 2, 3};`  <br>`int len = arr.length;`|
|**字符串**|`s.length()`|`String` 对象|`String s = "hello";`  <br>`int len = s.length();`|

- **`length`** → **数组**（`int[]`, `String[]` 等）。
    
- **`length()`** → **字符串**（`String`）。
    
- **`size()`** → **集合类**（`List`, `Set`, `Map` 等）。