spring的设计模式：单例、工厂、观察者（监听器）、模板方法
## Spring Framework
1. Spring Framework 是一个开源的 **Java/JavaEE 应用开发框架**，它的核心目标是 **简化企业级应用开发**，提供一套 **全面的编程和配置模型**，帮助开发者更高效地构建可维护、可扩展的应用程序。
2. 系统架构
	![Pasted image 20250711143442](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711143442.png)
### 核心容器（目标：充分解耦）
#### IoC（Inversion of Control）控制反转：
1. **IoC**：由主动new产生对象转换为外部（Spring提供的IoC容器）提供对象。对象控制权由程序转移到外部
2. **Bean**：在IoC容器中被创建或被管理的对象
	1. 别名
		1. ![Pasted image 20250711162344](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711162344.png)
	2. 作用范围
		1. ![Pasted image 20250711162533](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711162533.png)![Pasted image 20250711162655](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711162655.png)
	3. 实例化bean的三种
		1. 构造方法
			1. ![Pasted image 20250711171205](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711171205.png)
		2. 静态工厂实例化
			1. ![Pasted image 20250711171136](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711171136.png)
		3. 实例工厂
			1. ==实用==![Pasted image 20250711173003](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711173003.png)
			2. ![Pasted image 20250711171918](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711171918.png)
	4. 生命周期
		1. **Bean创建流程**
			1. 解析`@Configuration`类
			2. 创建配置类实例
			3. 处理配置类的依赖注入（@Resource/@Autowired）
			4. 调用`@Bean`方法或接口方法（如`addInterceptors`）
		2. ![Pasted image 20250711175009](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711175009.png)
		3. ![Pasted image 20250711175034](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711175034.png)
		4. ![Pasted image 20250711175059](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711175059.png)
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
		3. 配置service和bean的依赖关系![Pasted image 20250711161158](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711161158.png)
	2. 简单类型
		1. ![Pasted image 20250711193711](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711193711.png)
2. 构造器注入constructor-arg
	1. 简单类型
		1. ![Pasted image 20250711200047](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711200047.png)
3. 选择
	1. ![Pasted image 20250711200502](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711200502.png)
4. 自动装配
	1. ![Pasted image 20250711201851](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711201851.png)![Pasted image 20250711202108](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711202108.png)
5. 集合注入
	1. 数据源对象管理
		1. ![Pasted image 20250711205257](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711205257.png)
6. 加载properties文件
	1. 开命名空间![Pasted image 20250711210032](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711210032.png)
	2. ![Pasted image 20250711211629](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711211629.png)
	3. 注意点![Pasted image 20250711211940](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711211940.png)
#### 注解开发
1. 纯注解开发
```java
public class AppForAnnotation {  
    public static void main(String[] args) {  
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);  
    }  
}
```
2. bean生命周期
	1. ![Pasted image 20250712104533](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712104533.png)
3. 依赖注入
	1. 引用类型![Pasted image 20250712105302](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712105302.png)![Pasted image 20250712105328](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712105328.png)
	2. 简单类型：使用@Value("")进行注入
	3. 加载properties文件：使用@PropertySource({"",""})
4. 第三方bean管理
	1. ![Pasted image 20250712112249](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712112249.png)
	2. 依赖注入
		1. ![Pasted image 20250712112528](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712112528.png)
5. 对比
	1. ![Pasted image 20250712112850](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712112850.png)
#### 容器
1. 创建容器
	1. ![Pasted image 20250711212336](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711212336.png)
2. 获取bean
	1. ![Pasted image 20250711212426](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711212426.png)
3. 总结
	1. 容器相关![Pasted image 20250711212932](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711212932.png)
	2. bean![Pasted image 20250711213049](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711213049.png)
	3. 依赖注入![Pasted image 20250711213141](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250711213141.png)
### 整合
1. MyBatis
	1. MybatisConfig文件
		```java
		//factoryBean都是造对象的  
		public class MybatisConfig {  
		    @Bean  
		    public SqlSessionFactoryBean sqlSessionFactory(DataSource dataSource) {  
		        SqlSessionFactoryBean ssfb = new SqlSessionFactoryBean();  
		        ssfb.setTypeAliasesPackage("com.zytoame.domain");  
		        ssfb.setDataSource(dataSource);  
		        return ssfb;  
		    }  
		    @Bean  
		    public MapperScannerConfigurer mapperScannerConfigurer() {  
		        MapperScannerConfigurer msc = new MapperScannerConfigurer();  
		        msc.setBasePackage("com.zytoame.dao");  
		        return msc;  
		    }  
		}
		```
		1. ![Pasted image 20250712134742](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712134742.png)![Pasted image 20250712134804](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712134804.png)
2. 整合junit
	1. ![Pasted image 20250712143448](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712143448.png)
###  AOP
#### 原理
- AOP（Aspect-Oriented Programming，面向切面编程）是OOP（面向对象编程）的补充技术，用于**解耦横切关注点**（Cross-Cutting Concerns）。它通过动态代理等技术，将分散在多个类中的重复代码（如日志、事务、安全等）抽取到统一的模块中，使业务逻辑更纯净。
- **本质**：通过预编译或运行时动态代理，在**不修改源代码**的情况下给程序**动态添加功能**。
- **优势**：减少重复代码、降低耦合度、提升可维护性。 
-  **AOP的核心概念**

| 概念                  | 说明                                                     | 示例                                              |
| ------------------- | ------------------------------------------------------ | ----------------------------------------------- |
| **切面（Aspect）**      | 封装横切逻辑的模块（如日志、事务）描述通知与切入点的对应关系                         | `@Aspect`注解的类                                   |
| **连接点（Join Point）** | 程序执行的点（任意位置）（如方法调用、异常抛出）在spring中理解为方法的执行               | `UserService.createUser()`方法执行时                 |
| **通知（Advice）**      | 切面在连接点的动作（如方法前/后执行）在切入点处执行 的操作，共性功能                    | `@Before`, `@After`等注解的方法                       |
| 通知类                 | 定义通知的类                                                 |                                                 |
| **切点（Pointcut）**    | 匹配连接点的表达式（定义哪些方法需要增强）spring中一个切入点可以只描述一个具体方法，也可以匹配多个方法 | `@Pointcut("execution(* com.service.*.*(..))")` |
| **目标对象（Target）**    | 被代理的原始对象                                               | `UserService`实例                                 |
![Pasted image 20250712144410](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712144410.png)
#### 入门案例
1. pom.xml文件：1.导入坐标
	```java
	<dependency>  
	  <groupId>org.aspectj</groupId>  
	  <artifactId>aspectjweaver</artifactId>  
	  <version>1.9.4</version>  
	</dependency>  
	  context包含aop了
	<dependency>  
	  <groupId>org.springframework</groupId>  
	  <artifactId>spring-context</artifactId>  
	  <version>5.2.10.RELEASE</version>  
	</dependency>
	```
2. aop中的java类
```java
//6.定义通知类受spring容器管理，并定义当前类为切面类
@Component  
@Aspect  
public class MyAdvice {   
    //4.定义切入点  ，无参数无返回值
    @Pointcut("execution(void com.zytoame.dao.BookDao.update())")  
    private void pt(){}  
  
    //5.绑定切入点和通知  
    @Before("pt()")  
    //3.定义通知类  
    public void advice() {  
        System.out.println(System.currentTimeMillis());  
    }  
}
```
2.  7. springConfig文件中加入@EnableAspectJAutoProxy对AOP注解驱动支持，与@Aspect对应
#### 切入点
1. 切入点表达式：![Pasted image 20250712161848](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712161848.png)
2. 通配符
	1. 给所有业务层的查询方法加aop：@Pointcut("execution(* com.zytoame. * . * Service.find* (..))") ![Pasted image 20250712164117](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712164117.png)
	2. ![Pasted image 20250712162226](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712162226.png)
#### 通知
1. 环绕通知@Arround
	1. ![Pasted image 20250712165359](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712165359.png)
	```java
	@Around("pt()")
	public Object around(ProceedingJoinPoint pjp) throws Throwable{
		System.out.println("around before advice...");
		Object ret = pjp.proceed();
		System.out.println("around after advice...");
		return ret;
	}
	```
#### 案例
测量业务层接口执行效率(万次核心代码执行效率)
```java
@Around("ProjectAdvice.servicePt()")
public void runSpeed(ProceedingJoinPoint pjp) throws Throwable {
	//获取执行签名信息
	Signature signature = pjp.getSignature();
	//通过签名获取执行类型(接口名)
	String className = signature.getDeclaringTypeName();
	//通过签名获取执行操作名称(方法名)
	String methodName = signature.getName();
	long start = System.currentTimeMillis();
	for (int i = 0; i < 10000; i++) {
		pjp.proceed();
	}
	
	long end = System.currentTimeMillis();
	System.out.println("万次执行:"+className+"."+methodName+" --- >"+(end-start)+"ms");
}
```
#### 通知获取参数数据
1. 参数数据![Pasted image 20250712171411](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712171411.png)
2. 返回值![Pasted image 20250712171446](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712171446.png)
#### 案例：密码空格处理 
![Pasted image 20250712172916](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712172916.png)
### 事务：开到业务层上 
案例：银行账户转账：a账户减钱，b账户加钱
![Pasted image 20250712180604](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712180604.png)![Pasted image 20250712180612](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712180612.png)
jdbcConfig文件：![Pasted image 20250712180658](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712180658.png)
![Pasted image 20250712180716](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250712180716.png)
需求增加：对每次转账操作在数据库进行留痕记录（增加日志），无论转账是否成功
	存在问题：日志记录与转账操作隶属于同一个事务，同成功同失败。
		transfer操作中有三个事务（进钱，减钱，日志）三个事务都加入到同一个事务。
	解决：日志不加入，开一个新的事务
		在日志业务层接口处@**Transactional**(==propagation== = Propagation.**==REQUIRES_NEW==**)
- Spring事务角色
	- 事务管理员
	- 事务协调员
- 事务配置
	- 事务相关配置![Pasted image 20250713120412](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250713120412.png)
	- 异常回滚：error或者运行时异常会发生回滚；有些异常是默认不参与回滚的（IOException
		- 异常出现在业务层if(true){throw new IOException();}抛出异常
		- 在业务层接口@**Transactional**(==rollbackFor== = {IOExceprion.class})
		- ==rollbackFor==：设置事务回滚异常（class）
		- @**Transactional**开事务：在业务层接口添加Spring事务管理
	- 事务必定运行
		- try{可能不运行的事务}finally{一定要运行的事务}
- 事务传播行为
	- ![Pasted image 20250713120257](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250713120257.png)
## SpringMVC（表现层框架）
### 概述
1. 基于Java实现MVC模型的轻量级web框架：表现层开发
	1. web程序工作流程： web程序通过浏览器访问页面，前端通过异步提交的方式将请求发送给后端处理，后端服务器通过表现层，业务层，数据层三层架构的形式进行开发。页面发送的请求由表现层接受，获取用户的请求参数后传递给业务层，再由业务层访问数据层，从数据层得到的数据再返回给表现层。表现层拿到数据之后将数据转换为json格式发送给前端页面，前端接收数据之后解析成用户浏览的页面信息，交给浏览器。
	2. 后端三层架构：数据层（JDBC，MyBatis加速开发），表现层（servlet，springMVC）
### 入门(除了控制器类，其他都是一次性的)
1. 导入坐标
	```xml
	<dependency>  
	  <groupId>javax.servlet</groupId>  
	  <artifactId>javax.servlet-api</artifactId>  
	  <version>3.1.0</version>  
	  <scope>provided</scope>  
	</dependency>  
	  
	<dependency>  
	  <groupId>org.springframework</groupId>  
	  <artifactId>spring-webmvc</artifactId>  
	  <version>5.2.10.RELEASE</version>  
	</dependency>

	<plugins>  
		<plugin>    
			<groupId>org.opoo.maven</groupId>  
		    <artifactId>tomcat9-maven-plugin</artifactId>  
		    <version>3.0.1</version>  
		</plugin>
	</plugins>
	```
2. 创建springmvc控制器类（等同于Servlet功能）,用来处理请求
	```java
	//1.定义bean  
	@Controller  
	public class UserController {  
	    //2.设置当前操作的访问路径  
	    @RequestMapping("/save")  
	    //3.设置当前操作的返回值类型  返回值作为响应体返回给请求方
	    @ResponseBody  
	    public String save(){  
	        System.out.println("user save ...");  
	        return "{'module':'springmvc'}";  
	    }  
	}
	```
3. 初始化springmvc环境（同spring环境），设定springmvc加载对应的bean。（springmvc属于spring，所以所有的一切都要是bean，所以要加载bean）
	```java
	//4.创建springmvc的配置文件，加载controller对应的bean  
	@Configuration  
	@ComponentScan("com.zytoame.controller")  
	public class SpringMvcConfig {  
	}
	```
4. 初始化Servlet容器，加载springmvc环境，并设置springmvc技术处理的请求。（启动tomcat服务器的时候要保证加载到springmvc的配置。1.初始化一个web专用的WebAppllicationContext，2.把springmvc类注册上去，3.设置所有的请求交给springmvc处理
	```java
	//5.定义一个Servlet容器启动的配置类，在里面加载Spring的配置  
	public class ServletConfig extends AbstractDispatcherServletInitializer {  
	    //加载springmvc容器配置  
	    @Override  
	    protected WebApplicationContext createServletApplicationContext() {  
	        AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();  
	        ctx.register(SpringMvcConfig.class);  
	        return ctx;  
	    }  
	    //设置哪些请求归属springmv处理,all  
	    @Override  
	    protected String[] getServletMappings() {  
	        return new String[]{"/"};  
	    }  
	    //加载spring容器配置  
	    @Override  
	    protected WebApplicationContext createRootApplicationContext() {  
	        return null;  
	    }  
	}
	```
5. 简化开发
	```java
		public class ServletConfig extends AbstractAnnotationConfigDispatcherServletInitializer {  
	    @Override  
	    protected String[] getServletMappings() {  
	        return new String[]{"/"};  
	    }  
	    @Override  
	    protected Class<?>[] getRootConfigClasses() {  
	        return new Class[]{SpringConfig.class};  
	    }  
	    @Override  
	    protected Class<?>[] getServletConfigClasses() {  
	        return new Class[]{SpringMvcConfig.class};  
	    } 
	    //中文乱码处理  
		@Override  
		protected Filter[] getServletFilters() {  
		    CharacterEncodingFilter filter = new CharacterEncodingFilter();  
		    filter.setEncoding("UTF-8");  
		    return new Filter[]{filter};  
		} 
	}
	```
### の
- springmvc控制controller中的bean（表现层bean），spring控制除了controller以外的所有bean（业务bean，功能bean）
	```java
	//spring加载对应bean
	@Configuration  
	@ComponentScan(value = "com.zytoame",  
	    excludeFilters = @ComponentScan.Filter(  
	        type = FilterType.ANNOTATION,  
	        classes = Controller.class  
	    )  
	)  
	public class SpringConfig {  	}
	```
- 请求与响应
	- 请求参数
		- 普通参数，参数名与形参变量名不同，使用@RequestParam（“”）绑定参数关系
		- POJO参数
		- 数组参数
		- 集合参数：@RequestParam List< String> 形参变量名
		- 日期类型：@DateTimeFormat（pattern=“yyyy-MM-dd HH:mm:ss") 是url
		- 类型转换器：convert接口
	- 响应
		- 页面
		- json数据 
			- ![Pasted image 20250714101448](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250714101448.png)
- REST风格：书写简化，隐藏访问行为。使用restful开发
	- ![Pasted image 20250714102032](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250714102032.png)
	- ![Pasted image 20250714104636](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250714104636.png)
	- rustful简化开发
		```java
		@RestController
		@RequestMapping("/books")
		public class BookController2 {
		@PostMapping
		public String save(@RequestBody Book book){
		System.out.println("book save ... " + book);
		return "{'module': 'book save' }";
		}
		@DeleteMapping("/{id}")
		public String delete(@PathVariable Integer id){
		System.out.println("book delete ... " + id);
		return "{'module' : 'book delete'}";
		
		}
		```
	- 页面数据交互
		- ![Pasted image 20250714110503](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250714110503.png)
		- ![Pasted image 20250714110517](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250714110517.png)
		- ![Pasted image 20250714110531](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250714110531.png)
### ==ssm整合==
- ![Pasted image 20250714113744](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250714113744.png)
- 业务层测试test
- 事务处理
- 表现层数据封装
	- controller目录下Code文件
		```java
		public class Code {  
		    public static final Integer SAVE_OK = 20011;  
		    public static final Integer DELETE_OK = 20021;  
		    public static final Integer UPDATE_OK = 20031;  
		    public static final Integer GET_OK = 20041;  
		  
		    public static final Integer SAVE_ERR = 20010;  
		    public static final Integer DELETE_ERR = 20020;  
		    public static final Integer UPDATE_ERR = 20030;  
		    public static final Integer GET_ERR = 20040;  
		}
		```
	- Result文件
		```java
		public class Result {  
		    private Object data;  
		    private Integer code;  
		    private String msg;  
		  
		    public Result() {  
		    }  
		  
		    public Result(Integer code, Object data) {  
		        this.data = data;  
		        this.code = code;  
		    }  
		  
		    public Result(Integer code, Object data, String msg) {  
		        this.data = data;  
		        this.code = code;  
		        this.msg = msg;  
		    }
		getter和setter构造函数。。。
		```
	- 表现层数据封装Controller类
		- ![Pasted image 20250714163509](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250714163509.png)
		```java
		@GetMapping  
		public Result getAll() {  
		    List<Book> all = bookService.getAll();  
		    Integer code = all != null ? Code.GET_OK : Code.GET_ERR;  
		    String msg = all != null ? "" : "数据查询失败，请重试";  
		    return new Result(code, all, msg);  
		}
		```
- 异常处理：全都抛到表现层处理  **AOP**
	```java
	@RestControllerAdvice  
	public class ProjectExceptionAdvice {  
	    @ExceptionHandler(value = Exception.class)  
	    public Result doException(Exception ex) {  
	        System.out.println("异常处理");  
	        return new Result(666,null,"异常处理");  
	    }  
	}
	```
	- 自定义系统级异常和业务级异常
	- 自定义异常编码
	- 触发自定义异常
	- 拦截处理异常
- 拦截器：工作机制，做增强，在controller前后进行
## Springboot
- 属性配置
	- ![Pasted image 20250715103706](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250715103706.png)
	- yaml数据读取
		- 自定义对象封装指定数据（实体类封装 @ConfigurationProperties(prefix = "enterprise")  controller类中：@Autowired  private Enterprise enterprise;
	- 多环境启动配置![Pasted image 20250715110643](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250715110643.png)
	- 测试类整合junit进行单元测试：
		- ![Pasted image 20250715113753](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250715113753.png)
	- 整合Mybatis
		- 坐标
			```xml
			<!-- MyBatis Starter -->  
			<dependency>  
			    <groupId>org.mybatis.spring.boot</groupId>  
			    <artifactId>mybatis-spring-boot-starter</artifactId>  
			    <version>3.0.3</version>  
			</dependency>  
			  
			<!-- 数据库驱动（以MySQL为例） -->  
			<dependency>  
			    <groupId>com.mysql</groupId>  
			    <artifactId>mysql-connector-j</artifactId>  
			    <scope>runtime</scope>  
			</dependency>
			
			<!--druid-->
			<dependency>
			  <groupId>com.alibaba</groupId>
			  <artifactId>druid</artifactId>
			  <version>1.1.16</version>
			</dependency>
			```
		- 数据源参数：yml：
			- ![Pasted image 20250715140309](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250715140309.png)
		- 定义数据层接口Dao与映射配置@Mapper![Pasted image 20250715140404](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250715140404.png)
		- 测试![Pasted image 20250715140348](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250715140348.png)

## @Component和@Transactional和@Configuration

| 注解             | 主要用途       | 作用级别 | 是否创建bean |
| -------------- | ---------- | ---- | -------- |
| @Component     | 标识Spring组件 | 类    | 是        |
| @Transactional | 定义事务行为     | 类或方法 | 否        |
| @Configuration | 定义配置类      | 类    | 是(配置类本身) |
###  **1. @Component**

**适用场景**：

- **普通Bean管理**：当你需要让Spring管理某个类的实例（自动创建、依赖注入）时
    
- **组件扫描**：配合`@ComponentScan`让Spring自动发现和注册Bean
    
- **通用组件**：不适合用更专业注解（如`@Service`、`@Repository`）的类
    

**常见用例**：

```java
@Component
public class MyUtilityClass {
    // 工具类，没有明确的服务或仓库特征
}
```

**替代注解**（更语义化的`@Component`变体）：

- `@Service`：业务逻辑层（Service层）
    
- `@Repository`：数据访问层（DAO层）
    
- `@Controller`/`@RestController`：Web控制器
    

---

### **2. @Transactional**

**适用场景**：

- **数据库事务**：需要保证多个数据库操作要么全部成功，要么全部回滚
    
- **方法级事务控制**：某些方法需要独立的事务行为（如只读事务、特殊隔离级别）
    
- **声明式事务**：不想手动编写事务管理代码（如`try-catch`回滚逻辑）
    

**常见用例**：
```java
@Service
public class OrderService {

    @Transactional  // 整个方法在一个事务中执行
    public void placeOrder(Order order) {
        // 扣减库存
        // 创建订单
        // 支付处理
    }
    
    @Transactional(readOnly = true)  // 只读事务
    public Order getOrderById(Long id) {
        // 查询订单
    }
}
```

**关键配置选项**：

- `propagation`：事务传播行为（如`REQUIRED`、`REQUIRES_NEW`）
    
- `isolation`：隔离级别（如`READ_COMMITTED`）
    
- `timeout`：超时时间
    
- `rollbackFor`：指定哪些异常触发回滚
    

---

### **3. @Configuration**

**适用场景**：

- **显式Bean定义**：需要手动控制Bean的创建逻辑（如第三方库的集成）
    
- **条件化配置**：基于条件动态创建Bean（配合`@Conditional`）
    
- **替代XML配置**：用Java代码完全替代XML配置
    

**常见用例**：
```java
@Configuration
public class DatabaseConfig {

    @Bean
    @Profile("prod")  // 仅在生产环境生效
    public DataSource prodDataSource() {
        // 配置生产环境数据源
    }

    @Bean
    @ConditionalOnClass(RedisClient.class)
    public RedisTemplate redisTemplate() {
        // 当类路径存在RedisClient时才创建Bean
    }
}
```

**典型模式**：

- 定义`@Bean`方法返回需要管理的对象
    
- 组合其他注解实现条件化逻辑
    
- 导入其他配置（通过`@Import`）
    

---

### **选择注解的决策流程**

1. **是否需要事务管理？**
    
    - 是 → 用`@Transactional`
        
    - 否 → 进入下一步
        
2. **是否需要显式定义Bean的创建逻辑？**
    
    - 是 → 用`@Configuration` + `@Bean`
        
    - 否 → 进入下一步
        
3. **是否希望Spring自动扫描并管理这个类？**
    
    - 是 → 用`@Component`或其派生注解
        
    - 否 → 可能不需要任何注解
        

---

### **组合使用示例**
```java
@Configuration
@EnableTransactionManagement  // 启用事务管理
public class AppConfig {

    @Bean
    public PlatformTransactionManager transactionManager(DataSource dataSource) {
        return new DataSourceTransactionManager(dataSource);
    }
}

@Service
public class BankService {

    @Transactional
    public void transferMoney(Account from, Account to, BigDecimal amount) {
        // 转账业务逻辑
    }
}
```

**总结**：

- `@Component`：让Spring自动管理对象
    
- `@Transactional`：添加事务边界
    
- `@Configuration`：精细控制Bean的创建和组装


---

# @Autowired 和 @Resource 的区别详解

`@Autowired` 和 `@Resource` 都是用于依赖注入的注解，但它们来自不同的标准，在行为上有一些重要区别。

## 1. 来源不同

- **`@Autowired`**:
    
    - 是 Spring 框架特有的注解
        
    - 属于 `org.springframework.beans.factory.annotation` 包
        
- **`@Resource`**:
    
    - 是 Java 标准注解 (JSR-250)
        
    - 属于 `javax.annotation` 包
        
    - 不依赖于 Spring 框架，理论上可以在其他支持 JSR-250 的框架中使用
        

## 2. 注入方式不同

### `@Autowired` 注入机制

默认按**类型**(Type)进行自动装配:

```java
@Autowired
private UserRepository userRepository;
```

1. Spring 会在容器中查找 `UserRepository` 类型的 bean
    
2. 如果找到多个同类型 bean，会抛出 `NoUniqueBeanDefinitionException`
    
3. 可以通过 `@Qualifier` 注解指定 bean 名称来解决冲突
    
```java
@Autowired
@Qualifier("userRepositoryImpl") 
private UserRepository userRepository;
```

### `@Resource` 注入机制

默认按**名称**(Name)进行装配，其次按类型:
```java
@Resource
private UserRepository userRepository;
```

1. 首先尝试按名称匹配 - 查找名为 "userRepository" 的 bean
    
2. 如果找不到，则回退到按类型匹配
    
3. 可以通过 name 属性显式指定 bean 名称
    
```java
@Resource(name = "userRepositoryImpl")
private UserRepository userRepository;
```

## 3. 可选性不同

- **`@Autowired`**:
    
    - 默认情况下是强制依赖(required=true)
        
    - 可以设置为非强制: `@Autowired(required=false)`
        
- **`@Resource`**:
    
    - 默认情况下也是强制依赖
        
    - 没有直接设置可选性的属性，但可以通过 name 属性和类型回退机制实现类似效果
        

## 4. 适用范围

- **`@Autowired`**:
    
    - 可以用于**构造器**、方法、字段和参数
        
    - Spring 特有功能如 `@Primary`、`@Qualifier` 与其配合使用
        
- **`@Resource`**:
    
    - 只能用于字段和方法(不能用于构造器)
        
    - 更符合 Java 标准，但功能相对较少
        

## 5. 使用建议

**使用 `@Autowired` 当:**

- 项目完全基于 **Spring**生态, 与 Spring 生态集成更好
    
- 需要与 Spring 其他特性(如 `@Primary`、`@Qualifier`)配合使用
    
- 需要**构造器**注入时
    

**使用 `@Resource` 当:**

- 希望代码减少对 Spring 的依赖，保持更好的**可移植性**。需要**减少框架耦合**。
    
- 需要按名称明确指定依赖时
    
- 在**非 Spring 环境**中使用(如 Java EE 容器)
    

## 6. 示例对比

### `@Autowired` 示例

```java
@Service
public class UserService {
    
    @Autowired
    private UserRepository userRepository;
    
    @Autowired
    @Qualifier("auditLogger")
    private Logger logger;
    
    @Autowired(required = false)
    private Optional<CacheManager> cacheManager;
}
```

### `@Resource` 示例

```java
@Service
public class UserService {
    
    @Resource
    private UserRepository userRepository;
    
    @Resource(name = "auditLogger")
    private Logger logger;
    
    // 没有直接的 required=false 替代方案
    // 可以通过 Optional 或检查 null 实现
}
```

## 7. 总结对比表

|特性|`@Autowired`|`@Resource`|
|---|---|---|
|**来源**|Spring 特有|Java 标准(JSR-250)|
|**默认注入方式**|按类型|按名称，其次按类型|
|**构造器注入**|支持|不支持|
|**可选依赖**|支持(required=false)|不支持直接设置|
|**指定名称**|需配合`@Qualifier`|使用name属性|
|**与其他Spring特性集成**|更好(如`@Primary`)|有限|
|**可移植性**|仅Spring|任何JSR-250兼容环境|

--- 

