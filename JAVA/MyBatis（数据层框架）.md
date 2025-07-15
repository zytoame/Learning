持久层框架
用于JDBC开发
主要特性之一：动态sql

### **Mapper 接口 vs 传统方式**

| 特性            | Mapper 接口                                                                                                                                                    | 传统方式（直接调用 SqlSession）                                                                                                           |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| **类型安全**      | ✅ 编译时检查<br>方法名、参数类型、返回值类型都是 **Java 接口定义**，**编译器会检查错误**。<br>public interface UserMapper {<br>    User selectById(@Param("id") int id); // 编译时就能发现参数或返回值类型错误 } | ❌ 运行时可能出错<br>SqlSession.selectOne("namespace.id", param)<br>- SQL 语句的 `id` 是字符串，容易拼写错误，**运行时才会报错**。<br>- 参数和返回值的类型不强制约束，容易传错类型。 |
| **代码可读性**     | ✅ 方法名即语义<br>如 `selectById`、`insertUser`                                                                                                                      | ❌ 需维护字符串 ID<br>手动维护 `namespace.id` 的字符串映射                                                                                       |
| **IDE 支持**    | ✅ 自动补全、跳转                                                                                                                                                    | ❌ 无智能提示                                                                                                                         |
| **参数传递**      | ✅ 灵活（对象、Map、@Param）                                                                                                                                          | ❌ 需手动包装参数                                                                                                                       |
| **集成 Spring** | ✅ 自动注入                                                                                                                                                       | ❌ 需手动配置                                                                                                                         |
| **测试友好性**     | ✅ 易 Mock                                                                                                                                                     | ❌ 需模拟 SqlSession                                                                                                                |
## Mapper代理开发
快捷键：alt + 鼠标左键 整列编辑

alt + fn + insert：可以自动填充 tostring（）和 getter and setter（）

**List< Brand> brands = brandMapper.selectAll();**


![[Pasted image 20250703205751.png]]
核心配置文件的顶层结构
1. properties（属性）
2. settings（设置）
3. typeAliases（类型别名）
4. typesHandlers（类型处理器）
5. objectFactory（对象工厂）
6. plugins（插件）
7. environments（环境配置）
	1. environment（环境变量）
		1. transactionManager（事务管理器）
		2. dataSource（数据源）
8. databaseProvider（数据库厂商标识
9. mappers（映射器）
## 配置文件完成增删改查
1. 编写接口方法
	![[Pasted image 20250703222012.png]]
2. 编写sql
3. 执行方法
### 查询
1. **查询所有数据**（在mapper.xml文件中）
	1. 数据库表的字段名称   和  实体类的属性名称     不一样，则不能自动封装数据  
	  * 起别名：让别名和实体类的属性名一样（每次查询都要定义，不方便）  
	    * 解决：sql片段（不灵活  
	  * **resultMap**    
		* 1.定义< resultMap>标签  
		- 2.在< select>标签中，使用resultMap属性替换resultType属性
	```xml
	<?xml version="1.0" encoding="UTF-8" ?>  
	<!DOCTYPE mapper  
	  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"  
	  "https://mybatis.org/dtd/mybatis-3-mapper.dtd">  
	  
	<mapper namespace="com.zytoame.mapper.BrandMapper">
	
	<!--id:唯一标识  	type：映射类型，支持别名 	-->
	<resultMap id="brandResultMap" type="brand">
		<result column="brand_name" property="brandName" />  
		<result column="company_name" property="companyName" />  
	</resultMap>  
	  
	<select id="selectAll" resultMap="brandResultMap">  
	  select *  
	  from tb_brand;  
	</select>
	
	</mapper >
	```
2. **查看详情**
	1. 参数占位符
		1. ==#{}==：会将其替换为？，为了==防止sql注入==
			1. 使用时机：参数传递时
			2. #{}表示一个占位符号 相当于 `jdbc`中的 **?** 符号  
			#{}实现的是向prepareStatement中的预处理语句中设置参数值，sql语句中#{}表示一个占位符即?
			3. #{}将传入的数据都当成一个字符串，会对自动传入的数据加一个双引号。如：`select * from user where id= #{user_id}`，如果传入的值是11,那么解析成sql时的值为`where id="11"` ，
			4. 如果sql语句中只有`一个参数`,此时参数名称可以`随意定义`  
			如果sql语句有**多**个参数,此时参数名称应该是与当前表关联[ 实体类的属性名 ]或则[ Map集合关键字 ]，**不能随便写，必须对应**！如下图
			![[Pasted image 20250704111500.png]]
		2. ==${}==：拼sql，会存在sql注入问题
			1. 使用时机：表名或者列名不固定的情况下
			2. $ {}将传入的数据直接显示生成在sql中。如：`select * from user where id= $ {user_id}`，如果传入的值是11,那么解析成sql时的值为`where id=11`
			3. `$ {value}`中`value`值有限制只能写对应的value值不能随便写，因为`${}`不会自动进行jdbc类型转换
			4. 简单来说,在`JDBC`不支持使用占位符的地方,都可以使用`${}`
	2. sql注入
		1. 在前台有两个输入框，一个用户名，一个密码，**后台读取前台传入的两个参数，拼成一段SQL，**
			例如： select count(1) from tab where usesr=userinput and pass = passinput,把这段SQL连接数据后，看这个用户名/密码是否存在，如果存在的话，就可以登陆成功了，如果不存在，就报一个登陆失败的错误。  
		2. 但是有这样的情况，**这段SQL是根据用户输入拼出来**，如果用户故意输入可以让后台解析失败的字符串，这就是SQL注入，
			例如，用户在输入密码的时候，输入 ‘’’’ ’ or 1=1’’, 这样，后台的程序在解析的时候，拼成的SQL语句，可能是这样的： select count(1) from tab where user=userinput and pass=’’ or 1=1; 看这条语句，可以知道，在解析之后，用户没有输入密码，加了一个恒等的条件 1=1，这样，这段SQL执行的时候，返回的 count值肯定大于1的，如果程序的逻辑没加过多的判断，这样就能够使用用户名 userinput登陆，而不需要密码。  
		3. **防止SQL注入，首先要对密码输入中的单引号进行过滤，再在后面加其它的逻辑判断，或者不用这样的动态SQL拼**
	3. 特殊字符处理
		1. 转义字符
		2. CDATA区：<![ CDATA[  符号  ] ]> :快捷键：CD提示
3. 条件查询
	1. 多条件查询
		1. 编写接口方法：mapper接口
		2. 参数：所有查询条件
			1. 参数接受
				1. 散装参数：多个参数，需使用@Param（"SQL中的参数占位符名称"）
				2. 对象参数：保证SQL中的参数名和 实体类属性名 对应上
				3. map集合参数：保证SQL中的参数名和 map集合的键的名称 对应上
		3. 结果：List< Brand>
		4. mapper.java![[Pasted image 20250710211150.png]]
		5. 编写SQL语句：SQL映射文件
		6.  mapper.xml![[Pasted image 20250710211237.png]]
		7. 执行方法，测试
		8. test.java
			1. ![[Pasted image 20250710211401.png]]
	2. 动态条件查询xml
		1. if
		2. choose（when，otherwise）
			< choose>  类似于Switch
				< when test="">  类似于case
				< /when>
				< otherwise>  类似于default
				< /otherwise >
			< /choose>
		3. < where> 替换where
### 添加
1. 编写接口方法：*Mapper接口.java*：void add(Brand brand);
	1. 参数：除了id之外的所有数据
	2. 结果：void
2. 编写SQL语句：*SQL映射文件.xml*
	< insert id="add">  
	    insert into tb_brand (brand_name, company_name, ordered, description, status)  
	    values (#{brandName},#{companyName},#{ordered},#{description},#{status});  
	< /insert>
3. 执行方法，测试
	MyBatis事务：
		*openSession（）*：默认开启事务，进行增删改操作后需要使用sqlSession.commit();手动提交事务
		*openSession(true)*：可以设置为自动提交事务（关闭事务）；
- 主键返回：< insert useGeneratedKeys="true" keyProperty="id">
### 修改
1. 编写接口方法：Mapper接口.java：void update(Brand brand);
	1. 参数：所有数据
	2. 结果：void
2. 编写SQL语句：SQL映射文件.xml
	 < update id="update">  
	    update tb_brand
	    set brand_name = #{brandName}, company_name = #{companyName}, ordered = #{ordered}, description = #{description}, status = #{status})  
	    where id = #{id}；
	< /update>
	修改动态字段：
	< set>  
	    < if test="brandName != null and brandName != ''">  
	        brand_name = #{brandName},  
	    < /if>  
	< /set>
3. 执行方法，测试
### 删除
1. 编写接口方法:Mapper接口 ：
	1. 删除一个：void deleteByld(int id);
		参数:id
		结果:void
	2. 删除多个：void deleteBylds(@Param("ids") int[ ] ids);
		1. mybatis会将数组参数,封装为一个Map集合。
		* 默认: **array** = 数组  :
			*  .java :  void deleteBylds(int[ ] ids);
			*  .xml :  < forreach collection = "**array**" item="id" separator="," open="(" close=")">
		* 使用@Param注解改变map集合的默认key的名称
		参数:id数组
		结果:void
2. 编写SQL语句:SQL映射文件resources.com.zytoame.mapper.xxx.xml
	1. 删除一个
		< delete id="deleteBylds">
		delete from tb_brand where id = #{id}
		< /delete>
	2. 删除多个
		< delete id="deleteBylds">
		delete from tb_brand where id in (?,?,?)  // ？的个数随ids数组里的个数变化
		< /delete>
		
		< delete id="deleteBylds">
		delete from tb_brand 
		where id 
		in
			< forreach collection = "**ids**" item="id" separator="," open="(" close=")">  
			    #{id}  
			< /foreach>
		;
		< /delete>
3. 执行方法,测试
### 参数传递
MyBatis接口方法中可以接收各种各样的参数,MyBatis底层对于这些参数进行不同的封装处理方式
1. 单个参数:
	1. P0J0类型:直接使用,属性名 和 参数占位符名称 一致
	2. Map集合:直接使用,键名 和 参数占位符名称 一致
	3. Collection:封装为Map集合,可以使用@Param注解,替换Map集合中默认的arg键名
	map.put("arg0",collection集合);
	map.put("collection",collection集合〕;
	4. List:封装为Map集合,可以使用@Param注解,替换Map集合中默认的arg键名
	map.put("arg0",list集合〕;
	map.put("collection",list集合);
	map.put("List",List集合);
	5. Array:封装为Map集合,可以使用@Param注解,替换Map集合中默认的arg键名
	map.put("arg0",数组);
	map.put("array",数组);
	6. 其他类型:直接使用
2. 多个参数: 封装为Map集合,可以使用@Param注解,替换Map集合中默认的arg键名
	map.put("arg0",参数值1)
	map.put("param1",参数值1)
	map.put("param2",参数值2)
	map.put("agr1",参数值2〕
	-- @Param("username")
	map.put("username",参数值1)
	map.put("param1",参数值1)
	map.put("param2",参数值2)
	map.put("agr1",参数值2）
## 注解完成增删改查（完成简单功能）