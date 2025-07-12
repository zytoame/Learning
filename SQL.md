### DLL操作表
CRUD
1. 创建表：create table 表名(列名，数据类型)
	eg：create table tb_user(id int, username varchar(20), password carchar(32));
2. 查看表：show tables；     desc 表名称；
3. 删除表：DROP TABLE 表名；  DROP TABLE IF EXISTS 表名；
4. 修改表
	1. 修改表名：ALTER TABLE 表名 RENAME TO 表名；
	2. 添加一列：ALTER TABLE 表名 ADD 列名 数据类型；
	3. 修改数据类型：ALTER TABLE 表名 MODIFY 列名 新数据类型；
	4. 修改列名和数据类型：ALTER TABLE 表名 CHANGE 列名 新列名 新数据类型
	5. 删除列：ALTER TABLE 表名 DROP 列名；
### DML
1. 添加数据
	1. 给指定列：INSERT INTO 表名（列名1，列名2，···） VALUES（值1，值2，···）
	2. 批量添加：INSERT INTO 表名（列名1，列名2，···） VALUES（值1，值2，···），（值1，值2，···），（值1，值2，···）···；
2. 修改表数据：UPDATE 表名 SET 列名1 = 值1 ，列名2 = 值2，WHERE 条件；不加条件则表中数据全部修改
3. 删除数据：DELDETE FROM 表名 WHERE 条件
### DQL
1. SELECT  字段列表
	FROM  表名列表
	WHERE  条件列表
	GROUP BY 分组列表
	HAVING  分组后条件
	ORDER BY  排序字段
	LIMIT  分页限定
2. 基础查询
	1. 查询列数据：SELECT 列名 FROM 表名
	2. 去除重复记录：SELECT DISTINCT 列名 FROM 表名
	3. 起别名：AS或者空格代替：列名 别名；列名 AS 别名
3. 条件查询：SELECT 字段列表 FROM 表名 WHERE 条件列表
	1. 模糊查询：like ‘条件’     _ 任意单字符，%任意多字符
		1. 查询名字中包含‘德’的学员信息：SELECT * FROM stu WHERE name LIKE ‘%德%’；
4. 分组查询：SELECT  字段列表  FROM  表名  WHERE 分组前条件限定  GROUP BY  分组字段名  HAVING 分组后条件过滤
    **`GROUP BY` 的作用**：告诉数据库"按哪些列分组计算"。
5. 排序查询：SELECT  字段列表  FROM  表名  ORDER BY  条件列表     升序：ASC；降序：DESC
6. 聚合函数：SELECT 聚合函数（列名） FROM 表名
	1. null不参与所有聚合函数计算
	2. 计数count，COUNT(column_name)统计非空值的数量，count（* ）统计所有行数
	3. 求平均：avg（列名）
7. 分页查询：SELECT  字段列表  FROM  表名  LIMIT  起始索引，查询条目数
	1. 起始索引：（当前页码-1） * 每页显示的条数
### DCL
### 约束
1. 非空约束：NOT NULL
2. 唯一：UNIQUE
3. 主键：PRIMARY KEY
4. 检查：CHECK （MySQL不支持）
5. 默认：DEFAULT
6. 外键：FOREIGN KEY
7. 自动增长：auto_increment:当列是数字类型且唯一
### 多表查询
1. 子查询
	1. 单行单列：SELECT  字段列表  FROM  表名  WHERE  字段名 = （子查询）；%% 作为条件值，使用条件判断：=  ！=  >  <  %%
	2. 多行单列：SELECT  字段列表  FROM  表名  WHERE  字段名 in （子查询）；
	3. 多行多列：SELECT  字段列表  FROM  （子查询）  WHERE  条件；%%作为虚拟表%%
### 事务ACID
1. 开启：START TRANSACTION; 或者 BEGIN;
2. 提交事务：COMMIT
3. 回滚事务：ROLLBACK
4. 四大特征
	1. 原子性A：同时成功或者失败
	2. 一致性C：事务完成时，所有数据保持一致状态
	3. 隔离性I：多个事务之间，操作可见性
	4. 持久性D：事务一旦提交或回滚，对数据库中的数据改变是永久的
### lc整理
- 计算字符串中字符数： CHAR_LENGTH(str)
- 时间计算函数
	- `TIMESTAMPDIFF`可以计算相差天数、小时、分钟和秒，相比于`datediff`函数要灵活很多。格式是时间小的前，时间大的放在后面。
		- WHERE TIMESTAMPDIFF(DAY, w2.recordDate, w1.recordDate) = 1
	- `adddate()`函数:将指定的时间间隔添加到日期值date是表示日期的值，它可以是 `String`、`DATE（YEAR、MONTH 和 DAY）`、`DATETIME（HOURS、MINUTES 或 SECONDS）`或 `TIMESTAMP` 类型。
		- **ADDDATE( date , INTERVAL value addunit )**  **ADDDATE( date , days )**
			- **date**：必填。要修改的日期
			- **days**: 必填。要添加到日期的天数
			- **value**：必填。要添加的时间/日期间隔的值。允许正值和负值
			- **addunit**：必填。要添加的间隔类型。可以是以下值之一：`MICROSECON` 、 `DSECOND`、`MINUTE`、`HOUR`、`DAY`、`WEEK`、`MONTH`、`QUARTER`、`YEAR`、 `SECOND_MICROSECOND`、`YEAR_MONTH`、`MINUTE_MICROSECOND`、`MINUTE_SECOND` 、`HOUR_MICROSECOND`、`HOUR_SECOND` 、`HOUR_MINUTE`、`DAY_MICROSECOND`、`DAY_SECOND`、`DAY_MINUTE`、`DAY_HOUR`
			- a.recorddate = adddate(b.recorddate,INTERVAL 1 day)
- `round(avg(t2.timestamp - t1.timestamp), 3)` 是用于计算时间差平均值并四舍五入的SQL函数组合，具体含义如下：
	1. `t2.timestamp - t1.timestamp`：计算两个时间戳（t2和t1）之间的时间差
	2. `avg(...)`：计算所有这些时间差的平均值
	3. `round(..., 3)`：将平均值四舍五入到3位小数
	整体意思是：计算t2和t1时间戳差的平均值，并将结果保留3位小数。
- cross join
- group by：分组计算查询。按group by中的组别进行计算。
- order by
- ifnull(条件，0)：如果条件成立则返回条件值，否则返回0。作用：不显示null，将null值转为0
- ` round(ifnull(avg(c.action = 'confirmed'),0),2)`
	1. `c.action = 'confirmed'`是一个布尔表达式：当action 值为 'confirmed' 时，返回1，否则返回0
	2. `AVG()` 函数会对这些 1 和 0 计算平均值
	3. 实际上计算的是 **'confirmed' 记录所占的比例**
	4. 等价写法：avg(c.action = 'confirmed')
		1. COUNT(CASE WHEN c.action = 'confirmed' THEN 1 END) * 1.0 / COUNT(* )
		2. sum(if(action = 'confirmed',1,0))/count(action)
	5. ifnull(···，0)： 如果某个用户没有任何确认记录（即 `AVG` 返回 `NULL`），则返回0作为默认值。
	6. round( ··· ,2)：保留两位小数