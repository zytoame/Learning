# 数组存放
short arrTimeVal[3];
arrTimeVal[2]=
arrTimeVal[1]=
arrTimeVal[0]=
printf(,arrTimeVal[2],arrTimeVal[1],arrTimeVal[0]);
# 内部函数声明调用
//声明
static short CalcHour(int tick);
//函数实现
static short CalcHour(int tick)
{
short hour;
hour=;
return(hour)
}
//主函数
void/int main(void)
{
short hour;
**hour=CalcHour(tick)**;
system("pause");
return 0;
}
# 枚举
//定义枚举
typedef enum
{
MON=0,TUE,WED,THUS,FRI,SAT,SUN
}EnumWeekDay;
EnumWeekDay workDay,weekEnd;//定义
//使用
workDay=MON;
weekEnd=SUN;
# switch
switch(表达式)
{
case:
常量1;
语句1;
break;
default:
语句;
break;
}
# 指针
1. 注意事项：定义类型；使用前初始化
2. * (pTimeVal + 2)等效pTimeVal [ 2 ]
3. **结构体指针（内部函数）**
	static unsigned char 函数(int tick,结构体* 指针变量)
	{
		unsigned char 局部变量=0；
		if（）
		{
			局部变量=1；
			指针变量->结构体变量=xxxx；
		}
		return(局部变量)；
	}
	主函数`
	void main(void)`
	{`
		unsigned char *局部变量*;`
		结构体 结构体局部变量；
		printf
		scanf_s
		局部变量=函数（，&结构体局部变量）
		if(局部变量>0){}
		else{}
		system("pause");
	}
4. this指针：指向当前对象，用于区分成员变量和局部变量
5. 函数指针

# if
1. if(1== a).
# 1/0标志
unsigned char xxxx = 0;//初始值为0，即表示无效或失败
if (1== xxxx){}else{}
# 结构体
1. 定义一个变量，里面包含相互独立的变量，可以显示出这些变量之间的关联。如一个学生的学号，姓名，性别，班级等信息。
2. //声明结构体类型
	typedef struct
	{
		int num;
		char name[20];
		char sex;
		int age
	}StructStudent student1;//定义
	//使用
	student1.num=1234;
	student1.name="zhangsan"
	student1.sex='M';
	student1.age=20;
3. 内部函数和结构体:
	static 结构体 函数()
	{
		结构体 *结构体变量* ={x,x};//初始化为xx
		*结构体变量*.结构体中变量1=;
		*结构体变量*.结构体中变量2=;
		return(*结构体变量*)
	}
# 多文件
	头文件.h
		//防止重编译：
		#ifndef xxx
		#define xxx

		#endif 

		API函数声明：之后在相应的c文件对函数分别实现
	c文件
		1. 包含头文件区：包含c文件对应的h文件，#include"xxx.h"
		2. 宏定义:仅在c文件中使用的宏
		3. 枚举结构体定义：仅在c文件中使用
		4. 内部变量：定义c中函数之间所使用的变量
			1. 关键字：static
			2. 变量名：以s_开头
			3. 为了通过函数调用变量
		5. 内部函数声明
		6. 内部函数实现
		7. API函数实现：定义外部函数
			1. 预留初始化函数Initxxx，提前设置好，便于后期升级。
			void Initxxx(void){}
		8. App.c文件
			1. 包含头文件：
			 #include<stido.h>
			 #include<stdlib.h>

			  #include "xxx.h"
			2. API函数实现：main主函数


# u8:
#### 1. 8位无符号整数

通常情况下，`u8` 被定义为 `unsigned char`，即无符号的 8 位字符类型，因为在 C 语言中，`char` 类型通常占用 1 字节（8 位），而 `unsigned char` 只会表示非负整数。

**例如，`u8` 可以这样定义**：
typedef unsigned char u8;
int main()
{
	u8 a = 255; // 8 位无符号整数 
	printf("Value of a: %u\n", a); // 输出 255 
	return 0; 
}
这样，`u8` 就是 `unsigned char` 类型的别名，表示无符号的 8 位整数，范围通常为 0 到 255。

#### 2. 还有u16，u32，u64

# i16
 1. `i16` 通常定义为 `short` 或 `signed short`，表示一个 **16 位有符号整数**。在 C 语言中，`short` 类型通常占用 2 字节（16 位），并且其范围通常是 -32,768 到 32,767。
 2. 无符号类型是 `u16`，它代表 16 位无符号整数，范围是 0 到 65,535。

# 为什么要使用DataType.h文件
使用 DataType.h 文件通常是为了 定义和统一数据类型，使代码更加清晰、可维护、可移植。下面是一些常见的原因，解释为什么会使用 DataType.h 文件：
1. 定义统一的数据类型
- 在大型项目中，尤其是嵌入式系统、跨平台应用程序或者需要处理多种硬件平台的应用，可能需要使用特定大小和符号的整数类型（如 i8, u8, i16, u32, u64 等）。而 DataType.h 文件可以在一个地方集中定义这些类型，使得代码在多个文件中都能统一使用。
- 通过这种方式，项目中的数据类型可以保持一致性，避免在多个源文件中重复定义。
- 示例：

   // DataType.h
   typedef unsigned char u8;
   typedef signed char i8;
   typedef unsigned short u16;
   typedef signed short i16;
   typedef unsigned int u32;
   typedef signed int i32;

2. 平台无关性与可移植性

- 使用 DataType.h 文件可以帮助将平台相关的类型和数据定义集中管理。如果项目需要在不同的硬件平台或操作系统上运行，可以根据不同平台的要求调整数据类型大小和符号。
- 例如，某些平台上的 int 可能是 16 位，而在其他平台上则是 32 位。通过 DataType.h 文件，可以为不同平台提供统一的类型定义，方便跨平台开发。
示例：

   #ifdef PLATFORM_X
   typedef unsigned int u32;  // For platform X, u32 is 32-bit
   #else
   typedef unsigned long u32; // For another platform, u32 is 64-bit
   #endif

3. 增强代码的可读性

- .使用 DataType.h 文件，可以使代码更加自文档化（self-documenting）。比如，u8, i16 等类型名称清晰地表示这些类型的含义，比直接使用 unsigned char 或 short 更易于理解和维护。
- 如果你在多个文件中使用统一的数据类型，其他开发人员也能快速理解代码的意图，而不需要每次都去查看具体的类型定义。

4. 方便修改和扩展

- 如果某些数据类型需要修改（例如，改变数据大小或符号），只需在 DataType.h 文件中进行一次修改，所有使用该类型的源文件都会自动获得更新，避免了在多个文件中逐一修改。
- 例如，你可以改变 u32 类型的定义，如果修改了 DataType.h 文件，所有包含这个文件的代码会立刻生效，不会遗漏任何地方。
示例：

   // 修改 DataType.h 中的类型定义
   typedef unsigned long long u32;  // 假设需要改变为 64 位

5. 简化调试与测试

- 在测试和调试时，集中定义数据类型可以帮助快速定位问题。如果某个数据类型在使用时出错，开发人员可以通过修改 DataType.h 文件来调整数据类型的定义，而不必逐个文件去查找问题。

6. 与硬件相关的应用

- 在嵌入式编程中，硬件通常对数据类型的大小有特定的要求，使用 DataType.h 文件可以确保所有数据类型符合硬件要求。例如，某些微控制器可能要求 8 位的数据类型来与特定的寄存器进行交互。

总结
DataType.h 文件的作用在于集中定义和管理数据类型，以提高代码的可维护性、可移植性、可读性，并使得修改和扩展更加容易。它帮助开发人员避免重复定义，确保在不同平台之间的一致性，特别适用于嵌入式编程或大型项目的开发中。


# c++中的智能指针的用法以及应用场景

在 C++ 中，**智能指针（Smart Pointers）** 是用于自动管理动态内存的工具，通过 RAII（Resource Acquisition Is Initialization）机制，**避免内存泄漏和悬空指针**问题。C++11 引入了三种主要的智能指针：`std::unique_ptr`、`std::shared_ptr` 和 `std::weak_ptr`。以下是它们的详细用法和典型应用场景。

---

## **1. `std::unique_ptr`（独占所有权）**
### **特点**
- **独占所有权**：同一时间只能有一个 `unique_ptr` 指向某个对象。
- **轻量高效**：几乎无额外开销（与裸指针接近）。
- **不可复制**，但支持移动语义（`std::move`）。

### **基本用法**
```cpp
#include <memory>

// 创建一个动态分配的 int，由 unique_ptr 管理
std::unique_ptr<int> ptr1 = std::make_unique<int>(42);

// 移动所有权（ptr1 变为 nullptr）
std::unique_ptr<int> ptr2 = std::move(ptr1);

// 访问数据
if (ptr2) {
    std::cout << *ptr2 << std::endl; // 输出 42
}
```

### **应用场景**
1. **替代裸指针**，明确表示独占所有权。
   ```cpp
   void processData() {
       auto data = std::make_unique<Data>(); // 自动释放
       data->process();
   } // 此处 data 自动析构，内存释放
   ```
2. **工厂模式**返回对象：
   ```cpp
   std::unique_ptr<Base> createObject(int type) {
       if (type == 1) return std::make_unique<Derived1>();
       else return std::make_unique<Derived2>();
   }
   ```
3. **管理资源句柄**（如文件、套接字）：
   ```cpp
   std::unique_ptr<FILE, decltype(&fclose)> file(fopen("test.txt", "r"), &fclose);
   ```

---

## **2. `std::shared_ptr`（共享所有权）**
### **特点**
- **共享所有权**：多个 `shared_ptr` 可以指向同一对象，通过引用计数管理生命周期。
- **线程安全**：引用计数的增减是原子的（但对象访问需额外同步）。
- **开销略大**：需维护引用计数和控制块。

### **基本用法**
```cpp
#include <memory>

auto ptr1 = std::make_shared<int>(42); // 引用计数=1
{
    auto ptr2 = ptr1; // 引用计数=2
    std::cout << *ptr2 << std::endl;
} // ptr2 析构，引用计数=1
// 引用计数为0时，对象自动销毁
```

### **应用场景**
1. **共享数据**（如多线程缓存）：
   ```cpp
   std::shared_ptr<Cache> cache = std::make_shared<Cache>();
   std::thread t1([cache] { cache->read(); });
   std::thread t2([cache] { cache->write(); });
   ```
2. **复杂对象关系**（如图结构、观察者模式）：
   ```cpp
   struct Node {
       std::shared_ptr<Node> next;
   };
   auto node1 = std::make_shared<Node>();
   auto node2 = std::make_shared<Node>();
   node1->next = node2; // 循环引用需配合 weak_ptr
   ```

---

## **3. `std::weak_ptr`（弱引用）**
### **特点**
- **不增加引用计数**：用于观察 `shared_ptr` 管理的对象，避免循环引用。
- **需转换为 `shared_ptr`** 才能访问数据（通过 `lock()`）。

### **基本用法**
```cpp
auto sharedPtr = std::make_shared<int>(42);
std::weak_ptr<int> weakPtr = sharedPtr;

if (auto tempPtr = weakPtr.lock()) { // 尝试提升为 shared_ptr
    std::cout << *tempPtr << std::endl; // 成功访问
} else {
    std::cout << "对象已销毁" << std::endl;
}
```

### **应用场景**
1. **打破循环引用**：
   ```cpp
   struct Node {
       std::shared_ptr<Node> next;
       std::weak_ptr<Node> prev; // 避免循环引用
   };
   ```
2. **缓存系统**（观察对象是否存活）：
   ```cpp
   std::weak_ptr<Cache> cacheWeakRef = cache;
   if (auto cache = cacheWeakRef.lock()) {
       // 缓存仍有效
   }
   ```

---

## **4. 智能指针的选择指南**
| **场景**                          | **推荐指针类型**       | **理由**                     |
|-----------------------------------|-----------------------|-----------------------------|
| 独占资源（如工厂模式、文件句柄）  | `std::unique_ptr`     | 无额外开销，语义明确         |
| 共享数据（如多线程、复杂结构）    | `std::shared_ptr`     | 自动生命周期管理             |
| 避免循环引用（如双向链表、缓存）  | `std::weak_ptr`       | 不增加引用计数               |
| 需要自定义析构逻辑（如数据库连接）| `std::unique_ptr` 或 `std::shared_ptr` + 删除器 | 灵活控制资源释放 |

---

## **5. 注意事项**
1. **优先使用 `std::make_unique` 和 `std::make_shared`**：
   - 更高效（减少内存分配次数）。
   - 避免内存泄漏（如构造函数抛出异常时）。
   ```cpp
   auto ptr = std::make_shared<Data>(arg1, arg2); // 推荐
   ```

2. **避免循环引用**：
   - `shared_ptr` 的循环引用会导致内存泄漏，需用 `weak_ptr` 打破。

3. **不要混合使用裸指针和智能指针**：
   ```cpp
   int* rawPtr = new int(42);
   std::shared_ptr<int> ptr(rawPtr); // 危险！可能重复释放
   ```

4. **多线程安全**：
   - `shared_ptr` 的引用计数是线程安全的，但对象访问需单独加锁。

---

## **6. 示例：综合应用**
```cpp
#include <memory>
#include <iostream>

class Resource {
public:
    Resource() { std::cout << "Resource acquired\n"; }
    ~Resource() { std::cout << "Resource released\n"; }
    void use() { std::cout << "Resource used\n"; }
};

int main() {
    // unique_ptr 独占资源
    auto res1 = std::make_unique<Resource>();
    res1->use();

    // shared_ptr 共享资源
    auto res2 = std::make_shared<Resource>();
    {
        auto res3 = res2; // 引用计数=2
        res3->use();
    } // res3 析构，引用计数=1

    // weak_ptr 观察资源
    std::weak_ptr<Resource> weakRes = res2;
    if (auto temp = weakRes.lock()) {
        temp->use(); // 资源仍存在
    }

    return 0;
}
```

**输出**：
```
Resource acquired
Resource used
Resource acquired
Resource used
Resource used
Resource released
Resource released
```

---

## **总结**
- **`unique_ptr`**：轻量独占，适合替代裸指针。
- **`shared_ptr`**：共享所有权，需注意循环引用。
- **`weak_ptr`**：解决循环引用，用于观察。
- **优先使用 `make_*`** 创建智能指针，避免直接 `new`。

正确使用智能指针可以显著提升 C++ 代码的安全性和可维护性！ 🚀

# 重载
1. 成员函数形式的运算符重载：需遵循：返回值类型operator运算符（参数列表）
2. 加法运算符重载**Data operator+(Data);**：返回值类型-Data；operator+表示重载加法运算符；参数列表需要一个Data类型参数。
3. 全局函数的重载格式：**operator+(Data,Data)**
# 类与对象
# 构造函数（Constructor）

构造函数是C++中用于**初始化对象**的特殊成员函数，在对象创建时自动调用。以下是其核心特性和用法：

---

#### **1. 基本特性**
- **名称**：与类名相同（如`Point::Point`）。
- **无返回类型**（连`void`也不写）。
- **自动调用**：对象创建时（如`Point p(1,2);`）隐式执行。
- **不可手动调用**：不能像普通函数那样显式调用（如`p.Point()`是错误的）。

---

#### **2. 构造函数类型**
##### **(1) 默认构造函数**
- **无参数**或所有参数有默认值。
- **作用**：提供对象的默认初始化。
```cpp
class Point {
public:
    Point() { X=0; Y=0; }          // 显式定义
    Point(int x=0, int y=0);       // 带默认参数的默认构造
};
```
- **若未定义**：编译器自动生成一个（但若定义了其他构造函数，则不会生成）。

##### **(2) 参数化构造函数**
- 接受参数初始化对象。
```cpp
Point(int x, int y) : X(x), Y(y) {}  // 使用初始化列表
```

##### **(3) 拷贝构造函数**
- 用同类对象初始化新对象。
- **签名**：`ClassName(const ClassName &other)`
```cpp
Point(const Point &other) : X(other.X), Y(other.Y) {}
```
- **调用场景**：
  ```cpp
  Point p1(1,2);
  Point p2 = p1;  // 调用拷贝构造
  Point p3(p1);   // 直接调用
  ```

##### **(4) 委托构造函数（C++11）**
- 一个构造函数调用同类其他构造函数。
```cpp
Point() : Point(0, 0) {}  // 委托给参数化构造
```

##### **(5) 移动构造函数（C++11）**
- 通过“窃取”临时对象资源来初始化。
```cpp
Point(Point &&tmp) : X(tmp.X), Y(tmp.Y) {
    tmp.X = tmp.Y = 0;  // 置空原对象
}
```

---

#### **3. 初始化列表**
- **语法**：在构造函数参数后以冒号开头，用逗号分隔成员初始化。
```cpp
Point(int x, int y) : X(x), Y(y) {}
```
- **优势**：
  - 直接初始化成员（非先默认构造再赋值）。
  - **必须使用**的场景：
    - 初始化`const`成员（如`const int X`）。
    - 初始化引用成员。
    - 初始化没有默认构造函数的类成员。

---

#### **4. 关键规则**
1. **隐式调用**：  
   对象创建时自动调用匹配的构造函数。
   ```cpp
   Point p1;            // 默认构造
   Point p2(3,4);       // 参数化构造
   Point p3 = p2;       // 拷贝构造
   ```
2. **默认构造的陷阱**：  
   若定义了任何构造函数，编译器不再生成默认构造，此时`Point p;`会报错。
3. **explicit关键字**：  
   禁止隐式转换（避免意外构造）。
   ```cpp
   explicit Point(int x) : X(x) {}
   // Point p = 5;  // 错误！必须显式：Point p(5);
   ```

---

#### **5. 示例代码**
```cpp
class Point {
private:
    int X, Y;
public:
    Point() : X(0), Y(0) {}                          // 默认构造
    Point(int x, int y) : X(x), Y(y) {}              // 参数化构造
    Point(const Point &other) : X(other.X), Y(other.Y) {}  // 拷贝构造
    explicit Point(int x) : X(x), Y(0) {}            // 禁止隐式转换
};

int main() {
    Point p1;          // 默认构造
    Point p2(3,4);     // 参数化构造
    Point p3 = p2;     // 拷贝构造
    Point p4(5);       // 显式调用（explicit生效）
    // Point p5 = 6;   // 错误！explicit禁止隐式转换
}
```

---

#### **6. 常见问题**
**Q1**：构造函数能否是虚函数？  
**A**：不能。虚函数依赖虚表（vtable），而构造函数调用时对象尚未完全构建。

**Q2**：构造函数中能否调用其他成员函数？  
**A**：可以，但避免调用虚函数（此时多态未生效）。

**Q3**：如何避免拷贝构造被意外调用？  
**A**：用`=delete`显式删除：
```cpp
Point(const Point&) = delete;  // 禁止拷贝
```

---

#### **7. 设计建议**
1. **优先使用初始化列表**：提升效率（尤其对类类型成员）。
2. **对单参数构造用`explicit`**：防止隐式转换导致的歧义。
3. **遵循RAII**：在构造函数中获取资源（如内存、文件），在析构中释放。
# 静态成员函数static
1. 类的成员函数，直接通过类名调用。不依赖于任何对象实例。
2. 没有this指针：不能访问类的非静态成员（变量或函数）。若需访问成员，必须通过参数传入对象参数间接访问。不能声明为const
3. 属于类本身，而非类的某个对象。与对象无关，不参与多态。不能被override（覆盖是多态行为）。不能使用virtual
4. 语法
	```c
	class ClassName {
	public:
	    static ReturnType FunctionName(Parameters); // 声明
	};
	
	// 类外定义（可选，若在类内定义则自动内联）
	ReturnType ClassName::FunctionName(Parameters) {
	    // 函数体
	}
	```
5. 示例
	```c
	class Point {
	public:
		static void GetC(Point A, Point B) {  // 静态成员函数
			int z = sqrt((B.X-A.X)*(B.X-A.X) + (B.Y-A.Y)*(B.Y-A.Y)); //计算两点间距离
			cout << z << endl;
		}
	};
	```
6. 调用方式：通过类名直接调用
	```c
	//类名：：函数名（成员）
	Point::GetC(D, E);  // 无需对象实例
	```
7. 可访问成员：类的静态成员变量，其他**静态成员函数**，**通过参数传入的对象**的公有成员（如`GetC`中的`A.X`、`B.Y`）