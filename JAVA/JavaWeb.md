## HTTP
### 请求数据格式
● 请求数据分为3部分:
1. 请求行:请求数据的第一行。其中GET表示请求方式,/ 表示请求资源路径,HTTP/1.1表示协议版本
2. 请求头:第二行开始,格式为key:value形式。
	1. 常见的HTTP请求头:
		Host:表示请求的主机名
		User-Agent:浏览器版本,例如Chrome浏览器的标识类似Mozilla/5.0 ..
		Chrome/79,IE浏览器的标识类似Mozilla/5.0(Windows NT ... )like Gecko;
		Accept:表示浏览器能接收的资源类型,如text/* ,image/* 或者* /* 表示所有;
		Accept-Language:表示浏览器偏好的语言,服务器可以据此返回不同语言的网页;
		Accept-Encoding:表示浏览器可以支持的压缩类型,例如gzip, defla
		leflate等
3. 请求体:POST请求的最后一部分,存放请求参数
4. GET请求和POST请求区别:
	GET请求请求参数在请求行中,没有请求体。
	POST请求请求参数在请求体中
	GET请求请求参数大小有限制,POST没有
	1. GET /HTTP/1.1
		Host: www.itcast.cn
		Connection: keep-alive
		Cache-Control: max-age=0 Upgrade-Insecure-Requests: 1
		User-Agent: Mozilla/5.0 Chrome/91.0.4472.106
	2. POST / HTTP/1.1
		Host: www.itcast.cn
		Connection: keep-alive
		Cache-Control: max-age=0 Upgrade-Insecure-Requests: 1
		User-Agent: Mozilla/5.0 Chrome/91.0.4472.106
		
		username=superbaby&password=123456
### 响应数据格式
- 响应数据分为3部分:
	1. 响应行:响应数据的第一行。其中HTTP/1.1表示协议版
	本,200表示响应状态码,OK表示状态码描述
	2. 响应头:第二行开始,格式为key:value形式
	3. 响应体:最后一部分。存放响应数据
	4. HTTP/1.1 200 OK
		Server: Tengine
		Content-Type: text/html
		Transfer-Encoding: chunked ...
		
		< html>
		< head>
		< title>< /title>
		< /head>
		< body>< /body>
		< /html>
- 常见的HTTP响应头:
	Content-Type:表示该响应内容的类型,例如text/html, image/jpeg;
	Content-Length:表示该响应内容的长度(字节数);
	Content-Encoding:表示该响应压缩算法,例如gzip;
	Cache-Control:指示客户端应如何缓存,例如max-age-300 ，	表示可以最多纸存300秒
- 状态码分类
	- 1xx：响应中 -- 临时状态码,表示请求已经接受,告诉客户端应该继续请求或者如果它已经完成则忽略它
	- 2xx：成功 -- 表示请求已经被成功接收,处理已完成
	- 3xx：重定向一-重定向到其它地方:它让客户端再发起一个请求以完成整个处理。
	- 4xx：客户端错误 -- 处理发生错误,责任在客户端,如:客户端的请求一个不存在的资源,客户端未被授权,禁止访问等
	- 5xx：服务器端错误-一处理发生错误,责任在服务端,如:服务端抛出异常,路由出错,HTTP版本不支持等
## tomcat（Web服务器）servlet容器
- web服务器作用
	- 封装HTTP协议操作，简化开发
	- 可以将web项目部署到服务器中，对外提供网上浏览服务
- 插件
	- ![[Pasted image 20250706170226.png]]
	```xml
	<plugins>
	<plugin>
	<groupId>org.opoo.maven</groupId>
	<artifactId>tomcat9-maven-plugin</artifactId>
	<version>3.0.1</version>
	</plugin>
	</plugins>
	```
	- 	![[Pasted image 20250706181805.png]]
- servlet：动态 web资源开源技术。接口
	- 入门![[Pasted image 20250706172616.png]]
	- 执行流程![[Pasted image 20250706182141.png]]
	- 生命周期：对象从被创建到被销毁的整个过程![[Pasted image 20250706182609.png]]
	- 体系结构
	- ![[Pasted image 20250706205948.png]]
- request
	- 获取请求数据![[Pasted image 20250709161455.png]]
	- 通用![[Pasted image 20250709162254.png]]
	- 设置响应数据功能![[Pasted image 20250709215956.png]]
- 继承体系
	- ![[Pasted image 20250709172509.png]]
- 重定向
	- ![[Pasted image 20250710084543.png]]
- 路径问题
	- ![[Pasted image 20250710090817.png]]
- 响应字符数据
	- //设置流的编码  
		response.setContentType("text/html;charset=utf-8");  
		//获取字符输出流，  
		PrintWriter out = response.getWriter();
		out.write("< h1>hello< /h1>");   //输出标题为hello，大写
		out.write("hello");     
		out.write("你好");  //正常输出你好
	- 不需要关闭流，因为随着Response对象销毁，由服务器关闭
### 案例：
- 用户登录![[Pasted image 20250710094430.png]]![[Pasted image 20250710094912.png]]
- 用户注册![[Pasted image 20250710101510.png]]
	- 问题：重复创建factory，代码重复
		- 创建工具类
		- 静态代码块
		- 在java文件夹中com文件夹下创建一个util文件夹，创建SqlSessionFactoryUtils类
		```java
		package com.itheima.util;  
		  
		import org.apache.ibatis.io.Resources;  
		import org.apache.ibatis.session.SqlSessionFactory;  
		import org.apache.ibatis.session.SqlSessionFactoryBuilder;  
		  
		import java.io.IOException;  
		import java.io.InputStream;  
		  
		public class SqlSessionFactoryUtils {  
		  
		    //提升作用域  
		    private static SqlSessionFactory sqlSessionFactory;  
		  
		    static {  
		        //静态代码块会随着类的加载而自动执行，且只执行一次  
		        try {  
		            String resource = "mybatis-config.xml";  
		            InputStream inputStream = Resources.getResourceAsStream(resource);  
		            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);  
		        } catch (IOException e) {  
		            e.printStackTrace();  
		        }  
		    }  
		    public static SqlSessionFactory getSqlSessionFactory(){  
		        return sqlSessionFactory;  
		    }  
		}
		```
		- 在web里的servlet类中修改
		```java
		//2.1 获取SqlSessionFactory对象  
		/*String resource = "mybatis-config.xml";  
		InputStream inputStream = Resources.getResourceAsStream(resource);  
		SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);*/  
		SqlSessionFactory sqlSessionFactory = SqlSessionFactoryUtils.getSqlSessionFactory();
		```
## 会话技术
### 客户端cookie
1. 基本使用
	1. ![[Pasted image 20250710141608.png]]
2. 使用细节
	1. 设置存活时间：cookie.setMaxAge(60* 6* 24* 7);
	2. 编码解码
		1. String value = "张三";  
			//URL编码  
			value = URLEncoder.encode(value, "UTF-8");
			ookie cookie = new Cookie("username", value);  
			//设置cookie存活时间  
			cookie.setMaxAge(60* 6* 24* 7);  
			//发送cookie，  
			response.addCookie(cookie);
		2. //获取cookie数组  
			 Cookie[] cookies = request.getCookies();  
			//遍历数组，  
			for (Cookie cookie : cookies) {  
			    //获取数据  
			    String name = cookie.getName();  
			    if("username".equals(name)){  
			        String value = cookie.getValue();  
			        //URL解码  
			        value = URLDecoder.decode(value, "UTF-8");  
			        System.out.println(name + ":" + value);  
			    }  
			}
### 服务端session
1. 服务端会话跟踪技术：将数据保存到服务端
2. JavaEE提供HttpSession接口，来实现一次会话的多次请求间数据共享功能
3. 使用：
	1. 存储session数据
		1. //存储到session中  
			//获取对象  
			HttpSession session = request.getSession();  
			//存储数据  
			session.setAttribute("username", "zsz");
	2. 从session中获取数据
		1. //获取session对象  
			HttpSession session = request.getSession();  
			//获取数据  
			Object username = session.getAttribute("username");  
			System.out.println("username: " + username);
	3. session对象功能
### 对比
![[Pasted image 20250710151158.png]]
### 案例
基本逻辑![[Pasted image 20250710160705.png]]
注册![[Pasted image 20250711104118.png]]
1. 注册代码，registerServlet.java
	```java
	@Override  
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {  
	   //1. 获取用户名和密码数据  
	    String username = request.getParameter("username");  
	    String password = request.getParameter("password");  
		
		//封装对象
	    User user = new User();  
	    user.setUsername(username);  
	    user.setPassword(password);
		
		//2. 调用service 注册  
	    boolean flag = service.register(user);  
	    //3. 判断注册成功与否  
	    if(flag){  
	        //注册成功，跳转登陆页面  
	        request.setAttribute("register_msg","注册成功，请登录");  
	        request.getRequestDispatcher("/login.jsp").forward(request,response);  
	    }else {  
	        //注册失败，跳转到注册页面  
	        request.setAttribute("register_msg","用户名已存在");  
		    request.getRequestDispatcher("/register.jsp").forward(request,response);  
	    }  
	}
	```
2. 验证码：
	1. ![[Pasted image 20250711115001.png]]
	2. checkCodeUtil文件[file:/D:/Java/JavaCode/brand-demo/src/main/java/com/zytoame/util/CheckCodeUtil.java](file:///D:/Java/JavaCode/brand-demo/src/main/java/com/zytoame/util/CheckCodeUtil.java)
	3. register.jsp
		```java
		//刷新验证码图片，使用时间刷新保证不会重复出现同一张图  
		<script>  
		    document.getElementById("changeImg").onclick = function () {  
		        document.getElementById("checkCodeImg").src = "/brand-demo/checkCodeServlet?"+new Date().getMilliseconds();  
		    }  
		</script>
```
	4. CheckCodeServlet.java：
		```java
		// 生成验证码  
		ServletOutputStream os = response.getOutputStream();  
		String checkCode = CheckCodeUtil.outputVerifyImage(100, 50, os, 4);  
		  
		// 存入Session  
		HttpSession session = request.getSession();  
		session.setAttribute("checkCodeGen",checkCode);
		```
	5. RsgisterServlet.java：
		```java
		//获取内容，封装...
		// 获取用户输入的验证码
        String checkCode = request.getParameter("checkCode");

        // 程序生成的验证码，从Session获取
        HttpSession session = request.getSession();
        String checkCodeGen = (String) session.getAttribute("checkCodeGen");

        // 比对
        if(!checkCodeGen.equalsIgnoreCase(checkCode)){
            //允许注册
            request.setAttribute("register_msg","验证码错误");
            request.getRequestDispatcher("/register.jsp").forward(request,response);
            // 不允许注册
            return;
        }
        //调用service注册
		```
## 过滤器Filter
1. 入门
	![[Pasted image 20250711115319.png]]
2. 拦截路径：拦截之后过滤器才会被执行
	/* ：是拦截资源的路径，不是过滤器访问的路径
	![[Pasted image 20250711135157.png]]
3. 过滤器链：注解配置的Filter，优先级按照过滤器类名（字符串）的自然排序
	![[Pasted image 20250711135702.png]]
4. 案例：登录验证
	1. 判断是否登录成功：（将user存储到session中）session中是否有user对象