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


### 执行一条 SQL 查询语句，期间发生了什么？
1. 连接器：建立连接，管理连接、校验用户身份；
2. 查询缓存：查询语句如果命中查询缓存则直接返回，否则继续往下执行。MySQL 8.0 已删除该模块；
3. 解析 SQL，通过解析器对 SQL 查询语句进行词法分析、语法分析，然后构建语法树，方便后续模块读取表名、字段、语句类型；
4. 执行 SQL：执行 SQL 共有三个阶段：
	1. 预处理阶段：检查表或字段是否存在；将 select * 中的 * 符号扩展为表上的所有列。
	2. 优化阶段：基于查询成本的考虑， 选择查询成本最小的执行计划；
	3. 执行阶段：根据执行计划执行 SQL 查询语句，从存储引擎读取记录，返回给客户端；
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250816133108319.png)



联合索引的最左匹配原则，在遇到范围查询（如 >、<）的时候，就会停止匹配，也就是范围查询的字段可以用到联合索引，但是在范围查询字段的后面的字段无法用到联合索引。注意，对于 >=、<=、BETWEEN、like 前缀匹配的范围查询，并不会停止匹配，
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250816114122454.png)

索引的缺点：
需要占用物理空间，数量越大，占用空间越大； 
创建索引和维护索引要耗费时间，这种时间随着数据量的增加而增大； 
会降低表的增删改的效率，因为每次增删改索引，B+ 树为了维护索引有序性，都需要进行动态维护。

### 优化索引的方法

#### 前缀索引优化

前缀索引：
- 只索引字符串列的前N个字符
    
- 而不是索引整个字符串值
    
- 通过`INDEX(column_name(N))`语法创建（N表示前缀长度）

优点：
- 减少索引存储空间：索引体积更小
    
- 加快索引扫描速度：更小的索引意味着更高的缓存命中率
    
- 支持无法完整索引的大字段：如TEXT/BLOB类型通常不能整个被索引

缺点和注意事项
- 不适合后缀查询(`LIKE '%suffix'`)
    
- 可能增加重复键值风险
    
- 排序操作可能无法使用前缀索引
	
- InnoDB引擎前缀索引最长767字节(utf8mb4约191字符)
    
- 主键不能使用前缀索引
    
- 唯一索引使用前缀索引时要确保前缀的唯一性
	
- order by 不能使用前缀索引
	
- 不能把前缀索引用作覆盖索引

```sql
-- MySQL中创建前缀索引
ALTER TABLE users ADD INDEX idx_name (name(5));  -- 只索引name前5个字符

-- 创建表时指定
CREATE TABLE products (
    product_code VARCHAR(100),
    INDEX idx_code (product_code(10))
);
```
#### 覆盖索引优化

**覆盖索引**（Covering Index）是指：查询可以**完全通过索引**获取所需数据，而**无需访问表数据行**（避免回表操作）。
- 一个索引包含了查询需要的所有字段
    
- 执行查询时只需访问索引，不需回表查数据页
    
- 在EXPLAIN结果中显示"Using index"

优点：
1. **减少I/O操作**：只读取索引数据，不读数据页
    
2. **减少CPU消耗**：避免了解析完整行数据
    
3. **利用索引顺序**：索引通常比表数据更紧凑有序
    
4. **缓冲池效率**：更小的索引更容易被缓存在内存中

查询要成为覆盖查询必须满足：
- SELECT列表中的列都包含在索引中
    
- WHERE条件使用的列是索引的前导列
    
- 任何需要的排序列也在索引中

假设一个表有100万行，索引和数据分离存储：

| 查询类型 | 需要访问  | 估计I/O次数   | 执行时间     |
| ---- | ----- | --------- | -------- |
| 覆盖查询 | 仅索引   | 1-5次      | 1-5ms    |
| 普通查询 | 索引+数据 | 100-1000次 | 10-100ms |

限制与注意事项
1. 索引维护成本：覆盖索引包含更多列，会增大索引体积
    
2. 更新代价：表数据变更时需要维护更多索引数据
    
3. 存储空间：额外的索引需要更多磁盘空间
    
4. 不是所有查询都能转化为覆盖查询

```sql
-- 表结构
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(50),
    age INT,
    INDEX idx_username_age (username, age)
);

-- 覆盖查询示例1（使用复合索引）
EXPLAIN SELECT username, age FROM users WHERE username = 'john';
-- 结果会显示"Using index"

-- 覆盖查询示例2（使用主键）
EXPLAIN SELECT id FROM users WHERE id > 100;
-- 主键索引天然是覆盖索引

-- 非覆盖查询示例
EXPLAIN SELECT username, age, id FROM users WHERE username = 'john';
-- 虽然用了索引，但需要回表取id值
```

#### 主键索引最好是自增的

自增主键按顺序插入，为追加操作，不需要移动数据
非自增主键可能会发生页分裂，造成大量内存碎片，导致索引结构不紧凑，影响查询效率

主键字段越小，二级索引的叶子结点越小，所占空间越小

- 索引最好设置NOT NULL
	- 有NULL值会导致优化器在做索引选择的时候更加复杂，难以优化
	- NULL是没有意义的值但是会占用物理空间，带来存储空间的问题

常见扫描类型的执行效率从低到高的顺序为： 
All（全表扫描）； 
index（全索引扫描）； 
range（索引范围扫描）； 
ref（非唯一索引扫描）； 
eq_ref（唯一索引扫描）； 
const（结果只有一条的主键或唯一索引扫描）。

#### 防止索引失效

发生索引失效的情况
当我们使用左或者左右模糊匹配的时候，也就是 like %xx 或者 like %xx%这两种方式都会造成索引失效； 
当我们在查询条件中对索引列做了计算、函数、类型转换操作，这些情况下都会造成索引失效； 
联合索引要能正确使用需要遵循最左匹配原则，也就是按照最左优先的方式进行索引的匹配，否则就会导致索引失效。 
在 WHERE 子句中，如果在 OR 前的条件列是索引列，而在 OR 后的条件列不是索引列，那么索引会失效。

![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250816131046078.png)


### 索引下推

**索引下推**（Index Condition Pushdown）是指：
	
- 将WHERE条件中**索引相关部分**下推到存储引擎层执行
    
- 存储引擎在读取索引时就进行条件过滤
    
- 减少传给服务器层的数据量
    
- 在EXPLAIN中显示"Using index condition"

 没有ICP的传统流程
	
1. 存储引擎读取索引元组
    
2. 通过索引定位表记录（回表）
    
3. 服务器层对返回的数据应用WHERE条件过滤
    

 启用ICP的流程
	
1. 存储引擎读取索引元组
    
2. **在存储引擎层**评估WHERE条件中可下推的部分
    
3. 只对满足条件的索引项执行回表操作
    
4. 服务器层处理最终结果

ICP优化适用于以下场景：

- 需要访问表记录的查询（非覆盖查询）
    
- WHERE条件包含索引列和非索引列
    
- 特别是复合索引的非前导列条件
    
- InnoDB和MyISAM引擎支持

优势：
1. **减少回表次数**：只对真正符合条件的记录回表
    
2. **降低I/O压力**：减少了从存储引擎到服务器的数据传输
    
3. **提高缓存效率**：更少的数据被加载到内存中

限制条件
1. 只适用于二级索引（非聚簇索引）
    
2. 不适用于主键/聚簇索引查询
    
3. 虚拟列上的二级索引不支持ICP
    
4. 子查询、存储函数条件不能下推
    
5. 引用子表的条件不能下推

```sql
-- 表结构
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT,
    dept VARCHAR(50),
    INDEX idx_name_age (name, age)
);

-- 查询示例
SELECT * FROM employees 
WHERE name LIKE '张%' AND age > 25;

-- 没有ICP时：
-- 1. 先通过索引找到所有name以'张'开头的记录
-- 2. 对所有找到的记录回表取完整数据
-- 3. 在服务器层过滤age>25的记录

-- 启用ICP时：
-- 1. 通过索引找到name以'张'开头的记录
-- 2. 在存储引擎层直接检查这些记录的age>25条件
-- 3. 只对满足两个条件的记录回表
```


「变长字段长度列表」中的信息之所以要逆序存放，是因为这样可以使得位置靠前的记录的真实数据和数据对应的字段长度信息可以同时在一个+cpu+cache+line+中，这样就可以提高+cpu+cache+的命中率。

### MySQL的NULL值是怎么存放的?

MySQL的Compact行格式中会用「NULL值列表」来标记值为NULL的列,NULL值并不会存储在行格式
中的真实数据部分。

NULL 列表会占用1字节空间,当表中所有字段都定义成NOT NULL,行格式中就不会有NULL值列表,
这样可节省1字节的空间。

### MySQL怎么知道 varchar(n)实际占用数据的大小?

MySQL的Compact行格式中会用「变长字段长度列表」存储变长字段实际占用的数据大小。
<=255: 1；>255：2

### varchar(n)中n最大取值为多少?

一行记录最大能存储65535字节的数据,但是这个是包含「变长字段字节数列表所占用的字节数」和
「NULL值列表所占用的字节数」。所以,我们在算varchar(n)中n最大值时,需要减去这两个列表所占用的字节数。

如果一张表只有一个varchar(n)字段,且允许为NULL,字符集为ascii。varchar(n)中n最大取值为
65532。

计算公式:65535-变长字段字节数列表所占用的字节数-NULL值列表所占用的字节数=65535-2-1=
65532。

如果有多个字段的话,要保证所有字段的长度+变长字段字节数列表所占用的字节数+NULL值列表所占用的字节数 <= 65535。

### 行溢出后,MySQL是怎么处理的?

如果一个数据页存不了一条记录,InnoDB存储引擎会自动将溢出的数据存放到「溢出页」中。

Compact 行格式针对行溢出的处理是这样的:当发生行溢出时,在记录的真实数据处只会保存该列的一部分数据,而把剩余的数据放在「溢出页」中,然后真实数据处用20字节存储指向溢出页的地址,从而可
以找到剩余数据所在的页。

compressed和dynamic采取不同的方法，在记录的真实数据处只会用20字节保存溢出页的地址，把全部数据都放在溢出页中，

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