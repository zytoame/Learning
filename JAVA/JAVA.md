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

# JVM
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