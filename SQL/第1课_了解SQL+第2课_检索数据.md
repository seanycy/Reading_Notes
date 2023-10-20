# 1、了解SQL
## 1.了解数据库
1. 数据库
	1. 数据库（Database）：保存有组织的数据的容器
	2. 数据库软件应称作数据库管理系统（BDMS）。数据库是通过DBMS创建和操纵的容器
2. 表
	1. 表（Table）：结构化文件，可用来存储某种特定类型的数据
	2. 表名：使表名成为唯一的实际上使数据库名和表名的组合。同一数据库不能有两次使用相同的表名，但不同数据库可以
	3. 模式：关于数据库和表的布局及特性的信息；可以用来描述数据库中特定的表，也可以用来描述整个数据库
	4. 注意：存储在表中的数据是同一中类型的数据或清单
3. 列和数据类型
	1. 列（Column）：表由列组成，是表中的一个字段。所有表都是由一个或多个列组成
	2. 数据类型（DataType)：定义了列可以存储什么类型的数据，限制（或允许）该列中的数据
4. 行
	1. 行（Row）：表中数据按行存储，即表中的一个记录
	2. 数据库记录（Record）和行意义相同，技术上说，行是对的
5. 主键
	1. 主键（Primary Key）：一列或几列，其值可以唯一标识表中的一行或几行
	2. 作为主键的条件（表中任意列可作主键）：
		1. 任意两行不具有相同的主键值
		2. 每一行都必须具有一个主键值（主键列不允许空值NULL）
		3. 主键列中的值不允许修改或更行
		4. 主键值不能重用（如果某行从表中删除，它的主键不能赋给以后的新行

## 2.SQL——Structured Query Language（结构化查询语言）
Mysql—>MySQLWorkbench
Microsoft SQL Server Express—>SQL Server Management Studio

# 2.检索数据

## 2.1 SELECT语句
SELECT：从一个或多个表中检索信息
- 注意：关键字（KeyWord）作为SQL的保留字是不能用作表或者列的名字的
- 使用SELECT：想找什么，从哪里找

## 2.2 检索单个列
用SELECT从Products中检索一个名叫prod_name的列：
```sql
SELECT prod_name
FROM Products;
```
- 上句SELECT返回表中所有行
- 多条SQL语句以“;“分隔
- SQL不区分大小写，但表名、列名和值根据DBMS不同而不同
- 未排序数据：若查询时未明确是排序查询，啧返回数据无特定顺序

上述例句也有以下两种种写法：
第一种：
```sql
SELECT prod_name FROM Products;
```
第二种：
```sql
SELECT prod_name
FROM
Products;
```

## 2.3 检索多个列
从一个表中检索多个列，需要在SELECT后面给出多个列名，列名之间以逗号隔开。
**- 注意：最后一个列名不加逗号**
```sql
SELECT prod_id,prod_name,pro_price
FROM Products;
```

## 2.4 检索所有列
在实际列名的位置使用星号（* ）通配符可以实现：
```sql
SELECT *
FROM Products;
```
给定通配符返回表中所有列，列顺序由表中物理顺序出现
**- 注意：
	- 检索表中所有列通常会降低检索速度和应用程序性能
	- 通配符检索可以检索出名字未知的列**
## 2.5 检索不同值
```sql
SELECT DISTINCT vend_id
FROM Products;
```
SELECT DISTINCT vend_id 告诉DBMS值返回不同的值（此值具有唯一性）的vend_id行
**- 注意：DISTINCT要放在列名前面*，其作用于所有的列，不仅仅是跟在其后的那一列*

## 2.6 限制结果
在MySQL中，限制返回结果需要使用LIMIT
```sql
SELECT prod_name
FROM Products
LIMIT 5 OFFSET 5;
```
LIMIT 5 OFFSET 5指示MySQL返回从第五行起的五行数据。
LIMIT后面的5时检索的行数，OFFSET后面的5时指从哪里开始
也就是说，LIMIT指定返回的行数，后接OFFSET指定从哪里开始
**- 第一个被检索的行是第0行，不是第1行**

上述写法与下面写法等价：
```sql
LIMIT 5,5；
```
**- 注意：逗号前面的值对应OFFSET，逗号后面的值对应OFFSET，与全写相反**

## 2.7 注释
```sql
--这是一条注释，使用两个连字符

#这是一条注释，在一行开始使用，这一整行都作为注释，部分DBMS不支持
SELECT DISTINCT vend_id
FROM Products;

/*
多行注释
*/
```

## 2.8 作业
1. 编写 SQL 语句，从 Customers 表中检索所有的 ID（cust_id）
```sql
SELECT cust_id FROM Customers;
```

2. OrderItems 表包含了所有已订购的产品（有些已被订购多次）。编写SQL 语句，检索并列出已订购产品（prod_id）的清单（不用列每个订单，只列出不同产品的清单）。提示：最终应该显示 7 行。
```sql
SELECT DISTINCT prod_id FROM Orderitems LIMIT 7;
```

1. 编写 SQL语句，检索 Customers 表中所有的列，再编写另外的 SELECT语句，仅检索顾客的 ID。使用注释，注释掉一条 SELECT 语句，以便运行另一条 SELECT 语句。（当然，要测试这两个语句。）
```sql
SELECT * FROM Customers;
SELECT cust_id FROM Cutomers;
```