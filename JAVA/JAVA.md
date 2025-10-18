# 基本语法
1. 大小写敏感：**类名、接口名**首字母大写，**方法名**首字母小写。
2. **源文件名**必须和**类名**相同
3. 所有程序都是从public static void main(String[ ], args);开始
4. 标识符：类名、变量名、方法名、包名、常量名等。以字母、$、_ 、 开头。
5. **优先级**：`!` > `&&` > `||`
6. **`new boolean[n]`**：创建一个长度为 `n` 的布尔数组，初始值全为 `false`
7. Java 中基本数据类型（如 `int`）的参数传递是**值传递**，方法内修改不会影响原始变量。
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
8.  Character方法

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
9. **典型用途**：**快速初始化二维矩阵的某一行或列**。
	**`Arrays.fill(char[] a, char val)`**：      将字符数组 `a` 的所有元素赋值为 `val`。
	
10. 将字符数组 `data` 转换为一个新的 `String` 对象：**`String.copyValueOf(char[] data)`**
	
| **方法**                  | **区别**                                       |
| ----------------------- | -------------------------------------------- |
| `String.copyValueOf(c)` | 静态工厂方法，内部实际调用 `new String(c)`，语义更清晰（强调“拷贝”）。 |
| `new String(c)`         | 直接调用构造函数，功能相同。                               |
**本质无区别**：两者最终都创建新字符串，但 `copyValueOf` 可读性更好（适合处理字符数组）。
	
9. 将一个字符（`char`）转换为字符串，然后再解析为整数。 **Integer.parseInt(c + "")**
```java
char c = '5'; // 这是一个字符

// 分解步骤：
String str = c + "";    // 字符转换为字符串 → "5"
int num = Integer.parseInt(str); // 字符串解析为整数 → 5
```
	
10. (len & 1) == 0 ：速度快在某些底层优化场景中更高效
	偶数：二进制最低位为0
	奇数：二进制最低位为1
	&：位与运算，&1操作会保留最低位，其他位变为0；；所以偶数&1=0，奇数&1=1
	

### Stream
是collection集合类提供的方法，将集合转化为流Stream，进行函数式操作
不是数据结构，是对数据源（集合，数组）元素序列进行函数式操作的管道

1. 创建：Stream< String> stream = xxx.stream();   // xxx可以为集合数组list，arrays
    直接创建：Stream< String> stream = Stream.of("a", "b"); 
2. stream操作管道的组成
	```Java
	List<String> result = list.stream()    //源操作，顺序流
		.parallel()                        //并行流，根据情况选择，并不总是最快
		.filter(s -> s.length() > 3)       //中间操作（无状态
		.map(String::toUpperCase)         //中间操作（只构建不执行
		.collect(Collectors.toList());   //终端操作
	```
3. 终端操作
	```java
	List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
	 // forEach - 遍历
	names.stream().forEach(System.out::println);

	// collect - 收集为集合
	List<String> result = names.stream()
    .filter(name -> name.startsWith("A"))
    .collect(Collectors.toList());

	// count - 计数
	long count = names.stream().count();

	// anyMatch/allMatch/noneMatch - 匹配检查
	boolean hasA = names.stream().anyMatch(name -> name.startsWith("A"));

	// reduce - 归约
	Optional<String> concatenated = names.stream()
    .reduce((a, b) -> a + ", " + b);
	```
4. 中间操作
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

// filter - 过滤
Stream<String> filtered = names.stream()
    .filter(name -> name.length() > 3);

// map - 转换
Stream<Integer> lengths = names.stream()
    .map(String::length);

// sorted - 排序
Stream<String> sorted = names.stream()
    .sorted();

// distinct - 去重
Stream<String> distinct = names.stream()
    .distinct();

// limit - 限制数量
Stream<String> limited = names.stream()
    .limit(2);
```
5. 流只能使用一次
6. 空值处理：Optional

### 栈stack

#### **`Stack<TreeNode> stack = new Stack<>();` 详解**

在Java中，`Stack` 是一种 **后进先出（LIFO, Last In First Out）** 的线性数据结构，专门用于存储和操作数据。在您的代码中：

```java
Stack<TreeNode> stack = new Stack<>();
```

- **`Stack<TreeNode>`** 表示这是一个 **存储 `TreeNode` 对象** 的栈。
- **`new Stack<>()`** 创建了一个 **空栈**（使用 **泛型** 确保类型安全）。

---

##### **1. `Stack` 的基本特性**
| **特性**       | **说明** |
|--------------|---------|
| **数据结构**   | 后进先出（LIFO） |
| **继承关系**   | `Stack` 继承自 `Vector`（线程安全，但性能较低） |
| **主要方法**   | `push()`、`pop()`、`peek()`、`empty()`、`search()` |
| **线程安全**   | ✅ 是（所有方法用 `synchronized` 修饰） |
| **推荐替代**   | `Deque`（如 `ArrayDeque`，性能更高） |

---

##### **2. `Stack` 的常用方法**
###### **（1）`push(E item)` - 入栈**
```java
stack.push(node1);  // 将元素压入栈顶
stack.push(node2);
```
- **栈状态**：`[node2, node1]`（`node2` 在栈顶）

###### **（2）`pop()` - 出栈**
```java
TreeNode topNode = stack.pop();  // 移除并返回栈顶元素
```
- **栈状态**：`[node1]`（`node2` 被移除）
- **如果栈为空**：抛出 `EmptyStackException`

###### **（3）`peek()` - 查看栈顶元素（不移除）**
```java
TreeNode topNode = stack.peek();  // 返回栈顶元素但不移除
```
- **栈状态**：`[node2, node1]`（仍保留 `node2`）

###### **（4）`empty()` - 判断栈是否为空**
```java
boolean isEmpty = stack.empty();  // true 或 false
```

###### **（5）`search(Object o)` - 查找元素位置**
```java
int position = stack.search(node1);  // 返回元素位置（从栈顶开始计数，1-based）
```
- **如果不存在**：返回 `-1`

---

##### **3. `Stack` 的底层实现**
- **基于 `Vector`**（动态数组）实现：
  ```java
  public class Stack<E> extends Vector<E> { ... }
  ```
- **核心操作**：
  - `push()`：调用 `addElement(item)`（在数组末尾添加）
  - `pop()`：调用 `removeElementAt(size() - 1)`（移除最后一个元素）
- **线程安全**：所有方法用 `synchronized` 修饰（性能较低）。

---

##### **4. 为什么推荐使用 `Deque` 替代 `Stack`？**
| **对比项**       | **`Stack`** | **`Deque`（如 `ArrayDeque`）** |
|----------------|------------|-----------------------------|
| **继承体系**     | 继承 `Vector`（历史遗留） | 独立接口，实现类更灵活 |
| **线程安全**     | ✅ 是（同步开销大） | ❌ 否（但性能更高） |
| **功能扩展**     | 仅支持LIFO | 支持LIFO和FIFO（双端操作） |
| **性能**        | 较低（同步锁） | 更高（无锁竞争） |
| **推荐场景**     | 旧代码兼容 | 新代码首选 |

###### **使用 `ArrayDeque` 实现栈**
```java
Deque<TreeNode> stack = new ArrayDeque<>();  // 推荐替代方案
stack.push(node1);  // 入栈
TreeNode topNode = stack.pop();  // 出栈
```

---

##### **5. 典型应用场景**
###### **（1）深度优先搜索（DFS）**
```java
Stack<TreeNode> stack = new Stack<>();
stack.push(root);
while (!stack.empty()) {
    TreeNode node = stack.pop();
    if (node.right != null) stack.push(node.right);
    if (node.left != null) stack.push(node.left);
}
```

###### **（2）括号匹配检查**
```java
Stack<Character> stack = new Stack<>();
for (char c : s.toCharArray()) {
    if (c == '(') stack.push(')');
    else if (stack.isEmpty() || stack.pop() != c) return false;
}
return stack.isEmpty();
```

---

##### **6. 总结**
- **`Stack<TreeNode> stack = new Stack<>();`** 创建了一个 **存储 `TreeNode` 的栈**。
- **核心操作**：`push()`、`pop()`、`peek()`。
- **底层实现**：基于 `Vector`（动态数组），线程安全但性能较低。
- **现代替代方案**：优先使用 `Deque`（如 `ArrayDeque`），性能更高。

如果不需要线程安全，建议使用 `ArrayDeque` 代替 `Stack`！ 🚀



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

- **键（Key）和值（Value）均为 `Integer` 类型的 `HashMap`**：HashMap<Integer,Integer> map = new HashMap<>();

| 方法                                              | 功能说明                                                                                                                                                             | 示例                                                                                                                         |
| ----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `map.put(key, value)`                           | 插入键值对                                                                                                                                                            | `map.put(1, 100)`                                                                                                          |
| `map.get(key)`                                  | 获取键对应的值（不存在返回 `null`）                                                                                                                                            | `map.get(1)` → `100`                                                                                                       |
| `map.containsKey(key)`                          | 检查键是否存在                                                                                                                                                          | `map.containsKey(1)` → `true`                                                                                              |
| `map.remove(key)`                               | 删除键值对                                                                                                                                                            | `map.remove(1)`                                                                                                            |
| `map.size()`                                    | 返回键值对数量                                                                                                                                                          | `map.size()` → `1`                                                                                                         |
| `map.keySet()`                                  | 返回所有键的集合                                                                                                                                                         | `map.keySet()` → `[1]`                                                                                                     |
| **`map.getOrDefault(key, defaultValue)`**       | - 如果 `key`（即 `nums[i]`）存在于 `map` 中，返回对应的 `value`。<br>    <br>- 如果 `key` 不存在，返回默认值 `defaultValue`（这里设为 `0`）。                                                      | map.getOrDefault(key, 0) == 2<br>检查值是否等于某个数                                                                                |
| map.**merge**(key, value, Integer: :sum);       | 1. 如果键 `x` 在 map 中不存在：直接插入键值对：`x → 1`<br>2. 如果键 `x` 在 map 中已存在：1. 取出旧值 oldValue； 2. 计算新值：`Integer.sum(oldValue, 1)` （即 `oldValue + 1`）；3. 更新键值对：x → oldValue + 1 | 相当于<br>if (map.containsKey(key)) {<br>    map.put(key, map.get(key) + value);<br>} else {<br>    map.put(key, value);<br>} |
| int maxCnt = Collections.max(cnt.values());<br> | 获取Map中值的最大值<br>- **时间复杂度**：O(n)，需要遍历所有值<br>- **空间复杂度**：O(1)，不需要额外空间                                                                                              | 1. **`cnt.values()`** - 返回Map中所有值的Collection视图<br>2. **`Collections.max()`** - 返回集合中的最大元素                                  |

| 方法                       | 行为             | 风险                       |
| ------------------------ | -------------- | ------------------------ |
| `map.getOrDefault(k, 0)` | 键不存在时返回默认值 `0` | 无 `NullPointerException` |
| `map.get(k)`             | 键不存在时返回 `null` | 需判空，否则可能报错               |
**将map中的值按降序排序：**
List< Integer> freq = new ArrayList<>(cnt.values());
freq.sort(Collections.reverseOrder());
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
- 详细:
1. **Node 数组（Table）**：
    
    - 底层依然是一个 `Node<K,V>[] table` 数组。
        
    - 数组的每个位置称为一个 **"桶"**。
        
2. **链表和红黑树**：
    
    - 当发生哈希冲突时，会在同一个桶上形成链表（`Node` 结构）。
        
    - 当链表的长度超过一定阈值（默认为 **8**），并且数组的总长度大于等于 **64** 时，链表会转换为**红黑树**（`TreeNode` 结构）。
        
    - 当树的大小缩小到一定阈值（默认为 **6**）时，会退化为链表。
        
    - **为什么用红黑树？** 为了防止在极端情况下（哈希函数极差，所有元素都哈希到同一个桶），链表变得非常长，导致查询效率从O(1)退化为O(n)。红黑树能保证查询效率维持在O(log n)。
        
3. **并发控制机制（核心！）**：
    
    - **CAS + synchronized**：这是CHM实现高并发的关键。
        
    - 对**数组桶位的写操作**（如put, remove）：
        
        - 首先通过CAS操作**定位到具体的桶**。
            
        - 如果这个桶是空的（`null`），则直接用**CAS**来尝试写入新节点，避免了加锁。
            
        - 如果CAS失败（说明有其他线程在竞争），或者桶不为空（已有链表或树），则对这个桶的**头节点（第一个元素）** 使用 **`synchronized` 关键字进行加锁**。锁的粒度非常细，只锁住当前操作的这一个桶，其他桶的操作不受影响，极大提升了并发度。
            
    - **读操作**（如get）：
        
        - **通常完全无锁**，因为 `Node` 的 `val` 和 `next` 属性都用 `volatile` 修饰，保证了线程间的可见性。读操作可以安全地与其他读操作甚至某些写操作并发执行。
            

**对比JDK 1.7：**  
JDK 1.7使用**分段锁（Segment）**，将数组分成多个段，每个段一把锁。写操作锁住一个段，读操作基本无锁。但1.8的 `synchronized` + CAS 方案锁粒度更细（从段级别细化到桶级别），并且在JVM对 `synchronized` 做了大量优化（偏向锁、轻量级锁）后，性能更高。

**CAS** 是 **Compare-And-Swap** 的缩写，中文叫**比较并交换**。它是一种**无锁的**、**乐观的**原子操作算法。
工作原理：
	它包含三个操作数：
	1. **V**：要更新的内存位置（变量当前值）。
	2. **A**：期望的旧值（我认为的当前值）。
	3. **B**：想要设置的新值。
	    
**执行流程**：**“我认为位置 V 的值应该是 A。如果是，那么将 V 的值更新为 B；否则，什么都不做，并告诉我现在 V 的值实际是什么。”**

这个操作是一个**原子操作**，由CPU指令（如x86架构下的 `CMPXCHG` 指令）保证，不会被线程调度机制打断。

#### Java中的体现：
在Java中，CAS操作通过 `sun.misc.Unsafe` 类中的本地方法（`compareAndSwapObject`, `compareAndSwapInt`, `compareAndSwapLong`）实现。JUC包中的很多原子类（如 `AtomicInteger`）都基于CAS。
```java
// 一个典型的CAS使用示例：AtomicInteger的incrementAndGet
public final int incrementAndGet() {
    return U.getAndAddInt(this, VALUE, 1) + 1;
}

// Unsafe.getAndAddInt 内部实现
public final int getAndAddInt(Object o, long offset, int delta) {
    int v;
    do {
        v = getIntVolatile(o, offset); // 获取当前值，作为期望值A
        // 尝试用CAS更新：如果内存位置的值还是v，就把它设置为v+delta
        // 如果不是，循环重试（自旋）
    } while (!compareAndSwapInt(o, offset, v, v + delta));
    return v;
}
```

#### CAS的优缺点：

- **优点**：
    
    - **高性能**：避免了重量级锁（如 `synchronized`）带来的线程阻塞和唤醒的开销。
        
- **缺点**：
    
    1. **ABA问题**：（下面详细讲）
        
    2. **循环时间长开销大**：如果CAS长时间不成功，自旋会给CPU带来很大开销。
        
    3. **只能保证一个共享变量的原子操作**：对于多个共享变量，CAS无法保证原子性，但可以用 `AtomicReference` 来封装对象。

ABA问题是CAS机制的一个经典漏洞。

1. 线程1从内存位置V中取出值A。
    
2. 此时，线程2也从V中取出值A，并将其**先改为B，然后又改回A**。
    
3. 线程1接着进行CAS操作，它发现内存中的值仍然是A，于是**误以为没有人修改过**，操作成功。
    

**尽管线程1的CAS操作成功了，但这个过程可能已经产生了非预期的后果**（例如，链表结构可能已经发生了变化）。

#### 解决方案：原子引用 + 版本号

ABA问题的根源是状态值循环往复，无法区分“原值未变”和“原值变了又变回来”两种情况。解决方案是**不仅仅比较值，还要比较版本号**。

Java提供了 `AtomicStampedReference` 类来解决这个问题。

- `AtomicStampedReference<V>`：它维护了一个对象引用和一个整数“版本号”（Stamp）。每次修改版本号都会增加。
    
- CAS操作时，需要同时检查**当前引用**和**当前版本号**是否都与期望值一致，只有两者都一致时，才会更新成功。
    
```java
// 初始值为100，版本号为0
AtomicStampedReference<Integer> atomicStampedRef = new AtomicStampedReference<>(100, 0);

int expectedStamp = atomicStampedRef.getStamp(); // 获取当前版本号
Integer expectedReference = atomicStampedRef.getReference(); // 获取当前值

// 模拟中间有其他线程插队：A -> B -> A，并且版本号变了2次
atomicStampedRef.compareAndSet(100, 101, expectedStamp, expectedStamp + 1); // 成功，版本号变1
atomicStampedRef.compareAndSet(101, 100, 1, 2); // 成功，版本号变2

// 线程1现在尝试CAS
boolean success = atomicStampedRef.compareAndSet(
    expectedReference, // 期望值还是100
    200,               // 想更新为200
    expectedStamp,     // 期望版本号是0
    expectedStamp + 1  // 新版本号想设为1
);

System.out.println(success); // 输出 false！因为当前版本号是2，不等于期望的0，所以CAS失败。
```

**核心**：`AtomicStampedReference` 通过引入一个单调递增的**版本号**，使得“A->B->A”这种状态变化可以被探测到，从而有效解决了ABA问题。

**另一种方案**：`AtomicMarkableReference`，它用一个布尔值（`boolean`）来标记是否被修改过，适用于不关心修改次数，只关心**是否被修改过**的场景。

### 5. Hashtable
- **底层结构**：==数组+链表==
- **实现原理**：
  - 类似HashMap但==方法使用synchronized修饰==
- **特点**：
  - ==线程安全==但性能较差
  - ==不允许null键和null值==

### 6. 区别

| 需求        | 推荐类                 | 区别              |
| --------- | ------------------- | --------------- |
| **需要有序键** | `LinkedHashMap`     | 保持插入顺序或访问顺序     |
| **需要排序键** | `TreeMap`           | 按键的自然顺序或自定义顺序排序 |
| **线程安全**  | `ConcurrentHashMap` | 支持高并发操作         |

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

#### 1. 添加元素
```java
// 创建HashSet
HashSet<String> set = new HashSet<>();

// add(E e) - 添加元素，成功返回true，重复则返回false
boolean added1 = set.add("苹果"); // true
boolean added2 = set.add("苹果"); // false (重复元素)
boolean added3 = set.add("香蕉"); // true
boolean added4 = set.add(null);   // true (可以添加null)

System.out.println(set); // [null, 苹果, 香蕉]
```

#### 2. 删除元素
```java
// remove(Object o) - 删除指定元素，存在则删除并返回true
boolean removed1 = set.remove("苹果"); // true
boolean removed2 = set.remove("橘子"); // false (元素不存在)

// clear() - 清空所有元素
set.clear();
System.out.println(set); // []
```

#### 3. 检查元素是否存在
```java
set.add("苹果");
set.add("香蕉");

// contains(Object o) - 检查是否包含某元素
boolean hasApple = set.contains("苹果"); // true
boolean hasOrange = set.contains("橘子"); // false
```

#### 4. 集合信息查询
```java
// size() - 获取元素个数
int size = set.size(); // 2

// isEmpty() - 判断集合是否为空
boolean empty = set.isEmpty(); // false
```

#### 5. 集合操作
```java
HashSet<String> set1 = new HashSet<>();
set1.add("苹果");
set1.add("香蕉");
set1.add("橘子");

HashSet<String> set2 = new HashSet<>();
set2.add("香蕉");
set2.add("葡萄");
set2.add("芒果");

// addAll(Collection c) - 并集（添加另一个集合的所有元素）
set1.addAll(set2);
System.out.println("并集: " + set1); // [苹果, 葡萄, 橘子, 芒果, 香蕉]

// retainAll(Collection c) - 交集（只保留两个集合都有的元素）
set1.retainAll(set2);
System.out.println("交集: " + set1); // [葡萄, 芒果, 香蕉]

// removeAll(Collection c) - 差集（移除另一个集合中的所有元素）
set1.removeAll(set2);
System.out.println("差集: " + set1); // []
```

#### 6. 遍历集合
```java
HashSet<String> fruits = new HashSet<>();
fruits.add("苹果");
fruits.add("香蕉");
fruits.add("橘子");

// 方法1：增强for循环（最常用）
System.out.println("增强for循环:");
for (String fruit : fruits) {
    System.out.println(fruit);
}

// 方法2：迭代器Iterator
System.out.println("迭代器遍历:");
Iterator<String> iterator = fruits.iterator();
while (iterator.hasNext()) {
    String fruit = iterator.next();
    System.out.println(fruit);
}

// 方法3：Java 8+ Stream API
System.out.println("Stream遍历:");
fruits.stream().forEach(System.out::println);

// 方法4：转换为数组遍历
System.out.println("数组遍历:");
String[] fruitArray = fruits.toArray(new String[0]);
for (String fruit : fruitArray) {
    System.out.println(fruit);
}
```

#### 7. 集合转换
```java
// toArray() - 转换为数组
Object[] array = fruits.toArray();
String[] strArray = fruits.toArray(new String[0]);

// 从数组创建HashSet
String[] newFruits = {"梨", "桃子"};
HashSet<String> newSet = new HashSet<>(Arrays.asList(newFruits));
```

#### 完整综合示例

```java
import java.util.HashSet;
import java.util.Iterator;

public class HashSetMethodsDemo {
    public static void main(String[] args) {
        // 创建HashSet
        HashSet<String> shoppingCart = new HashSet<>();
        
        // 1. 添加商品
        shoppingCart.add("手机");
        shoppingCart.add("耳机");
        shoppingCart.add("充电器");
        shoppingCart.add("手机"); // 重复添加，无效
        
        System.out.println("购物车商品: " + shoppingCart);
        System.out.println("商品数量: " + shoppingCart.size());
        
        // 2. 检查商品
        System.out.println("有耳机吗? " + shoppingCart.contains("耳机"));
        System.out.println("有电脑吗? " + shoppingCart.contains("电脑"));
        
        // 3. 移除商品
        shoppingCart.remove("充电器");
        System.out.println("移除充电器后: " + shoppingCart);
        
        // 4. 遍历购物车
        System.out.println("购物车商品列表:");
        for (String item : shoppingCart) {
            System.out.println("- " + item);
        }
        
        // 5. 清空购物车
        shoppingCart.clear();
        System.out.println("清空后是否为空? " + shoppingCart.isEmpty());
    }
}
```

#### 方法总结表

| 方法 | 返回值 | 描述 |
|------|--------|------|
| `add(E e)` | `boolean` | 添加元素，成功返回true |
| `remove(Object o)` | `boolean` | 删除元素，成功返回true |
| `contains(Object o)` | `boolean` | 检查是否包含元素 |
| `size()` | `int` | 返回元素个数 |
| `isEmpty()` | `boolean` | 判断集合是否为空 |
| `clear()` | `void` | 清空所有元素 |
| `iterator()` | `Iterator<E>` | 返回迭代器 |
| `toArray()` | `Object[]` | 转换为数组 |
| `addAll(Collection c)` | `boolean` | 添加另一个集合的所有元素（并集） |
| `retainAll(Collection c)` | `boolean` | 保留两个集合都有的元素（交集） |
| `removeAll(Collection c)` | `boolean` | 移除另一个集合中的所有元素（差集） |

这些方法涵盖了 `HashSet` 95% 的日常使用场景，掌握它们就能熟练使用 `HashSet` 了。

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


# LinkedList的常用方法

LinkedList是Java集合框架中的一个重要实现，它实现了List接口和Deque接口，既可以作为列表使用，也可以作为队列或栈使用。

## 1. 基本操作

### 创建LinkedList
```java
// 创建空的LinkedList
LinkedList<String> list = new LinkedList<>();

// 从其他集合创建
List<String> initialList = Arrays.asList("A", "B", "C");
LinkedList<String> list2 = new LinkedList<>(initialList);
```

## 2. 添加元素

```java
LinkedList<String> list = new LinkedList<>();

// 在末尾添加元素
list.add("Apple");
list.addLast("Banana"); // 同add()

// 在开头添加元素
list.addFirst("First");

// 在指定位置插入元素
list.add(1, "Orange");

// 使用offer方法（队列操作）
list.offer("Grape");     // 添加到末尾
list.offerFirst("Mango"); // 添加到开头
list.offerLast("Peach");  // 添加到末尾

System.out.println(list); // [Mango, First, Apple, Orange, Banana, Grape, Peach]
```

## 3. 获取元素

```java
LinkedList<String> list = new LinkedList<>(Arrays.asList("A", "B", "C", "D"));

// 根据索引获取
String first = list.get(0);        // "A"
String firstElement = list.getFirst(); // "A"
String lastElement = list.getLast();   // "D"

// 队列方式获取（不删除）
String peek = list.peek();        // 获取第一个元素
String peekFirst = list.peekFirst(); // 获取第一个元素
String peekLast = list.peekLast();   // 获取最后一个元素

// 获取元素索引
int index = list.indexOf("B");    // 1
int lastIndex = list.lastIndexOf("C"); // 2
```

## 4. 删除元素

```java
LinkedList<String> list = new LinkedList<>(Arrays.asList("A", "B", "C", "D", "E"));

// 根据索引删除
String removed = list.remove(1);  // 删除并返回"B"

// 删除指定元素
boolean success = list.remove("C"); // true

// 删除首尾元素
String first = list.removeFirst(); // 删除并返回"A"
String last = list.removeLast();   // 删除并返回"E"

// 队列方式删除
String poll = list.poll();        // 删除并返回第一个元素
String pollFirst = list.pollFirst(); // 删除并返回第一个元素
String pollLast = list.pollLast();   // 删除并返回最后一个元素

// 清空列表
list.clear();
```

## 5. 栈操作（LIFO）

```java
LinkedList<String> stack = new LinkedList<>();

// 压栈
stack.push("First");   // 添加到开头
stack.push("Second");
stack.push("Third");

// 出栈
String top = stack.pop(); // "Third" - 移除并返回第一个元素

// 查看栈顶
String peek = stack.peek(); // "Second" - 查看第一个元素但不移除

System.out.println(stack); // [Second, First]
```

## 6. 队列操作（FIFO）

```java
LinkedList<String> queue = new LinkedList<>();

// 入队
queue.offer("First");
queue.offer("Second");
queue.offer("Third");

// 出队
String head = queue.poll(); // "First" - 移除并返回第一个元素

// 查看队首
String peek = queue.peek(); // "Second" - 查看第一个元素但不移除

System.out.println(queue); // [Second, Third]
```

## 7. 遍历操作

```java
LinkedList<String> list = new LinkedList<>(Arrays.asList("A", "B", "C", "D"));

// 1. for循环
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}

// 2. 增强for循环
for (String item : list) {
    System.out.println(item);
}

// 3. 迭代器
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    System.out.println(iterator.next());
}

// 4. 降序迭代器
Iterator<String> descIterator = list.descendingIterator();
while (descIterator.hasNext()) {
    System.out.println(descIterator.next()); // 从后往前遍历
}

// 5. forEach方法（Java 8+）
list.forEach(item -> System.out.println(item));
list.forEach(System.out::println);
```

## 8. 其他常用方法

```java
LinkedList<String> list = new LinkedList<>(Arrays.asList("A", "B", "C"));

// 检查元素是否存在
boolean contains = list.contains("B"); // true

// 获取大小
int size = list.size(); // 3

// 检查是否为空
boolean empty = list.isEmpty(); // false

// 转换为数组
Object[] array = list.toArray();
String[] strArray = list.toArray(new String[0]);

// 设置指定位置的元素
list.set(1, "NewB"); // 将索引1的元素改为"NewB"

// 子列表
List<String> subList = list.subList(0, 2); // [A, NewB]
```

## 9. 实际应用示例

```java
public class LinkedListExample {
    public static void main(String[] args) {
        // 作为队列使用
        LinkedList<String> queue = new LinkedList<>();
        queue.offer("Task1");
        queue.offer("Task2");
        queue.offer("Task3");
        
        while (!queue.isEmpty()) {
            String task = queue.poll();
            System.out.println("Processing: " + task);
        }
        
        // 作为栈使用
        LinkedList<String> stack = new LinkedList<>();
        stack.push("Page1");
        stack.push("Page2");
        stack.push("Page3");
        
        while (!stack.isEmpty()) {
            String page = stack.pop();
            System.out.println("Back to: " + page);
        }
    }
}
```

## 性能特点

- **优点**：
  - 插入和删除操作快（O(1)）
  - 实现了List和Deque接口，功能丰富
  - 动态大小，无需预先指定容量

- **缺点**：
  - 随机访问较慢（O(n)）
  - 占用内存比ArrayList多（每个元素需要额外的节点对象）

选择LinkedList还是ArrayList取决于具体的使用场景：频繁插入删除选LinkedList，频繁随机访问选ArrayList。
# Deque< Integer> s = new LinkedList<>() vs Stack< Integer> s = new Stack<>()

这两者都是栈的实现，但它们有重要的区别：

## 1. 所属的API体系不同

```java
// Java 1.0 的老式实现（不推荐）
Stack<Integer> stack = new Stack<>();

// Java 1.6+ 的现代实现（推荐）
Deque<Integer> deque = new LinkedList<>();
```

## 2. 方法命名差异

| 操作 | `Stack` 方法 | `Deque` 方法 |
|------|-------------|-------------|
| 入栈 | `push(e)` | `push(e)` |
| 出栈 | `pop()` | `pop()` |
| 查看栈顶 | `peek()` | `peek()` |
| 判断空 | `empty()` | `isEmpty()` |

## 3. 最重要的区别：线程安全性

```java
// Stack 是线程安全的（同步的）
Stack<Integer> stack = new Stack<>(); // 所有方法都有 synchronized 修饰

// Deque 不是线程安全的（非同步的）
Deque<Integer> deque = new LinkedList<>(); // 非线程安全，性能更好

// 如果需要线程安全的 Deque
Deque<Integer> safeDeque = Collections.synchronizedDeque(new LinkedList<>());
```

## 4. 性能差异

由于 `Stack` 的方法都是同步的，在单线程环境下性能较差：

```java
// 性能测试对比
public class PerformanceTest {
    public static void main(String[] args) {
        int n = 1000000;
        
        // Stack 测试
        long start1 = System.currentTimeMillis();
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < n; i++) {
            stack.push(i);
        }
        while (!stack.isEmpty()) {
            stack.pop();
        }
        long time1 = System.currentTimeMillis() - start1;
        
        // Deque 测试
        long start2 = System.currentTimeMillis();
        Deque<Integer> deque = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            deque.push(i);
        }
        while (!deque.isEmpty()) {
            deque.pop();
        }
        long time2 = System.currentTimeMillis() - start2;
        
        System.out.println("Stack time: " + time1 + "ms");
        System.out.println("Deque time: " + time2 + "ms");
    }
}
```

## 5. 设计理念差异

**`Stack` 的问题：**
- 继承自 `Vector`，违反了"组合优于继承"的原则
- 提供了非栈操作的方法（如 `get(i)`, `insertElementAt()` 等）

**`Deque` 的优势：**
- 纯粹的接口实现，更符合现代Java设计理念
- 只提供栈相关的操作，更安全

## 6. 实际使用示例

```java
import java.util.*;

public class StackVsDeque {
    public static void main(String[] args) {
        // 使用 Stack（不推荐）
        Stack<Integer> oldStack = new Stack<>();
        oldStack.push(1);
        oldStack.push(2);
        System.out.println("Stack peek: " + oldStack.peek()); // 2
        System.out.println("Stack pop: " + oldStack.pop());   // 2
        
        // 使用 Deque（推荐）
        Deque<Integer> newStack = new LinkedList<>();
        newStack.push(1);
        newStack.push(2);
        System.out.println("Deque peek: " + newStack.peek()); // 2
        System.out.println("Deque pop: " + newStack.pop());   // 2
        
        // Deque 的额外功能（作为双端队列）
        newStack.addLast(3);  // 添加到队尾
        newStack.addFirst(0); // 添加到队首
        System.out.println("As deque: " + newStack); // [0, 1, 3]
    }
}
```

## 7. 官方推荐

根据 **Java官方文档**，建议使用 `Deque` 代替 `Stack`：

> "A more complete and consistent set of LIFO stack operations is provided by the Deque interface and its implementations, which should be used in preference to this class."

## 总结对比

| 特性 | `Stack` | `Deque` |
|------|---------|---------|
| **推出时间** | Java 1.0 | Java 1.6 |
| **线程安全** | 是 | 否（性能更好） |
| **设计理念** | 继承Vector | 接口实现 |
| **方法纯度** | 提供非栈方法 | 纯栈操作 |
| **官方推荐** | 不推荐 | 推荐 |
| **性能** | 较差 | 较好 |
| **灵活性** | 只能作为栈 | 可作为栈或队列 |

## 结论

**应该优先使用 `Deque<Integer> deque = new LinkedList<>()`：**
- 性能更好
- 设计更现代
- 符合官方推荐
- 在需要时可以轻松转换为双端队列

只有在需要线程安全且不关心性能的特定场景下，才考虑使用 `Stack`。


# volatile
### 一、`volatile` 的核心作用

`volatile` 是一个轻量级的同步机制，它主要解决了**可见性**和**有序性**问题，但**不保证原子性**。

#### 1. 保证可见性
- **问题**：在 Java 内存模型中，每个线程都有自己的工作内存（可以理解为CPU高速缓存的抽象）。线程操作变量时，通常先从主内存拷贝一份到工作内存，操作完成后再刷新回主内存。这可能导致一个线程修改了变量，但另一个线程看不到修改后的值。
    
- **`volatile` 的解决**：当一个变量被声明为 `volatile` 后：
    
    - 任何线程**对该变量的写操作**都会立即刷新回主内存。
        
    - 任何线程**对该变量的读操作**都会强制从主内存中重新读取最新的值。
        
- **效果**：这确保了如果一个线程修改了 `volatile` 变量的值，这个新值对其他所有线程来说都是**立即可见**的。
    
#### 2. 禁止指令重排序
- **问题**：为了提升性能，编译器和处理器常常会对指令进行重排序（Reordering）。在单线程下，这不会影响最终结果（遵循 as-if-serial 语义），但在多线程下，可能会导致意想不到的问题。
    
- **`volatile` 的解决**：通过插入**内存屏障**（Memory Barrier）来实现。
    
    - **写屏障**：在 `volatile` 写操作之前插入的屏障，确保该屏障前的所有写操作（包括普通变量）都已刷新到主内存。
        
    - **读屏障**：在 `volatile` 读操作之后插入的屏障，确保该屏障后的所有读操作都能读到最新值。
        
- **效果**：这确保了 `volatile` 变量**读写操作的顺序**与程序代码中的顺序一致，防止了重排序导致的逻辑错误。
    
#### 3. 不保证原子性
这是最容易误解的一点。`volatile` **不能**保证复合操作的原子性。
- **原子操作**：指操作是不可中断的，要么完全执行成功，要么完全不执行。
    
- **例子**：`count++` 这个操作看似一步，实际上分为三步：
    
    1. 读取 `count` 的值
        
    2. 将值加 1
        
    3. 写回新的值
        
- **问题**：线程A可能在执行完第1步后被打断，线程B此时读取了旧的 `count` 值并完成了整个 `++` 操作。之后线程A恢复执行，它仍然基于旧的值进行加1并写回，这覆盖了线程B的操作结果。
    
- **结论**：`volatile` 无法防止这种**线程交错执行**导致的更新丢失问题。要保证原子性，需要使用 `synchronized` 或 `java.util.concurrent.atomic` 包下的原子类（如 `AtomicInteger`）。
    

---

### 二、`volatile` 的典型应用场景

由于 `volatile` 的特性，它非常适合用于两种场景：

#### 场景一：状态标志位

这是 `volatile` **最经典、最安全**的用法。用一个 `volatile` 布尔变量作为开关，控制线程的执行和终止。
```java
public class Server {
    // 使用volatile修饰状态标志
    private volatile boolean isRunning = true;

    public void run() {
        while (isRunning) { // 循环检查volatile变量
            // 执行服务器任务...
        }
        System.out.println("Server stopped.");
    }

    public void stop() {
        isRunning = false; // 其他线程通过修改volatile变量来通知工作线程停止
    }

    public static void main(String[] args) throws InterruptedException {
        Server server = new Server();
        Thread serverThread = new Thread(server::run);
        serverThread.start();

        // 运行3秒后停止服务器
        Thread.sleep(3000);
        server.stop(); // 主线程修改isRunning，对serverThread立即可见
    }
}
```

**为什么有效？**
- **可见性**：主线程调用 `stop()` 将 `isRunning` 设为 `false` 后，会立即写回主存。工作线程在下次检查 `while (isRunning)` 时，会直接从主存读取到 `false`，从而优雅地退出循环。如果没有 `volatile`，工作线程可能永远看不到停止信号，导致线程无法终止。
    
#### 场景二：独立观察（安全发布）

**安全发布**一个对象或值，确保其他线程看到的是完全初始化后的状态。
```java
class Config {
    private volatile static Config instance;

    private final String configValue;

    private Config() {
        // 模拟耗时的初始化操作
        this.configValue = loadConfigFromDB();
    }

    public static Config getInstance() {
        if (instance == null) { // 第一次检查（避免不必要的同步）
            synchronized (Config.class) {
                if (instance == null) { // 第二次检查（确保唯一）
                    instance = new Config(); // 对象初始化
                }
            }
        }
        return instance;
    }
}
```

**为什么有效？**（结合著名的**双重检查锁定**）

- `instance = new Config();` 这行代码实际上分为三步：
    
    1. 为 `Config` 对象分配内存空间
        
    2. 初始化 `Config` 对象（调用构造函数，为字段赋值）
        
    3. 将 `instance` 引用指向分配的内存地址
        
- **如果没有 `volatile`**：JVM 可能对步骤 2 和 3 进行**重排序**。导致其他线程可能在对象未完全初始化完成时，就拿到了一个非空的但内容不完整的 `instance` 引用，从而引发错误。
    
- **使用 `volatile`**：`volatile` 的禁止重排序特性确保了步骤 2 和 3 不会乱序。其他线程拿到 `instance` 时，它引用的必然是一个**已完全初始化好的对象**。
    
#### 场景三：低开销的读-写锁策略（“读多写少”）

当变量的写操作不依赖于当前值，或者只有一个线程在写，但有多个线程在读时，可以使用 `volatile` 替代锁，提升性能。

```java
public class PriceTracker {
    // 当前价格，只有一个线程会更新它，但很多线程会读取它
    private volatile double currentPrice;

    public double getCurrentPrice() {
        return currentPrice; // 读操作无锁，性能极高，且能读到最新值
    }

    public void updatePrice(double newPrice) {
        // 写操作不依赖于currentPrice的旧值，是简单的赋值
        this.currentPrice = newPrice; // volatile写，立即对其他线程可见
    }
}
```

**为什么有效？**
- 读操作（`getCurrentPrice`）非常频繁，使用 `volatile` 读是无锁的，性能远高于 `synchronized` 方法。
- 写操作（`updatePrice`）是简单的赋值，不依赖于旧值（即不是 `currentPrice = currentPrice + 1`），因此是线程安全的。
    

---

### 三、总结：何时使用 `volatile`？

|场景|是否适用 `volatile`|说明|
|---|---|---|
|**对变量的写操作不依赖于当前值**|✅ **适用**|如简单的赋值操作（`flag = false`）、发布新对象。|
|**该变量没有包含在具有其他变量的不变式中**|✅ **适用**|变量是独立的，它的状态不依赖于其他变量的状态。|
|**访问变量时没有加锁**|✅ **适用**|`volatile` 本身提供了轻量级的同步。|
|**需要保证原子性**|❌ **不适用**|如 `count++`，必须使用锁或原子类。|
|**写操作依赖于当前值**|❌ **不适用**|如 `count = count * 2`，这本质上是“读-改-写”复合操作，需要加锁。|
|**单个JVM中存在多个写线程**|⚠️ **谨慎**|如果多个线程都进行写操作，即使不依赖当前值，也可能需要更严格的同步来管理竞争。|

**核心决策流程**：

1. 你的变量是否需要被多个线程共享？
    
2. 对这些变量的操作是否是原子性的？（如果不是，`volatile` 无效）
    
3. 是否有多个线程会写入这个变量？（如果是，且操作非原子，`volatile` 无效）
    
4. 如果以上都满足，那么 `volatile` 是一个高性能的线程安全选择。
    

简单来说，`volatile` 是并发编程中的一把**精准的手术刀**，它在**状态标志**和**独立变量的安全发布**等特定场景下非常有效且高效，但它绝不是 `synchronized` 的万能替代品。
	
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
JVM 内存主要分为以下几大区域，其中**线程私有**的随线程生灭，**线程共享**的则与JVM进程同生命周期。

![deepseek_mermaid_20250910_f4832a.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/deepseek_mermaid_20250910_f4832a.png)

#### 1. 程序计数器

- **作用**：可以看作是当前线程所执行的**字节码的行号指示器**。字节码解释器通过改变这个计数器的值来选取下一条需要执行的字节码指令。
    
- **特性**：**线程私有**。这是唯一一个在《Java虚拟机规范》中**没有规定任何 `OutOfMemoryError`** 情况的区域。
    
#### 2. Java 虚拟机栈

- **作用**：描述 Java **方法执行的内存模型**。每个方法在执行的同时都会创建一个**栈帧**，用于存储：
    
    - **局部变量表**：存放基本数据类型（`int`, `double`, `boolean` 等）、对象引用（`reference` 类型）。
        
    - **操作数栈**：用于方法执行过程中的计算。
        
    - **动态链接**：指向运行时常量池中该栈帧所属方法的引用。
        
    - **方法出口**：返回地址等。
        
- **特性**：**线程私有**。
    
- **异常**：
    
    - `StackOverflowError`：如果线程请求的栈深度大于虚拟机所允许的深度（例如无限递归）。
        
    - `OutOfMemoryError`：如果虚拟机栈可以动态扩展，但在扩展时无法申请到足够的内存。
        

#### 3. 本地方法栈

- **作用**：与虚拟机栈非常相似，其区别不过是**为虚拟机使用到的 Native 方法服务**（如用 C/C++ 编写的方法）。
    
- **异常**：同样会抛出 `StackOverflowError` 和 `OutOfMemoryError`。
    

#### 4. 堆

- **作用**：**此内存区域的唯一目的就是存放对象实例和数组**。几乎所有通过 `new` 关键字创建的对象都会在这里分配内存。它是**垃圾收集器管理的主要区域**，因此也被称为“GC 堆”。
    
- **特性**：**线程共享**。
    
- **异常**：`OutOfMemoryError`：如果在堆中没有内存完成实例分配，并且堆也无法再扩展时。
    

#### 5. 方法区

- **作用**：存储已被虚拟机加载的：
    
    - **类型信息**（类名、访问修饰符、常量、字段描述、方法描述等）
        
    - **运行时常量池**
        
    - **静态变量**（`static`）
        
    - **即时编译器编译后的代码缓存**等。
        
- **特性**：**线程共享**。
    
- **实现**：
    
    - **JDK 7 之前**：被称为“永久代”，是堆的一部分。
        
    - **JDK 8+**：被称为“**元空间**”，使用**本地内存**，不再受JVM堆大小的直接限制，避免了永久代的OOM问题。
        

---

### 二、堆的分区 (Generations)

Java 堆是垃圾回收的重点区域，为了更高效地进行内存回收，JVM 将堆划分为**新生代**和**老年代**。
![deepseek_mermaid_20250910_adbb43.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/deepseek_mermaid_20250910_adbb43.png)

1. **新生代**
    
    - **Eden 区**：对象**首次创建**时分配内存的区域。是对象诞生的地方。
        
    - **Survivor 区**：分为 **From Survivor (S0)** 和 **To Survivor (S1)** 两个区域，它们大小相等，并且同一时间总有一个是空的。
        
2. **老年代**
    
    - 存放**长期存活的对象**和**大对象**（如很大的数组，可能直接分配在老年代）。
        

**对象晋升流程**：

1. 新对象首先在 **Eden** 区分配。
    
2. 当 Eden 区满时，会触发一次 **Minor GC**。存活下来的对象会被移动到 **Survivor0**。
    
3. 下一次 Minor GC 时，会同时清理 Eden 和 Survivor0 区。存活下来的对象会被移动到 **Survivor1**，同时将其**年龄**（Age）加 1。
    
4. 此后，每次 Minor GC，存活对象都会在 **S0 和 S1 之间来回移动**，同时年龄增加。
    
5. 当对象的年龄增加到一定阈值（默认为 **15**，可通过 `-XX:MaxTenuringThreshold` 设置）时，它就会被晋升到**老年代**。
    

---

### 三、新生代与老年代的垃圾回收

JVM 的垃圾回收行为因对象所在区域而异，主要分为两种：**Minor GC** 和 **Major GC / Full GC**。

#### 1. 新生代垃圾回收 (Minor GC)

- **触发条件**：当 **Eden 区空间不足**时触发。
    
- **算法**：使用 **复制算法**。
    
- **过程**：
    
    1. 把 Eden + **一个** Survivor (例如 S0) 中**所有存活的对象**，一次性复制到**另一个空的** Survivor (例如 S1) 中。
        
    2. 然后直接**清空** Eden 和刚才使用的那个 Survivor (S0)。
        
- **为什么高效**：
    
    - 新生代的对象 **“朝生夕死”**（死亡率高），每次 GC 后存活的对象很少，复制这些少量对象的成本很低。
        
    - 复制算法在**存活率低**的场景下效率最高。
        

#### 2. 老年代垃圾回收 (Major GC / Full GC)

- **触发条件**：
    
    1. 老年代空间不足。
        
    2. 方法区（元空间）空间不足。
        
    3. 调用 `System.gc()`，建议 JVM 执行 GC（不保证执行）。
        
    4. Minor GC 后存活的对象大小超过老年代的剩余空间（**晋升担保失败**）。
        
- **算法**：通常使用 **标记-清除** 或 **标记-整理** 算法。
    
    - **标记-清除**：先标记出所有需要回收的对象，然后统一回收。**会产生内存碎片**。
        
    - **标记-整理**：标记过程与“标记-清除”一样，但后续不是直接清理，而是让所有存活的对象都向一端移动，然后直接清理掉边界以外的内存。**解决了内存碎片问题**。
        
- **特点**：
    
    - **速度慢**：因为老年代存活对象多，需要处理的数据量大。
        
    - **STW时间长**：Full GC 会暂停所有应用线程（Stop-The-World），对应用性能影响非常大，是调优的重点规避对象。
        

### 总结

|区域|特点|GC 类型|GC 算法|目标|
|---|---|---|---|---|
|**新生代**|对象死亡率高|**Minor GC**|**复制算法**|快速清理短期对象，效率高|
|**老年代**|对象存活率高|**Major GC / Full GC**|**标记-清除/整理**|清理长期对象，减少碎片，减少STW|

理解这些分区和回收机制，是进行 JVM 性能调优（如调整 `-Xms`, `-Xmx`, `-XX:NewRatio`, `-XX:SurvivorRatio` 等参数）的基础。优化的核心目标通常是：**减少 Full GC 的发生频率和持续时间**。

## **Q1: OOM（OutOfMemoryError）怎么处理？**

- **堆内存不足**：调整 `-Xmx`，检查内存泄漏。`-Xmx`（最大堆大小）
- **元空间不足**：调整 `-XX:MetaspaceSize`。**增加元空间大小**
- **线程栈溢出**：减少 `-Xss`（默认1MB）。

好的，这是一个非常实战性的问题。OOM（OutOfMemoryError）是 Java 应用中令人头疼的异常，理解其发生场景、定位方法和解决方案是高级工程师的必备技能。

### 一、什么情况下会发生 OOM？

OOM 的本质是 **JVM 内存管理中各个区域无法再满足新的内存分配请求**。根据报错信息的不同，可以分为以下几种主要情况：

#### 1. Java 堆空间溢出 (`java.lang.OutOfMemoryError: Java heap space`)

*   **原因**：这是**最常见**的 OOM。创建新对象时，堆内存不足。
*   **根本原因**：
    *   **内存泄漏**：对象被无意地（如通过静态集合、错误的作用域）持有引用，无法被垃圾回收器回收，导致可用内存逐渐耗尽。
    *   **内存溢出**：**不是泄漏**。应用确实需要这么多内存来处理业务（如处理一个超大的文件、加载大量数据做计算），但分配的堆空间不够。

#### 2. 元空间溢出 (`java.lang.OutOfMemoryError: Metaspace`)

*   **原因**：JDK 8+ 中，**加载的类太多**，超出了元空间（Metaspace）的大小限制。
*   **根本原因**：
    *   动态生成大量类（如使用 CGLib、ASM、JSP 等）。
    *   同一个类被不同的类加载器多次加载（常见于 Tomcat 等应用服务器，应用重启后未清理）。
    *   第三方库或框架大量使用反射。

#### 3. GC 开销限制超出 (`java.lang.OutOfMemoryError: GC overhead limit exceeded`)

*   **原因**：这是一种“保护性”的 OOM。JVM 发现 GC 花费了**超过 98% 的时间**，但只回收了**不到 2% 的堆内存**。这意味着 GC 在徒劳地工作，应用基本已经卡死。
*   **根本原因**：通常是**内存泄漏**的晚期症状。堆几乎满了，GC 线程疯狂工作但几乎清理不出任何空间。

#### 4. 无法创建新 native 线程 (`java.lang.OutOfMemoryError: unable to create new native thread`)

*   **原因**：操作系统限制或内存不足，导致无法创建新的线程。
*   **根本原因**：
    *   应用创建了**太多线程**（如线程池配置不合理）。
    *   操作系统的**进程线程数限制**（如 Linux 的 `ulimit -u`）太低。
    *   服务器**内存不足**，无法为线程分配栈空间（每个线程都需要独立的栈内存）。

#### 5. 直接内存溢出 (`java.lang.OutOfMemoryError: Direct buffer memory`)

*   **原因**：NIO 使用的**堆外内存（Direct Memory）** 不足。
*   **根本原因**：
    *   使用了 `ByteBuffer.allocateDirect()` 申请了大量堆外内存，但未及时释放。
    *   使用了 NIO 框架（如 Netty），其内存池配置不合理。

---

### 二、如何定位问题？

当发生 OOM 时，不要惊慌，遵循以下步骤进行排查。**最关键的一步是获取堆转储文件**。

#### 第 1 步：立即保留现场（最关键！）

在 JVM 启动参数中添加以下参数，以便在发生 OOM 时自动生成堆转储文件（Heap Dump）。

```bash
-XX:+HeapDumpOnOutOfMemoryError # 在发生OOM时自动生成堆转储文件
-XX:HeapDumpPath=/path/to/heap/dump.hprof # 指定堆转储文件的保存路径
-XX:+PrintGCDetails # 打印详细的GC日志
-Xloggc:/path/to/gc.log # 将GC日志输出到文件
```

#### 第 2 步：分析堆转储文件

使用强大的内存分析工具（如 **Eclipse MAT** 或 **JProfiler**）打开生成的 `.hprof` 文件。

1.  **寻找大对象**：查看 `Histogram`（直方图）或 `Biggest Objects`，找到占用内存最多的对象类型。
2.  **分析支配树**：使用 `Dominator Tree`（支配树）功能，找到内存中存活的最大对象块，并查看是谁在引用它们（GC Roots）。
3.  **查找内存泄漏线索**：
    *   检查是否有**意外的静态集合**（如 `static Map`）引用了大量对象。
    *   检查是否有**线程局部变量**（`ThreadLocal`）使用后未清理。
    *   检查数据库连接、网络连接、文件流等资源是否未正确关闭。

#### 第 3 步：辅助分析工具

*   **`jps`**：列出当前系统上的所有 Java 进程 PID。
*   **`jstat`**：查看 GC 统计信息，观察各个内存区域的使用趋势和 GC 频率。
    ```bash
    jstat -gcutil <pid> 1000 # 每1秒打印一次GC统计信息
    ```
*   **`jmap`**：可以手动生成堆转储文件或查看堆内存摘要。
    ```bash
    jmap -heap <pid> # 查看堆概要信息
    jmap -histo:live <pid> # 查看堆中对象统计（直方图）
    jmap -dump:format=b,file=dump.hprof <pid> # 手动生成堆转储文件
    ```
*   **`jstack`**：打印线程快照，用于排查线程数过多的问题。
    ```bash
    jstack <pid> # 查看线程栈信息
    ```

---

### 三、如何解决？

根据定位到的根本原因，采取相应的解决方案。

#### 针对堆内存溢出 (`Java heap space`)

1.  **如果是内存泄漏**：
    *   **修复代码**：找到并切断那些本不该存在的引用链。例如：
        *   清理静态集合中不再需要的条目。
        *   确保正确关闭资源（使用 try-with-resources）。
        *   及时清理 `ThreadLocal` 变量（`remove()`）。
2.  **如果是内存溢出（业务需要）**：
    *   **增加堆大小**：调整 JVM 参数 `-Xms`（初始堆大小）和 `-Xmx`（最大堆大小）。但这只是权宜之计，无法根治。
    *   **优化程序**：
        *   **减少数据体积**：是否可以通过分页、分批处理来避免一次性加载所有数据？
        *   **使用流式处理**：对于大数据集，使用流（Streaming）来处理，而不是全部加载到内存。
        *   **优化数据结构**：使用更节省内存的数据结构（如使用原始类型集合库：Eclipse Collections, fastutil）。

#### 针对元空间溢出 (`Metaspace`)

1.  **增加元空间大小**：`-XX:MaxMetaspaceSize=256m`。
2.  **优化应用**：
    *   检查是否有类加载器泄漏（特别是在应用热部署、重启频繁的场景）。
    *   减少动态类的生成（如评估 CGLib 代理的使用是否必要）。

#### 针对 GC 开销限制超出 (`GC overhead limit exceeded`)

此错误通常是堆内存溢出的结果。**按照解决堆内存溢出的方法先进行排查**，它通常是内存泄漏的最终表现。

#### 针对无法创建新线程 (`unable to create new native thread`)

1.  **优化线程使用**：
    *   检查代码，避免无限制地创建线程。**使用线程池**来管理线程资源。
    *   合理配置线程池参数（核心线程数、最大线程数、队列大小）。
2.  **调整系统限制**：在 Linux 下，可以适当调高用户可创建进程数限制（`ulimit -u`）。
3.  **减少线程栈大小**：如果线程不需要很深的调用栈，可以减小每个线程的栈大小以节省内存（`-Xss256k`），从而允许创建更多线程。但这需谨慎，可能引发 `StackOverflowError`。

#### 针对直接内存溢出 (`Direct buffer memory`)

1.  **增加直接内存大小**：`-XX:MaxDirectMemorySize=256m`。
2.  **确保及时释放**：检查使用直接内存的代码（如 Netty 的 `ByteBuf`），确保调用了 `release()` 等方法将内存归还到池中。

### 总结：通用解决流程

1.  **设防**：首先在 JVM 参数中配置 `-XX:+HeapDumpOnOutOfMemoryError`，这是最重要的“黑匣子”。
2.  **复现**：尝试在测试环境复现问题。
3.  **分析**：使用 MAT 等工具分析生成的堆转储文件，找到“罪魁祸首”的对象和引用链。
4.  **解决**：
    *   **治标**：临时增加对应内存区域的大小。
    *   **治本**：修复代码中的 bug（如内存泄漏）、优化程序和算法（如分批处理）。
5.  **验证**：修复后，再次进行压测，确认问题是否解决。

记住，**盲目调大内存参数只能暂时掩盖问题，并不能根除它**。真正的解决方案几乎总是来自于对代码的深入分析和优化。


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


# `equals()` vs `  == `  在栈操作中的区别

这两行代码有**本质区别**，可能会产生完全不同的结果：

## 1. 对于 **Integer 类型**的栈

```java
Deque<Integer> stack = new LinkedList<>();
Deque<Integer> min_stack = new LinkedList<>();

// 示例数据
stack.push(1000);
min_stack.push(1000);
```

### 使用 `equals()`（正确）
```java
if(stack.pop().equals(min_stack.peek())){
    min_stack.pop();
}
// 会执行 min_stack.pop()，因为 1000.equals(1000) 返回 true
```

### 使用 ` == `（可能错误）
```java
if(stack.pop() == min_stack.peek()){
    min_stack.pop();
}
// 可能不会执行 min_stack.pop()，因为 1000 == 1000 可能返回 false
```

## 2. 原因分析：Integer 缓存机制

Java 对 **-128 到 127** 的 Integer 对象有缓存：

```java
Integer a = 127;
Integer b = 127;
System.out.println(a == b); // true（使用缓存）

Integer c = 128;
Integer d = 128;
System.out.println(c == d); // false（新建对象）

Integer e = 1000;
Integer f = 1000;
System.out.println(e == f); // false（新建对象）
```

## 3. 完整示例演示

```java
import java.util.*;

public class EqualsVsDoubleEqual {
    public static void main(String[] args) {
        Deque<Integer> stack = new LinkedList<>();
        Deque<Integer> min_stack = new LinkedList<>();
        
        // 测试小数字（在缓存范围内）
        stack.push(100);
        min_stack.push(100);
        
        System.out.println("=== 测试数字 100 ===");
        testComparison(stack, min_stack);
        
        // 测试大数字（不在缓存范围内）
        stack.push(1000);
        min_stack.push(1000);
        
        System.out.println("=== 测试数字 1000 ===");
        testComparison(stack, min_stack);
    }
    
    static void testComparison(Deque<Integer> stack, Deque<Integer> min_stack) {
        Integer stackValue = stack.peek();
        Integer minStackValue = min_stack.peek();
        
        System.out.println("stack.peek(): " + stackValue + " @ " + System.identityHashCode(stackValue));
        System.out.println("min_stack.peek(): " + minStackValue + " @ " + System.identityHashCode(minStackValue));
        
        System.out.println("== 比较: " + (stackValue == minStackValue));
        System.out.println("equals 比较: " + (stackValue.equals(minStackValue)));
        System.out.println();
    }
}
```

输出结果可能是：
```
=== 测试数字 100 ===
stack.peek(): 100 @ 366712642
min_stack.peek(): 100 @ 366712642
== 比较: true
equals 比较: true

=== 测试数字 1000 ===
stack.peek(): 1000 @ 1829164700
min_stack.peek(): 1000 @ 2018699554
== 比较: false
equals 比较: true
```

## 4. 对于其他对象类型

如果是自定义对象，区别更明显：

```java
class Person {
    String name;
    Person(String name) { this.name = name; }
}

// 使用 == 比较
Person p1 = new Person("Alice");
Person p2 = new Person("Alice");

System.out.println(p1 == p2);      // false（不同对象）
System.out.println(p1.equals(p2)); // false（需要重写equals方法）

// 重写equals后
@Override
public boolean equals(Object obj) {
    if (this == obj) return true;
    if (obj == null || getClass() != obj.getClass()) return false;
    Person person = (Person) obj;
    return Objects.equals(name, person.name);
}

System.out.println(p1.equals(p2)); // true
```

## 5. 在最小栈问题中的正确用法

```java
class MinStack {
    Deque<Integer> stack;
    Deque<Integer> min_stack;
    
    public MinStack() {
        stack = new LinkedList<>();
        min_stack = new LinkedList<>();
    }
    
    public void push(int val) {
        stack.push(val);
        if (min_stack.isEmpty() || val <= min_stack.peek()) {
            min_stack.push(val);
        }
    }
    
    public void pop() {
        // 正确：使用 equals() 比较值内容
        if (stack.pop().equals(min_stack.peek())) {
            min_stack.pop();
        }
        
        // 错误：使用 == 可能无法正确比较
        // if (stack.pop() == min_stack.peek()) {
        //     min_stack.pop();
        // }
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return min_stack.peek();
    }
}
```

## 6. 总结对比

| 比较方式          | `equals()`   | ` == `          |
| ------------- | ------------ | --------------- |
| **比较内容**      | 值内容          | 内存地址            |
| **Integer缓存** | 不受影响         | 受缓存影响（-128~127） |
| **自定义对象**     | 需要重写equals() | 总是比较引用          |
| **推荐程度**      | ✅ 推荐         | ❌ 不推荐           |
| **安全性**       | 高            | 低（可能产生bug）      |

## 7. 最佳实践

**总是使用 `equals()` 来比较对象的内容：**

```java
// 正确
if(stack.pop().equals(min_stack.peek())){
    min_stack.pop();
}

// 对于基本类型int的栈，可以这样避免问题
Deque<Integer> stack; // 存储Integer对象
// 或者使用IntStack等专门的基本类型集合
```

在栈操作中，特别是最小栈这种需要比较值的场景，**必须使用 `equals()`** 来确保正确性。


# 桶排序

1. **`List<Integer>[] buckets = new ArrayList[maxCnt + 1];`**
    
    - 创建足够数量的桶来容纳所有可能的频率值
        
2. **`Arrays.setAll(buckets, i -> new ArrayList<>());`**
    
    - 初始化每个桶为空列表

### 按频率排序元素

```java
public List<String> sortByFrequency(String[] words) {
    // 统计频率
    Map<String, Integer> freq = new HashMap<>();
    for (String word : words) {
        freq.merge(word, 1, Integer: :sum);
    }
    
    // 找到最大频率
    int maxFreq = Collections.max(freq.values());
    
    // 创建桶
    List<String>[] buckets = new ArrayList[maxFreq + 1];
    Arrays.setAll(buckets, i -> new ArrayList<>());
    
    // 填充桶
    for (Map.Entry<String, Integer> entry : freq.entrySet()) {
        buckets[entry.getValue()].add(entry.getKey());
    }
    
    // 按频率从高到低收集结果
    List<String> result = new ArrayList<>();
    for (int i = maxFreq; i > 0; i--) {
        Collections.sort(buckets[i]); // 同频率的按字母排序
        result.addAll(buckets[i]);
    }
    
    return result;
}
```


# **优先队列（PriorityQueue）

## 基本语法

```java
PriorityQueue<Integer> A = new PriorityQueue<>();
```

## 完整解释

### 默认行为：
- 创建一个小顶堆（最小堆）
- 元素按自然顺序排序（升序）
- 队首元素是最小的

## 不同类型的优先队列

### 1. 默认最小堆（升序）
```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
minHeap.offer(3);
minHeap.offer(1);
minHeap.offer(2);
System.out.println(minHeap.poll()); // 1 (最小)
System.out.println(minHeap.poll()); // 2
System.out.println(minHeap.poll()); // 3
```

### 2. 最大堆（降序）
```java
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
// 或者
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());

maxHeap.offer(3);
maxHeap.offer(1);
maxHeap.offer(2);
System.out.println(maxHeap.poll()); // 3 (最大)
System.out.println(maxHeap.poll()); // 2
System.out.println(maxHeap.poll()); // 1
```

### 3. 自定义比较器
```java
// 按字符串长度排序
PriorityQueue<String> lengthQueue = new PriorityQueue<>(
    (s1, s2) -> s1.length() - s2.length()
);

lengthQueue.offer("apple");
lengthQueue.offer("banana");
lengthQueue.offer("cat");
System.out.println(lengthQueue.poll()); // "cat" (最短)
System.out.println(lengthQueue.poll()); // "apple"
System.out.println(lengthQueue.poll()); // "banana"
```

## 常用操作和方法

### 添加元素：
```java
A.offer(5);    // 推荐：添加元素，返回boolean
A.add(5);      // 添加元素，失败时抛出异常
```

### 获取元素：
```java
int top = A.peek();    // 查看队首元素（不删除）
int element = A.poll(); // 取出队首元素（删除）
```

### 其他操作：
```java
int size = A.size();    // 元素数量
boolean isEmpty = A.isEmpty(); // 是否为空
boolean contains = A.contains(5); // 是否包含元素
A.clear();              // 清空队列
```

## 实际应用场景

### 场景1：找到前K个最大元素
```java
public int[] topKSmallest(int[] nums, int k) {
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
    
    for (int num : nums) {
        maxHeap.offer(num);
        if (maxHeap.size() > k) {
            maxHeap.poll(); // 移除最大的，保持k个最小元素
        }
    }
    
    int[] result = new int[k];
    for (int i = 0; i < k; i++) {
        result[i] = maxHeap.poll();
    }
    return result;
}
```

### 场景2：合并K个有序链表
```java
public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);
    
    // 将每个链表的头节点加入优先队列
    for (ListNode node : lists) {
        if (node != null) {
            pq.offer(node);
        }
    }
    
    ListNode dummy = new ListNode(0);
    ListNode current = dummy;
    
    while (!pq.isEmpty()) {
        ListNode smallest = pq.poll();
        current.next = smallest;
        current = current.next;
        
        if (smallest.next != null) {
            pq.offer(smallest.next);
        }
    }
    
    return dummy.next;
}
```

### 场景3：数据流的中位数
```java
class MedianFinder {
    PriorityQueue<Integer> maxHeap; // 存储较小的一半
    PriorityQueue<Integer> minHeap; // 存储较大的一半
    
    public MedianFinder() {
        maxHeap = new PriorityQueue<>((a, b) -> b - a);
        minHeap = new PriorityQueue<>();
    }
    
    public void addNum(int num) {
        maxHeap.offer(num);
        minHeap.offer(maxHeap.poll());
        
        if (maxHeap.size() < minHeap.size()) {
            maxHeap.offer(minHeap.poll());
        }
    }
    
    public double findMedian() {
        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        } else {
            return maxHeap.peek();
        }
    }
}
```

## 时间复杂度分析

| 操作 | 时间复杂度 | 说明 |
|------|------------|------|
| offer() | O(log n) | 插入元素 |
| poll() | O(log n) | 删除队首元素 |
| peek() | O(1) | 查看队首元素 |
| size() | O(1) | 获取元素数量 |

## 注意事项

### 1. 空队列处理
```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
// System.out.println(pq.poll()); // 返回null
// System.out.println(pq.remove()); // 抛出NoSuchElementException

// 安全操作
Integer value = pq.poll();
if (value != null) {
    // 处理元素
}
```

### 2. 并发访问
`PriorityQueue` 不是线程安全的，需要同步：
```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
// 同步访问
synchronized(pq) {
    pq.offer(1);
    pq.poll();
}
```

### 3. 迭代顺序
```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(3);
pq.offer(1);
pq.offer(2);

// 迭代顺序不保证有序！
for (int num : pq) {
    System.out.print(num + " "); // 可能是任意顺序
}
// 只有poll()保证有序
```

## 完整示例代码

```java
import java.util.*;

public class PriorityQueueExample {
    public static void main(String[] args) {
        // 1. 最小堆示例
        System.out.println("=== 最小堆 ===");
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        minHeap.offer(5);
        minHeap.offer(2);
        minHeap.offer(8);
        minHeap.offer(1);
        
        while (!minHeap.isEmpty()) {
            System.out.print(minHeap.poll() + " "); // 1 2 5 8
        }
        System.out.println();
        
        // 2. 最大堆示例
        System.out.println("=== 最大堆 ===");
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
        maxHeap.offer(5);
        maxHeap.offer(2);
        maxHeap.offer(8);
        maxHeap.offer(1);
        
        while (!maxHeap.isEmpty()) {
            System.out.print(maxHeap.poll() + " "); // 8 5 2 1
        }
        System.out.println();
        
        // 3. 自定义比较器示例
        System.out.println("=== 字符串长度排序 ===");
        PriorityQueue<String> lengthQueue = new PriorityQueue<>(
            (s1, s2) -> s1.length() - s2.length()
        );
        
        lengthQueue.offer("apple");
        lengthQueue.offer("banana");
        lengthQueue.offer("cat");
        lengthQueue.offer("dog");
        
        while (!lengthQueue.isEmpty()) {
            System.out.print(lengthQueue.poll() + " "); // cat dog apple banana
        }
        System.out.println();
        
        // 4. 对象排序示例
        System.out.println("=== 对象按年龄排序 ===");
        PriorityQueue<Person> ageQueue = new PriorityQueue<>(
            (p1, p2) -> p1.age - p2.age
        );
        
        ageQueue.offer(new Person("Alice", 25));
        ageQueue.offer(new Person("Bob", 20));
        ageQueue.offer(new Person("Charlie", 30));
        
        while (!ageQueue.isEmpty()) {
            System.out.print(ageQueue.poll().name + " "); // Bob Alice Charlie
        }
    }
    
    static class Person {
        String name;
        int age;
        
        Person(String name, int age) {
            this.name = name;
            this.age = age;
        }
    }
}
```

## 与其他数据结构的对比

| 特性 | PriorityQueue | TreeSet | LinkedList |
|------|---------------|---------|------------|
| **排序** | 是 | 是 | 否 |
| **重复元素** | 允许 | 不允许 | 允许 |
| **null元素** | 不允许 | 不允许 | 允许 |
| **访问时间** | O(log n) | O(log n) | O(1)插入，O(n)访问 |
| **使用场景** | 需要有序访问 | 需要有序且去重 | 简单队列 |

## 总结

`PriorityQueue<Integer> A = new PriorityQueue<>();` 创建了一个：

- ✅ **最小优先队列**（小顶堆）
- ✅ **元素按自然顺序排序**
- ✅ **队首永远是最小元素**

如果需要最大堆或自定义排序，必须提供比较器：
```java
// 最大堆
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);

// 自定义排序
PriorityQueue<Item> customQueue = new PriorityQueue<>(
    (a, b) -> a.priority - b.priority
);
```

优先队列在算法中非常有用，特别是处理Top K问题、调度问题、Dijkstra算法等场景！


# `charAt()` 方法详细解释

`charAt()` 是 Java 中 `String` 类的一个基本方法，用于获取字符串中指定位置的字符。

## 基本语法

```java
char charAt(int index)
```

## 方法说明

- **作用**：返回字符串中指定索引位置的字符
- **参数**：`index` - 字符的索引（从0开始）
- **返回值**：指定位置的字符
- **异常**：如果索引越界，抛出 `StringIndexOutOfBoundsException`

## 使用示例

### 基础用法：
```java
String str = "Hello";
char c1 = str.charAt(0); // 'H'
char c2 = str.charAt(1); // 'e'
char c3 = str.charAt(4); // 'o'
```

### 遍历字符串：
```java
String s = "Hello";
for (int i = 0; i < s.length(); i++) {
    System.out.println("索引 " + i + ": " + s.charAt(i));
}
// 输出：
// 索引 0: H
// 索引 1: e  
// 索引 2: l
// 索引 3: l
// 索引 4: o
```

## 常见应用场景

### 场景1：字符串处理
```java
// 统计字符出现次数
public int countChar(String str, char target) {
    int count = 0;
    for (int i = 0; i < str.length(); i++) {
        if (str.charAt(i) == target) {
            count++;
        }
    }
    return count;
}

// 使用
String text = "hello world";
int count = countChar(text, 'l'); // 3
```

### 场景2：回文检查
```java
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// 使用
System.out.println(isPalindrome("racecar")); // true
System.out.println(isPalindrome("hello"));   // false
```

### 场景3：字符串反转
```java
public String reverseString(String s) {
    StringBuilder reversed = new StringBuilder();
    for (int i = s.length() - 1; i >= 0; i--) {
        reversed.append(s.charAt(i));
    }
    return reversed.toString();
}

// 使用
String reversed = reverseString("hello"); // "olleh"
```

### 场景4：字符分类统计
```java
public void analyzeString(String s) {
    int letters = 0, digits = 0, others = 0;
    
    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        if (Character.isLetter(c)) {
            letters++;
        } else if (Character.isDigit(c)) {
            digits++;
        } else {
            others++;
        }
    }
    
    System.out.println("字母: " + letters);
    System.out.println("数字: " + digits);
    System.out.println("其他: " + others);
}

// 使用
analyzeString("Hello123!"); 
// 字母: 5, 数字: 3, 其他: 1
```

## 异常处理

### 索引越界异常：
```java
String str = "Hello";
try {
    char c = str.charAt(10); // 抛出StringIndexOutOfBoundsException
} catch (StringIndexOutOfBoundsException e) {
    System.out.println("索引越界: " + e.getMessage());
}
```

### 安全访问：
```java
public char safeCharAt(String str, int index) {
    if (str == null || index < 0 || index >= str.length()) {
        return '\0'; // 返回空字符或其他默认值
    }
    return str.charAt(index);
}
```

## 与相关方法的对比

### `charAt()` vs `toCharArray()`
```java
String str = "hello";

// 使用charAt()遍历
for (int i = 0; i < str.length(); i++) {
    char c = str.charAt(i);
    // 处理字符
}

// 使用toCharArray()遍历
char[] chars = str.toCharArray();
for (char c : chars) {
    // 处理字符
}
```

**区别：**
- `charAt()`：每次访问一个字符，不创建新数组
- `toCharArray()`：创建字符数组副本，占用更多内存

### `charAt()` vs `substring()`
```java
String str = "hello";

char c = str.charAt(2);       // 'l' (单个字符)
String s = str.substring(2, 3); // "l" (子字符串)
```

## 性能考虑

### 对于频繁访问：
```java
// 如果需要多次访问，考虑转换为字符数组
String longString = "很长的字符串...";
char[] charArray = longString.toCharArray();

// 然后使用数组访问，效率更高
for (int i = 0; i < charArray.length; i++) {
    char c = charArray[i];
    // 处理
}
```

### 测试性能：
```java
public void testPerformance() {
    String longString = "a".repeat(1000000);
    
    long start1 = System.currentTimeMillis();
    for (int i = 0; i < longString.length(); i++) {
        char c = longString.charAt(i);
    }
    long time1 = System.currentTimeMillis() - start1;
    
    long start2 = System.currentTimeMillis();
    char[] chars = longString.toCharArray();
    for (char c : chars) {
        // 处理
    }
    long time2 = System.currentTimeMillis() - start2;
    
    System.out.println("charAt() 时间: " + time1 + "ms");
    System.out.println("toCharArray() 时间: " + time2 + "ms");
}
```

## Unicode 字符处理

### 处理代理对（Surrogate Pairs）：
```java
String emoji = "😊"; // 这是一个代理对
System.out.println(emoji.length()); // 2
System.out.println(emoji.charAt(0)); // 返回代理对的第一个字符
System.out.println(emoji.charAt(1)); // 返回代理对的第二个字符

// 正确处理Unicode字符
int codePoint = emoji.codePointAt(0);
System.out.println(Character.toChars(codePoint)); // 😊
```

## 实际算法应用

### 字符串匹配：
```java
public int findFirstOccurrence(String text, String pattern) {
    for (int i = 0; i <= text.length() - pattern.length(); i++) {
        boolean found = true;
        for (int j = 0; j < pattern.length(); j++) {
            if (text.charAt(i + j) != pattern.charAt(j)) {
                found = false;
                break;
            }
        }
        if (found) {
            return i;
        }
    }
    return -1;
}
```

### 最长回文子串：
```java
public String longestPalindrome(String s) {
    if (s == null || s.length() < 1) return "";
    
    int start = 0, end = 0;
    for (int i = 0; i < s.length(); i++) {
        int len1 = expandAroundCenter(s, i, i);    // 奇数长度
        int len2 = expandAroundCenter(s, i, i + 1); // 偶数长度
        int len = Math.max(len1, len2);
        
        if (len > end - start) {
            start = i - (len - 1) / 2;
            end = i + len / 2;
        }
    }
    return s.substring(start, end + 1);
}

private int expandAroundCenter(String s, int left, int right) {
    while (left >= 0 && right < s.length() && 
           s.charAt(left) == s.charAt(right)) {
        left--;
        right++;
    }
    return right - left - 1;
}
```

## 总结

`charAt()` 方法是字符串处理的基础：

1. ✅ **基本功能**：获取指定位置的字符
2. ✅ **索引范围**：0 到 length()-1
3. ✅ **异常处理**：需要处理StringIndexOutOfBoundsException
4. ✅ **性能考虑**：频繁访问时考虑使用toCharArray()
5. ✅ **Unicode支持**：注意代理对的处理

这是一个简单但非常重要的方法，在算法和日常编程中经常使用！


# a