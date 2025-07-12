## Spring Framework
1. Spring Framework 是一个开源的 **Java/JavaEE 应用开发框架**，它的核心目标是 **简化企业级应用开发**，提供一套 **全面的编程和配置模型**，帮助开发者更高效地构建可维护、可扩展的应用程序。
2. 系统架构
	![[Pasted image 20250711143442.png]]
### 核心容器（目标：充分解耦）
#### IoC（Inversion of Control）控制反转：
1. **IoC**：由主动new产生对象转换为外部（Spring提供的IoC容器）提供对象。对象控制权由程序转移到外部
2. **Bean**：在IoC容器中被创建或被管理的对象
	1. 别名
		1. ![[Pasted image 20250711162344.png]]
	2. 作用范围
		1. ![[Pasted image 20250711162533.png]]![[Pasted image 20250711162655.png]]
	3. 实例化bean的三种
		1. 构造方法
			1. ![[Pasted image 20250711171205.png]]
		2. 静态工厂实例化
			1. ![[Pasted image 20250711171136.png]]
		3. 实例工厂
			1. ==实用==![[Pasted image 20250711173003.png]]
			2. ![[Pasted image 20250711171918.png]]
	4. 生命周期
		1. ![[Pasted image 20250711175009.png]]
		2. ![[Pasted image 20250711175034.png]]
		3. ![[Pasted image 20250711175059.png]]
3. 入门案例：
	1. 导入坐标：pom.xml文件中< groupId>org.springframework< /groupId>  < artifactId>spring-context< /artifactId>  < version>5.2.10.RELEASE< /version>
	2. 定义Spring管理的类（接口）
		1. 接口Interface类的BookService
		2. class类的BookServiceImpl implements BookService
	3. 创建Spring配置文件，配置对应类作为Spring管理的bean
		1. 创建spring配置的xml文件，< bean id="bookDao" class="com.zytoame.dao.impl.BookDaoImpl"/>
	4. 初始化IoC容器（Spring核心容器），通过容器获取bean
		```java
		public class App {  
		    public static void main(String[] args) {  
		        //获取IoC容器  
		        ApplicationContext ctx = new   
 ("applicationContext.xml");  
		  
		        BookDao bookDao = (BookDao) ctx.getBean("bookDao");  
		        bookDao.save();  
		    }  
		}
		```
####  DI（Dependency Injection）依赖注入：在容器中建立bean与bean之间的依赖关系的整个过程
1. setter注入
	1. 引用类型property
		1. 删除使用new的形式创建对象的代码
		2. 提供依赖对象对应的setter方法，容器在执行
		3. 配置service和bean的依赖关系![[Pasted image 20250711161158.png]]
	2. 简单类型
		1. ![[Pasted image 20250711193711.png]]
2. 构造器注入constructor-arg
	1. 简单类型
		1. ![[Pasted image 20250711200047.png]]
3. 选择
	1. ![[Pasted image 20250711200502.png]]
4. 自动装配
	1. ![[Pasted image 20250711201851.png]]![[Pasted image 20250711202108.png]]
5. 集合注入
	1. 数据源对象管理
		1. ![[Pasted image 20250711205257.png]]
6. 加载properties文件
	1. 开命名空间![[Pasted image 20250711210032.png]]
	2. ![[Pasted image 20250711211629.png]]
	3. 注意点![[Pasted image 20250711211940.png]]
#### 容器
1. 创建容器
	1. ![[Pasted image 20250711212336.png]]
2. 获取bean
	1. ![[Pasted image 20250711212426.png]]
3. 总结
	1. 容器相关![[Pasted image 20250711212932.png]]
	2. bean![[Pasted image 20250711213049.png]]
	3. 依赖注入![[Pasted image 20250711213141.png]]
### 整合
###  AOP
### 事务