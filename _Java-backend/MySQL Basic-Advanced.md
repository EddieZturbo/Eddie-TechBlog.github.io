---
title: "MySQL Basic-Advanced"
collection: Java-backend
permalink: /Java-backend/MySQL Basic-Advanced
excerpt: 'MySQL Basic-Advanced'
date: 2023-02-05
venue: 'February 5'
---
# Mysql Basic

![image-20220926085405282](/images/image-20220926085405282.png)

### MySQL★

**连接到MySQL数据库的操作**

1.服务启动--net start mysql(服务名) 服务关闭--net stop mysql(服务名)

2.登录（连接）--mysql -h 主机名 -P 端口 -u 用户名 -p密码 退出（断连）--exit

-p后不能出现空格

-p后没写密码的，回车会要求输入密码

如果没有写-h 主机，默认就是本机

如果没写-P 端口，默认就是3306

在实际工作中 端口一般会修改



![image-20220825205341677](/images/image-20220825205341677.png)

**SQL 分类 SQL语言在功能上主要分为如下3大类：** 

**DDL（Data Definition Languages、数据定义语言）**，这些语句定义了不同的数据库、表、视图、索 引等数据库对象，还可以用来创建、删除、修改数据库和数据表的结构。 

主要的语句关键字包括 **CREATE** 、 **DROP** 、 **ALTER** 等。 

**DML（Data Manipulation Language、数据操作语言）**，用于添加、删除、更新和查询数据库记 录，并检查数据完整性。 

主要的语句关键字包括 **INSERT** 、 **DELETE** 、 **UPDATE** 、 **SELECT** 等。 **SELECT**是SQL语言的基础，最为重要。 

**DCL（Data Control Language、数据控制语言）**，用于定义数据库、表、字段、用户的访问权限和 安全级别。 

主要的语句关键字包括 **GRANT** 、 **REVOKE** 、 **COMMIT** 、 **ROLLBACK** 、 **SAVEPOINT** 等

![image-20220901093814041](/images/image-20220901093814041.png)

**SQL语言的规则与规范**

![image-20220901093857419](/images/image-20220901093857419.png)

**数据导入指令**

![image-20220901093930942](/images/image-20220901093930942.png)

#### 数据库

```sql
#数据库操作
#create database db03 [IF NOT EXISTS] character set utf8 collate utf8_bin;
-- 创建一个数据空并使用 CHARACTER SER 指定字符集 同时使用 COLLATE 指定校验 
-- 其中[IF NOT EXISTS](开发中推荐使用)表示如果库已经存在就不创建 不存在就创建
#创建一个名为Eddie_db02的数据库
CREATE DATABASE Eddie_db02;
#删除数据库
DROP DATABASE Eddie_db02;
#创建一个使用utf8字符集的Eddie_db03数据库
CREATE DATABASE Eddie_db03 CHARACTER SET utf8;
#删除数据库
DROP DATABASE Eddie_db03;
#创建一个使用utf_8字符集，并带校对规则的Eddie_db04数据库
CREATE DATABASE Eddie_db04 CHARACTER SET utf8 COLLATE utf8_bin;
#删除数据库
DROP DATABASE Eddie_db04
#以下是表示查询sql语句；SELECT查询 *代表所有字段 FROM从哪个表中查询 WHRER表示从哪个字段查 NAME = 'Ivring' 表示查询名字为Ivring的
SELECT * FROM user1 WHERE NAME = 'Ivring';

#查看当前正在使用的库（当前在哪个库下）
SELECT DATABASE();
#查看有哪些数据库
SHOW DATABASES
#显示数据库的创建语句
SHOW CREATE DATABASE eddie_db03;
#删除数据库
DROP DATABASE eddie_db02;
#在创建数据库或者表的时候；为了规避关键字可以使用反引`CREATE`
CREATE DATABASE Eddie_db05 CHARACTER SET utf8 COLLATE utf8_bin
DROP DATABASE eddie_db05
SELECT * FROM user1
SELECT * FROM user1 WHERE NAME = 'Ivring';
CREATE DATABASE eddie_db05 CHARACTER SET utf8 COLLATE utf8_bin
CREATE TABLE 
```



##### 创建

```sql
#create database db03 [IF NOT EXISTS] character set utf8 collate utf8_bin;
-- 创建一个数据空并使用 CHARACTER SET 指定字符集 同时使用 COLLATE 指定校验 
-- （如果不指定默认字符集为utf-8 默认校对规则为 utf-8)_general_ci为不区分大小写）
-- 其中[IF NOT EXISTS](开发中推荐使用)表示如果库已经存在就不创建 不存在就创建
#在创建数据库或者表的时候；为了规避关键字可以使用反引`CREATE`
```

##### 查看，删除数据库

```sql
#查看有哪些数据库
SHOW DATABASES
#显示数据库的创建语句
SHOW CREATE DATABASE eddie_db03;

#删除数据库
DROP DATABASE eddie_db02;
-- For instance:
mysql> drop database db02;
Query OK, 4 rows affected (0.03 sec)

```

##### 备份，恢复数据库

```sql
#备份数据库:（注意要在DOS执行）命令行-*-这里备份数据库即把创建数据库的所有操作命令进行备份-->恢复数据库时即直接将所有操作命令运行一次即可
mysqldump -u root -p -B db02(数据库的名) >e:\\bal.sql(指定要备份到的磁盘路径 以及文件名.sql)
-- C:\WINDOWS\system32>mysqldump -u root -p -B db02 >e:\\bak2.sql
-- Enter password: ****
#恢复数据库:（注意要在Mysql命令执行）-*-这里备份数据库即把创建数据库的所有操作命令进行备份-->恢复数据库时即直接将所有操作命令运行一次即可
mysql> source e:\\bak2.sql
```



#### 表

##### 备份，恢复表

```sql
-- 备份表:（注意要在DOS执行）命令行-*-这里备份数据库的表即把创建数据库的表的所有操作命令进行备份-->恢复数据库时即直接将所有操作命令运行一次即可
mysqldump -u root -p db02(数据库的名) (表名)>e://backaccount.sql(指定要备份到的磁盘路径 以及文件名.sql)
-- C:\WINDOWS\system32>mysqldump -u root -p db01 account >e://backaccount.sql
-- Enter password: ****
#恢复表:（注意要在Mysql命令执行）-*-这里备份数据库的表即把创建数据库的表的所有操作命令进行备份-->恢复数据库时即直接将所有操作命令运行一次即可
mysql> source e://backaccount.sql;
```



```sql
CREATE TABLE [IF NOT EXISTS] 表名(
    字段1, 数据类型 [约束条件] [默认值], 字段2, 数据类型 [约束条件] [默认值], 字段3, 数据类型 [约束条件] [默认值], 
    …… 
    [表约束条件] );
    
    mysql> show tables from db02;-- 查看指定库中所有的表
+----------------+
| Tables_in_db02 |
+----------------+
| emp1           |
| employee1      |
| employee2      |
| employee3      |
+----------------+
4 rows in set (0.00 sec)

mysql> select * from emp1;-- 查看指定表中的完整数据
+------+------+------+------+
| id   | a    | b    | c    |
+------+------+------+------+
|    1 |  100 |  200 |  300 |
|    2 | 1000 | 2000 | 3000 |
+------+------+------+------+
2 rows in set (0.00 sec)

mysql> show create table emp1;-- 查看指定表的创建结构
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                               |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| emp1  | CREATE TABLE `emp1` (
  `id` int DEFAULT NULL,
  `a` int DEFAULT NULL,
  `b` int DEFAULT NULL,
  `c` int GENERATED ALWAYS AS ((`a` + `b`)) VIRTUAL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)

mysql> describe emp1;-- describe 查看表的详情描述
+-------+------+------+-----+---------+-------------------+
| Field | Type | Null | Key | Default | Extra             |
+-------+------+------+-----+---------+-------------------+
| id    | int  | YES  |     | NULL    |                   |
| a     | int  | YES  |     | NULL    |                   |
| b     | int  | YES  |     | NULL    |                   |
| c     | int  | YES  |     | NULL    | VIRTUAL GENERATED |
+-------+------+------+-----+---------+-------------------+
4 rows in set (0.00 sec)
```



##### 创建

```sql
#创建表指明表的字段
CREATE TABLE student4(
    id int,`name` VARCHAR(255),`password` VARCHAR(25),birthday DATE)
    CHARACTER SET utf8 COLLATE UTF8_bin ENGINE INNODB;
-- 使用CHARACTER SET 指明字符集 否则默认使用和表一样 使用COLLATE 指明校对规则 否则使用和表一样 使用ENGINE指明存储引擎
CREATE TABLE [IF NOT EXISTS] 表名(
    字段1, 数据类型 [约束条件] [默认值], 字段2, 数据类型 [约束条件] [默认值], 字段3, 数据类型 [约束条件] [默认值], 
    …… 
    [表约束条件] );
#创建表可以将另一个表的数据引用过来成为创建的新表的数据
-- 使用 AS subquery 选项，将创建表和插入数据结合起来
CREATE TABLE emp1 AS SELECT * FROM employees;-- 可以完全将一个表的数据作为新表的数据类似于复制了一份表-->也可以在命令中追加条件引用指定的数据
CREATE TABLE emp2 AS SELECT * FROM employees WHERE 1=2; -- 创建的emp2是空表
CREATE TABLE dept80
AS
SELECT employee_id, last_name, salary*12 ANNSAL, hire_date
FROM employees
WHERE department_id = 80;
-- 将另一个表的指定数据引用过来成为创建的新表的数据
mysql> create table emp2 as select id,a,b from emp1;
Query OK, 2 rows affected (0.02 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from emp2;
+------+------+------+
| id   | a    | b    |
+------+------+------+
|    1 |  100 |  200 |
|    2 | 1000 | 2000 |
+------+------+------+
2 rows in set (0.00 sec)
-- 将另一个表的指定数据并可以指定限定条件筛选后引用过来成为创建的新表的数据
mysql> create table emp3 select id,a,b from emp2 where b=2000;-- where后可指定限制条件
Query OK, 1 row affected (0.14 sec)
Records: 1  Duplicates: 0  Warnings: 0

mysql> select * from emp3;
+------+------+------+
| id   | a    | b    |
+------+------+------+
|    2 | 1000 | 2000 |
+------+------+------+
1 row in set (0.00 sec)

```

##### 修改 Alter

```sql
#MySQL ALTER命令
当我们需要修改数据表名或者修改数据表字段时，就需要使用到MySQL ALTER命令
#删除，添加或修改表字段
如下命令使用了 ALTER 命令及 DROP 子句来删除以上创建表的 i 字段：

mysql> ALTER TABLE testalter_tbl  DROP i;
如果数据表中只剩余一个字段则无法使用DROP来删除字段。

MySQL 中使用 ADD 子句来向数据表中添加列，如下实例在表 testalter_tbl 中添加 i 字段，并定义数据类型:

mysql> ALTER TABLE testalter_tbl ADD i INT;

#修改字段类型及名称
如果需要修改字段类型及名称, 你可以在ALTER命令中使用 MODIFY 或 CHANGE 子句 。

例如，把字段 c 的类型从 CHAR(1) 改为 CHAR(10)，可以执行以下命令:

mysql> ALTER TABLE testalter_tbl MODIFY c CHAR(10);
使用 CHANGE 子句, 语法有很大的不同。 在 CHANGE 关键字之后，紧跟着的是你要修改的字段名，然后指定新字段名及类型。尝试如下实例：

mysql> ALTER TABLE testalter_tbl CHANGE i j BIGINT;
mysql> ALTER TABLE testalter_tbl CHANGE j j INT;
ALTER TABLE 对 Null 值和默认值的影响
当你修改字段时，你可以指定是否包含值或者是否设置默认值
以下实例，指定字段 j 为 NOT NULL 且默认值为100 。

mysql> ALTER TABLE testalter_tbl 
    -> MODIFY j BIGINT NOT NULL DEFAULT 100;

#修改字段默认值
你可以使用 ALTER 来修改字段的默认值
你可以使用 ALTER 来修改字段的默认值，尝试以下实例：

mysql> ALTER TABLE testalter_tbl ALTER i SET DEFAULT 1000;
mysql> SHOW COLUMNS FROM testalter_tbl;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| c     | char(1) | YES  |     | NULL    |       |
| i     | int(11) | YES  |     | 1000    |       |
+-------+---------+------+-----+---------+-------+
2 rows in set (0.00 sec)
你也可以使用 ALTER 命令及 DROP子句来删除字段的默认值，如下实例：

mysql> ALTER TABLE testalter_tbl ALTER i DROP DEFAULT;
mysql> SHOW COLUMNS FROM testalter_tbl;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| c     | char(1) | YES  |     | NULL    |       |
| i     | int(11) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
2 rows in set (0.00 sec)
Changing a Table Type:

#修改表名
如果需要修改数据表的名称，可以在 ALTER TABLE 语句中使用 RENAME 子句来实现
尝试以下实例将数据表 testalter_tbl 重命名为 alter_tbl：

mysql> ALTER TABLE testalter_tbl RENAME TO alter_tbl;

#alter其他用途：

#修改存储引擎：修改为myisam

alter table tableName engine=myisam;
#删除外键约束：keyName是外键别名

alter table tableName drop foreign key keyName;
#修改字段的相对位置：这里name1为想要修改的字段，type1为该字段原来类型，first和after二选一，这应该显而易见，first放在第一位，after放在name2字段后面

alter table tableName modify name1 type1 first|after name2;
```



##### 删除

```sql
#在MySQL中，当一张数据表 没有与其他任何数据表形成关联关系 时，可以将当前数据表直接删除。
#数据和结构都被删除
#所有正在运行的相关事务被提交
#所有相关索引被删除
mysql> drop table [IF EXISTS] emp3;
-- DROP TABLE 语句不能回滚

#TRUNCATE TABLE语句：
#删除表中所有的数据
#释放表的存储空间
#举例：
TRUNCATE TABLE detail_dept;
-- TRUNCATE语句不能回滚，而使用 DELETE 语句删除数据，可以回滚
#delete from 表名
#删除表中所有的数据
mysql> delete from emp2;
Query OK, 2 rows affected (0.01 sec)

mysql> show tables from db02;
+----------------+
| Tables_in_db02 |
+----------------+
| emp1           |
| emp2           |
| employee1      |
| employee2      |
| employee3      |
+----------------+
5 rows in set (0.00 sec)

mysql> select * fm emp2;
Empty set (0.00 sec)


```



#### MySQL数据类型★

![image-20230202105323181](C:/Users/ZJH20/AppData/Roaming/Typora/typora-user-images/image-20230202105323181.png)

![image-20230202105347338](C:/Users/ZJH20/AppData/Roaming/Typora/typora-user-images/image-20230202105347338.png)

列类型/字段类型

![image-20220827203146462](/images/image-20220827203146462.png)

##### 数值类型

###### 整形

tInyint[一个字节]

smallint[两个字节]

mediumint[三个字节]

**int[四个字节]**

bigint[八个字节]

###### 小数类型

float（单精度）[四个字节]

**double（双精度）[八个字节]**

**decimal（M,D）[不确定大小]**

##### 文本类型（字符串类型）

**char(表数范围0-255)**

**varchar（表数范围0-65535【2^16-1】）**

**text(表数范围0-65535【2^16-1】)**

longtext(表数范围0-【2^32-1】)

##### 二进制数据类型

blob(表数范围0-65535【2^16-1】)

longblob(表数范围0-【2^32-1】)

##### 日期类型

date(日期 年月日)

time（时间 时分秒）

**datetime（日期时间 年月日 时分秒 YYYY-MM-DD hh:mm:ss）**

**timestamp(时间戳)**

year（年）

#### CRUD★

**Tip**: sql中的**null**值 查找使用 is

SELECT * FROM SOME_TABLE
**WHERE SOME_COLUMN `IS` NULL**

##### Insert

```sql
#SQL INSERT INTO 语句
INSERT INTO 语句用于向表中插入新记录

#INSERT INTO 语句可以有两种编写形式。
-- 第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：没有指定要插入数据的列名的形式需要列出插入行的每一列数据:

INSERT INTO table_name
VALUES (value1,value2,value3,...);
-- 第二种形式需要指定列名及被插入的值：

INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);

-- 扩展
-- 通过 SQL，您可以从一个表复制信息到另一个表。INSERT INTO SELECT 语句从一个表复制数据，然后把数据插入到一个已存在的表中
INSERT INTO SELECT

-- For instance:
mysql> select * from emp2;-- 第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：
Empty set (0.00 sec)

mysql> inert into emp2 values (1,22,33,55);
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'inert into emp2 values (1,22,33,55)' at line 1
mysql> insert into emp2 values (1,22,33,55);
Query OK, 1 row affected (0.01 sec)

mysql> select * from emp2;
+------+------+------+------+
| id   | a    | b    | sum  |
+------+------+------+------+
|    1 |   22 |   33 |   55 |
+------+------+------+------+
1 row in set (0.00 sec)

mysql>

mysql> insert into emp1 (id,a,b,d) values (6,5223,544,1001);-- 第二种形式需要指定列名及被插入的值：
Query OK, 1 row affected (0.00 sec)

mysql> select * from emp1;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 | NULL |
|    2 | 1000 | 2000 | 3000 | NULL |
|    3 |  120 |  520 |  640 | NULL |
|    4 |  120 |  520 |  640 | NULL |
|    5 |  120 |  520 |  640 | NULL |
|    6 | 5223 |  544 | 5767 | 1001 |
+------+------+------+------+------+
6 rows in set (0.00 sec)

mysql>

#SQL INSERT INTO SELECT 语句
-- 通过 SQL，您可以从一个表复制信息到另一个表。INSERT INTO SELECT 语句从一个表复制数据，然后把数据插入到一个已存在的表中

mysql> insert into emp2 (id,a,b,sum) select id,a,b,c from emp1 where id between 2 and 6;
Query OK, 5 rows affected (0.00 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> select * from emp2;
+------+------+------+------+
| id   | a    | b    | sum  |
+------+------+------+------+
|    1 |   22 |   33 |   55 |
|    2 | 1000 | 2000 | 3000 |
|    3 |  120 |  520 |  640 |
|    4 |  120 |  520 |  640 |
|    5 |  120 |  520 |  640 |
|    6 | 5223 |  544 | 5767 |
+------+------+------+------+
6 rows in set (0.00 sec)

mysql>

mysql> update emp1 set d=(id * 10);
Query OK, 6 rows affected (0.15 sec)
Rows matched: 6  Changed: 6  Warnings: 0

mysql> select * from emp1;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 |   10 |
|    2 | 1000 | 2000 | 3000 |   20 |
|    3 |  120 |  520 |  640 |   30 |
|    4 |  120 |  520 |  640 |   40 |
|    5 |  120 |  520 |  640 |   50 |
|    6 | 5223 |  544 | 5767 |   60 |
+------+------+------+------+------+
6 rows in set (0.00 sec)
```

##### Update

```sql
#SQL UPDATE 语句
UPDATE 语句用于更新表中已存在的记录。
-- SQL UPDATE 语法
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;

-- For instance
mysql> select * from emp1;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 | NULL |
|    2 | 1000 | 2000 | 3000 | NULL |
|    3 |  120 |  520 |  640 | NULL |
|    4 |  120 |  520 |  640 | NULL |
|    5 |  120 |  520 |  640 | NULL |
|    6 | 5223 |  544 | 5767 | 1001 |
+------+------+------+------+------+
6 rows in set (0.00 sec)

mysql> update emp1 set d=100 where c<=640;
Query OK, 4 rows affected (0.00 sec)
Rows matched: 4  Changed: 4  Warnings: 0

mysql> select * from emp1;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 |  100 |
|    2 | 1000 | 2000 | 3000 | NULL |
|    3 |  120 |  520 |  640 |  100 |
|    4 |  120 |  520 |  640 |  100 |
|    5 |  120 |  520 |  640 |  100 |
|    6 | 5223 |  544 | 5767 | 1001 |
+------+------+------+------+------+
6 rows in set (0.00 sec)

mysql> update emp1 set d=1002 where d;
Query OK, 5 rows affected (0.01 sec)
Rows matched: 5  Changed: 5  Warnings: 0

mysql> select * from emp1;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 | 1002 |
|    2 | 1000 | 2000 | 3000 | NULL |
|    3 |  120 |  520 |  640 | 1002 |
|    4 |  120 |  520 |  640 | 1002 |
|    5 |  120 |  520 |  640 | 1002 |
|    6 | 5223 |  544 | 5767 | 1002 |
+------+------+------+------+------+
6 rows in set (0.00 sec)

mysql> update emp1 set d=1002 where d is null;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from emp1;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 | 1002 |
|    2 | 1000 | 2000 | 3000 | 1002 |
|    3 |  120 |  520 |  640 | 1002 |
|    4 |  120 |  520 |  640 | 1002 |
|    5 |  120 |  520 |  640 | 1002 |
|    6 | 5223 |  544 | 5767 | 1002 |
+------+------+------+------+------+
6 rows in set (0.00 sec)

mysql>
```



##### Delete

```sql
#SQL DELETE 语句
DELETE 语句用于删除表中的行
-- SQL DELETE 语法
DELETE FROM table_name
WHERE some_column=some_value;-- WHERE 子句规定哪条记录或者哪些记录需要删除。如果您省略了 WHERE 子句，所有的记录都将被删除！

-- For instance
mysql> select * from emp1;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 |   10 |
|    2 | 1000 | 2000 | 3000 |   20 |
|    3 |  120 |  520 |  640 |   30 |
|    4 |  120 |  520 |  640 |   40 |
|    5 |  120 |  520 |  640 |   50 |
|    6 | 5223 |  544 | 5767 |   60 |
+------+------+------+------+------+
6 rows in set (0.00 sec)

mysql> delete from emp1 where d between 40 and 50;
Query OK, 2 rows affected (0.01 sec)

mysql> select * from emp1;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 |   10 |
|    2 | 1000 | 2000 | 3000 |   20 |
|    3 |  120 |  520 |  640 |   30 |
|    6 | 5223 |  544 | 5767 |   60 |
+------+------+------+------+------+
4 rows in set (0.00 sec)

删除所有数据
可以在不删除表的情况下，删除表中所有的行。这意味着表结构、属性、索引将保持不变：

DELETE FROM table_name;
注释：在删除记录时要格外小心！因为您不能重来！
mysql> select * from emp1;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 |   10 |
|    2 | 1000 | 2000 | 3000 |   20 |
|    3 |  120 |  520 |  640 |   30 |
|    6 | 5223 |  544 | 5767 |   60 |
+------+------+------+------+------+
4 rows in set (0.00 sec)

mysql> select * from emp2;
+------+------+------+------+
| id   | a    | b    | sum  |
+------+------+------+------+
|    1 |   22 |   33 |   55 |
|    2 | 1000 | 2000 | 3000 |
|    3 |  120 |  520 |  640 |
|    4 |  120 |  520 |  640 |
|    5 |  120 |  520 |  640 |
|    6 | 5223 |  544 | 5767 |
+------+------+------+------+
6 rows in set (0.00 sec)

mysql> delete from emp2;
Query OK, 6 rows affected (0.00 sec)

mysql> select * from emp2;
Empty set (0.00 sec)
```



##### Select★

###### 单表

```sql
基本的SELECT语句
#SELECT...
#SELECT 1; #没有任何子句
#SELECT 9/2; #没有任何子句
mysql> select * from emp1;
+------+------+------+------+
| id   | a    | b    | c    |
+------+------+------+------+
|    1 |  100 |  200 |  300 |
|    2 | 1000 | 2000 | 3000 |
+------+------+------+------+
2 rows in set (0.00 sec)

mysql> select 2000;-- 没有任何子句
+------+
| 2000 |
+------+
| 2000 |
+------+
1 row in set (0.00 sec)

mysql> select database();
+------------+
| database() |
+------------+
| db02       |
+------------+
1 row in set (0.00 sec)

mysql>

#SELECT ... FROM--在select后面可以使用表达式对查询的列进行运算 同时可使用AS给列定义一个别名
SELECT 标识选择哪些列
FROM 标识从哪个表中选择
#select * from 表名 返回指定表的所有列
mysql> select * from emp1;
+------+------+------+------+
| id   | a    | b    | c    |
+------+------+------+------+
|    1 |  100 |  200 |  300 |
|    2 | 1000 | 2000 | 3000 |
+------+------+------+------+
2 rows in set (0.00 sec)

#SELECT department_id, location_id,(列名),(列明) FROM departments（表名）where （条件）;-- 返回指定表中满足where后条件的的指定列
mysql> select id,a,b from emp1 where c=3000;
+------+------+------+
| id   | a    | b    |
+------+------+------+
|    2 | 1000 | 2000 |
+------+------+------+
1 row in set (0.00 sec)

#select id,(a + b)--可以进行运算 from emp2;-- 返回指定表中指定列且指定列之间运算的列-- 在select后面可以使用表达式对查询的列进行运算
mysql> select id,(a + b) from emp2;
Empty set (0.00 sec)

mysql> select id,(a + b) from emp1;
+------+---------+
| id   | (a + b) |
+------+---------+
|    1 |     300 |
|    2 |    3000 |
+------+---------+
2 rows in set (0.00 sec)

#select id,(a + b)可以进行运算 as 'sum' 通过AS给运算后的列定义一个'别名' from emp1;-- 返回指定表中指定列且指定列之间运算的定义别名后的列
mysql> select id,(a + b) as 'sum' from emp1;
+------+------+
| id   | sum  |
+------+------+
|    1 |  300 |
|    2 | 3000 |
+------+------+
2 rows in set (0.00 sec)

mysql>

-- 使用WHERE 子句，将不满足条件的行过滤掉
-- WHERE子句紧随 FROM子句
SELECT 字段1,字段2
FROM 表名
WHERE 过滤条件
-- For instance:
mysql> select * from emp1 where c>=640;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    2 | 1000 | 2000 | 3000 | NULL |
|    3 |  120 |  520 |  640 | NULL |
|    4 |  120 |  520 |  640 | NULL |
|    5 |  120 |  520 |  640 | NULL |
+------+------+------+------+------+
4 rows in set (0.00 sec)

mysql>

#列的别名
-- 重命名一个列
-- 便于计算
-- 紧跟列名，也可以在列名和别名之间加入关键字AS，别名使用双引号，以便在别名中包含空格或特
-- 殊的字符并区分大小写。
-- AS 可以省略
-- 建议别名简短，见名知意
-- 举例
SELECT last_name AS name, commission_pct comm
FROM employees;
mysql> select id,(a + b) as 'sum' from emp1;
+------+------+
| id   | sum  |
+------+------+
|    1 |  300 |
|    2 | 3000 |
+------+------+
2 rows in set (0.00 sec)

SELECT last_name "Name", salary*12 "Annual Salary"
FROM employees;
mysql> select id,(a + b) as "SumNumber" from emp1;
+------+-----------+
| id   | SumNumber |
+------+-----------+
|    1 |       300 |
|    2 |      3000 |
+------+-----------+
2 rows in set (0.00 sec)

mysql>
-- 默认情况下，查询会返回全部行，包括重复行。

#去除重复行
#在SELECT语句中使用关键字DISTINCT去除重复行
SELECT DISTINCT department_id-- 此处的列表示要以哪些列以及几个列为条件判断是否为重复
FROM employees;

mysql> select * from emp1;
+------+------+------+------+
| id   | a    | b    | c    |
+------+------+------+------+
|    1 |  100 |  200 |  300 |
|    2 | 1000 | 2000 | 3000 |
|    3 |  120 |  520 |  640 |
|    4 |  120 |  520 |  640 |
|    5 |  120 |  520 |  640 |
+------+------+------+------+
5 rows in set (0.00 sec)

mysql> select distinct * from emp1;
+------+------+------+------+
| id   | a    | b    | c    |
+------+------+------+------+
|    1 |  100 |  200 |  300 |
|    2 | 1000 | 2000 | 3000 |
|    3 |  120 |  520 |  640 |
|    4 |  120 |  520 |  640 |
|    5 |  120 |  520 |  640 |
+------+------+------+------+
5 rows in set (0.00 sec)

mysql> select distinct a from emp1;
+------+
| a    |
+------+
|  100 |
| 1000 |
|  120 |
+------+
3 rows in set (0.00 sec)

mysql> select distinct id,a,b,c form emp1;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'emp1' at line 1
mysql> select distinct id,a,b,c from emp1;
+------+------+------+------+
| id   | a    | b    | c    |
+------+------+------+------+
|    1 |  100 |  200 |  300 |
|    2 | 1000 | 2000 | 3000 |
|    3 |  120 |  520 |  640 |
|    4 |  120 |  520 |  640 |
|    5 |  120 |  520 |  640 |
+------+------+------+------+
5 rows in set (0.00 sec)

mysql> select distinct c from emp1;
+------+
| c    |
+------+
|  300 |
| 3000 |
|  640 |
+------+
3 rows in set (0.00 sec)

mysql>

#空值参与运算
-- 注意，在 MySQL 里面， 空值不等于空字符串。一个空字符串的长度是 0，而一个空值的长度是空。而且，在 MySQL 里面，空值是占用空间的
#所有运算符或列值遇到null值，运算的结果都为null
mysql> alter table emp1 add (d int);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from emp1;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 | NULL |
|    2 | 1000 | 2000 | 3000 | NULL |
|    3 |  120 |  520 |  640 | NULL |
|    4 |  120 |  520 |  640 | NULL |
|    5 |  120 |  520 |  640 | NULL |
+------+------+------+------+------+
5 rows in set (0.00 sec)

mysql> select id,(c + d) as 'sum' from emp1;
+------+------+
| id   | sum  |
+------+------+
|    1 | NULL |
|    2 | NULL |
|    3 | NULL |
|    4 | NULL |
|    5 | NULL |
+------+------+
5 rows in set (0.00 sec)

mysql>

#着重号 ``
-- 我们需要保证表中的字段、表名等没有和保留字、数据库系统或常用方法冲突。如果真的相同，请在SQL语句中使用一对``（着重号）引起来
CREATE TABLE student5(
    id TINYINT,`name` VARCHAR(255),`password` VARCHAR(25),birthday DATA)
    CHARACTER SET utf8 COLLATE utf8_bin ENGINE INNODB

# 显示表结构
-- 使用DESCRIBE 或 DESC 命令，表示表结构
mysql> describe emp1;
+-------+------+------+-----+---------+-------------------+
| Field | Type | Null | Key | Default | Extra             |
+-------+------+------+-----+---------+-------------------+
| id    | int  | YES  |     | NULL    |                   |
| a     | int  | YES  |     | NULL    |                   |
| b     | int  | YES  |     | NULL    |                   |
| c     | int  | YES  |     | NULL    | VIRTUAL GENERATED |
| d     | int  | YES  |     | NULL    |                   |
+-------+------+------+-----+---------+-------------------+
5 rows in set (0.00 sec)

mysql>
#其中，各个字段的含义分别解释如下：
-- Field：表示字段名称。
-- Type：表示字段类型，这里 barcode、goodsname 是文本型的，price 是整数类型的。
-- Null：表示该列是否可以存储NULL值。
-- Key：表示该列是否已编制索引。PRI表示该列是表主键的一部分；UNI表示该列是UNIQUE索引的一部分；MUL表示在列中某个给定值允许出现多次。
-- Default：表示该列是否有默认值，如果有，那么值是多少。
-- Extra：表示可以获取的与给定列有关的附加信息，例如AUTO_INCREMENT等。

# 显示表的创建信息
mysql> show create from emp1;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'from emp1' at line 1
mysql> show create db01;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'db01' at line 1
mysql> show create table emp1;
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                                                       |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| emp1  | CREATE TABLE `emp1` (
  `id` int DEFAULT NULL,
  `a` int DEFAULT NULL,
  `b` int DEFAULT NULL,
  `c` int GENERATED ALWAYS AS ((`a` + `b`)) VIRTUAL,
  `d` int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```

###### **Select语句的where子句**

**where**可以指明约束条件-- WHERE 子句用于过滤记录。

```sql
#SQL WHERE 语法
SELECT column_name,column_name
FROM table_name
WHERE column_name operator value;-- 指明约束条件-- WHERE 子句用于过滤记录。

```

**where**子句中的运算符

![image-20220901125539476](/images/image-20220901125539476.png)

![image-20220901130357689](/images/image-20220901130357689.png)

```sql
Where +条件（筛选行）
条件：列，比较运算符，值

比较运算符包涵：= > < >= ,<=, !=,<> 表示（不等于）

Select * from emp where ename='SMITH';
例子中的 SMITH 用单引号引起来，表示是字符串，字符串要区分大小写。

逻辑运算
And:与 同时满足两个条件的值。

Select * from emp where sal > 2000 and sal < 3000;
查询 EMP 表中 SAL 列中大于 2000 小于 3000 的值。

Or:或 满足其中一个条件的值

Select * from emp where sal > 2000 or comm > 500;
查询 emp 表中 SAL 大于 2000 或 COMM 大于500的值。

Not:非 满足不包含该条件的值。

select * from emp where not sal > 1500;
查询EMP表中 sal 小于等于 1500 的值。

逻辑运算的优先级：

()  >  not    >    and    >     or
特殊条件
1.空值判断：判断是否为空 is null ☆******************☆

Select * from emp where comm is null;
查询 emp 表中 comm 列中的空值。

2.between and (在 之间的值)-- 是闭区间

Select * from emp where sal between 1500 and 3000;
查询 emp 表中 SAL 列中大于 1500 的小于 3000 的值。

注意：大于等于 1500 且小于等于 3000， 1500 为下限，3000 为上限，下限在前，上限在后，查询的范围包涵有上下限的值。

3.In-- 在（条件,条件，条件）里面的

Select * from emp where sal in (5000,3000,1500);
查询 EMP 表 SAL 列中等于 5000，3000，1500 的值。

4.like

Like模糊查询

Select * from emp where ename like 'M%';
查询 EMP 表中 Ename 列中有 M 的值，M 为要查询内容中的模糊信息。

 % 表示多个字值，_ 下划线表示一个字符；
 M% : 为能配符，正则表达式，表示的意思为模糊查询信息为 M 开头的。
 %M% : 表示查询包含M的所有内容。
 %M_ : 表示查询以M在倒数第二位的所有内容。
 
#不带比较运算符的 WHERE 子句：

WHERE 子句并不一定带比较运算符，当不带运算符时，会执行一个隐式转换。当 0 时转化为 false，1 转化为 true。例如：

SELECT studentNO FROM student WHERE 0
则会返回一个空集，因为每一行记录 WHERE 都返回 false。

SELECT  studentNO  FROM student WHERE 1
返回 student 表所有行中 studentNO 列的值。因为每一行记录 WHERE 都返回 true。

-- For instance
mysql> select * from emp1 where 0;
Empty set (0.00 sec)

mysql> select * from emp1 where 1;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 |   10 |
|    2 | 1000 | 2000 | 3000 |   20 |
|    3 |  120 |  520 |  640 |   30 |
|    6 | 5223 |  544 | 5767 |   60 |
+------+------+------+------+------+
4 rows in set (0.00 sec)

mysql>
```

###### **Select**语句的**order by**子句

```sql
#SQL ORDER BY 关键字
ORDER BY 关键字用于对结果集按照一个列或者多个列进行排序。可以使用列的别名进行排序
ORDER BY 关键字默认按照升序(ascend)对记录进行排序。如果需要按照降序对记录进行排序，您可以使用 DESC （descend）降序关键字

ORDER BY 多列的时候，先按照第一个column name排序，在按照第二个column name排序；如上述教程最后一个例子：

 1）、先将country值这一列排序，同为CN的排前面，同属USA的排后面；
 2）、然后在同属CN的这些多行数据中，再根据alexa值的大小排列。
 3）、ORDER BY 排列时，不写明ASC DESC的时候，默认是ASC
 
 ORDER BY 多列的时候，eg:

order by A,B        这个时候都是默认按升序排列
order by A desc,B   这个时候 A 降序，B 升序排列
order by A ,B desc  这个时候 A 升序，B 降序排列
即 desc 或者 asc 只对它紧跟着的第一个列名有效，其他不受影响，仍然是默认的升序
 
-- SQL ORDER BY 语法
SELECT column_name,column_name
FROM table_name
ORDER BY column_name,column_name ASC|DESC;-- 默认使用ASC升序进行排序 可以指定排序方式

-- For instance-- 单列
mysql> select * from emp1 order by d;-- 默认使用ASC升序进行排序
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 |   10 |
|    2 | 1000 | 2000 | 3000 |   20 |
|    3 |  120 |  520 |  640 |   30 |
|    6 | 5223 |  544 | 5767 |   60 |
+------+------+------+------+------+
4 rows in set (0.00 sec)

mysql>

mysql> select * from emp1 order by c desc;-- 默认使用ASC升序进行排序 可以指定排序方式
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    6 | 5223 |  544 | 5767 |   60 |
|    2 | 1000 | 2000 | 3000 |   20 |
|    3 |  120 |  520 |  640 |   30 |
|    1 |  100 |  200 |  300 |   10 |
+------+------+------+------+------+
4 rows in set (0.00 sec)

mysql> select * from emp1 order by c DESC;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    6 | 5223 |  544 | 5767 |   60 |
|    2 | 1000 | 2000 | 3000 |   20 |
|    7 | 1000 | 2000 | 3000 |   40 |
|    3 |  120 |  520 |  640 |   30 |
|    1 |  100 |  200 |  300 |   10 |
+------+------+------+------+------+
5 rows in set (0.00 sec)

-- For instance-- 多列

mysql> select * from emp1 order by c,d desc;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    1 |  100 |  200 |  300 |   10 |
|    3 |  120 |  520 |  640 |   30 |
|    7 | 1000 | 2000 | 3000 |   40 |
|    2 | 1000 | 2000 | 3000 |   20 |
|    6 | 5223 |  544 | 5767 |   60 |
+------+------+------+------+------+
5 rows in set (0.00 sec)

mysql> select * from emp1 order by c desc,d desc;
+------+------+------+------+------+
| id   | a    | b    | c    | d    |
+------+------+------+------+------+
|    6 | 5223 |  544 | 5767 |   60 |
|    7 | 1000 | 2000 | 3000 |   40 |
|    2 | 1000 | 2000 | 3000 |   20 |
|    3 |  120 |  520 |  640 |   30 |
|    1 |  100 |  200 |  300 |   10 |
+------+------+------+------+------+
5 rows in set (0.00 sec)

mysql>

#可以使用别名进行排序

mysql> select id,a,b,(a + b) as 'sum',c,d from emp1 order by sum desc;
+------+------+------+------+------+------+
| id   | a    | b    | sum  | c    | d    |
+------+------+------+------+------+------+
|    6 | 5223 |  544 | 5767 | 5767 |   60 |
|    2 | 1000 | 2000 | 3000 | 3000 |   20 |
|    7 | 1000 | 2000 | 3000 | 3000 |   40 |
|    3 |  120 |  520 |  640 |  640 |   30 |
|    1 |  100 |  200 |  300 |  300 |   10 |
+------+------+------+------+------+------+
5 rows in set (0.00 sec)

#综合where & AS & 双列 & 列运算 条件使用order by
mysql> select id,a,b,(a + b) as 'sum',c,d from emp1 where id between 2 and 6 order by sum desc,d desc;
+------+------+------+------+------+------+
| id   | a    | b    | sum  | c    | d    |
+------+------+------+------+------+------+
|    6 | 5223 |  544 | 5767 | 5767 |   60 |
|    2 | 1000 | 2000 | 3000 | 3000 |   20 |
|    3 |  120 |  520 |  640 |  640 |   30 |
+------+------+------+------+------+------+
3 rows in set (0.00 sec)
```

###### 单表查询加强

```sql
-- select语句顺序 group by - having - order by - limit
select '列名','列名'... from '表名'
group by `列`
having `condition`
order by `列`
limit `start`,`rows`;
-- For instance 统计各个部门的平均工资仅保留2位小数，并且>1000,平均工资按照降序排序，并取出前两行;
mysql> select format(avg(sal),2),deptno from emp
    -> group by deptno
    -> having avg(sal)>1000
    -> order by avg(sal) desc
    -> limit 0,2;
+--------------------+--------+
| format(avg(sal),2) | deptno |
+--------------------+--------+
| 2,916.67           |     10 |
| 2,443.75           |     20 |
+--------------------+--------+
2 rows in set (0.00 sec)


#结合where子句对date进行条件筛选
-- 查询1991-01-01后入职的员工
mysql> select ename,hiredate from emp where hiredate>'1992-01-01';
+--------+------------+
| ename  | hiredate   |
+--------+------------+
| SCOTT  | 1997-04-19 |
| MILLER | 1992-01-23 |
+--------+------------+
2 rows in set (0.00 sec)

#Like模糊查询

Select * from emp where ename like 'M%';
查询 EMP 表中 Ename 列中有 M 的值，M 为要查询内容中的模糊信息。

 % 表示多个字值，_ 下划线表示一个字符；
 M% : 为能配符，正则表达式，表示的意思为模糊查询信息为 M 开头的。
 %M% : 表示查询包含M的所有内容。
 %M_ : 表示查询以M在倒数第二位的所有内容。
 
 -- For instance 显示姓名首字母为S的员工及其工资
 mysql> select ename,sal from emp where ename like 'S%';
+-------+---------+
| ename | sal     |
+-------+---------+
| SMITH |  800.00 |
| SCOTT | 3000.00 |
+-------+---------+
2 rows in set (0.00 sec)
-- For instance 显示姓名第三个字母为O的员工及其工资
mysql> select ename, sal from emp where ename like '__O%';
+-------+---------+
| ename | sal     |
+-------+---------+
| SCOTT | 3000.00 |
+-------+---------+
1 row in set (0.00 sec)

#is null 判断是否为null值
-- For instance 显示没有上级的员工信息（上级编号mgr为null的）
mysql> select * from emp where mgr is null;
+-------+-------+-----------+------+------------+---------+------+--------+
| empno | ename | job       | mgr  | hiredate   | sal     | comm | deptno |
+-------+-------+-----------+------+------------+---------+------+--------+
|  7839 | KING  | president | NULL | 1991-11-17 | 5000.00 | NULL |     10 |
+-------+-------+-----------+------+------------+---------+------+--------+
1 row in set (0.00 sec)

#order by 排序-- 默认升序（不指明desc即为asc）
-- For instance
mysql> select * from emp order by sal asc;-- 默认升序（不指明desc即为asc）
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7900 | JAMES  | clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7521 | WARD   | salesman  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7654 | MARTIN | salesman  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7934 | MILLER | clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
|  7844 | TURNER | salesman  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7499 | ALLEN  | salesman  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7782 | CLARK  | manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7698 | BLAKE  | manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7566 | JONES  | manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7788 | SCOTT  | analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7902 | FORD   | analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7839 | KING   | president | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

mysql> select * from emp order by sal desc;-- 默认升序（不指明desc即为asc）
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7839 | KING   | president | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7788 | SCOTT  | analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7902 | FORD   | analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7566 | JONES  | manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7698 | BLAKE  | manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7499 | ALLEN  | salesman  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7844 | TURNER | salesman  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7934 | MILLER | clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
|  7521 | WARD   | salesman  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7654 | MARTIN | salesman  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7900 | JAMES  | clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7369 | SMITH  | clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

-- 先按照部门编号升序然后按照工资降序排序显示员工信息
mysql> select * from emp order by deptno asc , sal desc;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7839 | KING   | president | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7782 | CLARK  | manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7934 | MILLER | clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
|  7788 | SCOTT  | analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7902 | FORD   | analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7566 | JONES  | manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7369 | SMITH  | clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7698 | BLAKE  | manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7499 | ALLEN  | salesman  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7844 | TURNER | salesman  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7521 | WARD   | salesman  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7654 | MARTIN | salesman  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7900 | JAMES  | clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

#分页查询
-- 基本语法select...limit start，rows 从start + 1行开始 取出rows行 start从0开始计算
-- limit 每页显要显示的行数 *（第几页 - 1），每页显要显示的行数
-- 第1页
mysql> select * from emp order by sal desc limit 0,5;-- limit 每页显要显示的行数 *（第几页 - 1），每页显要显示的行数
+-------+-------+-----------+------+------------+---------+------+--------+
| empno | ename | job       | mgr  | hiredate   | sal     | comm | deptno |
+-------+-------+-----------+------+------------+---------+------+--------+
|  7839 | KING  | president | NULL | 1991-11-17 | 5000.00 | NULL |     10 |
|  7788 | SCOTT | analyst   | 7566 | 1997-04-19 | 3000.00 | NULL |     20 |
|  7902 | FORD  | analyst   | 7566 | 1991-12-03 | 3000.00 | NULL |     20 |
|  7566 | JONES | manager   | 7839 | 1991-04-02 | 2975.00 | NULL |     20 |
|  7698 | BLAKE | manager   | 7839 | 1991-05-01 | 2850.00 | NULL |     30 |
+-------+-------+-----------+------+------------+---------+------+--------+
5 rows in set (0.00 sec)
-- 第二页
mysql> select * from emp order by sal desc limit 5,5;-- limit 每页显要显示的行数 *（第几页 - 1），每页显要显示的行数
+-------+--------+----------+------+------------+---------+--------+--------+
| empno | ename  | job      | mgr  | hiredate   | sal     | comm   | deptno |
+-------+--------+----------+------+------------+---------+--------+--------+
|  7782 | CLARK  | manager  | 7839 | 1991-06-09 | 2450.00 |   NULL |     10 |
|  7499 | ALLEN  | salesman | 7698 | 1991-02-20 | 1600.00 | 300.00 |     30 |
|  7844 | TURNER | salesman | 7698 | 1991-09-08 | 1500.00 |   NULL |     30 |
|  7934 | MILLER | clerk    | 7782 | 1992-01-23 | 1300.00 |   NULL |     10 |
|  7521 | WARD   | salesman | 7698 | 1991-02-22 | 1250.00 | 500.00 |     30 |
+-------+--------+----------+------+------------+---------+--------+--------+
5 rows in set (0.00 sec)
-- 第三页
mysql> select * from emp order by sal desc limit 10,5;-- limit 每页显要显示的行数 *（第几页 - 1），每页显要显示的行数
+-------+--------+----------+------+------------+---------+---------+--------+
| empno | ename  | job      | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+----------+------+------------+---------+---------+--------+
|  7654 | MARTIN | salesman | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7900 | JAMES  | clerk    | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7369 | SMITH  | clerk    | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
+-------+--------+----------+------+------------+---------+---------+--------+
3 rows in set (0.00 sec)

#分组函数&分组子句GROUP BY
-- For instance 显示每种岗位的雇员总数和平均工资
mysql> select count(*),avg(sal) from emp group by job;
+----------+-------------+
| count(*) | avg(sal)    |
+----------+-------------+
|        3 | 1016.666667 |
|        4 | 1400.000000 |
|        3 | 2758.333333 |
|        2 | 3000.000000 |
|        1 | 5000.000000 |
+----------+-------------+
5 rows in set (0.00 sec)
-- For instance 获取雇员总数以及获得了补助（comm不为null的）的雇员数
mysql> select count(*),count(comm) from emp;-- count（*）与count（列）的区别是count（列）会过滤列中的null值 而count（*）返回总列数
+----------+-------------+
| count(*) | count(comm) |
+----------+-------------+
|       13 |           3 |
+----------+-------------+
1 row in set (0.00 sec)
-- For instance 获取雇员总数以及没有补助（comm为null的）的雇员数
mysql> select count(*),count(if(comm is null,1,null)) from emp;
+----------+--------------------------------+
| count(*) | count(if(comm is null,1,null)) |
+----------+--------------------------------+
|       13 |                             10 |
+----------+--------------------------------+
mysql> select if(comm is null,1,null) from emp;
-- 其中 if(comm is null,1,null)
+-------------------------+
| if(comm is null,1,null) |
+-------------------------+
|                       1 |
|                    NULL |
|                    NULL |
|                       1 |
|                    NULL |
|                       1 |
|                       1 |
|                       1 |
|                       1 |
|                       1 |
|                       1 |
|                       1 |
|                       1 |
+-------------------------+
13 rows in set (0.00 sec)
1 row in set (0.00 sec)
-- else method
mysql> select count(*),count(*) - count(comm) from emp;
+----------+------------------------+
| count(*) | count(*) - count(comm) |
+----------+------------------------+
|       13 |                     10 |
+----------+------------------------+
1 row in set (0.00 sec)

-- For instance 显示员工中manager的总数
mysql> select count(job) as 'manager_count' from emp where job='manager';
+---------------+
| manager_count |
+---------------+
|             3 |
+---------------+
1 row in set (0.00 sec)

-- For instance 显示员工的工资最大差额
mysql> select max(sal) - min(sal) as '最大工资差额' from emp;
+--------------------+
| 最大工资差额       |
+--------------------+
|            4200.00 |
+--------------------+
1 row in set (0.00 sec)
```



###### 多表

```sql
#多表查询即基于两个或两个以上的表查询
#笛卡尔集
mysql> select count(*) from dept,emp,salgrade;
+----------+
| count(*) |
+----------+
|      260 |
+----------+
count（*）的结果为每个表的行数相X（乘）count（*）=dept.rows x emp.rows x salgrade 笛卡尔集
1 row in set (0.01 sec)
-- 避免出现笛卡尔集 Tip：多表查询的条件不能少于 表的个数 - 1；
mysql> select ename,sal,emp.deptno from emp,dept where emp.deptno=dept.deptno;-- 可以给两个表限制条件进行查询（思考过滤条件）
-- 如果多表中出现同名列 则需要使用 表名.列名 的形式指明列 否则系统无法识别会报错
+--------+---------+--------+
| ename  | sal     | deptno |
+--------+---------+--------+
| SMITH  |  800.00 |     20 |
| ALLEN  | 1600.00 |     30 |
| WARD   | 1250.00 |     30 |
| JONES  | 2975.00 |     20 |
| MARTIN | 1250.00 |     30 |
| BLAKE  | 2850.00 |     30 |
| CLARK  | 2450.00 |     10 |
| SCOTT  | 3000.00 |     20 |
| KING   | 5000.00 |     10 |
| TURNER | 1500.00 |     30 |
| JAMES  |  950.00 |     30 |
| FORD   | 3000.00 |     20 |
| MILLER | 1300.00 |     10 |
+--------+---------+--------+
13 rows in set (0.00 sec)

-- For instance 查询显示员工的姓名 工资 以及 工资等级
mysql> select ename,sal,grade from emp,salgrade where emp.sal between salgrade.losal and salgrade.hisal
    -> ;
+--------+---------+-------+
| ename  | sal     | grade |
+--------+---------+-------+
| SMITH  |  800.00 |     1 |
| ALLEN  | 1600.00 |     3 |
| WARD   | 1250.00 |     2 |
| JONES  | 2975.00 |     4 |
| MARTIN | 1250.00 |     2 |
| BLAKE  | 2850.00 |     4 |
| CLARK  | 2450.00 |     4 |
| SCOTT  | 3000.00 |     4 |
| KING   | 5000.00 |     5 |
| TURNER | 1500.00 |     3 |
| JAMES  |  950.00 |     1 |
| FORD   | 3000.00 |     4 |
| MILLER | 1300.00 |     2 |
+--------+---------+-------+
13 rows in set (0.00 sec)
```

##### 子查询

```sql
#子查询-- 嵌套查询
-- For instance
-- 查询和smith同一个部门的所有员工  先查出smith所在部门 然后查此部门的所有员工
mysql> select * from emp where deptno = (select deptno from emp where ename = 'SMITH');
+-------+-------+---------+------+------------+---------+------+--------+
| empno | ename | job     | mgr  | hiredate   | sal     | comm | deptno |
+-------+-------+---------+------+------------+---------+------+--------+
|  7369 | SMITH | clerk   | 7902 | 1990-12-17 |  800.00 | NULL |     20 |
|  7566 | JONES | manager | 7839 | 1991-04-02 | 2975.00 | NULL |     20 |
|  7788 | SCOTT | analyst | 7566 | 1997-04-19 | 3000.00 | NULL |     20 |
|  7902 | FORD  | analyst | 7566 | 1991-12-03 | 3000.00 | NULL |     20 |
+-------+-------+---------+------+------------+---------+------+--------+
4 rows in set (0.00 sec)

```

##### 多行子查询

```sql
#多行子查询 嵌套查询 子查询返回的是多行的情况-- Tip:where后的条件返回的是多行时 要使用关键字 IN 
-- For instance
-- 查询和20号部门的工作相同的雇员的 姓名 岗位 工资 部门号 但是不包含20号部门中的雇员
mysql> select ename,job,sal,deptno from emp
    -> where job IN (select distinct job from emp where deptno = 20) AND deptno <> 20
    -> ;
+--------+---------+---------+--------+
| ename  | job     | sal     | deptno |
+--------+---------+---------+--------+
| BLAKE  | manager | 2850.00 |     30 |
| CLARK  | manager | 2450.00 |     10 |
| JAMES  | clerk   |  950.00 |     30 |
| MILLER | clerk   | 1300.00 |     10 |
+--------+---------+---------+--------+
4 rows in set (0.00 sec)
```

##### 临时表

```sql
#子查询当作临时表来使用
-- For instance
-- 查询ecshop中各个类别中 价格最高的goods-- 可以将子查询作为一张临时表来使用
mysql> select goods_id,cat_id,goods_name,shop_price from ecs_goods;
+----------+--------+----------------------------------------+------------+
| goods_id | cat_id | goods_name                             | shop_price |
+----------+--------+----------------------------------------+------------+
|        1 |      4 | KD876                                  |    1388.00 |
|        4 |      8 | 诺基亚N85原装充电器                    |      58.00 |
|        3 |      8 | 诺基亚原装5800耳机                     |      68.00 |
|        5 |     11 | 索爱原装M2卡读卡器                     |      20.00 |
|        6 |     11 | 胜创KINGMAX内存卡                      |      42.00 |
|        7 |      8 | 诺基亚N85原装立体声耳机HS-82           |     100.00 |
|        8 |      3 | 飞利浦9@9v                             |     399.00 |
|        9 |      3 | 诺基亚E66                              |    2298.00 |
|       10 |      3 | 索爱C702c                              |    1328.00 |
|       11 |      3 | 索爱C702c                              |    1300.00 |
|       12 |      3 | 摩托罗拉A810                           |     983.00 |
|       13 |      3 | 诺基亚5320 XpressMusic                 |    1311.00 |
|       14 |      4 | 诺基亚5800XM                           |    2625.00 |
|       15 |      3 | 摩托罗拉A810                           |     788.00 |
|       16 |      2 | 恒基伟业G101                           |     823.33 |
|       17 |      3 | 夏新N7                                 |    2300.00 |
|       18 |      4 | 夏新T5                                 |    2878.00 |
|       19 |      3 | 三星SGH-F258                           |     858.00 |
|       20 |      3 | 三星BC01                               |     280.00 |
|       21 |      3 | 金立 A30                               |    2000.00 |
|       22 |      3 | 多普达Touch HD                         |    5999.00 |
|       23 |      5 | 诺基亚N96                              |    3700.00 |
|       24 |      3 | P806                                   |    2000.00 |
|       25 |     13 | 小灵通/固话50元充值卡                  |      48.00 |
|       26 |     13 | 小灵通/固话20元充值卡                  |      19.00 |
|       27 |     15 | 联通100元充值卡                        |      95.00 |
|       28 |     15 | 联通50元充值卡                         |      45.00 |
|       29 |     14 | 移动100元充值卡                        |      90.00 |
|       30 |     14 | 移动20元充值卡                         |      18.00 |
|       31 |      3 | 摩托罗拉E8                             |    1337.00 |
|       32 |      3 | 诺基亚N85                              |    3010.00 |
+----------+--------+----------------------------------------+------------+
31 rows in set (0.00 sec)

mysql> select goods_id,ecs_goods.cat_id,goods_name,shop_price
-- 此处from后的表可以使用select出的子查询作为临时表 并给临时表另名
    -> from (select cat_id,MAX(shop_price) as 'max_shop_price' from ecs_goods GROUP BY cat_id) temp,ecs_goods
    -> where temp.cat_id=ecs_goods.cat_id and max_shop_price = shop_price
    -> ;
+----------+--------+----------------------------------------+------------+
| goods_id | cat_id | goods_name                             | shop_price |
+----------+--------+----------------------------------------+------------+
|       16 |      2 | 恒基伟业G101                           |     823.33 |
|       22 |      3 | 多普达Touch HD                         |    5999.00 |
|       18 |      4 | 夏新T5                                 |    2878.00 |
|       23 |      5 | 诺基亚N96                              |    3700.00 |
|        7 |      8 | 诺基亚N85原装立体声耳机HS-82           |     100.00 |
|        6 |     11 | 胜创KINGMAX内存卡                      |      42.00 |
|       25 |     13 | 小灵通/固话50元充值卡                  |      48.00 |
|       29 |     14 | 移动100元充值卡                        |      90.00 |
|       27 |     15 | 联通100元充值卡                        |      95.00 |
+----------+--------+----------------------------------------+------------+
9 rows in set (0.00 sec)

```

##### all&any的使用

```sql
#all&any的使用
-- all 表示所有
-- For instance
-- 显示工资比部门30的所有员工都要高的员工的姓名，工资和部门号-- 相当于比最高还要高
mysql> select ename,sal,deptno from emp
    -> where sal > ALL(select sal from emp where deptno=30);
+-------+---------+--------+
| ename | sal     | deptno |
+-------+---------+--------+
| JONES | 2975.00 |     20 |
| SCOTT | 3000.00 |     20 |
| KING  | 5000.00 |     10 |
| FORD  | 3000.00 |     20 |
+-------+---------+--------+
4 rows in set (0.00 sec)

-- any 表示任何一个
-- For instance
-- 显示工资比部分30中的其中任意一个员工工资高的员工的姓名，工资和部门号-- 相当于只要比最低的到
mysql> select ename,sal,deptno from emp
    -> where sal > any(select sal from emp where deptno = 30);
+--------+---------+--------+
| ename  | sal     | deptno |
+--------+---------+--------+
| ALLEN  | 1600.00 |     30 |
| WARD   | 1250.00 |     30 |
| JONES  | 2975.00 |     20 |
| MARTIN | 1250.00 |     30 |
| BLAKE  | 2850.00 |     30 |
| CLARK  | 2450.00 |     10 |
| SCOTT  | 3000.00 |     20 |
| KING   | 5000.00 |     10 |
| TURNER | 1500.00 |     30 |
| FORD   | 3000.00 |     20 |
| MILLER | 1300.00 |     10 |
+--------+---------+--------+
11 rows in set (0.00 sec)
```

##### 多列子查询

```sql
#多列子查询
-- 子查询结果为多列的 --（列名，列名）= （子查询）
-- For instance
-- 查询和ALLEN的部门和岗位完全相同的所有雇员（并不包含ALLEN本人）
mysql> select * from emp
    -> where (deptno,job) = (select deptno,job from emp where ename = 'ALLEN') AND ename <> 'ALLEN'
    -> ;
+-------+--------+----------+------+------------+---------+---------+--------+
| empno | ename  | job      | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+----------+------+------------+---------+---------+--------+
|  7521 | WARD   | salesman | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7654 | MARTIN | salesman | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7844 | TURNER | salesman | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
+-------+--------+----------+------+------------+---------+---------+--------+
3 rows in set (0.00 sec)

-- For instance
-- 查询和宋江 数学，英语，语文成绩完全相同的同学
mysql> select * from student
    -> where (chinese,english,math) = (select chinese,english,math from student where name = '宋江');
+----+--------+---------+---------+------+
| id | name   | chinese | english | math |
+----+--------+---------+---------+------+
|  3 | 宋江   |      87 |      78 |   77 |
+----+--------+---------+---------+------+
1 row in set (0.00 sec)

-- For instance
-- -- 查询每个部门工资高于本部门平均工资水平的人的数据
select * from emp;
-- 首先列出每个部门的平均工资
select avg(sal) as '平均工资',deptno from emp GROUP BY deptno;
-- 将每个部门的平均工资和部门的多列结果作为子查询并命为临时表
select ename,emp.sal,emp.deptno,temp.`平均工资`
from emp,(select avg(sal) as '平均工资',deptno from emp GROUP BY deptno) temp 
where emp.deptno = temp.deptno and emp.sal > temp.`平均工资`
ORDER BY emp.deptno DESC;

mysql> select ename,emp.sal,emp.deptno,temp.`平均工资`
    -> from emp,(select avg(sal) as '平均工资',deptno from emp GROUP BY deptno) temp
    -> where emp.deptno = temp.deptno and emp.sal > temp.`平均工资`
    -> ORDER BY emp.deptno DESC;
+-------+---------+--------+--------------+
| ename | sal     | deptno | 平均工资     |
+-------+---------+--------+--------------+
| BLAKE | 2850.00 |     30 |  1566.666667 |
| ALLEN | 1600.00 |     30 |  1566.666667 |
| FORD  | 3000.00 |     20 |  2443.750000 |
| SCOTT | 3000.00 |     20 |  2443.750000 |
| JONES | 2975.00 |     20 |  2443.750000 |
| KING  | 5000.00 |     10 |  2916.666667 |
+-------+---------+--------+--------------+
6 rows in set (0.00 sec)

-- For instance
-- 显示每个部门的信息包括（部门名，编号，地址） 和人员的数量
-- 首先先显示部门的信息（部门名，编号，地址）
select dept.deptno,dept.dname,dept.loc from dept;

mysql> select dept.deptno,dept.dname,dept.loc from dept;
+--------+------------+----------+
| deptno | dname      | loc      |
+--------+------------+----------+
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
|     40 | OPERATIONS | BOSTON   |
+--------+------------+----------+
4 rows in set (0.00 sec)
mysql> select dept.* from dept;-- select 列名.* from dept;表名将此表中的所有列的显示出来
+--------+------------+----------+
| deptno | dname      | loc      |
+--------+------------+----------+
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
|     40 | OPERATIONS | BOSTON   |
+--------+------------+----------+
4 rows in set (0.00 sec)

mysql>
select dept.deptno,dept.dname,dept.loc,temp.`部门的人员数量`
from dept,(select emp.deptno,count(emp.deptno) as '部门的人员数量' from emp GROUP BY emp.deptno) temp
where temp.deptno = dept.deptno;

mysql> select dept.deptno,dept.dname,dept.loc,temp.`部门的人员数量`
    -> from dept,(select emp.deptno,count(emp.deptno) as '部门的人员数量' from emp GROUP BY emp.deptno) temp
    -> where temp.deptno = dept.deptno;
+--------+------------+----------+-----------------------+
| deptno | dname      | loc      | 部门的人员数量        |
+--------+------------+----------+-----------------------+
|     10 | ACCOUNTING | NEW YORK |                     3 |
|     20 | RESEARCH   | DALLAS   |                     4 |
|     30 | SALES      | CHICAGO  |                     6 |
+--------+------------+----------+-----------------------+
3 rows in set (0.00 sec)


```

##### 表复制

```sql
#表复制-- 自我复制（蠕虫复制）
-- 创建一个和student表相同结构的my_student表
create table my_student1 like my_student;-- 可以使用create table 新表 like 需要引用结构的表
create table my_student (
  `id` int NOT NULL DEFAULT '1',
  `name` varchar(20) COLLATE utf8mb3_bin NOT NULL DEFAULT '',
  `chinese` float NOT NULL DEFAULT '0',
  `english` float NOT NULL DEFAULT '0',
  `math` float NOT NULL DEFAULT '0'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 COLLATE=utf8mb3_bin
-- 将student表insert into进my_student表
insert into my_student select * from student;
-- my_student表进行多次的自我复制（蠕虫复制）
insert into my_student select * from my_student;
select count(*) from my_student;
mysql> select count(*) from my_student;
+----------+
| count(*) |
+----------+
|      224 |
+----------+
1 row in set (0.00 sec)

```

##### 表去重

```sql
#表去重
-- 思路 
-- ①创建一个临时表的结构与想要去重的表的结构一致 
-- ②对临时表进行distinct去重 
-- ③将想要去重的表的数据全部删除 
-- ④将临时表的数据insert into进原表 
-- ⑤drop零时表

-- 实现流程
-- 创建一个临时表的结构与想要去重的表的结构一致 
create table temp_table like my_student;
-- 对临时表进行distinct去重 
insert into temp_table select distinct * from my_student;
-- 将想要去重的表的数据全部删除
delete from my_student;
-- 将临时表的数据insert into进原表
insert into my_student select * from temp_table;
-- drop零时表
drop table temp_table;
```

##### UNION操作符 合并查询

```sql
#UNION
#MySQL UNION 操作符用于连接两个以上的 SELECT 语句的结果组合到一个结果集合中。多个 SELECT 语句会删除重复的数据。
#MySQL UNION 操作符语法格式：
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions]
UNION [ALL | DISTINCT]
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions];
#参数
expression1, expression2, ... expression_n: 要检索的列。

tables: 要检索的数据表。

WHERE conditions: 可选， 检索条件。

DISTINCT: 可选，删除结果集中重复的数据。默认情况下 UNION 操作符已经删除了重复数据，所以 DISTINCT 修饰符对结果没啥影响。

ALL: 可选，返回所有结果集，包含重复数据
-- tip:
UNION 语句：用于将不同表中相同列中查询的数据展示出来；（不包括重复数据）

UNION ALL 语句：用于将不同表中相同列中查询的数据展示出来；（包括重复数据）

使用形式如下：

SELECT 列名称 FROM 表名称 UNION SELECT 列名称 FROM 表名称 ORDER BY 列名称；
SELECT 列名称 FROM 表名称 UNION ALL SELECT 列名称 FROM 表名称 ORDER BY 列名称；
```

#### 函数★

##### 统计函数

```sql
# SQL 函数

------

SQL 拥有很多可用于计数和计算的内建函数。

------

## SQL Aggregate 函数

SQL Aggregate 函数计算从列中取得的值，返回一个单一的值。

有用的 Aggregate 函数：

- AVG() - 返回平均值
- COUNT() - 返回行数
- FIRST() - 返回第一个记录的值
- LAST() - 返回最后一个记录的值
- MAX() - 返回最大值
- MIN() - 返回最小值
- SUM() - 返回总和

------
# SQL COUNT() 函数

------

COUNT() 函数返回匹配指定条件的行数。

------

### SQL COUNT(column_name) 语法

COUNT(column_name) 函数返回指定列的值的数目（NULL 不计入）：-- 统计满足条件的某列有多少个（会排除null）

SELECT COUNT(column_name) FROM table_name;

### SQL COUNT(*) 语法

COUNT(*) 函数返回表中的记录数：-- 返回满足条件的记录的行数

SELECT COUNT(*) FROM table_name;

### SQL COUNT(DISTINCT column_name) 语法

COUNT(DISTINCT column_name) 函数返回指定列的不同值的数目：

SELECT COUNT(DISTINCT column_name) FROM table_name;

**注释：**COUNT(DISTINCT) 适用于 ORACLE 和 Microsoft SQL Server，但是无法用于 Microsoft Access

-- For instance
mysql> select * from access1;
+------+---------+-------+------------+
| aid  | site_id | count | date       |
+------+---------+-------+------------+
|    1 |       1 |    45 | 2016-05-10 |
|    2 |       3 |   100 | 2016-05-13 |
|    3 |       1 |   230 | 2016-05-14 |
|    4 |       2 |    10 | 2016-05-14 |
|    5 |       5 |   205 | 2016-05-14 |
|    6 |       4 |    13 | 2016-05-15 |
|    7 |       3 |   220 | 2016-05-15 |
|    8 |       5 |   545 | 2016-05-16 |
|    9 |       3 |   201 | 2016-05-17 |
|   10 |       3 |  NULL | 2016-05-25 |
|   11 |       3 |  NULL | 2016-05-26 |
+------+---------+-------+------------+
11 rows in set (0.00 sec)

mysql> select count(*) from access1 where site_id=3;-- 返回满足条件的记录的行数
+----------+
| count(*) |
+----------+
|        5 |
+----------+
1 row in set (0.00 sec)

mysql> select count(count) from access1 where site_id=3;-- 统计满足条件的某列有多少个（会排除null）
+--------------+
| count(count) |
+--------------+
|            3 |
+--------------+
1 row in set (0.00 sec)

mysql> select count(distinct site_id) from access1 where site_id=3;-- 函数返回指定列的不同值（非重复）的数目：
+-------------------------+
| count(distinct site_id) |
+-------------------------+
|                       1 |
+-------------------------+
1 row in set (0.01 sec)

mysql> select count(site_id) from access1 where site_id=3;
+----------------+
| count(site_id) |
+----------------+
|              5 |
+----------------+
1 row in set (0.00 sec)

#AVG() 函数
AVG() 函数返回数值列的平均值。

SQL AVG() 语法
SELECT AVG(column_name) FROM table_name

-- For instance
mysql> select * from access1;
+------+---------+-------+------------+
| aid  | site_id | count | date       |
+------+---------+-------+------------+
|    1 |       1 |    45 | 2016-05-10 |
|    2 |       3 |   100 | 2016-05-13 |
|    3 |       1 |   230 | 2016-05-14 |
|    4 |       2 |    10 | 2016-05-14 |
|    5 |       5 |   205 | 2016-05-14 |
|    6 |       4 |    13 | 2016-05-15 |
|    7 |       3 |   220 | 2016-05-15 |
|    8 |       5 |   545 | 2016-05-16 |
|    9 |       3 |   201 | 2016-05-17 |
|   10 |       3 |  NULL | 2016-05-25 |
|   11 |       3 |  NULL | 2016-05-26 |
+------+---------+-------+------------+
11 rows in set (0.01 sec)

mysql> select average(count) from access1;
ERROR 1305 (42000): FUNCTION db02.average does not exist
mysql> select avg(count) as `CountAverage` from access1;
+--------------+
| CountAverage |
+--------------+
|     174.3333 |
+--------------+
1 row in set (0.00 sec)

mysql> select site_id from access1 where count >= (select avg(count) from access1);
+---------+
| site_id |
+---------+
|       1 |
|       5 |
|       3 |
|       5 |
|       3 |
+---------+
5 rows in set (0.13 sec)

mysql> select site_id,count from access1 where count >= (select avg(count) from access1);
+---------+-------+
| site_id | count |
+---------+-------+
|       1 |   230 |
|       5 |   205 |
|       3 |   220 |
|       5 |   545 |
|       3 |   201 |
+---------+-------+
5 rows in set (0.00 sec)

#SUM() 函数
SUM() 函数返回数值列的总数。

SQL SUM() 语法
SELECT SUM(column_name) FROM table_name;-- 仅对数值起作用

-- For instance
mysql> select * from student_score1;
+-----------+--------+------------+---------------+---------------+
| name      | number | Math_score | Chinese_score | English_score |
+-----------+--------+------------+---------------+---------------+
| 张锦豪    |   1001 |         99 |            95 |            91 |
| 欧文      |   1002 |         92 |            94 |            99 |
| 詹姆斯    |   1003 |         93 |            95 |            99 |
| 杜兰特    |   1004 |         92 |            91 |            99 |
| 库里      |   1005 |         92 |            92 |            98 |
| 哈登      |   1006 |         90 |            91 |            94 |
| 东七七    |   1007 |         91 |            93 |            98 |
+-----------+--------+------------+---------------+---------------+
7 rows in set (0.00 sec)

mysql> select sum(Math_score + Chinese_score + English_score) as sum_score from student_score1;
+-----------+
| sum_score |
+-----------+
|      1978 |
+-----------+
1 row in set (0.00 sec)

mysql> select sum(Math_score + Chinese_score + English_score) / count(*) as sum_score from student_score1;
+--------------------+
| sum_score          |
+--------------------+
| 282.57142857142856 |
+--------------------+
1 row in set (0.00 sec)

mysql>

#MAX() 函数
MAX() 函数返回指定列的最大值。

SQL MAX() 语法
SELECT MAX(column_name) FROM table_name;
#MIN() 函数
MIN() 函数返回指定列的最小值。

SQL MIN() 语法
SELECT MIN(column_name) FROM table_name;

-- For instance
mysql> select * from access1;
+------+---------+-------+------------+
| aid  | site_id | count | date       |
+------+---------+-------+------------+
|    1 |       1 |    45 | 2016-05-10 |
|    2 |       3 |   100 | 2016-05-13 |
|    3 |       1 |   230 | 2016-05-14 |
|    4 |       2 |    10 | 2016-05-14 |
|    5 |       5 |   205 | 2016-05-14 |
|    6 |       4 |    13 | 2016-05-15 |
|    7 |       3 |   220 | 2016-05-15 |
|    8 |       5 |   545 | 2016-05-16 |
|    9 |       3 |   201 | 2016-05-17 |
|   10 |       3 |  NULL | 2016-05-25 |
|   11 |       3 |  NULL | 2016-05-26 |
+------+---------+-------+------------+
11 rows in set (0.00 sec)

mysql> select max(Math_score + Chinese_score + English_score) as max_sum_score from student_score1;
+---------------+
| max_sum_score |
+---------------+
|           287 |
+---------------+
1 row in set (0.00 sec)

mysql>
mysql> select min(Math_score + Chinese_score + English_score) as min_sum_score from student_score1;
+---------------+
| min_sum_score |
+---------------+
|           275 |
+---------------+
1 row in set (0.00 sec)

mysql>

#SQL GROUP BY 语句
GROUP BY 语句
GROUP BY 语句用于结合聚合函数，根据一个或多个列对结果集进行分组。

SQL GROUP BY 语法
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name;
#SQL HAVING 子句
HAVING 子句
在 SQL 中增加 HAVING 子句原因是，WHERE 关键字无法与聚合函数一起使用。

HAVING 子句可以让我们筛选分组后的各组数据。

SQL HAVING 语法
SQL HAVING 语法
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name) operator value;

-- For instance
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7900 | JAMES  | CLERK     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

mysql> CREATE TABLE salgrade
    -> (
    -> grade MEDIUMINT UNSIGNED NOT NULL DEFAULT 0, /*工资级别*/
    -> losal DECIMAL(17,2) NOT NULL, /* 该级别的最低工资 */
    -> hisal DECIMAL(17,2) NOT NULL /* 该级别的最高工资*/
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> INSERT INTO salgrade VALUES (1,700,1200);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO salgrade VALUES (2,1201,1400);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO salgrade VALUES (3,1401,2000);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO salgrade VALUES (4,2001,3000);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO salgrade VALUES (5,3001,9999);
Query OK, 1 row affected (0.00 sec)

mysql> select * from salgrade;
+-------+---------+---------+
| grade | losal   | hisal   |
+-------+---------+---------+
|     1 |  700.00 | 1200.00 |
|     2 | 1201.00 | 1400.00 |
|     3 | 1401.00 | 2000.00 |
|     4 | 2001.00 | 3000.00 |
|     5 | 3001.00 | 9999.00 |
+-------+---------+---------+
5 rows in set (0.00 sec)

mysql> select avg(sal) as `avg`,max(sal) as `max` from emp;
+-------------+---------+
| avg         | max     |
+-------------+---------+
| 2148.076923 | 5000.00 |
+-------------+---------+
1 row in set (0.00 sec)

mysql> select avg(sal),max(sal),deptno from emp group by deptno;-- group by 根据列进行分组
+-------------+----------+--------+
| avg(sal)    | max(sal) | deptno |
+-------------+----------+--------+
| 2443.750000 |  3000.00 |     20 |
| 1566.666667 |  2850.00 |     30 |
| 2916.666667 |  5000.00 |     10 |
+-------------+----------+--------+
3 rows in set (0.00 sec)

mysql> select avg(sal),max(sal),deptno from emp group by deptno having avg(sal)>2000.00;-- group by 根据列进行分组 having 条件筛选
+-------------+----------+--------+
| avg(sal)    | max(sal) | deptno |
+-------------+----------+--------+
| 2443.750000 |  3000.00 |     20 |
| 2916.666667 |  5000.00 |     10 |
+-------------+----------+--------+
2 rows in set (0.00 sec)


```



##### 时间日期

```sql
#CURDATE()	返回当前日期	
SELECT CURDATE();
-> 2018-09-19
#CURRENT_DATE()	返回当前日期	
SELECT CURRENT_DATE();
-> 2018-09-19

#CURRENT_TIME	返回当前时间	
SELECT CURRENT_TIME();
-> 19:59:02

#LAST_DAY   返回某个月的最后一天
mysql> select last_day(now());
+-----------------+
| last_day(now()) |
+-----------------+
| 2022-09-30      |
+-----------------+
1 row in set (0.00 sec)

mysql> select LAST_DAY('2022-08-04');
+------------------------+
| LAST_DAY('2022-08-04') |
+------------------------+
| 2022-08-31             |
+------------------------+
1 row in set (0.00 sec)

#CURTIME()	返回当前时间	
SELECT CURTIME();
-> 19:59:02

#CURRENT_TIMESTAMP()	返回当前日期和时间(时间戳)	
SELECT CURRENT_TIMESTAMP()
-> 2018-09-19 20:57:43

#DATE()	从日期或日期时间表达式中提取日期值	
SELECT DATE("2017-06-15");    
-> 2017-06-15
-- For instance
mysql> select current_timestamp();
+---------------------+
| current_timestamp() |
+---------------------+
| 2022-09-02 19:38:25 |
+---------------------+
1 row in set (0.00 sec)

mysql> select date(current_timestamp());
+---------------------------+
| date(current_timestamp()) |
+---------------------------+
| 2022-09-02                |
+---------------------------+
1 row in set (0.00 sec)

#DATE_ADD(d，INTERVAL expr type)	计算起始日期 d 加上一个时间段后的日期，type 值可以是：
MICROSECOND
SECOND
MINUTE
HOUR
DAY
WEEK
MONTH
QUARTER
YEAR
SECOND_MICROSECOND
MINUTE_MICROSECOND
MINUTE_SECOND
HOUR_MICROSECOND
HOUR_SECOND
HOUR_MINUTE
DAY_MICROSECOND
DAY_SECOND
DAY_MINUTE
DAY_HOUR
YEAR_MONTH
SELECT DATE_ADD("2017-06-15", INTERVAL 10 DAY);    
-> 2017-06-25

SELECT DATE_ADD("2017-06-15 09:34:21", INTERVAL 15 MINUTE);
-> 2017-06-15 09:49:21

SELECT DATE_ADD("2017-06-15 09:34:21", INTERVAL -3 HOUR);
->2017-06-15 06:34:21

SELECT DATE_ADD("2017-06-15 09:34:21", INTERVAL -3 MONTH);
->2017-04-15
-- For instance
mysql> select current_timestamp();
+---------------------+
| current_timestamp() |
+---------------------+
| 2022-09-02 19:43:51 |
+---------------------+
1 row in set (0.00 sec)
mysql> select date_add(current_timestamp(),interval 3 month);
+------------------------------------------------+
| date_add(current_timestamp(),interval 3 month) |
+------------------------------------------------+
| 2022-12-02 19:43:08                            |
+------------------------------------------------+
1 row in set (0.00 sec)

-- 开发中常用:判断是否于某个时间段内的
-- 查看员工表中工龄达到31year的员工及其入职日期



#DATE_SUB(date,INTERVAL expr type)	函数从日期减去指定的时间间隔。	
Orders 表中 OrderDate 字段减去 2 天：
SELECT OrderId,DATE_SUB(OrderDate,INTERVAL 2 DAY) AS OrderPayDate
FROM Orders
-- For instance
mysql> select current_timestamp();
+---------------------+
| current_timestamp() |
+---------------------+
| 2022-09-02 19:43:51 |
+---------------------+
1 row in set (0.00 sec)

mysql> select date_sub(current_timestamp(),interval 3 month);
+------------------------------------------------+
| date_sub(current_timestamp(),interval 3 month) |
+------------------------------------------------+
| 2022-06-02 19:46:16                            |
+------------------------------------------------+
1 row in set (0.00 sec)

#TIMEDIFF(time1, time2)	计算时间差值	单位是 时:分:秒
mysql> SELECT TIMEDIFF("13:10:11", "13:10:10");
-> 00:00:01
mysql> SELECT TIMEDIFF('2000:01:01 00:00:00',
    ->                 '2000:01:01 00:00:00.000001');
        -> '-00:00:00.000001'
mysql> SELECT TIMEDIFF('2008-12-31 23:59:59.000001',
    ->                 '2008-12-30 01:01:01.000002');
        -> '46:58:57.999999'

#DATEDIFF(d1,d2)	计算日期 d1->d2 之间相隔的天数	单位是 天
SELECT DATEDIFF('2001-01-01','2001-02-02')
-> -32
-- 假设活到80岁 看看从现在开始还能活几天
mysql> select datediff(date_add('2001-01-01',interval 80 year),current_date);
+----------------------------------------------------------------+
| datediff(date_add('2001-01-01',interval 80 year),current_date) |
+----------------------------------------------------------------+
|                                                          21306 |
+----------------------------------------------------------------+
1 row in set (0.00 sec)

#TO_DAYS(d)	计算日期 d 距离 0000 年 1 月 1 日的天数	
SELECT TO_DAYS('0001-01-01 01:01:01')
-> 366

#NOW()	返回当前日期和时间	
SELECT NOW()
-> 2018-09-19 20:57:43
-- For instance
mysql> select now();
+---------------------+
| now()               |
+---------------------+
| 2022-09-02 19:50:49 |
+---------------------+
1 row in set (0.00 sec)

mysql> select year(now());
+-------------+
| year(now()) |
+-------------+
|        2022 |
+-------------+
1 row in set (0.00 sec)

mysql> select month(now());
+--------------+
| month(now()) |
+--------------+
|            9 |
+--------------+
1 row in set (0.00 sec)

mysql> select day(now());
+------------+
| day(now()) |
+------------+
|          2 |
+------------+
1 row in set (0.00 sec)

# unix_timestamp()返回1970年1月1日至此的毫秒数
mysql> select unix_timestamp();
+------------------+
| unix_timestamp() |
+------------------+
|       1662128229 |
+------------------+
1 row in set (0.00 sec)

# from_unixtime(一个时间戳,'指定格式')-- 可以把时间戳转成指定的格式
-- 在开发中会使用一个int来保存unix时间戳 然后进行转换
mysql> select from_unixtime(1662128229,'%y-%m-%d');-- 固定格式
+--------------------------------------+
| from_unixtime(1662128229,'%y-%m-%d') |
+--------------------------------------+
| 22-09-02                             |
+--------------------------------------+
1 row in set (0.00 sec)
mysql> select from_unixtime(1662128229,'%Y-%m-%d');-- 固定格式
+--------------------------------------+
| from_unixtime(1662128229,'%Y-%m-%d') |
+--------------------------------------+
| 2022-09-02                           |
+--------------------------------------+
1 row in set (0.00 sec)
mysql> select from_unixtime(1662128229,'%Y-%m-%d %H:%i:%s');-- 固定格式
+-----------------------------------------------+
| from_unixtime(1662128229,'%Y-%m-%d %H:%i:%s') |
+-----------------------------------------------+
| 2022-09-02 22:17:09                           |
+-----------------------------------------------+
1 row in set (0.00 sec)
```



##### 字符串函数

```sql
## SQL Scalar 函数

SQL Scalar 函数基于输入值，返回一个单一的值。

有用的 Scalar 函数：

- UCASE() - 将某个字段转换为大写
- LCASE() - 将某个字段转换为小写
- MID() - 从某个文本字段提取字符，MySql 中使用
- SubString(字段，1，end) - 从某个文本字段提取字符
- LEN() - 返回某个文本字段的长度
- ROUND() - 对某个数值字段进行指定小数位数的四舍五入
- NOW() - 返回当前的系统日期和时间
- FORMAT() - 格式化某个字段的显示方式

#UCASE() 函数
UCASE() 函数把字段的值转换为大写。

SQL UCASE() 语法
SELECT UCASE(column_name) FROM table_name;
用于 SQL Server 的语法
SELECT UPPER(column_name) FROM table_name;
-- For instance
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | salesman  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | salesman  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | salesman  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | president | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | salesman  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7900 | JAMES  | clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

mysql> update emp set job=ucase(job) where job='salesman';
Query OK, 4 rows affected (0.00 sec)
Rows matched: 4  Changed: 4  Warnings: 0

mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | president | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7900 | JAMES  | clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

#LCASE() 函数
LCASE() 函数把字段的值转换为小写。

SQL LCASE() 语法
SELECT LCASE(column_name) FROM table_name;
用于 SQL Server 的语法
SELECT LOWER(column_name) FROM table_name;

-- For instance
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | president | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7900 | JAMES  | clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

mysql> update emp set job=lcase(job) where job='SALESMAN';
Query OK, 4 rows affected (0.00 sec)
Rows matched: 4  Changed: 4  Warnings: 0

mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | salesman  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | salesman  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | salesman  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | president | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | salesman  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7900 | JAMES  | clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

#MID() 函数
-- MID() 函数用于从文本字段中提取字符。-- 相当于substr
SQL MID()
SELECT MID(column_name,start[,length]) FROM table_name;
-- 参数	       描述
-- column_name	必需。要提取字符的字段。
-- start	    必需。规定开始位置（起始值是 1）。
-- length	    可选。要返回的字符数。如果省略，则 MID() 函数返回剩余文本。

-- For instance
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | salesman  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | salesman  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | salesman  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | president | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | salesman  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7900 | JAMES  | clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

mysql> select mid(hiredate,1,4) from emp;
+-------------------+
| mid(hiredate,1,4) |
+-------------------+
| 1990              |
| 1991              |
| 1991              |
| 1991              |
| 1991              |
| 1991              |
| 1991              |
| 1997              |
| 1991              |
| 1991              |
| 1991              |
| 1991              |
| 1992              |
+-------------------+
13 rows in set (0.00 sec)

mysql> select mid(hiredate,1) as 'HireDate' from emp;-- length	    可选。要返回的字符数。如果省略，则 MID() 函数返回剩余文本。
+------------+
| HireDate   |
+------------+
| 1990-12-17 |
| 1991-02-20 |
| 1991-02-22 |
| 1991-04-02 |
| 1991-09-28 |
| 1991-05-01 |
| 1991-06-09 |
| 1997-04-19 |
| 1991-11-17 |
| 1991-09-08 |
| 1991-12-03 |
| 1991-12-03 |
| 1992-01-23 |
+------------+
13 rows in set (0.00 sec)

mysql>

#LEN() 函数
LEN() 函数返回文本字段中值的长度。

SQL LEN() 语法
SELECT LEN(column_name) FROM table_name;
MySQL 中函数为 LENGTH():

SELECT LENGTH(column_name) FROM table_name;

mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | salesman  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | salesman  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | salesman  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | president | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | salesman  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7900 | JAMES  | clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

mysql> select length(ename) as 'EmployeeNameLength' from emp;
+--------------------+
| EmployeeNameLength |
+--------------------+
|                  5 |
|                  5 |
|                  4 |
|                  5 |
|                  6 |
|                  5 |
|                  5 |
|                  5 |
|                  4 |
|                  6 |
|                  5 |
|                  4 |
|                  6 |
+--------------------+
13 rows in set (0.00 sec)

mysql>

#CONCAT(s1,s2...sn)	字符串 s1,s2 等多个字符串合并为一个字符串	
-- 合并多个字符串

SELECT CONCAT("SQL ", "Runoob ", "Gooogle ", "Facebook") AS ConcatenatedString;

-- For instance
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | salesman  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | salesman  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | salesman  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | president | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | salesman  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7900 | JAMES  | clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

mysql> select concat(ename,"--",job) from emp where sal>=3000.00;
+------------------------+
| concat(ename,"--",job) |
+------------------------+
| SCOTT--analyst         |
| KING--president        |
| FORD--analyst          |
+------------------------+
3 rows in set (0.00 sec)

#CONCAT(s1,s2...sn)	字符串 s1,s2 等多个字符串合并为一个字符串 可以是运算或者日期加上字符串合并成一个字符串
mysql> select ename,CONCAT('已入职:',TRUNCATE((DATEDIFF(now(),hiredate)/365),0),'年',TRUNCATE((TRUNCATE((DATEDIFF(now(),hiredate)%365),0))/30,0),'月',
    -> TRUNCATE((TRUNCATE((DATEDIFF(now(),hiredate)%365),0))%30,0),'天') AS '入职年限' from emp;
+--------+---------------------------+
| ename  | 入职年限                  |
+--------+---------------------------+
| SMITH  | 已入职:31年9月1天         |
| ALLEN  | 已入职:31年6月26天        |
| WARD   | 已入职:31年6月24天        |
| JONES  | 已入职:31年5月15天        |
| MARTIN | 已入职:30年11月21天       |
| BLAKE  | 已入职:31年4月16天        |
| CLARK  | 已入职:31年3月7天         |
| SCOTT  | 已入职:25年4月26天        |
| KING   | 已入职:30年10月1天        |
| TURNER | 已入职:31年0月6天         |
| JAMES  | 已入职:30年9月15天        |
| FORD   | 已入职:30年9月15天        |
| MILLER | 已入职:30年7月24天        |
+--------+---------------------------+
13 rows in set (0.00 sec)

mysql> update emp set job=concat(upper(left(job,1)),mid(job,2));
-- 修改字段中的字符串将首字符改成小写
-- 1.使用left（列名，1）将字符串中的首字母拿到
-- 1.1使用upper（1）将拿到的字符串首字母转换成大写的
-- 2.使用mid（列名，2）将字符串中除了首字母的剩余字符拿到
-- 3.使用concat（1.1，2）将拿到的两个部分组合起来
-- 4.使用update 表名 set 列名=3；使用update方法进行修改
Query OK, 13 rows affected (0.01 sec)
Rows matched: 13  Changed: 13  Warnings: 0

mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | Clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | Salesman  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | Salesman  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | Manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | Salesman  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | Manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | Manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | Analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | President | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | Salesman  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7900 | JAMES  | Clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | Analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | Clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)

mysql> update emp set ename=concat(left(ename,1),lower(mid(ename,2)));
Query OK, 13 rows affected (0.00 sec)
Rows matched: 13  Changed: 13  Warnings: 0

mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | Smith  | clerk     | 7902 | 1990-12-17 |  800.00 |    NULL |     20 |
|  7499 | Allen  | salesman  | 7698 | 1991-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | Ward   | salesman  | 7698 | 1991-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | Jones  | manager   | 7839 | 1991-04-02 | 2975.00 |    NULL |     20 |
|  7654 | Martin | salesman  | 7698 | 1991-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | Blake  | manager   | 7839 | 1991-05-01 | 2850.00 |    NULL |     30 |
|  7782 | Clark  | manager   | 7839 | 1991-06-09 | 2450.00 |    NULL |     10 |
|  7788 | Scott  | analyst   | 7566 | 1997-04-19 | 3000.00 |    NULL |     20 |
|  7839 | King   | president | NULL | 1991-11-17 | 5000.00 |    NULL |     10 |
|  7844 | Turner | salesman  | 7698 | 1991-09-08 | 1500.00 |    NULL |     30 |
|  7900 | James  | clerk     | 7698 | 1991-12-03 |  950.00 |    NULL |     30 |
|  7902 | Ford   | analyst   | 7566 | 1991-12-03 | 3000.00 |    NULL |     20 |
|  7934 | Miller | clerk     | 7782 | 1992-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
13 rows in set (0.00 sec)


#REPLACE(s,s1,s2)	将字符串 s2 替代字符串 s 中的字符串 s1	
-- 将字符串 abc 中的字符 a 替换为字符 x：

SELECT REPLACE('abc','a','x') --xbc

-- For instance
-- 将emp表中的job列的数据首字符的小写字母replace为大写字母
mysql> select replace(
    -> job,left(job,1),upper(left(job,1))
    -> ) from emp;
+-----------------------------------------------+
| replace(
job,left(job,1),upper(left(job,1))
) |
+-----------------------------------------------+
| Clerk                                         |
| SaleSman                                      |
| SaleSman                                      |
| Manager                                       |
| SaleSman                                      |
| Manager                                       |
| Manager                                       |
| AnAlyst                                       |
| President                                     |
| SaleSman                                      |
| Clerk                                         |
| AnAlyst                                       |
| Clerk                                         |
+-----------------------------------------------+
13 rows in set (0.00 sec)

```



##### 数学函数

```sql
#ABS(x)	返回 x 的绝对值　　	
-- 返回 -1 的绝对值：
SELECT ABS(-1) -- 返回1
-- For instance
mysql> select abs(-125);
+-----------+
| abs(-125) |
+-----------+
|       125 |
+-----------+
1 row in set (0.00 sec)

#BIN(x)	返回 x 的二进制编码	
-- 15 的 2 进制编码:
SELECT BIN(15); -- 1111
-- For instance
mysql> select bin(56);
+---------+
| bin(56) |
+---------+
| 111000  |
+---------+
1 row in set (0.00 sec)

#CONV(x,f1,f2)	返回 f1 进制数变成 f2 进制数	
SELECT CONV(15, 10, 2);
-> 1111

#CEILING(x)	返回大于或等于 x 的最小整数　
SELECT CEILING(1.5); -- 返回2
-- For instance
mysql> select ceiling(1.1);
+--------------+
| ceiling(1.1) |
+--------------+
|            2 |
+--------------+
1 row in set (0.00 sec)
mysql> select ceiling(-2.9);
+---------------+
| ceiling(-2.9) |
+---------------+
|            -2 |
+---------------+
1 row in set (0.00 sec)

#FLOOR(x)	返回小于或等于 x 的最大整数　　
-- 小于或等于 1.5 的整数：
SELECT FLOOR(1.5) -- 返回1
-- For instance
mysql> select floor(1.9);
+------------+
| floor(1.9) |
+------------+
|          1 |
+------------+
1 row in set (0.00 sec)
mysql> select floor(-1.1);
+-------------+
| floor(-1.1) |
+-------------+
|          -2 |
+-------------+
1 row in set (0.00 sec)

#TRUNCATE(x,y)	返回数值 x 保留到小数点后 y 位的值（最后一位不会进行四舍五入）
SELECT TRUNCATE(1.23456,3) -- 1.234

#FORMAT(x,n)	函数可以将数字 x 进行格式化 "#,###.##", 将 x 保留到小数点后 n 位，最后一位四舍五入。	
-- 格式化数字 "#,###.##" 形式：
SELECT FORMAT(250500.5634, 2);     -- 输出 250,500.56
-- For instance
mysql> select sal from emp;
+---------+
| sal     |
+---------+
|  800.00 |
| 1600.00 |
| 1250.00 |
| 2975.00 |
| 1250.00 |
| 2850.00 |
| 2450.00 |
| 3000.00 |
| 5000.00 |
| 1500.00 |
|  950.00 |
| 3000.00 |
| 1300.00 |
+---------+
13 rows in set (0.00 sec)
mysql> select format(sal,5) from emp;
+---------------+
| format(sal,5) |
+---------------+
| 800.00000     |
| 1,600.00000   |
| 1,250.00000   |
| 2,975.00000   |
| 1,250.00000   |
| 2,850.00000   |
| 2,450.00000   |
| 3,000.00000   |
| 5,000.00000   |
| 1,500.00000   |
| 950.00000     |
| 3,000.00000   |
| 1,300.00000   |
+---------------+
13 rows in set (0.00 sec)

#LEAST(expr1, expr2, expr3, ...)	返回列表中的最小值	
-- 返回以下数字列表中的最小值：
SELECT LEAST(3, 12, 34, 8, 25); -- 3
-- 返回以下字符串列表中的最小值：
SELECT LEAST("Google", "Runoob", "Apple");   -- Apple

#MOD(x,y)	返回 x 除以 y 以后的余数　	
-- 5 除于 2 的余数：
SELECT MOD(5,2) -- 1

#RAND()	返回 0 到 1 的随机数　　	
SELECT RAND() --0.93099315644334
-- RAND(seed) 在开发中指定了seed则会固定得到一个0-1的随机数
-- For instance
mysql> select rand();
+--------------------+
| rand()             |
+--------------------+
| 0.9477880121653788 |
+--------------------+
1 row in set (0.00 sec)
mysql> select rand();
+--------------------+
| rand()             |
+--------------------+
| 0.7799059001541752 |
+--------------------+
1 row in set (0.00 sec)

mysql> select rand(5);
+---------------------+
| rand(5)             |
+---------------------+
| 0.40613597483014313 |
+---------------------+
1 row in set (0.00 sec)
-- RAND(seed) 在开发中指定了seed则会固定得到一个0-1的随机数
mysql> select rand(5);
+---------------------+
| rand(5)             |
+---------------------+
| 0.40613597483014313 |
+---------------------+
1 row in set (0.00 sec)

mysql> select rand(5);
+---------------------+
| rand(5)             |
+---------------------+
| 0.40613597483014313 |
+---------------------+
1 row in set (0.00 sec)

#ROUND(x)	返回离 x 最近的整数	
SELECT ROUND(1.23456) --1

```

##### 系统函数&加密函数

```sql
#USER()	返回当前用户	
SELECT USER();
-> guest@%

#DATABASE()	返回当前数据库名	
SELECT DATABASE();   
-> runoob

# MD5（str） 为字符串算出一个MD5 char(32) 的字符串--用户密码加密
-- root 密码存入的是加密后的
mysql> select MD5('zjhzjhzjh');
+----------------------------------+
| MD5('zjhzjhzjh')                 |
+----------------------------------+
| 4192290b1061348ea435f0595e65e933 |
+----------------------------------+
1 row in set (0.00 sec)
mysql> insert into student4 values(1001,'张锦豪',MD5('zjh20001207'),current_date);
Query OK, 1 row affected (0.14 sec)

mysql> select * from student4;
+------+-----------+----------------------------------+------------+
| id   | name      | password                         | birthday   |
+------+-----------+----------------------------------+------------+
| 1001 | 张锦豪    | dd60ed8124010280d53bda4cfd3bb6a5 | 2022-09-02 |
+------+-----------+----------------------------------+------------+
1 row in set (0.00 sec)

```



##### 流程控制

```sql
#IF(expr,v1,v2)	如果表达式 expr 成立，返回结果 v1；否则，返回结果 v2。	
SELECT IF(1 > 0,'正确','错误')    
->正确

#IFNULL(v1,v2)	如果 v1 的值不为 NULL，则返回 v1，否则返回 v2。	
SELECT IFNULL(null,'Hello Word')
->Hello Word

#CASE expression
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
   ...
    WHEN conditionN THEN resultN
    ELSE result
	END	
CASE 表示函数开始，END 表示函数结束。如果 condition1 成立，则返回 result1, 如果 condition2 成立，则返回 result2，当全部不成立则返回 result，而当有一个成立之后，后面的就不执行了。	
SELECT CASE 
　　WHEN 1 > 0
　　THEN '1 > 0'
　　WHEN 2 > 0
　　THEN '2 > 0'
　　ELSE '3 > 0'
　　END
->1 > 0

-- For instance
mysql> select case
    ->     -> when job='clerk'
    ->     -> then '职员'
    ->     -> when job='manager'
    ->     -> then '经理'
    ->     -> when job='salesman'
    ->     -> when job='salesman'^C
mysql> select case
    -> when job='clerk' then '职员'
    -> when job='manager' then '经理'
    -> when job='salesman' then '销售'
    -> else job
    -> end
    -> from emp;
+---------------------------------------------------------------------------------------------------------------------+
| case
when job='clerk' then '职员'
when job='manager' then '经理'
when job='salesman' then '销售'
else job
end       |
+---------------------------------------------------------------------------------------------------------------------+
| 职员                                                                                                                |
| 销售                                                                                                                |
| 销售                                                                                                                |
| 经理                                                                                                                |
| 销售                                                                                                                |
| 经理                                                                                                                |
| 经理                                                                                                                |
| analyst                                                                                                             |
| president                                                                                                           |
| 销售                                                                                                                |
| 职员                                                                                                                |
| analyst                                                                                                             |
| 职员                                                                                                                |
+---------------------------------------------------------------------------------------------------------------------+
13 rows in set (0.00 sec)
```



#### 内连接

```sql
#自连接-- 把同一张表当作两张表来使用 需要给表命别名来区分 （表名 别名 表名 别名）列名不明确时要给列 AS 别名
#开发中常用
-- For instance
-- 把一张表当作两张表来使用 from后给同一张表命两个别名来作为两张表进行区分 列的输入使用 表别名.列的形式 条件限制找到关联处
mysql> select worker.ename as 'woker',leader.ename as 'leader' from emp worker,emp leader where worker.mgr=leader.empno;
+--------+--------+
| woker  | leader |
+--------+--------+
| FORD   | JONES  |
| SCOTT  | JONES  |
| JAMES  | BLAKE  |
| TURNER | BLAKE  |
| MARTIN | BLAKE  |
| WARD   | BLAKE  |
| ALLEN  | BLAKE  |
| MILLER | CLARK  |
| CLARK  | KING   |
| BLAKE  | KING   |
| JONES  | KING   |
| SMITH  | FORD   |
+--------+--------+
12 rows in set (0.00 sec)
```



#### 外连接★

```sql
#JOIN 按照功能大致分为如下三类：

INNER JOIN（内连接,或等值连接）：获取两个表中字段匹配关系的记录。
LEFT JOIN（左连接）：获取左表所有记录，即使右表没有对应匹配的记录。
RIGHT JOIN（右连接）： 与 LEFT JOIN 相反，用于获取右表所有记录，即使左表没有对应匹配的记录。

-- 
mysql> select * from tb1;
+------+---------------+--------------+------------+
| id   | title         | author       | date       |
+------+---------------+--------------+------------+
|    1 | 学习 PHP      | 菜鸟教程     | 2017-04-12 |
|    2 | 学习 MySQL    | 菜鸟教程     | 2017-04-12 |
|    3 | 学习 Java     | RUNOOB.COM   | 2015-05-01 |
|    4 | 学习 Python   | RUNOOB.COM   | 2016-03-06 |
|    5 | 学习 C        | FK           | NULL       |
+------+---------------+--------------+------------+
5 rows in set (0.00 sec)

mysql> select * from tb2;
+--------------+-------+
| author       | count |
+--------------+-------+
| 菜鸟教程     |    10 |
| RUNOOB.COM   |    20 |
| Google       |    22 |
+--------------+-------+
3 rows in set (0.00 sec)

#INNER JOIN（内连接,或等值连接）：获取两个表中字段匹配关系的记录。
-- For instance -- (inner) join on
mysql> select * from tb1 join tb2 on tb1.author = tb2.author;
+------+---------------+--------------+------------+--------------+-------+
| id   | title         | author       | date       | author       | count |
+------+---------------+--------------+------------+--------------+-------+
|    1 | 学习 PHP      | 菜鸟教程     | 2017-04-12 | 菜鸟教程     |    10 |
|    2 | 学习 MySQL    | 菜鸟教程     | 2017-04-12 | 菜鸟教程     |    10 |
|    3 | 学习 Java     | RUNOOB.COM   | 2015-05-01 | RUNOOB.COM   |    20 |
|    4 | 学习 Python   | RUNOOB.COM   | 2016-03-06 | RUNOOB.COM   |    20 |
+------+---------------+--------------+------------+--------------+-------+
4 rows in set (0.00 sec)
-- 相当于使用where子句
mysql> select * from tb1 ,tb2 where tb1.author = tb2.author;
+------+---------------+--------------+------------+--------------+-------+
| id   | title         | author       | date       | author       | count |
+------+---------------+--------------+------------+--------------+-------+
|    1 | 学习 PHP      | 菜鸟教程     | 2017-04-12 | 菜鸟教程     |    10 |
|    2 | 学习 MySQL    | 菜鸟教程     | 2017-04-12 | 菜鸟教程     |    10 |
|    3 | 学习 Java     | RUNOOB.COM   | 2015-05-01 | RUNOOB.COM   |    20 |
|    4 | 学习 Python   | RUNOOB.COM   | 2016-03-06 | RUNOOB.COM   |    20 |
+------+---------------+--------------+------------+--------------+-------+
4 rows in set (0.00 sec)

#LEFT JOIN（左连接）：获取左表所有记录，即使右表没有对应匹配的记录。
mysql> select * from tb1 left join tb2 on tb1.author = tb2.author;
+------+---------------+--------------+------------+--------------+-------+
| id   | title         | author       | date       | author       | count |
+------+---------------+--------------+------------+--------------+-------+
|    1 | 学习 PHP      | 菜鸟教程     | 2017-04-12 | 菜鸟教程     |    10 |
|    2 | 学习 MySQL    | 菜鸟教程     | 2017-04-12 | 菜鸟教程     |    10 |
|    3 | 学习 Java     | RUNOOB.COM   | 2015-05-01 | RUNOOB.COM   |    20 |
|    4 | 学习 Python   | RUNOOB.COM   | 2016-03-06 | RUNOOB.COM   |    20 |
|    5 | 学习 C        | FK           | NULL       | NULL         |  NULL |
+------+---------------+--------------+------------+--------------+-------+
5 rows in set (0.00 sec)

#RIGHT JOIN（右连接）： 与 LEFT JOIN 相反，用于获取右表所有记录，即使左表没有对应匹配的记录。
mysql> select * from tb1 right join tb2 on tb1.author = tb2.author;
+------+---------------+--------------+------------+--------------+-------+
| id   | title         | author       | date       | author       | count |
+------+---------------+--------------+------------+--------------+-------+
|    2 | 学习 MySQL    | 菜鸟教程     | 2017-04-12 | 菜鸟教程     |    10 |
|    1 | 学习 PHP      | 菜鸟教程     | 2017-04-12 | 菜鸟教程     |    10 |
|    4 | 学习 Python   | RUNOOB.COM   | 2016-03-06 | RUNOOB.COM   |    20 |
|    3 | 学习 Java     | RUNOOB.COM   | 2015-05-01 | RUNOOB.COM   |    20 |
| NULL | NULL          | NULL         | NULL       | Google       |    22 |
+------+---------------+--------------+------------+--------------+-------+
5 rows in set (0.00 sec)

```



#### 约束

```sql
#约束
-- SQL 约束（Constraints）
-- SQL 约束用于规定表中的数据规则。

-- 如果存在违反约束的数据行为，行为会被约束终止。

-- 约束可以在创建表时规定（通过 CREATE TABLE 语句），或者在表创建之后规定（通过 ALTER TABLE 语句）。

SQL CREATE TABLE + CONSTRAINT 语法
CREATE TABLE table_name
(
column_name1 data_type(size) constraint_name,
column_name2 data_type(size) constraint_name,
column_name3 data_type(size) constraint_name,
....
);
在 SQL 中，我们有如下约束：

NOT NULL - 指示某列不能存储 NULL 值。
UNIQUE - 保证某列的每行必须有唯一的值。
PRIMARY KEY - NOT NULL 和 UNIQUE 的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。
FOREIGN KEY - 保证一个表中的数据匹配另一个表中的值的参照完整性。
CHECK - 保证列中的值符合指定的条件。
DEFAULT - 规定没有给列赋值时的默认值

-- 通过 show create table 表名 可以查看所有constraint -- 尤其是可以查看到忘记命名的constraint 系统自动生成的constraint命名
mysql> show create table student_test2;
+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table         | Create Table                                                                                                                                                                                                                                                                                                                                                                                                                                               |
+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| student_test2 | CREATE TABLE `student_test2` (
  `id` int NOT NULL DEFAULT '0',
  `address` varchar(25) COLLATE utf8mb3_bin NOT NULL DEFAULT 'CHINA',
  `birthday` date NOT NULL DEFAULT '2000-01-01',
  KEY `fk_id` (`id`),
  CONSTRAINT `fk_id` FOREIGN KEY (`id`) REFERENCES `student_test1` (`id`),
  CONSTRAINT `chk_birthday` CHECK ((`birthday` between _utf8mb3'1983-01-01' and _utf8mb3'2002-01-01')),
  CONSTRAINT `student_test2_chk_1` CHECK ((`id` between 0 and 100))
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 COLLATE=utf8mb3_bin |
+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

```

##### not null

```sql
#not null
SQL NOT NULL 约束
#在默认的情况下，表的列接受 NULL 值。

SQL NOT NULL 约束
NOT NULL 约束强制列不接受 NULL 值。

NOT NULL 约束强制字段始终包含值。这意味着，如果不向字段添加值，就无法插入新记录或者更新记录。

下面的 SQL 强制 "ID" 列、 "LastName" 列以及 "FirstName" 列不接受 NULL 值：

实例
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
#添加 NOT NULL 约束
在一个已创建的表的 "Age" 字段中添加 NOT NULL 约束如下所示：

实例
ALTER TABLE Persons
MODIFY Age int NOT NULL;
mysql> describe student_test1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | YES  |     | NULL    |       |
| name  | varchar(25) | NO   |     | 学生    |       |
| major | varchar(25) | NO   |     | IT      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

mysql> alter table student_test1 modify id int not null;
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> describe student_test1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   |     | NULL    |       |
| name  | varchar(25) | NO   |     | 学生    |       |
| major | varchar(25) | NO   |     | IT      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
#删除 NOT NULL 约束
在一个已创建的表的 "Age" 字段中删除 NOT NULL 约束如下所示：

实例
ALTER TABLE Persons
MODIFY Age int NULL;
mysql> describe student_test1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   |     | 0       |       |
| name  | varchar(25) | NO   |     | 学生    |       |
| major | varchar(25) | NO   |     | IT      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

mysql> alter table student_test1 modify id int null;
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> describe student_test1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | YES  |     | NULL    |       |
| name  | varchar(25) | NO   |     | 学生    |       |
| major | varchar(25) | NO   |     | IT      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```



##### unique

```sql
#SQL UNIQUE 约束-- 如果没有指定not null 则unique字段可以有多个null；
-- 如果制定了not null 同时指定了unique 等同于primary key
UNIQUE 约束唯一标识数据库表中的每条记录。

UNIQUE 和 PRIMARY KEY 约束均为列或列集合提供了唯一性的保证。

PRIMARY KEY 约束拥有自动定义的 UNIQUE 约束。

请注意，每个表可以有多个 UNIQUE 约束，但是每个表只能有一个 PRIMARY KEY 约束。

CREATE TABLE 时的 SQL UNIQUE 约束
下面的 SQL 在 "Persons" 表创建时在 "P_Id" 列上创建 UNIQUE 约束：

MySQL：

CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
UNIQUE (P_Id)
)
#ALTER TABLE 时的 SQL UNIQUE 约束
当表已被创建时，如需在 "P_Id" 列创建 UNIQUE 约束，请使用下面的 SQL：

MySQL / SQL Server / Oracle / MS Access：

ALTER TABLE Persons
ADD UNIQUE (P_Id)
如需命名 UNIQUE 约束，并定义多个列的 UNIQUE 约束，请使用下面的 SQL 语法：

MySQL / SQL Server / Oracle / MS Access：

ALTER TABLE Persons
ADD CONSTRAINT uc_PersonID UNIQUE (P_Id,LastName)

mysql> alter table student_test1 add constraint unique (id);
Query OK, 0 rows affected (0.07 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> describe student_test1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   | PRI | NULL    |       |
| name  | varchar(25) | NO   |     | 学生    |       |
| major | varchar(25) | NO   |     | IT      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

#撤销 UNIQUE 约束
如需撤销 UNIQUE 约束，请使用下面的 SQL：

MySQL：

ALTER TABLE Persons
DROP INDEX uc_PersonID
```



##### primary key

```sql
#主键
SQL PRIMARY KEY 约束
PRIMARY KEY 约束唯一标识数据库表中的每条记录。

主键必须包含唯一的值。

主键列不能包含 NULL 值。

每个表都应该有一个主键，并且每个表只能有一个主键

#单列主键
mysql> create table sutdennt_test1 
(`id` int not null default 0,`name` varchar(25) not null default "学生",`major` varchar(25) not null default "IT",
 primary key(id))
 character set utf8 collate utf8_bin;
Query OK, 0 rows affected, 2 warnings (0.15 sec)
mysql> describe student_test1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   | PRI | 0       |       |
| name  | varchar(25) | NO   |     | 学生    |       |
| major | varchar(25) | NO   |     | IT      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
mysql> insert into student_test1 values(1002,'James','Basketball'),(1003,'Ivring','Basketball');
Query OK, 2 rows affected (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from student_test1;
+------+------------+------------+
| id   | name       | major      |
+------+------------+------------+
| 1001 | EddieZhang | Java       |
| 1002 | James      | Basketball |
| 1003 | Ivring     | Basketball |
+------+------------+------------+
3 rows in set (0.00 sec)
mysql> insert into student_test1 values(1001,'Durant','Basketball');-- 主键的数据必须非空且唯一
ERROR 1062 (23000): Duplicate entry '1001' for key 'student_test1.PRIMARY'
mysql> insert into student_test1 values(1004,'Durant','Basketball');
Query OK, 1 row affected (0.00 sec)
#（复合主键）多列主键-- 将多个列作为主键 
#只有同时满足主键的多个列都相等时才会ERROR 1062 (23000): Duplicate entry '1001-EddieZhang' for key 'student_test1.PRIMARY'
mysql> alter table student_test1 add primary key(id,name);
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> describe student_test1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   | PRI | 0       |       |
| name  | varchar(25) | NO   | PRI | 学生    |       |
| major | varchar(25) | NO   |     | IT      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
mysql> insert into student_test1 values(1001,'EddieZ','Java');
Query OK, 1 row affected (0.14 sec)

mysql> select * from student_test1;
+------+------------+------------+
| id   | name       | major      |
+------+------------+------------+
| 1001 | EddieZ     | Java       |
| 1001 | EddieZhang | Java       |
| 1002 | James      | Basketball |
| 1003 | Ivring     | Basketball |
| 1004 | Durant     | Basketball |
+------+------------+------------+
5 rows in set (0.00 sec)
mysql> insert into student_test1 values(1001,'EddieZhang','Java');
ERROR 1062 (23000): Duplicate entry '1001-EddieZhang' for key 'student_test1.PRIMARY'
mysql>
#alter table add主键
mysql> alter table student_test1 add primary key(id,name);
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> describe student_test1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   | PRI | 0       |       |
| name  | varchar(25) | NO   | PRI | 学生    |       |
| major | varchar(25) | NO   |     | IT      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
#drop 删除主键
删除PRIMARY KEY约束时，不论约束条件为一列还是多列，对于MySQL，撤销都是

ALTER TABLE Persons
DROP PRIMARY KEY
由于PRIMARY KEY唯一性，MYSQL处理办法简单
mysql> insert into student_test1 values(1001,'EddieZhang','Java');
ERROR 1062 (23000): Duplicate entry '1001-EddieZhang' for key 'student_test1.PRIMARY'
mysql> describe student_test1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   | PRI | 0       |       |
| name  | varchar(25) | NO   | PRI | 学生    |       |
| major | varchar(25) | NO   |     | IT      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

mysql> alter table student_test1 drop primary key;
Query OK, 5 rows affected (0.02 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> describe student_test1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   |     | 0       |       |
| name  | varchar(25) | NO   |     | 学生    |       |
| major | varchar(25) | NO   |     | IT      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

```

##### foreign key

```sql
#SQL FOREIGN KEY 约束-- 用于定义主表和从表之间的关系
-- 外键约束要定义在从表上，主表则必须具有主键约束或者unique约束。
-- 当定义外键后，要求外键列数据必须在在主表的主键列存在或者为null;
-- FOREIGN KEY 约束用于预防破坏表之间连接的行为。
-- FOREIGN KEY 约束也能防止非法数据插入外键列，因为它必须是它指向的那个表中的值之一
-- 表的engine必须是innodb 这样的表才支持外键;
-- 外键字段类型要与主键字段类型一致（长度可以不同）
一个表中的 FOREIGN KEY 指向另一个表中的 UNIQUE KEY(唯一约束的键)
-- 在创建外键约束时，必须先创建外键约束所依赖的表（先创建主表），并且该列为该表的主键
-- 子表：谁创建外键谁就是子表 父表：这个外键所依赖的表
一、删除时，未指定cascade时

  1）删除父表/数据

      a.因为子表与父表一一对应，删除父表数据时，需要先把子表对应数据删除否则无法删除

     b. 同理，删除表的时候，也需要先删除子表再删除父表

解决方案：

     a.指定cascade，删除父表、数据

        CASCADE指当删除主表中被引用列的数据时，级联删除子表中相应的数据行。

     b.禁用约束（子表的外键约束）

         ALTER TABLE 表名 disable constraint 约束名;

 2）删除子表：可以删除子表或者数据不报错

二、更新时

        a.更新父表会违反约束

        b.可以更新子表

        c.没有针对约束的级联更新

三、插入时

         a.父表可以插入

         b.子表插入会违反约束
         
#在创建表的时候指定外键约束

CREATE TABLE 表名
    (
        column1 datatype null/not null,
        column2 datatype null/not null,
        ...
        CONSTRAINT 外键约束名 FOREIGN KEY  (column1,column2,... column_n) 
        REFERENCES 外键依赖的表 (column1,column2,...column_n)
        ON DELETE CASCADE--级联删除
    );
    
    mysql> create table student_test2 (
    -> `id` int not null default 0,
    -> `address` varchar(25) not null default 'CHINA',
    -> `birthday` date not null default '2000-01-01',
    -> constraint fk_id foreign key (id) references student_test1 (id))
    -> character set utf8 collate utf8_bin;
Query OK, 0 rows affected, 2 warnings (0.03 sec)

#在创建表后增加外键约束

ALTER TABLE 表名
    ADD CONSTRAINT 外键约束名
    FOREIGN KEY (column1, column2,...column_n) 
    REFERENCES 外键所依赖的表 (column1,column2,...column_n)
    ON DELETE CASCADE;--级联删除
    
    mysql> alter table student_test2 add constraint fk_id foreign key (id) references student_test1 (id);
Query OK, 4 rows affected (0.15 sec)
Records: 4  Duplicates: 0  Warnings: 0
    
#撤销 FOREIGN KEY 约束
如需撤销 FOREIGN KEY 约束，请使用下面的 SQL：

MySQL：

ALTER TABLE Orders
DROP FOREIGN KEY fk_PerOrders

mysql> alter table student_test2 drop constraint fk_id;
Query OK, 0 rows affected (0.01 sec)


```



##### check

```sql
#check
SQL CHECK 约束
CHECK 约束用于限制列中的值的范围。

如果对单个列定义 CHECK 约束，那么该列只允许特定的值。

如果对一个表定义 CHECK 约束，那么此约束会基于行中其他列的值在特定的列中对值进行限制

#CREATE TABLE 时的 SQL CHECK 约束
MySQL：

CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CHECK (P_Id>0)
)

mysql> create table student_test3 (
    -> `id` int not null default 0,
    -> `address` varchar(25) not null default 'CHINA',
    -> `birthday` date not null default '2000-01-01',
    -> constraint fk_student_test3_id foreign key (id) references student_test1 (id),
    -> constraint chk_id check (id between 0 and 100))
    -> character set utf8 collate utf8_bin engine innodb;
Query OK, 0 rows affected, 2 warnings (0.02 sec)

#ALTER TABLE 时的 SQL CHECK 约束
MySQL / SQL Server / Oracle / MS Access:

ALTER TABLE Persons
ADD CHECK (P_Id>0)

mysql> alter table student_test3
    -> add constraint chk_birth check (birthday between '1985-01-01' and '2002-01-01')
    -> ;
Query OK, 0 rows affected (0.04 sec)

#如需命名 CHECK 约束，并定义多个列的 CHECK 约束，请使用下面的 SQL 语法
CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CONSTRAINT chk_Person CHECK (P_Id>0 AND City='Sandnes')
)

mysql> alter table student_test3 add constraint chk_student_test3 check (id between 0 and 100
    -> and birthday between '1985-01-01' and '2002-01-01');
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0
mysql> show create table student_test3;
+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table         | Create Table                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| student_test3 | CREATE TABLE `student_test3` (
  `id` int NOT NULL DEFAULT '0',
  `address` varchar(25) COLLATE utf8mb3_bin NOT NULL DEFAULT 'CHINA',
  `birthday` date NOT NULL DEFAULT '2000-01-01',
  KEY `fk_student_test3_id` (`id`),
  CONSTRAINT `fk_student_test3_id` FOREIGN KEY (`id`) REFERENCES `student_test1` (`id`),
  CONSTRAINT `chk_student_test3` CHECK (((`id` between 0 and 100) and (`birthday` between _utf8mb3'1985-01-01' and _utf8mb3'2002-01-01')))
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 COLLATE=utf8mb3_bin |
+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
#撤销 CHECK 约束
SQL Server / Oracle / MS Access：

ALTER TABLE Persons
DROP CONSTRAINT chk_Person

mysql> alter table student_test3
    -> add constraint chk_birth check (birthday between '1985-01-01' and '2002-01-01')
    -> ;
Query OK, 0 rows affected (0.04 sec)

```

![image-20220904211021997](/images/image-20220904211021997.png)

```sql
#例题训练
create table goods (
goods_id int not null default 0 PRIMARY key,
goods_name varchar(25) not null default '',
unitprice double not null default 0,
category int not null default 0,
provider varchar(35) not null default '')
character set utf8 collate utf8_bin engine innodb;
alter table goods modify unitprice int not null default 0 constraint chk_price check (unitprice >= 1.0 and unitprice <= 9999.99);

create table customer (
customer_id int not null default 0 primary key,
`name` varchar(25) not null default '',
`address` varchar(55) not null default '',
`email` varchar(55) not null default '' unique,
`sex` enum ('男','女'),
card_id varchar(35) not null default '')
character set utf8 collate utf8_bin;

create table purchase (
order_id int not null default 0 primary key,
customer_id int not null default 0,
goods_id int not null default 0,
constraint fk_customer foreign key (customer_id) references customer (customer_id),
constraint fk_goods foreign key (goods_id) references goods (goods_id)
)character set utf8 collate utf8_bin engine innodb;

```



##### auto_increment

**清空数据表并且自增从头开始的sql命令**

**truncate** table table_name; *//table_name 该数据表名称* 

删除完还没有新增数据，即还没有出现不连贯的数据ID时，执行以下语句：

ALTER TABLE 表名 AUTO_INCREMENT = 1;
1
**如果已知下一条数据自增的ID（假设是10），可以直接写成ALTER TABLE 表名 AUTO_INCREMENT = 10;这样再插入数据时，自增ID会从10开始**，也可以用这个语法来跳过一些编号。此外，如果AUTO_INCREMENT 的值小于ID的最大值，那么ID是从MAX(ID)+1开始自增，所以当AUTO_INCREMENT = 1时，一般默认ID是从最大值加一开始自增的。

表中已经出现不连贯的数据ID时，执行以下语句进行修改

SET @auto_id = 0;
UPDATE 表名 SET 自增字段名 = (@auto_id := @auto_id + 1);
ALTER TABLE 表名 AUTO_INCREMENT = 1;


如果需要清空表的数据的话，最好使用TRUNCATE TABLE 表名来删除，这样新增的数据自增ID会从1开始，如果使用DELETE来删除，新增的数据会沿着之前的ID

```sql
#自增长 auto increment
#AUTO INCREMENT 字段
我们通常希望在每次插入新记录时，自动地创建主键字段的值。

我们可以在表中创建一个 auto-increment 字段。

用于 MySQL 的语法
下面的 SQL 语句把 "Persons" 表中的 "ID" 列定义为 auto-increment 主键字段：

CREATE TABLE Persons
(
ID int NOT NULL AUTO_INCREMENT,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
PRIMARY KEY (ID)
)
MySQL 使用 AUTO_INCREMENT 关键字来执行 auto-increment 任务。

默认地，AUTO_INCREMENT 的开始值是 1，每条新记录递增 1。

要让 AUTO_INCREMENT 序列以其他的值起始，请使用下面的 SQL 语法：

ALTER TABLE Persons AUTO_INCREMENT=100
要在 "Persons" 表中插入新记录，我们不必为 "ID" 列规定值（会自动添加一个唯一的值）：

INSERT INTO Persons (FirstName,LastName)
VALUES ('Lars','Monsen')
上面的 SQL 语句会在 "Persons" 表中插入一条新记录。"ID" 列会被赋予一个唯一的值。"FirstName" 列会被设置为 "Lars"，"LastName" 列会被设置为 "Monsen"

#给已经存在的colume添加自增语法：

ALTER TABLE table_name CHANGE column_name column_name data_type(size) constraint_name AUTO_INCREMENT;
比如：

ALTER TABLE student CHANGE id id INT( 11 ) NOT NULL AUTO_INCREMENT;

#在添加数据时给自增长字段列指定值；则以指定的值为准且后续的值按照指定值开始自增长
mysql> select * from student_test4;
+-----+-----------+
| id  | name      |
+-----+-----------+
| 100 | 张锦豪    |
| 101 | 欧文      |
| 102 | 詹姆斯    |
| 103 | 杜兰特    |
| 104 | 库里      |
+-----+-----------+
5 rows in set (0.00 sec)

mysql> insert into student_test4 values(660,'东七七');
Query OK, 1 row affected (0.00 sec)

mysql> insert into student_test4 (`name`) values('塔图姆');
Query OK, 1 row affected (0.12 sec)

mysql> select * from student_test4;
+-----+-----------+
| id  | name      |
+-----+-----------+
| 100 | 张锦豪    |
| 101 | 欧文      |
| 102 | 詹姆斯    |
| 103 | 杜兰特    |
| 104 | 库里      |
| 660 | 东七七    |
| 661 | 塔图姆    |
+-----+-----------+
7 rows in set (0.00 sec)
```



#### 索引★

```sql
MySQL索引的建立对于MySQL的高效运行是很重要的，索引可以大大提高MySQL的检索速度。只对创建了索引的列有效

打个比方，如果合理的设计且使用索引的MySQL是一辆兰博基尼的话，那么没有设计和使用索引的MySQL就是一个人力三轮车。

拿汉语字典的目录页（索引）打比方，我们可以按拼音、笔画、偏旁部首等排序的目录（索引）快速查找到需要的字。

索引分单列索引和组合索引。单列索引，即一个索引只包含单个列，一个表可以有多个单列索引，但这不是组合索引。组合索引，即一个索引包含多个列。

创建索引时，你需要确保该索引是应用在 SQL 查询语句的条件(一般作为 WHERE 子句的条件)。

实际上，索引也是一张表，该表保存了主键与索引字段，并指向实体表的记录。

上面都在说使用索引的好处，但过多的使用索引将会造成滥用。因此索引也会有它的缺点：虽然索引大大提高了查询速度，同时却会降低更新表的速度，如对表进行INSERT、UPDATE和DELETE。因为更新表时，MySQL不仅要保存数据，还要保存一下索引文件。

建立索引会占用磁盘空间的索引文件

```

![image-20220905074911013](/images/image-20220905074911013.png)

![image-20220905075120329](/images/image-20220905075120329.png)

![image-20220905102533069](/images/image-20220905102533069.png)

##### 主键索引

```sql
#主键索引
主键自动为主索引（类型primary key）
```

##### 唯一索引（UNIQUE）

```sql
#唯一索引
它与前面的普通索引类似，不同的就是：索引列的值必须唯一，但允许有空值。如果是组合索引，则列值的组合必须唯一。它有以下几种创建方式：

创建索引
CREATE UNIQUE INDEX indexName ON mytable(username(length)) 

create unique index index_emp on emp(empno);

修改表结构
ALTER table mytable ADD UNIQUE [indexName] (username(length))
创建表的时候直接指定
CREATE TABLE mytable(  
 
ID INT NOT NULL,   
 
username VARCHAR(16) NOT NULL,  
 
UNIQUE [indexName] (username(length))  
 
);  
使用ALTER 命令添加和删除索引
有四种方式来添加数据表的索引：

ALTER TABLE tbl_name ADD PRIMARY KEY (column_list): 该语句添加一个主键，这意味着索引值必须是唯一的，且不能为NULL。
ALTER TABLE tbl_name ADD UNIQUE index_name (column_list): 这条语句创建索引的值必须是唯一的（除了NULL外，NULL可能会出现多次）。
ALTER TABLE tbl_name ADD INDEX index_name (column_list): 添加普通索引，索引值可出现多次。
ALTER TABLE tbl_name ADD FULLTEXT index_name (column_list):该语句指定了索引为 FULLTEXT ，用于全文索引。
以下实例为在表中添加索引。

mysql> ALTER TABLE testalter_tbl ADD INDEX (c);
你还可以在 ALTER 命令中使用 DROP 子句来删除索引。尝试以下实例删除索引:

mysql> ALTER TABLE testalter_tbl DROP INDEX c;
使用 ALTER 命令添加和删除主键
主键作用于列上（可以一个列或多个列联合主键），添加主键索引时，你需要确保该主键默认不为空（NOT NULL）。实例如下：

mysql> ALTER TABLE testalter_tbl MODIFY i INT NOT NULL;
mysql> ALTER TABLE testalter_tbl ADD PRIMARY KEY (i);
你也可以使用 ALTER 命令删除主键：

mysql> ALTER TABLE testalter_tbl DROP PRIMARY KEY;
删除主键时只需指定 PRIMARY KEY，但在删除索引时，你必须知道索引名

```



##### 普通索引（INDEX）

```sql
#普通索引
创建索引
这是最基本的索引，它没有任何限制。它有以下几种创建方式：

CREATE INDEX indexName ON table_name (column_name)
如果是CHAR，VARCHAR类型，length可以小于字段实际长度；如果是BLOB和TEXT类型，必须指定 length

create index index_emp on emp (empno);

修改表结构(添加索引)
ALTER table tableName ADD INDEX indexName(columnName)

alter table emp.emp add index index_emp (empno);

创建表的时候直接指定
CREATE TABLE mytable(  
 
ID INT NOT NULL,   
 
username VARCHAR(16) NOT NULL,  
 
INDEX [indexName] (username(length))  
 
);  
删除索引的语法
DROP INDEX [indexName] ON mytable;

```



##### 全文索引

#### 事务

![image-20220905103719377](/images/image-20220905103719377.png)

![image-20220905104030470](/images/image-20220905104030470.png)

![image-20220905235904013](/images/image-20220905235904013.png)

![image-20220905104709042](/images/image-20220905104709042.png)

![image-20220905104832325](/images/image-20220905104832325.png)

##### 事务管理

##### save point

##### rollback

##### commit

##### 事务控制语句

```sql
BEGIN 或 START TRANSACTION 显式地开启一个事务；

COMMIT 也可以使用 COMMIT WORK，不过二者是等价的。COMMIT 会提交事务，并使已对数据库进行的所有修改成为永久性的；

ROLLBACK 也可以使用 ROLLBACK WORK，不过二者是等价的。回滚会结束用户的事务，并撤销正在进行的所有未提交的修改；

SAVEPOINT identifier，SAVEPOINT 允许在事务中创建一个保存点，一个事务中可以有多个 SAVEPOINT；

RELEASE SAVEPOINT identifier 删除一个事务的保存点，当没有指定的保存点时，执行该语句会抛出一个异常；

ROLLBACK TO identifier 把事务回滚到标记点；

SET TRANSACTION 用来设置事务的隔离级别。InnoDB 存储引擎提供事务的隔离级别有READ UNCOMMITTED、READ COMMITTED、REPEATABLE READ 和 SERIALIZABLE。
MYSQL 事务处理主要有两种方法：
1、用 BEGIN, ROLLBACK, COMMIT来实现

BEGIN 开始一个事务
ROLLBACK 事务回滚
COMMIT 事务确认
2、直接用 SET 来改变 MySQL 的自动提交模式:

SET AUTOCOMMIT=0 禁止自动提交
SET AUTOCOMMIT=1 开启自动提交
```



##### 隔离级别

```sql
# You can set the isolationlevel for the whole server in the configuration file, or just foryour session:
mysql> SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;
# You can set the isolationlevel for the whole server(global) in the configuration file, or just foryour session:
mysql> set global transaction isolation level read committed;
```

![image-20220905105530766](/images/image-20220905105530766.png)

![image-20220905105812053](/images/image-20220905105812053.png)

##### ACID

```sql
事务是必须满足4个条件（ACID）：
原子性（Atomicity，或称不可分割性）、
一致性（Consistency）、
隔离性（Isolation，又称独立性）、
持久性（Durability）。

原子性：一个事务（transaction）中的所有操作，要么全部完成，要么全部不完成，不会结束在中间某个环节。事务在执行过程中发生错误，会被回滚（Rollback）到事务开始前的状态，就像这个事务从来没有执行过一样。

一致性：在事务开始之前和事务结束以后，数据库的完整性没有被破坏。这表示写入的资料必须完全符合所有的预设规则，这包含资料的精确度、串联性以及后续数据库可以自发性地完成预定的工作。

隔离性：数据库允许多个并发事务同时对其数据进行读写和修改的能力，隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。事务隔离分为不同级别，包括读未提交（Read uncommitted）、读提交（read committed）、可重复读（repeatable read）和串行化（Serializable）。

持久性：事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。
```



#### 视图

视图的理解

1.可以看作是一个虚拟的表，本身不存储数据 试图的可以理解为存储起来的select语句

2.试图创建时select语句设计的表 称之为基表

3.针对对视图进行的DML操作 会影响到基表 反之亦然

4.删除视图 不会导致到基表本身的数据被删除

5.视图的应用场景 针对于小型项目不建议使用视图 针对于大型项目推荐使用视图

6.视图的作用及优点 简化查询（将一次查询持久储存起来）；权限管理 （让不同权限的人员 看到表中不同范围的数据 控制数据的访问）

![image-20220905144613234](/images/image-20220905144613234.png)

```sql
#SQL 视图（Views）
视图是可视化的表。

本章讲解如何创建、更新和删除视图。

SQL CREATE VIEW 语句
在 SQL 中，视图是基于 SQL 语句的结果集的可视化的表。

视图包含行和列，就像一个真实的表。视图中的字段就是来自一个或多个数据库中的真实的表中的字段。

您可以向视图添加 SQL 函数、WHERE 以及 JOIN 语句，也可以呈现数据，就像这些数据来自于某个单一的表一样。

SQL CREATE VIEW 语法

CREATE VIEW view_name AS
SELECT column_name(s)
FROM table_name
WHERE condition
注释：视图总是显示最新的数据！每当用户查询视图时，数据库引擎通过使用视图的 SQL 语句重建数据

-- For instance
mysql> create view view_emp1 as select empno,ename,job from emp where deptno = 30;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from view_emp1;
+-------+--------+----------+
| empno | ename  | job      |
+-------+--------+----------+
|  7499 | ALLEN  | salesman |
|  7521 | WARD   | salesman |
|  7654 | MARTIN | salesman |
|  7698 | BLAKE  | manager  |
|  7844 | TURNER | salesman |
|  7900 | JAMES  | clerk    |
+-------+--------+----------+
6 rows in set (0.00 sec)

#SQL 更新视图
您可以使用下面的语法来更新视图：

SQL CREATE OR REPLACE VIEW 语法

CREATE OR REPLACE VIEW view_name AS
SELECT column_name(s)
FROM table_name
WHERE condition
现在，我们希望向 "Current Product List" 视图添加 "Category" 列。我们将通过下列 SQL 更新视图：

CREATE VIEW [Current Product List] AS
SELECT ProductID,ProductName,Category
FROM Products
WHERE Discontinued=No

-- For instance
mysql> create or replace view view_emp1 as select empno,ename,job,deptno from emp where deptno = 30;
Query OK, 0 rows affected (0.12 sec)

mysql> select * from view_emp1;
+-------+--------+----------+--------+
| empno | ename  | job      | deptno |
+-------+--------+----------+--------+
|  7499 | ALLEN  | salesman |     30 |
|  7521 | WARD   | salesman |     30 |
|  7654 | MARTIN | salesman |     30 |
|  7698 | BLAKE  | manager  |     30 |
|  7844 | TURNER | salesman |     30 |
|  7900 | JAMES  | clerk    |     30 |
+-------+--------+----------+--------+
6 rows in set (0.00 sec)

#SQL 撤销视图
您可以通过 DROP VIEW 命令来删除视图。

SQL DROP VIEW 语法
DROP VIEW view_name

-- For instance
mysql> drop view view_emp1;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from view_emp1;
#ERROR 1146 (42S02): Table 'db02.view_emp1' doesn't exist


#视图的作用：

1、视图隐藏了底层的表结构，简化了数据访问操作，客户端不再需要知道底层表的结构及其之间的关系。

2、视图提供了一个统一访问数据的接口。（即可以允许用户通过视图访问数据的安全机制，而不授予用户直接访问底层表的权限）

3、从而加强了安全性，使用户只能看到视图所显示的数据。

4、视图还可以被嵌套，一个视图中可以嵌套另一个视图。
```

#### Mysql用户管理

```sql
#Mysql用户管理
-- 应用场景:当我们做项目开发时，可以根据不同的开发人员，赋给他们相应的Mysql操作权限	
-- Mysql数据库管理人员（root） 可以根据需要创建不同的用户，赋予相应的权限，供人员使用

#创建新的用户
create user 'EddieZ'@'localhost' identified by 'eddiez';
-- '用户名'@'指定端口号' identified by '密码'; -- Tip:存入到Mysql.user表时的密码是加密过的

#查看用户
select * from mysql.user-- 查看所有信息

mysql> select `user`,`host`,`authentication_string` from mysql.user;--查看指定信息

#删除用户
drop user 'EddieZ'@'localhost'

#登录
-- 不同的用户登录到数据库管理系统（DBMS）后，根据自身的相应权限，可以操作的数据库和数据对象（表，试图，触发器）都不一样。

#修改密码
-- 自己有权限修改自己的密码
set password = password('newpassword');
-- 非root无权修改别的用户的密码

-- root有权限修改别的用户的密码
set password for 'EddieZ'@'localhost' = password('newpassword');


```

不同的用户登录到数据库管理系统（DBMS）后，根据自身的相应权限，可以操作的数据库和数据对象（表，试图，触发器）都不一样。

![image-20220906135039895](/images/image-20220906135039895.png)

![image-20220906142425068](/images/image-20220906142425068.png)

```sql
mysql> create user eddiez;-- 创建用户的时候未指定host 则host为% 即表示所有的ip都有连接权限
Query OK, 0 rows affected (0.01 sec)

mysql> select `user`,`host` from mysql.user;
+------------------+-----------+
| user             | host      |
+------------------+-----------+
| eddiez           | %         |
| mysql.infoschema | localhost |
| mysql.session    | localhost |
| mysql.sys        | localhost |
| root             | localhost |
+------------------+-----------+
5 rows in set (0.00 sec)

mysql> drop user eddiez;-- 如果删除的用户为指明端口 则只需要输入用户名即可
Query OK, 0 rows affected (0.01 sec)

mysql> create user 'eddiez'@'192.168.1.%';-- 创建用户的时候指定'192.168.1.%'端口号表示用户可以在192.168.1.*的ip（这个ip范围中）都可以登录
Query OK, 0 rows affected (0.12 sec)

mysql> select `user`,`host` from mysql.user;
+------------------+-------------+
| user             | host        |
+------------------+-------------+
| eddiez           | 192.168.1.% |
| mysql.infoschema | localhost   |
| mysql.session    | localhost   |
| mysql.sys        | localhost   |
| root             | localhost   |
+------------------+-------------+
5 rows in set (0.00 sec)

mysql> drop user 'eddiez'@'192.168.1.%';
Query OK, 0 rows affected (0.00 sec)-- 删除的用户指明了端口的 要输入用户完整的格式信息才能删除
```



#### Mysql权限管理

![image-20220906135412880](/images/image-20220906135412880.png)

![image-20220906135605307](/images/image-20220906135605307.png)

```sql
-- root用户给其他用户赋予权限
grant select,insert on db03.salgrade to 'EddieZ'@'localhost';
-- grant 权限列表 on 库.对象名 to 用户名 

-- root用户给其他用户增加权限
grant update on db03.salgrade to 'EddieZ'@'localhost';

-- root用户回收其他用户的权限
revoke update on db03.salgrade from 'Eddie'@'localhost';
revoke all on db03.salgrade from 'Eddie'@'localhost';-- 回收所有权限
-- root用户修改其他用户的密码
set password for 'EddieZ'@'localhost' = password('newpassword');

```



```sql
#test
#使用简单查询语句
-- 显示所有部门名称
select distinct dname from dept;
-- 显示所有雇员名以及其全年的收入 13月（工资加补助）指明别名 年收入
select ename,(sal + if((comm is null),0.0,comm))*13 as '年收入' from emp;
#限制查询语句
-- 显示工资超过2850的雇员的姓名和工资
select ename,sal from emp where sal > 2850;
-- 显示工资不在1500到2850之间的所有雇员名及其工资
select ename,sal from emp where NOT (sal between 1500 and 2850);
-- 显示编号为7566的雇员姓名及其所在部门编号
select ename,deptno from emp where empno = 7566;
-- 显示部门10和30中工资超过1500的雇员名及工资
select ename,sal from emp where 
(deptno = 10 or deptno = 30) and sal >= 1500;
-- 显示无管理者的雇员名及岗位
select ename,job from emp where mgr is null;
#排序数据
-- 显示在1991-02-01到1991-05-01之间雇佣的雇员名，岗位，及雇佣日期，并以雇佣日期进行排序
select ename,job,hiredate from emp where hiredate between '1991-02-01' and '1991-05-01' order by hiredate desc ;
-- 显示获得补助的所有员工名，工资及补助 并以工资降序排序
select ename,sal,comm from emp where comm is not null order by sal desc;
#6.
-- 1.
select * from emp where deptno = 30;
-- 2.
select ename,empno,deptno from emp where job = 'clerk';
-- 3.
select * from emp where comm > sal;
-- 4.
select * from emp where comm > (sal*0.6);
-- 5.
select * from emp where (deptno = 10 and job = 'manager') or (deptno = 20 and job = 'clerk');
-- 6.
select * from emp where (deptno = 10 and job = 'manager') or (deptno = 20 and job = 'clerk') or (job <> 'manager' and job <> 'clerk' and sal >= 2000);
-- 7.
select distinct job from emp where comm is not null;
-- 8.
select * from emp where comm is null or comm < 100;
-- 9.
select * from emp where DATEDIFF(LAST_DAY(hiredate),hiredate) <= 3;
-- 10.
select * from emp where DATE_ADD(hiredate,interval 31 YEAR) < NOW();
-- 11.
select CONCAT(LCASE(MID(ename,1,1)),(MID(ename,2))) from emp;
-- 12.
select ename from emp where LENGTH(ename) = 5;
-- 13.
select * from emp where ename not like '%R%';
-- 14.
select MID(ename,1,3) from emp;
-- 15.
select REPLACE(ename,'A','a') from emp;
-- 16.
select ename,hiredate from emp where DATE_ADD(hiredate,INTERVAL 12 year) <= NOW();
-- 17.
select * from emp ORDER BY ename DESC;
-- 18.
select ename,hiredate from emp order by hiredate asc;
-- 19.
select ename,job,sal from emp ORDER BY job desc , sal asc;
-- 20.
select ename,YEAR(hiredate),MONTH(hiredate),hiredate from emp order by MONTH(hiredate) , DAY(hiredate);
-- 21.
select TRUNCATE(sal/30,0) as '日薪资' from emp;
-- 22.
select * from emp where MONTH(hiredate) = 2;
-- 23.
select DATEDIFF(now(),hiredate) from emp;
-- 24.
select ename from emp where ename like '%A%';
-- 25.
select ename,CONCAT('已入职:',TRUNCATE((DATEDIFF(now(),hiredate)/365),0),'年',TRUNCATE((TRUNCATE((DATEDIFF(now(),hiredate)%365),0))/30,0),'月',
TRUNCATE((TRUNCATE((DATEDIFF(now(),hiredate)%365),0))%30,0),'天') AS '入职年限' from emp;
#7
-- 1.
select distinct emp.deptno from emp,dept where emp.deptno = dept.deptno;
select count(*) as 'num',deptno from emp group by deptno HAVING num >= 1;
-- 2.
select * from emp where sal > (select sal from emp where ename = 'SMITH');
-- 3.-- 把一张表看作是两张表来处理
select worker.ename as '员工名',worker.hiredate as '员工入职时间',leader.ename as '直接上级名',leader.hiredate as '上级入职时间'
			from emp as worker,emp as leader
			where worker.hiredate > leader.hiredate and worker.mgr = leader.empno;
-- 4.-- 使用外连接
select dept.dname,emp.*
			from dept LEFT JOIN emp on dept.deptno = emp.deptno;
-- 5.
select emp.ename,dept.dname
			from emp,dept where job = 'clerk' and emp.deptno = dept.deptno;
-- 6.
select distinct job from emp GROUP BY job HAVING min(sal) > 1500;
-- 7.
select ename from emp where deptno = 30;
-- 8.
select * from emp where sal > (select avg(sal) from emp);

#7
-- 9.
select * from emp where job = (select job from emp where ename = 'SCOTT');
-- 10.
select ename,sal from emp where sal > (select max(sal) from emp where deptno = 30);
-- 11.
select count(*) as '部门人数',avg(sal) as '平均工资',FORMAT(avg(DATEDIFF(NOW(),hiredate) / 356),1) as '平均服务期限（单位年）' from emp GROUP BY deptno;
-- 12.
select emp.ename,dept.dname,emp.sal
      from emp,dept
			where emp.deptno = dept.deptno;
-- 13.
select * from dept,(select count(*) as '部门人数',deptno from emp GROUP BY deptno) AS temp where temp.deptno = dept.deptno;
-- 14.
select job,min(sal) as '最低工资' from emp GROUP BY job;
-- 15.
select min(sal) as 'manager的最低工资' from emp where job = 'manager';
-- 16.
select ename,((sal + IFNULL(comm,0)) * 13) as yearsal from emp order by yearsal desc;

#8
create table `class` (
classid int not null default 0 primary key,`subject` varchar(15) not null default '',`deptname` varchar(15) not null default '',
enrolltime date not null default '2000-01-01')character set utf8 collate utf8_bin engine innodb;
desc class;
alter table class modify enrolltime YEAR;
alter table class add num tinyint not null default 0;
desc class;
insert into class values (101,'软件','计算机','1995',20),(102,'微电子','计算机','1996',30),(111,'无机化学','化学','1995',29),(112,'高分子化学','化学','1996',25),(121,'统计数学','数学','1995',20),(131,'现代语言','中文','1996',20),(141,'国际贸易','经济','1997',30),(142,'国际金融','经济','1996',14);
select * from class;
create table `student_table` (
`studentid` int not null default 0 primary key,`name` varchar(10) not null default '',`age` tinyint not null default 0,
classid int not null default 0,
constraint fk_classid foreign key (classid) references class (classid))character set utf8 collate utf8_bin engine innodb;
desc student_table;
insert into student_table values (8101,'张三',18,101),(8102,'钱四',16,121),(8103,'玉玲',17,131),(8105,'李飞',19,102),(8109,'赵四',18,141),(8110,'李可',20,142),(8201,'张飞',18,111),(8302,'周瑜',16,112),(8303,'王亮',17,111),(8305,'董庆',19,102),(8409,'赵龙',18,101),(8510,'李丽',20,142);
select * from student_table;
create table `department` (
departmentid int not null default 0 primary key,deptname varchar(15) not null default '',
constraint unique (deptname))character set utf8 collate utf8_bin engine innodb;
desc department;
insert into department values (001,'数学'),(002,'计算机'),(003,'化学'),(004,'中文'),(005,'经济');
select * from department;

#test
-- 1.
select * from student_table where name like '李%';
-- 2.
select distinct class.deptname from class,(select deptname,count(*) as num from class GROUP BY deptname) as temp_table where temp_table.num > 1 and 
temp_table.deptname = class.deptname;
-- 3.
select distinct department.departmentid,department.deptname,temp_table1.sum
			from department,(select class.deptname,sum(class.num) as sum from class GROUP BY deptname) as temp_table1 where department.deptname = temp_table1.deptname and temp_table1.sum >= 30;
-- 4.
insert into department values (006,'物理');
select * from department;
select * from class;
-- 5.-- 使用事务
-- 开启事务
start transaction;
-- 进行操作

update class set num = (num - 1) where classid = (select student_table.classid from student_table where student_table.`name` = '张三');-- 将班表中的人数变更
delete from student_table where student_table.`name` = '张三';-- 从学生表中删除
-- 确认无误 提交事务
commit;
select * from class;
select * from student_table;



-- 把系表中的id类型改为varchar(10)
delete from department;
alter table department MODIFY departmentid varchar(10) not null;
insert into department values ('001','数学'),('002','计算机'),('003','化学'),('004','中文'),('005','经济');
insert into department values ('006','物理');
desc department;
select * from department;
			



```

# Mysql系统变量查询

在 MySQL 数据库，变量分为**系统变量**和**用户自定义变量**。

**系统变量以 @@ 开头**，

- @@global 仅仅用于标记全局变量；
- @@session 仅仅用于标记会话变量；
- @@ 首先标记会话变量，如果会话变量不存在，则标记全局变量。

**用户自定义变量以 @ 开头**。

 

服务器维护着两种系统变量，即

**全局变量（GLOBAL VARIABLES）**和**会话变量（SESSION VARIABLES）**。

全局变量影响 MySQL 服务的整体运行方式，会话变量影响具体客户端连接的操作。

 每一个客户端成功连接服务器后，都会产生与之对应的会话。会话期间，MySQL 服务实例会在服务器内存中生成与该会话对应的会话变量，这些会话变量的初始值是全局变量值的拷贝。

## 查询设置全局变量：show global variables \G;

**没有指定**修改全局变量还是会话变量，**服务器会当作会话变量**来**处理**

```sql
SHOW GLOBAL VARIABLES; 
SHOW GLOBAL VARIABLES LIKE 'innodb_data_file_path';
SHOW GLOBAL VARIABLES LIKE 'character_set_client';


SET @@global.innodb_file_per_table=default;
SET @@global.innodb_file_per_table=ON;
SET global innodb_file_per_table=ON;
```



## 查询设置会话变量：show session variables \G;或show variables；

**没有指定**修改全局变量还是会话变量，**服务器会当作会话变量**来**处理**

```sql
SHOW SESSION VARIABLES LIKE 'character_set_client';
SHOW VARIABLES LIKE 'character_set_client';
SHOW SESSION VARIABLES LIKE 'pseudo_thread_id';
SHOW SESSION VARIABLES LIKE 'innodb_data_file_path';
SHOW VARIABLES LIKE 'innodb_data_file_path';
SHOW SESSION VARIABLES;


SET @@session.pseudo_thread_id=5;
SET session pseudo_thread_id=5;
SET @@pseudo_thread_id=5;
SET pseudo_thread_id = 5;
SET @@sort_buffer_size = 50000;
```



# Mysql相关优质学习资料

[28 | 读写分离有哪些坑？ (geekbang.org)](https://time.geekbang.org/column/article/77636)

## MySQL实战45讲精选

### 00开篇词 这一次，让我们一起来搞懂MySQL

你好，我是林晓斌，网名“丁奇”，欢迎加入我的专栏，和我一起开始 MySQL 学习之旅。我曾先后在百度和阿里任职，从事 MySQL  数据库方面的工作，一步步地从一个数据库小白成为 MySQL 内核开发人员。回想起来，从我第一次带着疑问翻 MySQL  的源码查到答案至今，已经有十个年头了。在这个过程中，走了不少弯路，但同时也收获了很多的知识和思考，希望能在这个专栏里分享给你。

记得刚开始接触 MySQL，是我在百度贴吧做权限系统的时候。我们遇到了一个奇怪的问题，一个正常 10 毫秒就能完成的 SQL  查询请求偶尔要执行 100  多毫秒才结束。当时主管问我是什么原因，我其实也搞不清楚，就上网查答案，但怎么找都找不到，又脸皮薄不想说自己不知道，只好硬着头皮翻源码。后来遇到了越来越多的问题，也是类似的情景，所以我逐步养成了通过分析源码理解原理的习惯。

当时，我自己的感觉是，即使我只是一个开发工程师，只是 MySQL  的用户，在了解了一个个系统模块的原理后，再来使用它，感觉是完全不一样的。当在代码里写下一行数据库命令的时候，我就能想到它在数据库端将怎么执行，它的性能是怎么样的，怎样写能让我的应用程序访问数据库的性能最高。进一步，哪些数据处理让数据库系统来做性能会更好，哪些数据处理在缓存里做性能会更好，我心里也会更清楚。在建表和建索引的时候，我也会更有意识地为将来的查询优化做综合考虑，比如确定是否使用递增主键、主键的列怎样选择，等等。

但随后我又有了一个新的困惑，我觉得自己了解的 MySQL 知识点是零散的，没有形成网络。于是解决完一个问题后，很容易忘记。再碰到类似的问题，我又得再翻一次代码。

所幸在阿里工作的时候，我参与了阿里云关系型数据库服务内核的开发，并且负责开发开源分支 AliSQL，让我对 MySQL  内核和源码有了更深层次的研究和理解。在服务内部客户和公有云客户的过程中，我有机会面对和解决足够多的问题，再通过手册进行系统的学习，算是比较坎坷地将 MySQL 的知识网络补了起来。

所以，在回顾这个过程的时候，我的第一个感受是，如果一开始就有一些从理论到实战的系统性指导，那该多好啊，也许我可以学习得更快些。

在极客时间团队跟我联系策划这个专栏的时候，我还是持怀疑态度的。为什么呢？现在不比当年了，犹记得十余年前，你使用 MySQL 的过程中碰到问题的话，基本上都只能到代码里去找答案，因为那时网上的资料太少了。

而近十年来，MySQL 在中国广泛普及，技术分享文章可以说是浩如烟海。所以，现在要系统地介绍一遍 MySQL 的话，恐怕里面提及的大多数知识点，都可以在社区文章中找到。那么我们做这个专栏的意义在哪里，而它又凭什么可以收费呢？

直到收到极客时间团队的答复，我才开始对这个专栏“想做和可以做”的事情感觉清晰起来。数据库是一个综合系统，其背后是发展了几十年的数据库理论。同时，数据库系统也是一个应用系统，可能一个业务开发人员用了两三年 MySQL，还未必清楚那些自己一直在用的“最佳实践”为什么是最佳的。

于是，我希望这个专栏能够帮助这样的一些开发者：他们正在使用 MySQL，知道如何写出逻辑正确的 SQL  语句来实现业务目标，却不确定这个语句是不是最优的；他们听说了一些使用数据库的最佳实践，但是更想了解为什么这么做；他们使用的数据库偶尔会出问题，亟需了解如何更快速、更准确地定位问题，甚至自己解决问题……

在过去的七年里，我带过十几个应届毕业生，看着他们成长，要求他们原理先行，再实践验证。几年下来，他们的成长速度都很快，其中好几个毕业没两年就成为团队的骨干力量了。我也在社招的时候面试过很多有着不错的运维实践经验和能力的候选人，但都因为对数据库原理仅有一知半解的了解，而最终遗憾地没有通过面试。

因此，我希望这个专栏能够激发开发者对数据库原理的探索欲，从而更好地理解工作中遇到的问题，更能知道背后的为什么。所以**我会选那些平时使用数据库时高频出现的知识，如事务、索引、锁等内容构成专栏的主线**。这些主线上是一个个的知识点。每个点就是一个概念、一个机制或者一个原理说明。在每个说明之后，我会和你讨论一个实践相关的问题。

希望能以这样的方式，让你对 MySQL 的几条主线有一个整体的认识，并且了解基本概念。在之后的实践篇中，我会引用到这些主线的知识背景，并着力说明它们是怎样指导实践的。这样，**你可以从点到线，再到面，形成自己的 MySQL 知识网络。**

在这里，有一份目录，你也可以先了解下整个专栏的知识结构。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/a78db0b99bbf1149c39b7960f7183c7e-1584367387923.jpg)

如前面说的，这几条主线上的每个知识点几乎都不是最新的，有些甚至十年前就这样，并没有改过。但我希望针对这些点的说明，可以让你在使用 MySQL 时心里更有底，知道怎么做选择，并且明白为什么。了解了原理，才能在实践中不断创新，提升个人的价值和工作输出。

从这里开始，跟我一起搞懂 MySQL!

### 01 基础架构：一条SQL查询语句是如何执行的？

你好，我是林晓斌。

这是专栏的第一篇文章，我想来跟你聊聊 MySQL  的基础架构。我们经常说，看一个事儿千万不要直接陷入细节里，你应该先鸟瞰其全貌，这样能够帮助你从高维度理解问题。同样，对于 MySQL  的学习也是这样。平时我们使用数据库，看到的通常都是一个整体。比如，你有个最简单的表，表里只有一个 ID 字段，在执行下面这个查询语句时：

```csharp
mysql> select * from T where ID=10；
```

我们看到的只是输入一条语句，返回一个结果，却不知道这条语句在 MySQL 内部的执行过程。

所以今天我想和你一起把 MySQL 拆解一下，看看里面都有哪些“零件”，希望借由这个拆解过程，让你对 MySQL 有更深入的理解。这样当我们碰到 MySQL 的一些异常或者问题时，就能够直戳本质，更为快速地定位并解决问题。

下面我给出的是 MySQL 的基本架构示意图，从中你可以清楚地看到 SQL 语句在 MySQL 的各个功能模块中的执行过程。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/0d2070e8f84c4801adbfa03bda1f98d9-1584367388001.png)

MySQL 的逻辑架构图

大体来说，MySQL 可以分为 Server 层和存储引擎层两部分。

Server 层包括连接器、查询缓存、分析器、优化器、执行器等，涵盖 MySQL 的大多数核心服务功能，以及所有的内置函数（如日期、时间、数学和加密函数等），所有跨存储引擎的功能都在这一层实现，比如存储过程、触发器、视图等。

而存储引擎层负责数据的存储和提取。其架构模式是插件式的，支持 InnoDB、MyISAM、Memory 等多个存储引擎。现在最常用的存储引擎是 InnoDB，它从 MySQL 5.5.5 版本开始成为了默认存储引擎。

也就是说，你执行 create table 建表的时候，如果不指定引擎类型，默认使用的就是  InnoDB。不过，你也可以通过指定存储引擎的类型来选择别的引擎，比如在 create table 语句中使用 engine=memory,  来指定使用内存引擎创建表。不同存储引擎的表数据存取方式不同，支持的功能也不同，在后面的文章中，我们会讨论到引擎的选择。

从图中不难看出，不同的存储引擎共用一个**Server 层**，也就是从连接器到执行器的部分。你可以先对每个组件的名字有个印象，接下来我会结合开头提到的那条 SQL 语句，带你走一遍整个执行流程，依次看下每个组件的作用。

#### 连接器

第一步，你会先连接到这个数据库上，这时候接待你的就是连接器。连接器负责跟客户端建立连接、获取权限、维持和管理连接。连接命令一般是这么写的：

```bash
mysql -h$ip -P$port -u$user -p
```

输完命令之后，你就需要在交互对话里面输入密码。虽然密码也可以直接跟在 -p 后面写在命令行中，但这样可能会导致你的密码泄露。如果你连的是生产服务器，强烈建议你不要这么做。

连接命令中的 mysql 是客户端工具，用来跟服务端建立连接。在完成经典的 TCP 握手后，连接器就要开始认证你的身份，这个时候用的就是你输入的用户名和密码。

- 如果用户名或密码不对，你就会收到一个"Access denied for user"的错误，然后客户端程序结束执行。
- 如果用户名密码认证通过，连接器会到权限表里面查出你拥有的权限。之后，这个连接里面的权限判断逻辑，都将依赖于此时读到的权限。

这就意味着，一个用户成功建立连接后，即使你用管理员账号对这个用户的权限做了修改，也不会影响已经存在连接的权限。修改完成后，只有再新建的连接才会使用新的权限设置。

连接完成后，如果你没有后续的动作，这个连接就处于空闲状态，你可以在 show processlist 命令中看到它。文本中这个图是  show processlist 的结果，其中的 Command 列显示为“Sleep”的这一行，就表示现在系统里面有一个空闲连接。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/f2da4aa3a672d48ec05df97b9f992fed-1584367388034.png)客户端如果太长时间没动静，连接器就会自动将它断开。这个时间是由参数 wait_timeout 控制的，默认值是 8 小时。

如果在连接被断开之后，客户端再次发送请求的话，就会收到一个错误提醒： Lost connection to MySQL server during query。这时候如果你要继续，就需要重连，然后再执行请求了。

数据库里面，长连接是指连接成功后，如果客户端持续有请求，则一直使用同一个连接。短连接则是指每次执行完很少的几次查询就断开连接，下次查询再重新建立一个。

建立连接的过程通常是比较复杂的，所以我建议你在使用中要尽量减少建立连接的动作，也就是尽量使用长连接。

但是全部使用长连接后，你可能会发现，有些时候 MySQL 占用内存涨得特别快，这是因为 MySQL  在执行过程中临时使用的内存是管理在连接对象里面的。这些资源会在连接断开的时候才释放。所以如果长连接累积下来，可能导致内存占用太大，被系统强行杀掉（OOM），从现象看就是 MySQL 异常重启了。

怎么解决这个问题呢？你可以考虑以下两种方案。

1. 定期断开长连接。使用一段时间，或者程序里面判断执行过一个占用内存的大查询后，断开连接，之后要查询再重连。
2. 如果你用的是 MySQL 5.7 或更新版本，可以在每次执行一个比较大的操作后，通过执行 mysql_reset_connection 来重新初始化连接资源。这个过程不需要重连和重新做权限验证，但是会将连接恢复到刚刚创建完时的状态。

#### 查询缓存

连接建立完成后，你就可以执行 select 语句了。执行逻辑就会来到第二步：查询缓存。

MySQL 拿到一个查询请求后，会先到查询缓存看看，之前是不是执行过这条语句。之前执行过的语句及其结果可能会以 key-value  对的形式，被直接缓存在内存中。key 是查询的语句，value 是查询的结果。如果你的查询能够直接在这个缓存中找到 key，那么这个 value 就会被直接返回给客户端。

如果语句不在查询缓存中，就会继续后面的执行阶段。执行完成后，执行结果会被存入查询缓存中。你可以看到，如果查询命中缓存，MySQL 不需要执行后面的复杂操作，就可以直接返回结果，这个效率会很高。

**但是大多数情况下我会建议你不要使用查询缓存，为什么呢？因为查询缓存往往弊大于利。**

查询缓存的失效非常频繁，只要有对一个表的更新，这个表上所有的查询缓存都会被清空。因此很可能你费劲地把结果存起来，还没使用呢，就被一个更新全清空了。对于更新压力大的数据库来说，查询缓存的命中率会非常低。除非你的业务就是有一张静态表，很长时间才会更新一次。比如，一个系统配置表，那这张表上的查询才适合使用查询缓存。

好在 MySQL 也提供了这种“按需使用”的方式。你可以将参数 query_cache_type 设置成 DEMAND，这样对于默认的  SQL 语句都不使用查询缓存。而对于你确定要使用查询缓存的语句，可以用 SQL_CACHE 显式指定，像下面这个语句一样：

```csharp
mysql> select SQL_CACHE * from T where ID=10；
```

需要注意的是，MySQL 8.0 版本直接将查询缓存的整块功能删掉了，也就是说 8.0 开始彻底没有这个功能了。

#### 分析器

如果没有命中查询缓存，就要开始真正执行语句了。首先，MySQL 需要知道你要做什么，因此需要对 SQL 语句做解析。

分析器先会做“词法分析”。你输入的是由多个字符串和空格组成的一条 SQL 语句，MySQL 需要识别出里面的字符串分别是什么，代表什么。

MySQL 从你输入的"select"这个关键字识别出来，这是一个查询语句。它也要把字符串“T”识别成“表名 T”，把字符串“ID”识别成“列 ID”。

做完了这些识别以后，就要做“语法分析”。根据词法分析的结果，语法分析器会根据语法规则，判断你输入的这个 SQL 语句是否满足 MySQL 语法。

如果你的语句不对，就会收到“You have an error in your SQL syntax”的错误提醒，比如下面这个语句 select 少打了开头的字母“s”。

```vbnet
mysql> elect * from t where ID=1; 
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'elect * from t where ID=1' at line 1
```

一般语法错误会提示第一个出现错误的位置，所以你要关注的是紧接“use near”的内容。

#### 优化器

经过了分析器，MySQL 就知道你要做什么了。在开始执行之前，还要先经过优化器的处理。

优化器是在表里面有多个索引的时候，决定使用哪个索引；或者在一个语句有多表关联（join）的时候，决定各个表的连接顺序。比如你执行下面这样的语句，这个语句是执行两个表的 join：

```csharp
mysql> select * from t1 join t2 using(ID)  where t1.c=10 and t2.d=20;
```

- 既可以先从表 t1 里面取出 c=10 的记录的 ID 值，再根据 ID 值关联到表 t2，再判断 t2 里面 d 的值是否等于 20。
- 也可以先从表 t2 里面取出 d=20 的记录的 ID 值，再根据 ID 值关联到 t1，再判断 t1 里面 c 的值是否等于 10。

这两种执行方法的逻辑结果是一样的，但是执行的效率会有不同，而优化器的作用就是决定选择使用哪一个方案。

优化器阶段完成后，这个语句的执行方案就确定下来了，然后进入执行器阶段。如果你还有一些疑问，比如优化器是怎么选择索引的，有没有可能选择错等等，没关系，我会在后面的文章中单独展开说明优化器的内容。

#### 执行器

MySQL 通过分析器知道了你要做什么，通过优化器知道了该怎么做，于是就进入了执行器阶段，开始执行语句。

开始执行的时候，要先判断一下你对这个表 T 有没有执行查询的权限，如果没有，就会返回没有权限的错误，如下所示 (在工程实现上，如果命中查询缓存，会在查询缓存返回结果的时候，做权限验证。查询也会在优化器之前调用 precheck 验证权限)。

```sql
mysql> select * from T where ID=10; 
ERROR 1142 (42000): SELECT command denied to user 'b'@'localhost' for table 'T'
```

如果有权限，就打开表继续执行。打开表的时候，执行器就会根据表的引擎定义，去使用这个引擎提供的接口。

比如我们这个例子中的表 T 中，ID 字段没有索引，那么执行器的执行流程是这样的：

1. 调用 InnoDB 引擎接口取这个表的第一行，判断 ID 值是不是 10，如果不是则跳过，如果是则将这行存在结果集中；
2. 调用引擎接口取“下一行”，重复相同的判断逻辑，直到取到这个表的最后一行。
3. 执行器将上述遍历过程中所有满足条件的行组成的记录集作为结果集返回给客户端。

至此，这个语句就执行完成了。

对于有索引的表，执行的逻辑也差不多。第一次调用的是“取满足条件的第一行”这个接口，之后循环取“满足条件的下一行”这个接口，这些接口都是引擎中已经定义好的。

你会在数据库的慢查询日志中看到一个 rows_examined 的字段，表示这个语句执行过程中扫描了多少行。这个值就是在执行器每次调用引擎获取数据行的时候累加的。

在有些场景下，执行器调用一次，在引擎内部则扫描了多行，因此**引擎扫描行数跟 rows_examined 并不是完全相同的。**我们后面会专门有一篇文章来讲存储引擎的内部机制，里面会有详细的说明。

#### 小结

今天我给你介绍了 MySQL 的逻辑架构，希望你对一个 SQL 语句完整执行流程的各个阶段有了一个初步的印象。由于篇幅的限制，我只是用一个查询的例子将各个环节过了一遍。如果你还对每个环节的展开细节存有疑问，也不用担心，后续在实战章节中我还会再提到它们。

我给你留一个问题吧，如果表 T 中没有字段 k，而你执行了这个语句 select * from T where k=1,  那肯定是会报“不存在这个列”的错误： “Unknown column ‘k’ in ‘where  clause’”。你觉得这个错误是在我们上面提到的哪个阶段报出来的呢？

感谢你的收听，欢迎你给我留言，也欢迎分享给更多的朋友一起阅读。

### 02 日志系统：一条SQL更新语句是如何执行的？

前面我们系统了解了一个查询语句的执行流程，并介绍了执行过程中涉及的处理模块。相信你还记得，一条查询语句的执行过程一般是经过连接器、分析器、优化器、执行器等功能模块，最后到达存储引擎。

那么，一条更新语句的执行流程又是怎样的呢？

之前你可能经常听 DBA 同事说，MySQL 可以恢复到半个月内任意一秒的状态，惊叹的同时，你是不是心中也会不免会好奇，这是怎样做到的呢？

我们还是从一个表的一条更新语句说起，下面是这个表的创建语句，这个表有一个主键 ID 和一个整型字段 c：

```sql
mysql> create table T(ID int primary key, c int);
```

如果要将 ID=2 这一行的值加 1，SQL 语句就会这么写：

```r
mysql> update T set c=c+1 where ID=2;
```

前面我有跟你介绍过 SQL 语句基本的执行链路，这里我再把那张图拿过来，你也可以先简单看看这个图回顾下。首先，可以确定的说，查询语句的那一套流程，更新语句也是同样会走一遍。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/0d2070e8f84c4801adbfa03bda1f98d9-1550568677558-1584367387960.png)

MySQL 的逻辑架构图

你执行语句前要先连接数据库，这是连接器的工作。

前面我们说过，在一个表上有更新的时候，跟这个表有关的查询缓存会失效，所以这条语句就会把表 T 上所有缓存结果都清空。这也就是我们一般不建议使用查询缓存的原因。

接下来，分析器会通过词法和语法解析知道这是一条更新语句。优化器决定要使用 ID 这个索引。然后，执行器负责具体执行，找到这一行，然后更新。

与查询流程不一样的是，更新流程还涉及两个重要的日志模块，它们正是我们今天要讨论的主角：redo log（重做日志）和  binlog（归档日志）。如果接触 MySQL，那这两个词肯定是绕不过的，我后面的内容里也会不断地和你强调。不过话说回来，redo log 和  binlog 在设计上有很多有意思的地方，这些设计思路也可以用到你自己的程序里。

#### 重要的日志模块：redo log

不知道你还记不记得《孔乙己》这篇文章，酒店掌柜有一个粉板，专门用来记录客人的赊账记录。如果赊账的人不多，那么他可以把顾客名和账目写在板上。但如果赊账的人多了，粉板总会有记不下的时候，这个时候掌柜一定还有一个专门记录赊账的账本。

如果有人要赊账或者还账的话，掌柜一般有两种做法：

- 一种做法是直接把账本翻出来，把这次赊的账加上去或者扣除掉；
- 另一种做法是先在粉板上记下这次的账，等打烊以后再把账本翻出来核算。

在生意红火柜台很忙时，掌柜一定会选择后者，因为前者操作实在是太麻烦了。首先，你得找到这个人的赊账总额那条记录。你想想，密密麻麻几十页，掌柜要找到那个名字，可能还得带上老花镜慢慢找，找到之后再拿出算盘计算，最后再将结果写回到账本上。

这整个过程想想都麻烦。相比之下，还是先在粉板上记一下方便。你想想，如果掌柜没有粉板的帮助，每次记账都得翻账本，效率是不是低得让人难以忍受？

同样，在 MySQL 里也有这个问题，如果每一次的更新操作都需要写进磁盘，然后磁盘也要找到对应的那条记录，然后再更新，整个过程 IO 成本、查找成本都很高。为了解决这个问题，MySQL 的设计者就用了类似酒店掌柜粉板的思路来提升更新效率。

而粉板和账本配合的整个过程，其实就是 MySQL 里经常说到的 WAL 技术，WAL 的全称是 Write-Ahead Logging，它的关键点就是先写日志，再写磁盘，也就是先写粉板，等不忙的时候再写账本。

具体来说，当有一条记录需要更新的时候，InnoDB 引擎就会先把记录写到 redo  log（粉板）里面，并更新内存，这个时候更新就算完成了。同时，InnoDB  引擎会在适当的时候，将这个操作记录更新到磁盘里面，而这个更新往往是在系统比较空闲的时候做，这就像打烊以后掌柜做的事。

如果今天赊账的不多，掌柜可以等打烊后再整理。但如果某天赊账的特别多，粉板写满了，又怎么办呢？这个时候掌柜只好放下手中的活儿，把粉板中的一部分赊账记录更新到账本中，然后把这些记录从粉板上擦掉，为记新账腾出空间。

与此类似，InnoDB 的 redo log 是固定大小的，比如可以配置为一组 4 个文件，每个文件的大小是 1GB，那么这块“粉板”总共就可以记录 4GB 的操作。从头开始写，写到末尾就又回到开头循环写，如下面这个图所示。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/b075250cad8d9f6c791a52b6a600f69c-1584367387977.jpg)

write pos 是当前记录的位置，一边写一边后移，写到第 3 号文件末尾后就回到 0 号文件开头。checkpoint 是当前要擦除的位置，也是往后推移并且循环的，擦除记录前要把记录更新到数据文件。

write pos 和 checkpoint 之间的是“粉板”上还空着的部分，可以用来记录新的操作。如果 write pos 追上  checkpoint，表示“粉板”满了，这时候不能再执行新的更新，得停下来先擦掉一些记录，把 checkpoint 推进一下。

有了 redo log，InnoDB 就可以保证即使数据库发生异常重启，之前提交的记录都不会丢失，这个能力称为**crash-safe**。

要理解 crash-safe 这个概念，可以想想我们前面赊账记录的例子。只要赊账记录记在了粉板上或写在了账本上，之后即使掌柜忘记了，比如突然停业几天，恢复生意后依然可以通过账本和粉板上的数据明确赊账账目。

#### 重要的日志模块：binlog

前面我们讲过，MySQL 整体来看，其实就有两块：一块是 Server 层，它主要做的是 MySQL  功能层面的事情；还有一块是引擎层，负责存储相关的具体事宜。上面我们聊到的粉板 redo log 是 InnoDB 引擎特有的日志，而  Server 层也有自己的日志，称为 binlog（归档日志）。

我想你肯定会问，为什么会有两份日志呢？

因为最开始 MySQL 里并没有 InnoDB 引擎。MySQL 自带的引擎是 MyISAM，但是 MyISAM 没有  crash-safe 的能力，binlog 日志只能用于归档。而 InnoDB 是另一个公司以插件形式引入 MySQL 的，既然只依靠  binlog 是没有 crash-safe 能力的，所以 InnoDB 使用另外一套日志系统——也就是 redo log 来实现  crash-safe 能力。

这两种日志有以下三点不同。

1. redo log 是 InnoDB 引擎特有的；binlog 是 MySQL 的 Server 层实现的，所有引擎都可以使用。
2. redo log 是物理日志，记录的是“在某个数据页上做了什么修改”；binlog 是逻辑日志，记录的是这个语句的原始逻辑，比如“给 ID=2 这一行的 c 字段加 1 ”。
3. redo log 是循环写的，空间固定会用完；binlog 是可以追加写入的。“追加写”是指 binlog 文件写到一定大小后会切换到下一个，并不会覆盖以前的日志。

有了对这两个日志的概念性理解，我们再来看执行器和 InnoDB 引擎在执行这个简单的 update 语句时的内部流程。

1. 执行器先找引擎取 ID=2 这一行。ID 是主键，引擎直接用树搜索找到这一行。如果 ID=2 这一行所在的数据页本来就在内存中，就直接返回给执行器；否则，需要先从磁盘读入内存，然后再返回。
2. 执行器拿到引擎给的行数据，把这个值加上 1，比如原来是 N，现在就是 N+1，得到新的一行数据，再调用引擎接口写入这行新数据。
3. 引擎将这行新数据更新到内存中，同时将这个更新操作记录到 redo log 里面，此时 redo log 处于 prepare 状态。然后告知执行器执行完成了，随时可以提交事务。
4. 执行器生成这个操作的 binlog，并把 binlog 写入磁盘。
5. 执行器调用引擎的提交事务接口，引擎把刚刚写入的 redo log 改成提交（commit）状态，更新完成。

这里我给出这个 update 语句的执行流程图，图中浅色框表示是在 InnoDB 内部执行的，深色框表示是在执行器中执行的。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/2e5bff4910ec189fe1ee6e2ecc7b4bbe-1584367387984.png)

update 语句执行流程

你可能注意到了，最后三步看上去有点“绕”，将 redo log 的写入拆成了两个步骤：prepare 和 commit，这就是"两阶段提交"。

#### 两阶段提交

为什么必须有“两阶段提交”呢？这是为了让两份日志之间的逻辑一致。要说明这个问题，我们得从文章开头的那个问题说起：**怎样让数据库恢复到半个月内任意一秒的状态？**

前面我们说过了，binlog 会记录所有的逻辑操作，并且是采用“追加写”的形式。如果你的 DBA  承诺说半个月内可以恢复，那么备份系统中一定会保存最近半个月的所有  binlog，同时系统会定期做整库备份。这里的“定期”取决于系统的重要性，可以是一天一备，也可以是一周一备。

当需要恢复到指定的某一秒时，比如某天下午两点发现中午十二点有一次误删表，需要找回数据，那你可以这么做：

- 首先，找到最近的一次全量备份，如果你运气好，可能就是昨天晚上的一个备份，从这个备份恢复到临时库；
- 然后，从备份的时间点开始，将备份的 binlog 依次取出来，重放到中午误删表之前的那个时刻。

这样你的临时库就跟误删之前的线上库一样了，然后你可以把表数据从临时库取出来，按需要恢复到线上库去。

好了，说完了数据恢复过程，我们回来说说，为什么日志需要“两阶段提交”。这里不妨用反证法来进行解释。

由于 redo log 和 binlog 是两个独立的逻辑，如果不用两阶段提交，要么就是先写完 redo log 再写 binlog，或者采用反过来的顺序。我们看看这两种方式会有什么问题。

仍然用前面的 update 语句来做例子。假设当前 ID=2 的行，字段 c 的值是 0，再假设执行 update 语句过程中在写完第一个日志后，第二个日志还没有写完期间发生了 crash，会出现什么情况呢？

1. **先写 redo log 后写 binlog**。假设在 redo log 写完，binlog  还没有写完的时候，MySQL 进程异常重启。由于我们前面说过的，redo log  写完之后，系统即使崩溃，仍然能够把数据恢复回来，所以恢复后这一行 c 的值是 1。 但是由于 binlog 没写完就 crash 了，这时候  binlog 里面就没有记录这个语句。因此，之后备份日志的时候，存起来的 binlog 里面就没有这条语句。 然后你会发现，如果需要用这个  binlog 来恢复临时库的话，由于这个语句的 binlog 丢失，这个临时库就会少了这一次更新，恢复出来的这一行 c 的值就是  0，与原库的值不同。
2. **先写 binlog 后写 redo log**。如果在 binlog 写完之后 crash，由于 redo log 还没写，崩溃恢复以后这个事务无效，所以这一行 c 的值是 0。但是 binlog 里面已经记录了“把 c 从 0 改成  1”这个日志。所以，在之后用 binlog 来恢复的时候就多了一个事务出来，恢复出来的这一行 c 的值就是 1，与原库的值不同。

可以看到，如果不使用“两阶段提交”，那么数据库的状态就有可能和用它的日志恢复出来的库的状态不一致。

你可能会说，这个概率是不是很低，平时也没有什么动不动就需要恢复临时库的场景呀？

其实不是的，不只是误操作后需要用这个过程来恢复数据。当你需要扩容的时候，也就是需要再多搭建一些备库来增加系统的读能力的时候，现在常见的做法也是用全量备份加上应用 binlog 来实现的，这个“不一致”就会导致你的线上出现主从数据库不一致的情况。

简单说，redo log 和 binlog 都可以用于表示事务的提交状态，而两阶段提交就是让这两个状态保持逻辑上的一致。

#### 小结

今天，我介绍了 MySQL 里面最重要的两个日志，即物理日志 redo log 和逻辑日志 binlog。

redo log 用于保证 crash-safe 能力。innodb_flush_log_at_trx_commit 这个参数设置成 1  的时候，表示每次事务的 redo log 都直接持久化到磁盘。这个参数我建议你设置成 1，这样可以保证 MySQL 异常重启之后数据不丢失。

sync_binlog 这个参数设置成 1 的时候，表示每次事务的 binlog 都持久化到磁盘。这个参数我也建议你设置成 1，这样可以保证 MySQL 异常重启之后 binlog 不丢失。

我还跟你介绍了与 MySQL 日志系统密切相关的“两阶段提交”。两阶段提交是跨系统维持数据逻辑一致性时常用的一个方案，即使你不做数据库内核开发，日常开发中也有可能会用到。

文章的最后，我给你留一个思考题吧。前面我说到定期全量备份的周期“取决于系统重要性，有的是一天一备，有的是一周一备”。那么在什么场景下，一天一备会比一周一备更有优势呢？或者说，它影响了这个数据库系统的哪个指标？

你可以把你的思考和观点写在留言区里，我会在下一篇文章的末尾给出我的答案。

感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

### 03 事务隔离：为什么你改了我还看不见？

提到事务，你肯定不陌生，和数据库打交道的时候，我们总是会用到事务。最经典的例子就是转账，你要给朋友小王转 100 块钱，而此时你的银行卡只有 100 块钱。

转账过程具体到程序里会有一系列的操作，比如查询余额、做加减法、更新余额等，这些操作必须保证是一体的，不然等程序查完之后，还没做减法之前，你这 100 块钱，完全可以借着这个时间差再查一次，然后再给另外一个朋友转账，如果银行这么整，不就乱了么？这时就要用到“事务”这个概念了。

简单来说，事务就是要保证一组数据库操作，要么全部成功，要么全部失败。在 MySQL 中，事务支持是在引擎层实现的。你现在知道，MySQL  是一个支持多引擎的系统，但并不是所有的引擎都支持事务。比如 MySQL 原生的 MyISAM 引擎就不支持事务，这也是 MyISAM 被  InnoDB 取代的重要原因之一。

今天的文章里，我将会以 InnoDB 为例，剖析 MySQL 在事务支持方面的特定实现，并基于原理给出相应的实践建议，希望这些案例能加深你对 MySQL 事务原理的理解。

#### 隔离性与隔离级别

提到事务，你肯定会想到 ACID（Atomicity、Consistency、Isolation、Durability，即原子性、一致性、隔离性、持久性），今天我们就来说说其中 I，也就是“隔离性”。

当数据库上有多个事务同时执行的时候，就可能出现脏读（dirty read）、不可重复读（non-repeatable read）、幻读（phantom read）的问题，为了解决这些问题，就有了“隔离级别”的概念。

在谈隔离级别之前，你首先要知道，你隔离得越严实，效率就会越低。因此很多时候，我们都要在二者之间寻找一个平衡点。SQL  标准的事务隔离级别包括：读未提交（read uncommitted）、读提交（read committed）、可重复读（repeatable  read）和串行化（serializable ）。下面我逐一为你解释：

- 读未提交是指，一个事务还没提交时，它做的变更就能被别的事务看到。
- 读提交是指，一个事务提交之后，它做的变更才会被其他事务看到。
- 可重复读是指，一个事务执行过程中看到的数据，总是跟这个事务在启动时看到的数据是一致的。当然在可重复读隔离级别下，未提交变更对其他事务也是不可见的。
- 串行化，顾名思义是对于同一行记录，“写”会加“写锁”，“读”会加“读锁”。当出现读写锁冲突的时候，后访问的事务必须等前一个事务执行完成，才能继续执行。

其中“读提交”和“可重复读”比较难理解，所以我用一个例子说明这几种隔离级别。假设数据表 T 中只有一列，其中一行的值为 1，下面是按照时间顺序执行两个事务的行为。

```sql
mysql> create table T(c int) engine=InnoDB;
insert into T(c) values(1);
```

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/7dea45932a6b722eb069d2264d0066f8-1584367388045.png)我们来看看在不同的隔离级别下，事务 A 会有哪些不同的返回结果，也就是图里面 V1、V2、V3 的返回值分别是什么。

- 若隔离级别是“读未提交”， 则 V1 的值就是 2。这时候事务 B 虽然还没有提交，但是结果已经被 A 看到了。因此，V2、V3 也都是 2。
- 若隔离级别是“读提交”，则 V1 是 1，V2 的值是 2。事务 B 的更新在提交后才能被 A 看到。所以， V3 的值也是 2。
- 若隔离级别是“可重复读”，则 V1、V2 是 1，V3 是 2。之所以 V2 还是 1，遵循的就是这个要求：事务在执行期间看到的数据前后必须是一致的。
- 若隔离级别是“串行化”，则在事务 B 执行“将 1 改成 2”的时候，会被锁住。直到事务 A 提交后，事务 B 才可以继续执行。所以从 A 的角度看， V1、V2 值是 1，V3 的值是 2。

在实现上，数据库里面会创建一个视图，访问的时候以视图的逻辑结果为准。在“可重复读”隔离级别下，这个视图是在事务启动时创建的，整个事务存在期间都用这个视图。在“读提交”隔离级别下，这个视图是在每个 SQL  语句开始执行的时候创建的。这里需要注意的是，“读未提交”隔离级别下直接返回记录上的最新值，没有视图概念；而“串行化”隔离级别下直接用加锁的方式来避免并行访问。

我们可以看到在不同的隔离级别下，数据库行为是有所不同的。Oracle 数据库的默认隔离级别其实就是“读提交”，因此对于一些从 Oracle 迁移到 MySQL 的应用，为保证数据库隔离级别的一致，你一定要记得将 MySQL 的隔离级别设置为“读提交”。

配置的方式是，将启动参数 transaction-isolation 的值设置成 READ-COMMITTED。你可以用 show variables 来查看当前的值。

```sql
mysql> show variables like 'transaction_isolation'; 
+-----------------------+----------------+ 
| Variable_name | Value | 
+-----------------------+----------------+ 
| transaction_isolation | READ-COMMITTED | 
+-----------------------+----------------+
```

总结来说，存在即合理，哪个隔离级别都有它自己的使用场景，你要根据自己的业务情况来定。我想**你可能会问那什么时候需要“可重复读”的场景呢**？我们来看一个数据校对逻辑的案例。

假设你在管理一个个人银行账户表。一个表存了每个月月底的余额，一个表存了账单明细。这时候你要做数据校对，也就是判断上个月的余额和当前余额的差额，是否与本月的账单明细一致。你一定希望在校对过程中，即使有用户发生了一笔新的交易，也不影响你的校对结果。

这时候使用“可重复读”隔离级别就很方便。事务启动时的视图可以认为是静态的，不受其他事务更新的影响。

#### 事务隔离的实现

理解了事务的隔离级别，我们再来看看事务隔离具体是怎么实现的。这里我们展开说明“可重复读”。

在 MySQL 中，实际上每条记录在更新的时候都会同时记录一条回滚操作。记录上的最新值，通过回滚操作，都可以得到前一个状态的值。

假设一个值从 1 被按顺序改成了 2、3、4，在回滚日志里面就会有类似下面的记录。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/d9c313809e5ac148fc39feff532f0fee-1584367388025.png)当前值是 4，但是在查询这条记录的时候，不同时刻启动的事务会有不同的 read-view。如图中看到的，在视图 A、B、C 里面，这一个记录的值分别是  1、2、4，同一条记录在系统中可以存在多个版本，就是数据库的多版本并发控制（MVCC）。对于 read-view A，要得到  1，就必须将当前值依次执行图中所有的回滚操作得到。

同时你会发现，即使现在有另外一个事务正在将 4 改成 5，这个事务跟 read-view A、B、C 对应的事务是不会冲突的。

你一定会问，回滚日志总不能一直保留吧，什么时候删除呢？答案是，在不需要的时候才删除。也就是说，系统会判断，当没有事务再需要用到这些回滚日志时，回滚日志会被删除。

什么时候才不需要了呢？就是当系统里没有比这个回滚日志更早的 read-view 的时候。

基于上面的说明，我们来讨论一下为什么建议你尽量不要使用长事务。

长事务意味着系统里面会存在很老的事务视图。由于这些事务随时可能访问数据库里面的任何数据，所以这个事务提交之前，数据库里面它可能用到的回滚记录都必须保留，这就会导致大量占用存储空间。

在 MySQL 5.5 及以前的版本，回滚日志是跟数据字典一起放在 ibdata 文件里的，即使长事务最终提交，回滚段被清理，文件也不会变小。我见过数据只有 20GB，而回滚段有 200GB 的库。最终只好为了清理回滚段，重建整个库。

除了对回滚段的影响，长事务还占用锁资源，也可能拖垮整个库，这个我们会在后面讲锁的时候展开。

事务的启动方式

如前面所述，长事务有这些潜在风险，我当然是建议你尽量避免。其实很多时候业务开发同学并不是有意使用长事务，通常是由于误用所致。MySQL 的事务启动方式有以下几种：

1. 显式启动事务语句， begin 或 start transaction。配套的提交语句是 commit，回滚语句是 rollback。
2. set autocommit=0，这个命令会将这个线程的自动提交关掉。意味着如果你只执行一个 select 语句，这个事务就启动了，而且并不会自动提交。这个事务持续存在直到你主动执行 commit 或 rollback 语句，或者断开连接。

有些客户端连接框架会默认连接成功后先执行一个 set autocommit=0 的命令。这就导致接下来的查询都在事务中，如果是长连接，就导致了意外的长事务。

因此，我会建议你总是使用 set autocommit=1, 通过显式语句的方式来启动事务。

但是有的开发同学会纠结“多一次交互”的问题。对于一个需要频繁使用事务的业务，第二种方式每个事务在开始时都不需要主动执行一次 “begin”，减少了语句的交互次数。如果你也有这个顾虑，我建议你使用 commit work and chain 语法。

在 autocommit 为 1 的情况下，用 begin 显式启动的事务，如果执行 commit 则提交事务。如果执行 commit  work and chain，则是提交事务并自动启动下一个事务，这样也省去了再次执行 begin  语句的开销。同时带来的好处是从程序开发的角度明确地知道每个语句是否处于事务中。

你可以在 information_schema 库的 innodb_trx 这个表中查询长事务，比如下面这个语句，用于查找持续时间超过 60s 的事务。

```csharp
select * from information_schema.innodb_trx where TIME_TO_SEC(timediff(now(),trx_started))>60
```

#### 小结

这篇文章里面，我介绍了 MySQL 的事务隔离级别的现象和实现，根据实现原理分析了长事务存在的风险，以及如何用正确的方式避免长事务。希望我举的例子能够帮助你理解事务，并更好地使用 MySQL 的事务特性。

我给你留一个问题吧。你现在知道了系统里面应该避免长事务，如果你是业务开发负责人同时也是数据库负责人，你会有什么方案来避免出现或者处理这种情况呢？

你可以把你的思考和观点写在留言区里，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。



### 04 深入浅出索引（上）

提到数据库索引，我想你并不陌生，在日常工作中会经常接触到。比如某一个 SQL 查询比较慢，分析完原因之后，你可能就会说“给某个字段加个索引吧”之类的解决方案。但到底什么是索引，索引又是如何工作的呢？今天就让我们一起来聊聊这个话题吧。

数据库索引的内容比较多，我分成了上下两篇文章。索引是数据库系统里面最重要的概念之一，所以我希望你能够耐心看完。在后面的实战文章中，我也会经常引用这两篇文章中提到的知识点，加深你对数据库索引的理解。

一句话简单来说，索引的出现其实就是为了提高数据查询的效率，就像书的目录一样。一本 500 页的书，如果你想快速找到其中的某一个知识点，在不借助目录的情况下，那我估计你可得找一会儿。同样，对于数据库的表而言，索引其实就是它的“目录”。

#### 索引的常见模型

索引的出现是为了提高查询效率，但是实现索引的方式却有很多种，所以这里也就引入了索引模型的概念。可以用于提高读写效率的数据结构很多，这里我先给你介绍三种常见、也比较简单的数据结构，它们分别是哈希表、有序数组和搜索树。

下面我主要从使用的角度，为你简单分析一下这三种模型的区别。

哈希表是一种以键 - 值（key-value）存储数据的结构，我们只要输入待查找的值即 key，就可以找到其对应的值即 Value。哈希的思路很简单，把值放在数组里，用一个哈希函数把 key 换算成一个确定的位置，然后把 value 放在数组的这个位置。

不可避免地，多个 key 值经过哈希函数的换算，会出现同一个值的情况。处理这种情况的一种方法是，拉出一个链表。

假设，你现在维护着一个身份证信息和姓名的表，需要根据身份证号查找对应的名字，这时对应的哈希索引的示意图如下所示：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/0c62b601afda86fe5d0fe57346ace957-1584367388037.png)

图 1 哈希表示意图

图中，User2 和 User4 根据身份证号算出来的值都是 N，但没关系，后面还跟了一个链表。假设，这时候你要查 ID_card_n2  对应的名字是什么，处理步骤就是：首先，将 ID_card_n2 通过哈希函数算出 N；然后，按顺序遍历，找到 User2。

需要注意的是，图中四个 ID_card_n 的值并不是递增的，这样做的好处是增加新的 User 时速度会很快，只需要往后追加。但缺点是，因为不是有序的，所以哈希索引做区间查询的速度是很慢的。

你可以设想下，如果你现在要找身份证号在 [ID_card_X, ID_card_Y] 这个区间的所有用户，就必须全部扫描一遍了。

所以，**哈希表这种结构适用于只有等值查询的场景**，比如 Memcached 及其他一些 NoSQL 引擎。

而**有序数组在等值查询和范围查询场景中的性能就都非常优秀**。还是上面这个根据身份证号查名字的例子，如果我们使用有序数组来实现的话，示意图如下所示：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/bfc907a92f99cadf5493cf0afac9ca49-1584367388058.png)

图 2 有序数组示意图

这里我们假设身份证号没有重复，这个数组就是按照身份证号递增的顺序保存的。这时候如果你要查 ID_card_n2 对应的名字，用二分法就可以快速得到，这个时间复杂度是 O(log(N))。

同时很显然，这个索引结构支持范围查询。你要查身份证号在 [ID_card_X, ID_card_Y] 区间的 User，可以先用二分法找到 ID_card_X（如果不存在 ID_card_X，就找到大于 ID_card_X 的第一个 User），然后向右遍历，直到查到第一个大于  ID_card_Y 的身份证号，退出循环。

如果仅仅看查询效率，有序数组就是最好的数据结构了。但是，在需要更新数据的时候就麻烦了，你往中间插入一个记录就必须得挪动后面所有的记录，成本太高。

所以，**有序数组索引只适用于静态存储引擎**，比如你要保存的是 2017 年某个城市的所有人口信息，这类不会再修改的数据。

二叉搜索树也是课本里的经典数据结构了。还是上面根据身份证号查名字的例子，如果我们用二叉搜索树来实现的话，示意图如下所示：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/04fb9d24065635a6a637c25ba9ddde68-1584367388076.png)

图 3 二叉搜索树示意图

二叉搜索树的特点是：每个节点的左儿子小于父节点，父节点又小于右儿子。这样如果你要查 ID_card_n2 的话，按照图中的搜索顺序就是按照 UserA -> UserC -> UserF -> User2 这个路径得到。这个时间复杂度是 O(log(N))。

当然为了维持 O(log(N)) 的查询复杂度，你就需要保持这棵树是平衡二叉树。为了做这个保证，更新的时间复杂度也是 O(log(N))。

树可以有二叉，也可以有多叉。多叉树就是每个节点有多个儿子，儿子之间的大小保证从左到右递增。二叉树是搜索效率最高的，但是实际上大多数的数据库存储却并不使用二叉树。其原因是，索引不止存在内存中，还要写到磁盘上。

你可以想象一下一棵 100 万节点的平衡二叉树，树高 20。一次查询可能需要访问 20  个数据块。在机械硬盘时代，从磁盘随机读一个数据块需要 10 ms 左右的寻址时间。也就是说，对于一个 100  万行的表，如果使用二叉树来存储，单独访问一个行可能需要 20 个 10 ms 的时间，这个查询可真够慢的。

为了让一个查询尽量少地读磁盘，就必须让查询过程访问尽量少的数据块。那么，我们就不应该使用二叉树，而是要使用“N 叉”树。这里，“N 叉”树中的“N”取决于数据块的大小。

以 InnoDB 的一个整数字段索引为例，这个 N 差不多是 1200。这棵树高是 4 的时候，就可以存 1200 的 3  次方个值，这已经 17 亿了。考虑到树根的数据块总是在内存中的，一个 10 亿行的表上一个整数字段的索引，查找一个值最多只需要访问 3  次磁盘。其实，树的第二层也有很大概率在内存中，那么访问磁盘的平均次数就更少了。

N 叉树由于在读写上的性能优点，以及适配磁盘的访问模式，已经被广泛应用在数据库引擎中了。

不管是哈希还是有序数组，或者 N 叉树，它们都是不断迭代、不断优化的产物或者解决方案。数据库技术发展到今天，跳表、LSM 树等数据结构也被用于引擎设计中，这里我就不再一一展开了。

你心里要有个概念，数据库底层存储的核心就是基于这些数据模型的。每碰到一个新数据库，我们需要先关注它的数据模型，这样才能从理论上分析出这个数据库的适用场景。

截止到这里，我用了半篇文章的篇幅和你介绍了不同的数据结构，以及它们的适用场景，你可能会觉得有些枯燥。但是，我建议你还是要多花一些时间来理解这部分内容，毕竟这是数据库处理数据的核心概念之一，在分析问题的时候会经常用到。当你理解了索引的模型后，就会发现在分析问题的时候会有一个更清晰的视角，体会到引擎设计的精妙之处。

现在，我们一起进入相对偏实战的内容吧。

在 MySQL  中，索引是在存储引擎层实现的，所以并没有统一的索引标准，即不同存储引擎的索引的工作方式并不一样。而即使多个存储引擎支持同一种类型的索引，其底层的实现也可能不同。由于 InnoDB 存储引擎在 MySQL 数据库中使用最为广泛，所以下面我就以 InnoDB 为例，和你分析一下其中的索引模型。

#### InnoDB 的索引模型

在 InnoDB 中，表都是根据主键顺序以索引的形式存放的，这种存储方式的表称为索引组织表。又因为前面我们提到的，InnoDB 使用了 B+ 树索引模型，所以数据都是存储在 B+ 树中的。

每一个索引在 InnoDB 里面对应一棵 B+ 树。

假设，我们有一个主键列为 ID 的表，表中有字段 k，并且在 k 上有索引。

这个表的建表语句是：

```sql
mysql> create table T(
id int primary key, 
k int not null, 
name varchar(16),
index (k))engine=InnoDB;
```

表中 R1~R5 的 (ID,k) 值分别为 (100,1)、(200,2)、(300,3)、(500,5) 和 (600,6)，两棵树的示例示意图如下。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/dcda101051f28502bd5c4402b292e38d-1584367388237.png)

图 4 InnoDB 的索引组织结构

从图中不难看出，根据叶子节点的内容，索引类型分为主键索引和非主键索引。

主键索引的叶子节点存的是整行数据。在 InnoDB 里，主键索引也被称为聚簇索引（clustered index）。

非主键索引的叶子节点内容是主键的值。在 InnoDB 里，非主键索引也被称为二级索引（secondary index）。

根据上面的索引结构说明，我们来讨论一个问题：**基于主键索引和普通索引的查询有什么区别？**

- 如果语句是 select * from T where ID=500，即主键查询方式，则只需要搜索 ID 这棵 B+ 树；
- 如果语句是 select * from T where k=5，即普通索引查询方式，则需要先搜索 k 索引树，得到 ID 的值为 500，再到 ID 索引树搜索一次。这个过程称为回表。

也就是说，基于非主键索引的查询需要多扫描一棵索引树。因此，我们在应用中应该尽量使用主键查询。

#### 索引维护

B+ 树为了维护索引有序性，在插入新值的时候需要做必要的维护。以上面这个图为例，如果插入新的行 ID 值为 700，则只需要在 R5 的记录后面插入一个新记录。如果新插入的 ID 值为 400，就相对麻烦了，需要逻辑上挪动后面的数据，空出位置。

而更糟的情况是，如果 R5 所在的数据页已经满了，根据 B+ 树的算法，这时候需要申请一个新的数据页，然后挪动部分数据过去。这个过程称为页分裂。在这种情况下，性能自然会受影响。

除了性能外，页分裂操作还影响数据页的利用率。原本放在一个页的数据，现在分到两个页中，整体空间利用率降低大约 50%。

当然有分裂就有合并。当相邻两个页由于删除了数据，利用率很低之后，会将数据页做合并。合并的过程，可以认为是分裂过程的逆过程。

基于上面的索引维护过程说明，我们来讨论一个案例：

> 你可能在一些建表规范里面见到过类似的描述，要求建表语句里一定要有自增主键。当然事无绝对，我们来分析一下哪些场景下应该使用自增主键，而哪些场景下不应该。

自增主键是指自增列上定义的主键，在建表语句中一般是这么定义的： NOT NULL PRIMARY KEY AUTO_INCREMENT。

插入新记录的时候可以不指定 ID 的值，系统会获取当前 ID 最大值加 1 作为下一条记录的 ID 值。

也就是说，自增主键的插入数据模式，正符合了我们前面提到的递增插入的场景。每次插入一条新记录，都是追加操作，都不涉及到挪动其他记录，也不会触发叶子节点的分裂。

而有业务逻辑的字段做主键，则往往不容易保证有序插入，这样写数据成本相对较高。

除了考虑性能外，我们还可以从存储空间的角度来看。假设你的表中确实有一个唯一字段，比如字符串类型的身份证号，那应该用身份证号做主键，还是用自增字段做主键呢？

由于每个非主键索引的叶子节点上都是主键的值。如果用身份证号做主键，那么每个二级索引的叶子节点占用约 20 个字节，而如果用整型做主键，则只要 4 个字节，如果是长整型（bigint）则是 8 个字节。

**显然，主键长度越小，普通索引的叶子节点就越小，普通索引占用的空间也就越小。**

所以，从性能和存储空间方面考量，自增主键往往是更合理的选择。

有没有什么场景适合用业务字段直接做主键的呢？还是有的。比如，有些业务的场景需求是这样的：

1. 只有一个索引；
2. 该索引必须是唯一索引。

你一定看出来了，这就是典型的 KV 场景。

由于没有其他索引，所以也就不用考虑其他索引的叶子节点大小的问题。

这时候我们就要优先考虑上一段提到的“尽量使用主键查询”原则，直接将这个索引设置为主键，可以避免每次查询需要搜索两棵树。

#### 小结

今天，我跟你分析了数据库引擎可用的数据结构，介绍了 InnoDB 采用的 B+ 树结构，以及为什么 InnoDB 要这么选择。B+ 树能够很好地配合磁盘的读写特性，减少单次查询的磁盘访问次数。

由于 InnoDB 是索引组织表，一般情况下我会建议你创建一个自增主键，这样非主键索引占用的空间最小。但事无绝对，我也跟你讨论了使用业务逻辑字段做主键的应用场景。

最后，我给你留下一个问题吧。对于上面例子中的 InnoDB 表 T，如果你要重建索引 k，你的两个 SQL 语句可以这么写：

```sql
alter table T drop index k;
alter table T add index(k);
```

如果你要重建主键索引，也可以这么写：

```sql
alter table T drop primary key;
alter table T add primary key(id);
```

我的问题是，对于上面这两个重建索引的作法，说出你的理解。如果有不合适的，为什么，更好的方法是什么？

你可以把你的思考和观点写在留言区里，我会在下一篇文章的末尾给出我的参考答案。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

我在上一篇文章末尾给你留下的问题是：如何避免长事务对业务的影响？

这个问题，我们可以从应用开发端和数据库端来看。

**首先，从应用开发端来看：**

1. 确认是否使用了 set autocommit=0。这个确认工作可以在测试环境中开展，把 MySQL 的 general_log  开起来，然后随便跑一个业务逻辑，通过 general_log  的日志来确认。一般框架如果会设置这个值，也就会提供参数来控制行为，你的目标就是把它改成 1。
2. 确认是否有不必要的只读事务。有些框架会习惯不管什么语句先用 begin/commit 框起来。我见过有些是业务并没有这个需要，但是也把好几个 select 语句放到了事务中。这种只读事务可以去掉。
3. 业务连接数据库的时候，根据业务本身的预估，通过 SET MAX_EXECUTION_TIME 命令，来控制每个语句执行的最长时间，避免单个语句意外执行太长时间。（为什么会意外？在后续的文章中会提到这类案例）

**其次，从数据库端来看：**

1. 监控 information_schema.Innodb_trx 表，设置长事务阈值，超过就报警 / 或者 kill；
2. Percona 的 pt-kill 这个工具不错，推荐使用；
3. 在业务功能测试阶段要求输出所有的 general_log，分析日志行为提前发现问题；
4. 如果使用的是 MySQL 5.6 或者更新版本，把 innodb_undo_tablespaces 设置成 2（或更大的值）。如果真的出现大事务导致回滚段过大，这样设置后清理起来更方便。

感谢 @壹笙☞漂泊 @王凯 @易翔 留下的高质量评论。

### 05 深入浅出索引（下）

在上一篇文章中，我和你介绍了 InnoDB 索引的数据结构模型，今天我们再继续聊聊跟 MySQL 索引有关的概念。

在开始这篇文章之前，我们先来看一下这个问题：

在下面这个表 T 中，如果我执行 select * from T where k between 3 and 5，需要执行几次树的搜索操作，会扫描多少行？

下面是这个表的初始化语句。

```sql
mysql> create table T (
ID int primary key,
k int NOT NULL DEFAULT 0, 
s varchar(16) NOT NULL DEFAULT '',
index k(k))
engine=InnoDB; 
insert into T values(100,1, 'aa'),(200,2,'bb'),(300,3,'cc'),(500,5,'ee'),(600,6,'ff'),(700,7,'gg');
```

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/dcda101051f28502bd5c4402b292e38d-1550568785632-1584367388458.png)

图 1 InnoDB 的索引组织结构

现在，我们一起来看看这条 SQL 查询语句的执行流程：

1. 在 k 索引树上找到 k=3 的记录，取得 ID = 300；
2. 再到 ID 索引树查到 ID=300 对应的 R3；
3. 在 k 索引树取下一个值 k=5，取得 ID=500；
4. 再回到 ID 索引树查到 ID=500 对应的 R4；
5. 在 k 索引树取下一个值 k=6，不满足条件，循环结束。

在这个过程中，**回到主键索引树搜索的过程，我们称为回表**。可以看到，这个查询过程读了 k 索引树的 3 条记录（步骤 1、3 和 5），回表了两次（步骤 2 和 4）。

在这个例子中，由于查询结果所需要的数据只在主键索引上有，所以不得不回表。那么，有没有可能经过索引优化，避免回表过程呢？

#### 覆盖索引

如果执行的语句是 select ID from T where k between 3 and 5，这时只需要查 ID 的值，而 ID  的值已经在 k 索引树上了，因此可以直接提供查询结果，不需要回表。也就是说，在这个查询里面，索引 k  已经“覆盖了”我们的查询需求，我们称为覆盖索引。

**由于覆盖索引可以减少树的搜索次数，显著提升查询性能，所以使用覆盖索引是一个常用的性能优化手段。**

需要注意的是，在引擎内部使用覆盖索引在索引 k 上其实读了三个记录，R3~R5（对应的索引 k 上的记录项），但是对于 MySQL 的 Server 层来说，它就是找引擎拿到了两条记录，因此 MySQL 认为扫描行数是 2。

> 备注：关于如何查看扫描行数的问题，我将会在第 16 文章《如何正确地显示随机消息？》中，和你详细讨论。

基于上面覆盖索引的说明，我们来讨论一个问题：**在一个市民信息表上，是否有必要将身份证号和名字建立联合索引？**

假设这个市民表的定义是这样的：

```r
CREATE TABLE `tuser` (
  `id` int(11) NOT NULL,
  `id_card` varchar(32) DEFAULT NULL,
  `name` varchar(32) DEFAULT NULL,
  `age` int(11) DEFAULT NULL,
  `ismale` tinyint(1) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `id_card` (`id_card`),
  KEY `name_age` (`name`,`age`)
) ENGINE=InnoDB
```

我们知道，身份证号是市民的唯一标识。也就是说，如果有根据身份证号查询市民信息的需求，我们只要在身份证号字段上建立索引就够了。而再建立一个（身份证号、姓名）的联合索引，是不是浪费空间？

如果现在有一个高频请求，要根据市民的身份证号查询他的姓名，这个联合索引就有意义了。它可以在这个高频请求上用到覆盖索引，不再需要回表查整行记录，减少语句的执行时间。

当然，索引字段的维护总是有代价的。因此，在建立冗余索引来支持覆盖索引时就需要权衡考虑了。这正是业务 DBA，或者称为业务数据架构师的工作。

#### 最左前缀原则

看到这里你一定有一个疑问，如果为每一种查询都设计一个索引，索引是不是太多了。如果我现在要按照市民的身份证号去查他的家庭地址呢？虽然这个查询需求在业务中出现的概率不高，但总不能让它走全表扫描吧？反过来说，单独为一个不频繁的请求创建一个（身份证号，地址）的索引又感觉有点浪费。应该怎么做呢？

这里，我先和你说结论吧。**B+ 树这种索引结构，可以利用索引的“最左前缀”，来定位记录。**

为了直观地说明这个概念，我们用（name，age）这个联合索引来分析。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/89f74c631110cfbc83298ef27dcd6370-1584367388561.jpg)

图 2 （name，age）索引示意图

可以看到，索引项是按照索引定义里面出现的字段顺序排序的。

当你的逻辑需求是查到所有名字是“张三”的人时，可以快速定位到 ID4，然后向后遍历得到所有需要的结果。

如果你要查的是所有名字第一个字是“张”的人，你的 SQL 语句的条件是"where name like ‘张 %’"。这时，你也能够用上这个索引，查找到第一个符合条件的记录是 ID3，然后向后遍历，直到不满足条件为止。

可以看到，不只是索引的全部定义，只要满足最左前缀，就可以利用索引来加速检索。这个最左前缀可以是联合索引的最左 N 个字段，也可以是字符串索引的最左 M 个字符。

基于上面对最左前缀索引的说明，我们来讨论一个问题：**在建立联合索引的时候，如何安排索引内的字段顺序。**

这里我们的评估标准是，索引的复用能力。因为可以支持最左前缀，所以当已经有了 (a,b) 这个联合索引后，一般就不需要单独在 a 上建立索引了。因此，**第一原则是，如果通过调整顺序，可以少维护一个索引，那么这个顺序往往就是需要优先考虑采用的。**

所以现在你知道了，这段开头的问题里，我们要为高频请求创建 (身份证号，姓名）这个联合索引，并用这个索引支持“根据身份证号查询地址”的需求。

那么，如果既有联合查询，又有基于 a、b 各自的查询呢？查询条件里面只有 b 的语句，是无法使用 (a,b) 这个联合索引的，这时候你不得不维护另外一个索引，也就是说你需要同时维护 (a,b)、(b) 这两个索引。

这时候，我们要**考虑的原则就是空间**了。比如上面这个市民表的情况，name 字段是比 age 字段大的 ，那我就建议你创建一个（name,age) 的联合索引和一个 (age) 的单字段索引。

#### 索引下推

上一段我们说到满足最左前缀原则的时候，最左前缀可以用于在索引中定位记录。这时，你可能要问，那些不符合最左前缀的部分，会怎么样呢？

我们还是以市民表的联合索引（name, age）为例。如果现在有一个需求：检索出表中“名字第一个字是张，而且年龄是 10 岁的所有男孩”。那么，SQL 语句是这么写的：

```sql
mysql> select * from tuser where name like '张 %' and age=10 and ismale=1;
```

你已经知道了前缀索引规则，所以这个语句在搜索索引树的时候，只能用 “张”，找到第一个满足条件的记录 ID3。当然，这还不错，总比全表扫描要好。

然后呢？

当然是判断其他条件是否满足。

在 MySQL 5.6 之前，只能从 ID3 开始一个个回表。到主键索引上找出数据行，再对比字段值。

而 MySQL 5.6 引入的索引下推优化（index condition pushdown)， 可以在索引遍历过程中，对索引中包含的字段先做判断，直接过滤掉不满足条件的记录，减少回表次数。

图 3 和图 4，是这两个过程的执行流程图。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/b32aa8b1f75611e0759e52f5915539ac-1584367388568.jpg)

图 3 无索引下推执行流程

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/76e385f3df5a694cc4238c7b65acfe1b-1584367388573.jpg)

图 4 索引下推执行流程

在图 3 和 4 这两个图里面，每一个虚线箭头表示回表一次。

图 3 中，在 (name,age) 索引里面我特意去掉了 age 的值，这个过程 InnoDB 并不会去看 age 的值，只是按顺序把“name 第一个字是’张’”的记录一条条取出来回表。因此，需要回表 4 次。

图 4 跟图 3 的区别是，InnoDB 在 (name,age) 索引内部就判断了 age 是否等于 10，对于不等于 10 的记录，直接判断并跳过。在我们的这个例子中，只需要对 ID4、ID5 这两条记录回表取数据判断，就只需要回表 2 次。

#### 小结

今天这篇文章，我和你继续讨论了数据库索引的概念，包括了覆盖索引、前缀索引、索引下推。你可以看到，在满足语句需求的情况下， 尽量少地访问资源是数据库设计的重要原则之一。我们在使用数据库的时候，尤其是在设计表结构时，也要以减少资源消耗作为目标。

接下来我给你留下一个问题吧。

实际上主键索引也是可以使用多个字段的。DBA 小吕在入职新公司的时候，就发现自己接手维护的库里面，有这么一个表，表结构定义类似这样的：

```go
CREATE TABLE `geek` (
  `a` int(11) NOT NULL,
  `b` int(11) NOT NULL,
  `c` int(11) NOT NULL,
  `d` int(11) NOT NULL,
  PRIMARY KEY (`a`,`b`),
  KEY `c` (`c`),
  KEY `ca` (`c`,`a`),
  KEY `cb` (`c`,`b`)
) ENGINE=InnoDB;
```

公司的同事告诉他说，由于历史原因，这个表需要 a、b 做联合主键，这个小吕理解了。

但是，学过本章内容的小吕又纳闷了，既然主键包含了 a、b 这两个字段，那意味着单独在字段 c 上创建一个索引，就已经包含了三个字段了呀，为什么要创建“ca”“cb”这两个索引？

同事告诉他，是因为他们的业务里面有这样的两种语句：

```vbnet
select * from geek where c=N order by a limit 1;
select * from geek where c=N order by b limit 1;
```

我给你的问题是，这位同事的解释对吗，为了这两个查询模式，这两个索引是否都是必须的？为什么呢？

你可以把你的思考和观点写在留言区里，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

上期的问题是，通过两个 alter 语句重建索引 k，以及通过两个 alter 语句重建主键索引是否合理。

在评论区，有同学问到为什么要重建索引。我们文章里面有提到，索引可能因为删除，或者页分裂等原因，导致数据页有空洞，重建索引的过程会创建一个新的索引，把数据按顺序插入，这样页面的利用率最高，也就是索引更紧凑、更省空间。

这道题目，我给你的“参考答案”是：

重建索引 k  的做法是合理的，可以达到省空间的目的。但是，重建主键的过程不合理。不论是删除主键还是创建主键，都会将整个表重建。所以连着执行这两个语句的话，第一个语句就白做了。这两个语句，你可以用这个语句代替 ： alter table T engine=InnoDB。在专栏的第 12  篇文章《为什么表数据删掉一半，表文件大小不变？》中，我会和你分析这条语句的执行流程。

评论区留言中， @壹笙☞漂泊 做了很详细的笔记，@高枕 帮同学解答了问题，@约书亚 提了一个很不错的面试问题。在这里，我要和你们道一声感谢。

PS：如果你在面试中，曾有过被 MySQL 相关问题难住的经历，也可以把这个问题发到评论区，我们一起来讨论。如果解答这个问题，需要的篇幅会很长的话，我可以放到答疑文章展开。

### 06 全局锁和表锁 ：给表加个字段怎么有这么多阻碍？

今天我要跟你聊聊 MySQL 的锁。数据库锁设计的初衷是处理并发问题。作为多用户共享的资源，当出现并发访问的时候，数据库需要合理地控制资源的访问规则。而锁就是用来实现这些访问规则的重要数据结构。

**根据加锁的范围，MySQL 里面的锁大致可以分成全局锁、表级锁和行锁三类**。今天这篇文章，我会和你分享全局锁和表级锁。而关于行锁的内容，我会留着在下一篇文章中再和你详细介绍。

这里需要说明的是，锁的设计比较复杂，这两篇文章不会涉及锁的具体实现细节，主要介绍的是碰到锁时的现象和其背后的原理。

#### 全局锁

顾名思义，全局锁就是对整个数据库实例加锁。MySQL 提供了一个加全局读锁的方法，命令是 Flush tables with read  lock  (FTWRL)。当你需要让整个库处于只读状态的时候，可以使用这个命令，之后其他线程的以下语句会被阻塞：数据更新语句（数据的增删改）、数据定义语句（包括建表、修改表结构等）和更新类事务的提交语句。

**全局锁的典型使用场景是，做全库逻辑备份。**也就是把整库每个表都 select 出来存成文本。

以前有一种做法，是通过 FTWRL 确保不会有其他线程对数据库做更新，然后对整个库做备份。注意，在备份过程中整个库完全处于只读状态。

但是让整库都只读，听上去就很危险：

- 如果你在主库上备份，那么在备份期间都不能执行更新，业务基本上就得停摆；
- 如果你在从库上备份，那么备份期间从库不能执行主库同步过来的 binlog，会导致主从延迟。

看来加全局锁不太好。但是细想一下，备份为什么要加锁呢？我们来看一下不加锁会有什么问题。

假设你现在要维护“极客时间”的购买系统，关注的是用户账户余额表和用户课程表。

现在发起一个逻辑备份。假设备份期间，有一个用户，他购买了一门课程，业务逻辑里就要扣掉他的余额，然后往已购课程里面加上一门课。

如果时间顺序上是先备份账户余额表 (u_account)，然后用户购买，然后备份用户课程表 (u_course)，会怎么样呢？你可以看一下这个图：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/cbfd4a0bbb1210792064bcea4e49b0cd-1584367388578.png)

图 1 业务和备份状态图

可以看到，这个备份结果里，用户 A 的数据状态是“账户余额没扣，但是用户课程表里面已经多了一门课”。如果后面用这个备份来恢复数据的话，用户 A 就发现，自己赚了。

作为用户可别觉得这样可真好啊，你可以试想一下：如果备份表的顺序反过来，先备份用户课程表再备份账户余额表，又可能会出现什么结果？

也就是说，不加锁的话，备份系统备份的得到的库不是一个逻辑时间点，这个视图是逻辑不一致的。

说到视图你肯定想起来了，我们在前面讲事务隔离的时候，其实是有一个方法能够拿到一致性视图的，对吧？

是的，就是在可重复读隔离级别下开启一个事务。

> 备注：如果你对事务隔离级别的概念不是很清晰的话，可以再回顾一下第 3 篇文章[《事务隔离：为什么你改了我还看不见？》]中的相关内容。

官方自带的逻辑备份工具是 mysqldump。当 mysqldump 使用参数–single-transaction 的时候，导数据之前就会启动一个事务，来确保拿到一致性视图。而由于 MVCC 的支持，这个过程中数据是可以正常更新的。

你一定在疑惑，有了这个功能，为什么还需要 FTWRL 呢？**一致性读是好，但前提是引擎要支持这个隔离级别。**比如，对于 MyISAM  这种不支持事务的引擎，如果备份过程中有更新，总是只能取到最新的数据，那么就破坏了备份的一致性。这时，我们就需要使用 FTWRL 命令了。

所以，**single-transaction 方法只适用于所有的表使用事务引擎的库。**如果有的表使用了不支持事务的引擎，那么备份就只能通过 FTWRL 方法。这往往是 DBA 要求业务开发人员使用 InnoDB 替代 MyISAM 的原因之一。

你也许会问，**既然要全库只读，为什么不使用 set global readonly=true 的方式呢**？确实 readonly 方式也可以让全库进入只读状态，但我还是会建议你用 FTWRL 方式，主要有两个原因：

- 一是，在有些系统中，readonly 的值会被用来做其他逻辑，比如用来判断一个库是主库还是备库。因此，修改 global 变量的方式影响面更大，我不建议你使用。
- 二是，在异常处理机制上有差异。如果执行 FTWRL 命令之后由于客户端发生异常断开，那么 MySQL  会自动释放这个全局锁，整个库回到可以正常更新的状态。而将整个库设置为 readonly 之后，如果客户端发生异常，则数据库就会一直保持  readonly 状态，这样会导致整个库长时间处于不可写状态，风险较高。

业务的更新不只是增删改数据（DML)，还有可能是加字段等修改表结构的操作（DDL）。不论是哪种方法，一个库被全局锁上以后，你要对里面任何一个表做加字段操作，都是会被锁住的。

但是，即使没有被全局锁住，加字段也不是就能一帆风顺的，因为你还会碰到接下来我们要介绍的表级锁。

#### 表级锁

MySQL 里面表级别的锁有两种：一种是表锁，一种是元数据锁（meta data lock，MDL)。

**表锁的语法是 lock tables … read/write。**与 FTWRL 类似，可以用 unlock tables  主动释放锁，也可以在客户端断开的时候自动释放。需要注意，lock tables 语法除了会限制别的线程的读写外，也限定了本线程接下来的操作对象。

举个例子, 如果在某个线程 A 中执行 lock tables t1 read, t2 write; 这个语句，则其他线程写 t1、读写  t2 的语句都会被阻塞。同时，线程 A 在执行 unlock tables 之前，也只能执行读 t1、读写 t2 的操作。连写 t1  都不允许，自然也不能访问其他表。

在还没有出现更细粒度的锁的时候，表锁是最常用的处理并发的方式。而对于 InnoDB 这种支持行锁的引擎，一般不使用 lock tables 命令来控制并发，毕竟锁住整个表的影响面还是太大。

**另一类表级的锁是 MDL（metadata lock)。**MDL 不需要显式使用，在访问一个表的时候会被自动加上。MDL  的作用是，保证读写的正确性。你可以想象一下，如果一个查询正在遍历一个表中的数据，而执行期间另一个线程对这个表结构做变更，删了一列，那么查询线程拿到的结果跟表结构对不上，肯定是不行的。

因此，在 MySQL 5.5 版本中引入了 MDL，当对一个表做增删改查操作的时候，加 MDL 读锁；当要对表做结构变更操作的时候，加 MDL 写锁。

- 读锁之间不互斥，因此你可以有多个线程同时对一张表增删改查。
- 读写锁之间、写锁之间是互斥的，用来保证变更表结构操作的安全性。因此，如果有两个线程要同时给一个表加字段，其中一个要等另一个执行完才能开始执行。

虽然 MDL 锁是系统默认会加的，但却是你不能忽略的一个机制。比如下面这个例子，我经常看到有人掉到这个坑里：给一个小表加个字段，导致整个库挂了。

你肯定知道，给一个表加字段，或者修改字段，或者加索引，需要扫描全表的数据。在对大表操作的时候，你肯定会特别小心，以免对线上服务造成影响。而实际上，即使是小表，操作不慎也会出问题。我们来看一下下面的操作序列，假设表 t 是一个小表。

> 备注：这里的实验环境是 MySQL 5.6。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/7cf6a3bf90d72d1f0fc156ececdfb0ce-1584367388165.jpg)

我们可以看到 session A 先启动，这时候会对表 t 加一个 MDL 读锁。由于 session B 需要的也是 MDL 读锁，因此可以正常执行。

之后 session C 会被 blocked，是因为 session A 的 MDL 读锁还没有释放，而 session C 需要 MDL 写锁，因此只能被阻塞。

如果只有 session C 自己被阻塞还没什么关系，但是之后所有要在表 t 上新申请 MDL 读锁的请求也会被 session C 阻塞。前面我们说了，所有对表的增删改查操作都需要先申请 MDL 读锁，就都被锁住，等于这个表现在完全不可读写了。

如果某个表上的查询语句频繁，而且客户端有重试机制，也就是说超时后会再起一个新 session 再请求的话，这个库的线程很快就会爆满。

你现在应该知道了，事务中的 MDL 锁，在语句执行开始时申请，但是语句结束后并不会马上释放，而会等到整个事务提交后再释放。

基于上面的分析，我们来讨论一个问题，**如何安全地给小表加字段？**

首先我们要解决长事务，事务不提交，就会一直占着 MDL 锁。在 MySQL 的 information_schema 库的  innodb_trx 表中，你可以查到当前执行中的事务。如果你要做 DDL 变更的表刚好有长事务在执行，要考虑先暂停 DDL，或者 kill  掉这个长事务。

但考虑一下这个场景。如果你要变更的表是一个热点表，虽然数据量不大，但是上面的请求很频繁，而你不得不加个字段，你该怎么做呢？

这时候 kill 可能未必管用，因为新的请求马上就来了。比较理想的机制是，在 alter table  语句里面设定等待时间，如果在这个指定的等待时间里面能够拿到 MDL 写锁最好，拿不到也不要阻塞后面的业务语句，先放弃。之后开发人员或者 DBA  再通过重试命令重复这个过程。

MariaDB 已经合并了 AliSQL 的这个功能，所以这两个开源分支目前都支持 DDL NOWAIT/WAIT n 这个语法。

```sql
ALTER TABLE tbl_name NOWAIT add column ...
ALTER TABLE tbl_name WAIT N add column ... 
```

#### 小结

今天，我跟你介绍了 MySQL 的全局锁和表级锁。

全局锁主要用在逻辑备份过程中。对于全部是 InnoDB 引擎的库，我建议你选择使用–single-transaction 参数，对应用会更友好。

表锁一般是在数据库引擎不支持行锁的时候才会被用到的。如果你发现你的应用程序里有 lock tables 这样的语句，你需要追查一下，比较可能的情况是：

- 要么是你的系统现在还在用 MyISAM 这类不支持事务的引擎，那要安排升级换引擎；
- 要么是你的引擎升级了，但是代码还没升级。我见过这样的情况，最后业务开发就是把 lock tables 和 unlock tables 改成 begin 和 commit，问题就解决了。

MDL 会直到事务提交才释放，在做表结构变更的时候，你一定要小心不要导致锁住线上查询和更新。

最后，我给你留一个问题吧。备份一般都会在备库上执行，你在用–single-transaction 方法做逻辑备份的过程中，如果主库上的一个小表做了一个 DDL，比如给一个表上加了一列。这时候，从备库上会看到什么现象呢？

你可以把你的思考和观点写在留言区里，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

说明：这篇文章没有介绍到物理备份，物理备份会有一篇单独的文章。

#### 上期问题时间

上期的问题是关于对联合主键索引和 InnoDB 索引组织表的理解。

我直接贴 @老杨同志 的回复略作修改如下（我修改的部分用橙色标出）：

表记录 –a--|–b--|–c--|–d-- 1 2 3 d 1 3 2 d 1 4 3 d 2 1 3 d 2 2 2 d 2 3 4 d 主键 a，b 的聚簇索引组织顺序相当于 order by a,b ，也就是先按 a 排序，再按 b 排序，c 无序。

索引 ca 的组织是先按 c 排序，再按 a 排序，同时记录主键 –c--|–a--|–主键部分b-- （注意，这里不是 ab，而是只有 b） 2 1 3 2 2 2 3 1 2 3 1 4 3 2 1 4 2 3 这个跟索引 c 的数据是一模一样的。

索引 cb 的组织是先按 c 排序，在按 b 排序，同时记录主键 –c--|–b--|–主键部分a-- （同上） 2 2 2 2 3 1 3 1 2 3 2 1 3 4 1 4 3 2

所以，结论是 ca 可以去掉，cb 需要保留。

评论区留言点赞：

> @浪里白条 帮大家总结了复习要点； @约书亚 的问题里提到了 MRR 优化； @HwangZHen 留言言简意赅。

### 07 行锁功过：怎么减少行锁对性能的影响？

在上一篇文章中，我跟你介绍了 MySQL 的全局锁和表级锁，今天我们就来讲讲 MySQL 的行锁。

MySQL 的行锁是在引擎层由各个引擎自己实现的。但并不是所有的引擎都支持行锁，比如 MyISAM  引擎就不支持行锁。不支持行锁意味着并发控制只能使用表锁，对于这种引擎的表，同一张表上任何时刻只能有一个更新在执行，这就会影响到业务并发度。InnoDB 是支持行锁的，这也是 MyISAM 被 InnoDB 替代的重要原因之一。

我们今天就主要来聊聊 InnoDB 的行锁，以及如何通过减少锁冲突来提升业务并发度。

顾名思义，行锁就是针对数据表中行记录的锁。这很好理解，比如事务 A 更新了一行，而这时候事务 B 也要更新同一行，则必须等事务 A 的操作完成后才能进行更新。

当然，数据库中还有一些没那么一目了然的概念和设计，这些概念如果理解和使用不当，容易导致程序出现非预期行为，比如两阶段锁。

#### 从两阶段锁说起

我先给你举个例子。在下面的操作序列中，事务 B 的 update 语句执行时会是什么现象呢？假设字段 id 是表 t 的主键。![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/51f501f718e420244b0a2ec2ce858710-1584367388584.jpg)

这个问题的结论取决于事务 A 在执行完两条 update 语句后，持有哪些锁，以及在什么时候释放。你可以验证一下：实际上事务 B 的 update 语句会被阻塞，直到事务 A 执行 commit 之后，事务 B 才能继续执行。

知道了这个答案，你一定知道了事务 A 持有的两个记录的行锁，都是在 commit 的时候才释放的。

也就是说，**在 InnoDB 事务中，行锁是在需要的时候才加上的，但并不是不需要了就立刻释放，而是要等到事务结束时才释放。这个就是两阶段锁协议。**

知道了这个设定，对我们使用事务有什么帮助呢？那就是，如果你的事务中需要锁多个行，要把最可能造成锁冲突、最可能影响并发度的锁尽量往后放。我给你举个例子。

假设你负责实现一个电影票在线交易业务，顾客 A 要在影院 B 购买电影票。我们简化一点，这个业务需要涉及到以下操作：

1. 从顾客 A 账户余额中扣除电影票价；
2. 给影院 B 的账户余额增加这张电影票价；
3. 记录一条交易日志。

也就是说，要完成这个交易，我们需要 update 两条记录，并 insert 一条记录。当然，为了保证交易的原子性，我们要把这三个操作放在一个事务中。那么，你会怎样安排这三个语句在事务中的顺序呢？

试想如果同时有另外一个顾客 C 要在影院 B 买票，那么这两个事务冲突的部分就是语句 2 了。因为它们要更新同一个影院账户的余额，需要修改同一行数据。

根据两阶段锁协议，不论你怎样安排语句顺序，所有的操作需要的行锁都是在事务提交的时候才释放的。所以，如果你把语句 2 安排在最后，比如按照 3、1、2 这样的顺序，那么影院账户余额这一行的锁时间就最少。这就最大程度地减少了事务之间的锁等待，提升了并发度。

好了，现在由于你的正确设计，影院余额这一行的行锁在一个事务中不会停留很长时间。但是，这并没有完全解决你的困扰。

如果这个影院做活动，可以低价预售一年内所有的电影票，而且这个活动只做一天。于是在活动时间开始的时候，你的 MySQL 就挂了。你登上服务器一看，CPU 消耗接近 100%，但整个数据库每秒就执行不到 100 个事务。这是什么原因呢？

这里，我就要说到死锁和死锁检测了。

#### 死锁和死锁检测

当并发系统中不同线程出现循环资源依赖，涉及的线程都在等待别的线程释放资源时，就会导致这几个线程都进入无限等待的状态，称为死锁。这里我用数据库中的行锁举个例子。![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/4d0eeec7b136371b79248a0aed005a52-1584367388586.jpg)

这时候，事务 A 在等待事务 B 释放 id=2 的行锁，而事务 B 在等待事务 A 释放 id=1 的行锁。 事务 A 和事务 B 在互相等待对方的资源释放，就是进入了死锁状态。当出现死锁以后，有两种策略：

- 一种策略是，直接进入等待，直到超时。这个超时时间可以通过参数 innodb_lock_wait_timeout 来设置。
- 另一种策略是，发起死锁检测，发现死锁后，主动回滚死锁链条中的某一个事务，让其他事务得以继续执行。将参数 innodb_deadlock_detect 设置为 on，表示开启这个逻辑。

在 InnoDB 中，innodb_lock_wait_timeout 的默认值是  50s，意味着如果采用第一个策略，当出现死锁以后，第一个被锁住的线程要过 50s  才会超时退出，然后其他线程才有可能继续执行。对于在线服务来说，这个等待时间往往是无法接受的。

但是，我们又不可能直接把这个时间设置成一个很小的值，比如 1s。这样当出现死锁的时候，确实很快就可以解开，但如果不是死锁，而是简单的锁等待呢？所以，超时时间设置太短的话，会出现很多误伤。

所以，正常情况下我们还是要采用第二种策略，即：主动死锁检测，而且 innodb_deadlock_detect 的默认值本身就是 on。主动死锁检测在发生死锁的时候，是能够快速发现并进行处理的，但是它也是有额外负担的。

你可以想象一下这个过程：每当一个事务被锁的时候，就要看看它所依赖的线程有没有被别人锁住，如此循环，最后判断是否出现了循环等待，也就是死锁。

那如果是我们上面说到的所有事务都要更新同一行的场景呢？

每个新来的被堵住的线程，都要判断会不会由于自己的加入导致了死锁，这是一个时间复杂度是 O(n) 的操作。假设有 1000  个并发线程要同时更新同一行，那么死锁检测操作就是 100 万这个量级的。虽然最终检测的结果是没有死锁，但是这期间要消耗大量的 CPU  资源。因此，你就会看到 CPU 利用率很高，但是每秒却执行不了几个事务。

根据上面的分析，我们来讨论一下，怎么解决由这种热点行更新导致的性能问题呢？问题的症结在于，死锁检测要耗费大量的 CPU 资源。

**一种头痛医头的方法，就是如果你能确保这个业务一定不会出现死锁，可以临时把死锁检测关掉。**但是这种操作本身带有一定的风险，因为业务设计的时候一般不会把死锁当做一个严重错误，毕竟出现死锁了，就回滚，然后通过业务重试一般就没问题了，这是业务无损的。而关掉死锁检测意味着可能会出现大量的超时，这是业务有损的。

**另一个思路是控制并发度。**根据上面的分析，你会发现如果并发能够控制住，比如同一行同时最多只有 10  个线程在更新，那么死锁检测的成本很低，就不会出现这个问题。一个直接的想法就是，在客户端做并发控制。但是，你会很快发现这个方法不太可行，因为客户端很多。我见过一个应用，有 600 个客户端，这样即使每个客户端控制到只有 5 个并发线程，汇总到数据库服务端以后，峰值并发数也可能要达到 3000。

因此，这个并发控制要做在数据库服务端。如果你有中间件，可以考虑在中间件实现；如果你的团队有能修改 MySQL 源码的人，也可以做在  MySQL 里面。基本思路就是，对于相同行的更新，在进入引擎之前排队。这样在 InnoDB 内部就不会有大量的死锁检测工作了。

可能你会问，**如果团队里暂时没有数据库方面的专家，不能实现这样的方案，能不能从设计上优化这个问题呢？**

你可以考虑通过将一行改成逻辑上的多行来减少锁冲突。还是以影院账户为例，可以考虑放在多条记录上，比如 10 个记录，影院的账户总额等于这  10 个记录的值的总和。这样每次要给影院账户加金额的时候，随机选其中一条记录来加。这样每次冲突概率变成原来的  1/10，可以减少锁等待个数，也就减少了死锁检测的 CPU 消耗。

这个方案看上去是无损的，但其实这类方案需要根据业务逻辑做详细设计。如果账户余额可能会减少，比如退票逻辑，那么这时候就需要考虑当一部分行记录变成 0 的时候，代码要有特殊处理。

#### 小结

今天，我和你介绍了 MySQL 的行锁，涉及了两阶段锁协议、死锁和死锁检测这两大部分内容。

其中，我以两阶段协议为起点，和你一起讨论了在开发的时候如何安排正确的事务语句。这里的原则 / 我给你的建议是：如果你的事务中需要锁多个行，要把最可能造成锁冲突、最可能影响并发度的锁的申请时机尽量往后放。

但是，调整语句顺序并不能完全避免死锁。所以我们引入了死锁和死锁检测的概念，以及提供了三个方案，来减少死锁对数据库的影响。减少死锁的主要方向，就是控制访问相同资源的并发事务量。

最后，我给你留下一个问题吧。如果你要删除一个表里面的前 10000 行数据，有以下三种方法可以做到：

- 第一种，直接执行 delete from T limit 10000;
- 第二种，在一个连接中循环执行 20 次 delete from T limit 500;
- 第三种，在 20 个连接中同时执行 delete from T limit 500。

你会选择哪一种方法呢？为什么呢？

你可以把你的思考和观点写在留言区里，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

上期我给你留的问题是：当备库用–single-transaction 做逻辑备份的时候，如果从主库的 binlog 传来一个 DDL 语句会怎么样？

假设这个 DDL 是针对表 t1 的， 这里我把备份过程中几个关键的语句列出来：

```sql
Q1:SET SESSION TRANSACTION ISOLATION LEVEL REPEATABLE READ;
Q2:START TRANSACTION  WITH CONSISTENT SNAPSHOT；
/* other tables */
Q3:SAVEPOINT sp;
/* 时刻 1 */
Q4:show create table `t1`;
/* 时刻 2 */
Q5:SELECT * FROM `t1`;
/* 时刻 3 */
Q6:ROLLBACK TO SAVEPOINT sp;
/* 时刻 4 */
/* other tables */
```

在备份开始的时候，为了确保 RR（可重复读）隔离级别，再设置一次 RR 隔离级别 (Q1);

启动事务，这里用 WITH CONSISTENT SNAPSHOT 确保这个语句执行完就可以得到一个一致性视图（Q2)；

设置一个保存点，这个很重要（Q3）；

show create 是为了拿到表结构 (Q4)，然后正式导数据 （Q5），回滚到 SAVEPOINT sp，在这里的作用是释放 t1 的 MDL 锁 （Q6）。当然这部分属于“超纲”，上文正文里面都没提到。

DDL 从主库传过来的时间按照效果不同，我打了四个时刻。题目设定为小表，我们假定到达后，如果开始执行，则很快能够执行完成。

参考答案如下：

1. 如果在 Q4 语句执行之前到达，现象：没有影响，备份拿到的是 DDL 后的表结构。
2. 如果在“时刻 2”到达，则表结构被改过，Q5 执行的时候，报 Table definition has changed, please retry transaction，现象：mysqldump 终止；
3. 如果在“时刻 2”和“时刻 3”之间到达，mysqldump 占着 t1 的 MDL 读锁，binlog 被阻塞，现象：主从延迟，直到 Q6 执行完成。
4. 从“时刻 4”开始，mysqldump 释放了 MDL 读锁，现象：没有影响，备份拿到的是 DDL 前的表结构。

评论区留言点赞板：

> @Aurora 给了最接近的答案； @echo＿陈 问了一个好问题； @壹笙☞漂泊 做了很好的总结。

### 08 事务到底是隔离的还是不隔离的？

我在第 3 篇文章和你讲事务隔离级别的时候提到过，如果是可重复读隔离级别，事务 T 启动的时候会创建一个视图 read-view，之后事务 T 执行期间，即使有其他事务修改了数据，事务 T  看到的仍然跟在启动时看到的一样。也就是说，一个在可重复读隔离级别下执行的事务，好像与世无争，不受外界影响。

但是，我在上一篇文章中，和你分享行锁的时候又提到，一个事务要更新一行，如果刚好有另外一个事务拥有这一行的行锁，它又不能这么超然了，会被锁住，进入等待状态。问题是，既然进入了等待状态，那么等到这个事务自己获取到行锁要更新数据的时候，它读到的值又是什么呢？

我给你举一个例子吧。下面是一个只有两行的表的初始化语句。

```sql
mysql> CREATE TABLE `t` (
  `id` int(11) NOT NULL,
  `k` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB;
insert into t(id, k) values(1,1),(2,2);
```

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/823acf76e53c0bdba7beab45e72e90d6-1584367388592.png)

图 1 事务 A、B、C 的执行流程

这里，我们需要注意的是事务的启动时机。

begin/start transaction 命令并不是一个事务的起点，在执行到它们之后的第一个操作 InnoDB  表的语句（第一个快照读语句），事务才真正启动。如果你想要马上启动一个事务，可以使用 start transaction with  consistent snapshot 这个命令。

还需要注意的是，在整个专栏里面，我们的例子中如果没有特别说明，都是默认 autocommit=1。

在这个例子中，事务 C 没有显式地使用 begin/commit，表示这个 update 语句本身就是一个事务，语句完成的时候会自动提交。事务 B 在更新了行之后查询 ; 事务 A 在一个只读事务中查询，并且时间顺序上是在事务 B 的查询之后。

这时，如果我告诉你事务 B 查到的 k 的值是 3，而事务 A 查到的 k 的值是 1，你是不是感觉有点晕呢？

所以，今天这篇文章，我其实就是想和你说明白这个问题，希望借由把这个疑惑解开的过程，能够帮助你对 InnoDB 的事务和锁有更进一步的理解。

在 MySQL 里，有两个“视图”的概念：

- 一个是 view。它是一个用查询语句定义的虚拟表，在调用的时候执行查询语句并生成结果。创建视图的语法是 create view ... ，而它的查询方法与表一样。
- 另一个是 InnoDB 在实现 MVCC 时用到的一致性读视图，即 consistent read view，用于支持 RC（Read Committed，读提交）和 RR（Repeatable Read，可重复读）隔离级别的实现。

它没有物理结构，作用是事务执行期间用来定义“我能看到什么数据”。

在第 3 篇文章[《事务隔离：为什么你改了我还看不见？》]中，我跟你解释过一遍 MVCC 的实现逻辑。今天为了说明查询和更新的区别，我换一个方式来说明，把 read view 拆开。你可以结合这两篇文章的说明来更深一步地理解 MVCC。

#### “快照”在 MVCC 里是怎么工作的？

在可重复读隔离级别下，事务在启动的时候就“拍了个快照”。注意，这个快照是基于整库的。

这时，你会说这看上去不太现实啊。如果一个库有 100G，那么我启动一个事务，MySQL 就要拷贝 100G 的数据出来，这个过程得多慢啊。可是，我平时的事务执行起来很快啊。

实际上，我们并不需要拷贝出这 100G 的数据。我们先来看看这个快照是怎么实现的。

InnoDB 里面每个事务有一个唯一的事务 ID，叫作 transaction id。它是在事务开始的时候向 InnoDB 的事务系统申请的，是按申请顺序严格递增的。

而每行数据也都是有多个版本的。每次事务更新数据的时候，都会生成一个新的数据版本，并且把 transaction id 赋值给这个数据版本的事务 ID，记为 row trx_id。同时，旧的数据版本要保留，并且在新的数据版本中，能够有信息可以直接拿到它。

也就是说，数据表中的一行记录，其实可能有多个版本 (row)，每个版本有自己的 row trx_id。

如图 2 所示，就是一个记录被多个事务连续更新后的状态。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/68d08d277a6f7926a41cc5541d3dfced-1584367388595.png)

图 2 行状态变更图

图中虚线框里是同一行数据的 4 个版本，当前最新版本是 V4，k 的值是 22，它是被 transaction id 为 25 的事务更新的，因此它的 row trx_id 也是 25。

你可能会问，前面的文章不是说，语句更新会生成 undo log（回滚日志）吗？那么，**undo log 在哪呢？**

实际上，图 2 中的三个虚线箭头，就是 undo log；而 V1、V2、V3 并不是物理上真实存在的，而是每次需要的时候根据当前版本和 undo log 计算出来的。比如，需要 V2 的时候，就是通过 V4 依次执行 U3、U2 算出来。

明白了多版本和 row trx_id 的概念后，我们再来想一下，InnoDB 是怎么定义那个“100G”的快照的。

按照可重复读的定义，一个事务启动的时候，能够看到所有已经提交的事务结果。但是之后，这个事务执行期间，其他事务的更新对它不可见。

因此，一个事务只需要在启动的时候声明说，“以我启动的时刻为准，如果一个数据版本是在我启动之前生成的，就认；如果是我启动以后才生成的，我就不认，我必须要找到它的上一个版本”。

当然，如果“上一个版本”也不可见，那就得继续往前找。还有，如果是这个事务自己更新的数据，它自己还是要认的。

在实现上， InnoDB 为每个事务构造了一个数组，用来保存这个事务启动瞬间，当前正在“活跃”的所有事务 ID。“活跃”指的就是，启动了但还没提交。

数组里面事务 ID 的最小值记为低水位，当前系统里面已经创建过的事务 ID 的最大值加 1 记为高水位。

这个视图数组和高水位，就组成了当前事务的一致性视图（read-view）。

而数据版本的可见性规则，就是基于数据的 row trx_id 和这个一致性视图的对比结果得到的。

这个视图数组把所有的 row trx_id 分成了几种不同的情况。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/882114aaf55861832b4270d44507695e-1584367388624.png)

图 3 数据版本可见性规则

这样，对于当前事务的启动瞬间来说，一个数据版本的 row trx_id，有以下几种可能：

1. 如果落在绿色部分，表示这个版本是已提交的事务或者是当前事务自己生成的，这个数据是可见的；
2. 如果落在红色部分，表示这个版本是由将来启动的事务生成的，是肯定不可见的；
3. 如果落在黄色部分，那就包括两种情况 a. 若 row trx_id 在数组中，表示这个版本是由还没提交的事务生成的，不可见； b. 若 row trx_id 不在数组中，表示这个版本是已经提交了的事务生成的，可见。

比如，对于图 2 中的数据来说，如果有一个事务，它的低水位是 18，那么当它访问这一行数据时，就会从 V4 通过 U3 计算出 V3，所以在它看来，这一行的值是 11。

你看，有了这个声明后，系统里面随后发生的更新，是不是就跟这个事务看到的内容无关了呢？因为之后的更新，生成的版本一定属于上面的 2 或者 3(a) 的情况，而对它来说，这些新的数据版本是不存在的，所以这个事务的快照，就是“静态”的了。

所以你现在知道了，**InnoDB 利用了“所有数据都有多个版本”的这个特性，实现了“秒级创建快照”的能力。**

接下来，我们继续看一下图 1 中的三个事务，分析下事务 A 的语句返回的结果，为什么是 k=1。

这里，我们不妨做如下假设：

1. 事务 A 开始前，系统里面只有一个活跃事务 ID 是 99；
2. 事务 A、B、C 的版本号分别是 100、101、102，且当前系统里只有这四个事务；
3. 三个事务开始前，(1,1）这一行数据的 row trx_id 是 90。

这样，事务 A 的视图数组就是 [99,100], 事务 B 的视图数组是 [99,100,101], 事务 C 的视图数组是 [99,100,101,102]。

为了简化分析，我先把其他干扰语句去掉，只画出跟事务 A 查询逻辑有关的操作：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/9416c310e406519b7460437cb0c5c149-1584367388631.png)

图 4 事务 A 查询数据逻辑图

从图中可以看到，第一个有效更新是事务 C，把数据从 (1,1) 改成了 (1,2)。这时候，这个数据的最新版本的 row trx_id 是 102，而 90 这个版本已经成为了历史版本。

第二个有效更新是事务 B，把数据从 (1,2) 改成了 (1,3)。这时候，这个数据的最新版本（即 row trx_id）是 101，而 102 又成为了历史版本。

你可能注意到了，在事务 A 查询的时候，其实事务 B 还没有提交，但是它生成的 (1,3) 这个版本已经变成当前版本了。但这个版本对事务 A 必须是不可见的，否则就变成脏读了。

好，现在事务 A 要来读数据了，它的视图数组是 [99,100]。当然了，读数据都是从当前版本读起的。所以，事务 A 查询语句的读数据流程是这样的：

- 找到 (1,3) 的时候，判断出 row trx_id=101，比高水位大，处于红色区域，不可见；
- 接着，找到上一个历史版本，一看 row trx_id=102，比高水位大，处于红色区域，不可见；
- 再往前找，终于找到了（1,1)，它的 row trx_id=90，比低水位小，处于绿色区域，可见。

这样执行下来，虽然期间这一行数据被修改过，但是事务 A 不论在什么时候查询，看到这行数据的结果都是一致的，所以我们称之为一致性读。

这个判断规则是从代码逻辑直接转译过来的，但是正如你所见，用于人肉分析可见性很麻烦。

所以，我来给你翻译一下。一个数据版本，对于一个事务视图来说，除了自己的更新总是可见以外，有三种情况：

1. 版本未提交，不可见；
2. 版本已提交，但是是在视图创建后提交的，不可见；
3. 版本已提交，而且是在视图创建前提交的，可见。

现在，我们用这个规则来判断图 4 中的查询结果，事务 A 的查询语句的视图数组是在事务 A 启动的时候生成的，这时候：

- (1,3) 还没提交，属于情况 1，不可见；
- (1,2) 虽然提交了，但是是在视图数组创建之后提交的，属于情况 2，不可见；
- (1,1) 是在视图数组创建之前提交的，可见。

你看，去掉数字对比后，只用时间先后顺序来判断，分析起来是不是轻松多了。所以，后面我们就都用这个规则来分析。

#### 更新逻辑

细心的同学可能有疑问了：**事务 B 的 update 语句，如果按照一致性读，好像结果不对哦？**

你看图 5 中，事务 B 的视图数组是先生成的，之后事务 C 才提交，不是应该看不见 (1,2) 吗，怎么能算出 (1,3) 来？

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/86ad7e8abe7bf16505b97718d8ac149f-1584367388692.png)

图 5 事务 B 更新逻辑图

是的，如果事务 B 在更新之前查询一次数据，这个查询返回的 k 的值确实是 1。

但是，当它要去更新数据的时候，就不能再在历史版本上更新了，否则事务 C 的更新就丢失了。因此，事务 B 此时的 set k=k+1 是在（1,2）的基础上进行的操作。

所以，这里就用到了这样一条规则：**更新数据都是先读后写的，而这个读，只能读当前的值，称为“当前读”（current read）。**

因此，在更新的时候，当前读拿到的数据是 (1,2)，更新后生成了新版本的数据 (1,3)，这个新版本的 row trx_id 是 101。

所以，在执行事务 B 查询语句的时候，一看自己的版本号是 101，最新数据的版本号也是 101，是自己的更新，可以直接使用，所以查询得到的 k 的值是 3。

这里我们提到了一个概念，叫作当前读。其实，除了 update 语句外，select 语句如果加锁，也是当前读。

所以，如果把事务 A 的查询语句 select * from t where id=1 修改一下，加上 lock in share  mode 或 for update，也都可以读到版本号是 101 的数据，返回的 k 的值是 3。下面这两个 select  语句，就是分别加了读锁（S 锁，共享锁）和写锁（X 锁，排他锁）。

```csharp
mysql> select k from t where id=1 lock in share mode;
mysql> select k from t where id=1 for update;
```

再往前一步，假设事务 C 不是马上提交的，而是变成了下面的事务 C’，会怎么样呢？

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/cda2a0d7decb61e59dddc83ac51efb6e-1584367388922.png)

图 6 事务 A、B、C'的执行流程

事务 C’的不同是，更新后并没有马上提交，在它提交前，事务 B 的更新语句先发起了。前面说过了，虽然事务 C’还没提交，但是 (1,2) 这个版本也已经生成了，并且是当前的最新版本。那么，事务 B 的更新语句会怎么处理呢？

这时候，我们在上一篇文章中提到的“两阶段锁协议”就要上场了。事务 C’没提交，也就是说 (1,2) 这个版本上的写锁还没释放。而事务 B 是当前读，必须要读最新版本，而且必须加锁，因此就被锁住了，必须等到事务 C’释放这个锁，才能继续它的当前读。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/540967ea905e8b63630e496786d84c92-1584367388924.png)

图 7 事务 B 更新逻辑图（配合事务 C'）

到这里，我们把一致性读、当前读和行锁就串起来了。

现在，我们再回到文章开头的问题：**事务的可重复读的能力是怎么实现的？**

可重复读的核心就是一致性读（consistent read）；而事务更新数据的时候，只能用当前读。如果当前的记录的行锁被其他事务占用的话，就需要进入锁等待。

而读提交的逻辑和可重复读的逻辑类似，它们最主要的区别是：

- 在可重复读隔离级别下，只需要在事务开始的时候创建一致性视图，之后事务里的其他查询都共用这个一致性视图；
- 在读提交隔离级别下，每一个语句执行前都会重新算出一个新的视图。

那么，我们再看一下，在读提交隔离级别下，事务 A 和事务 B 的查询语句查到的 k，分别应该是多少呢？

这里需要说明一下，“start transaction with consistent snapshot;  ”的意思是从这个语句开始，创建一个持续整个事务的一致性快照。所以，在读提交隔离级别下，这个用法就没意义了，等效于普通的 start  transaction。

下面是读提交时的状态图，可以看到这两个查询语句的创建视图数组的时机发生了变化，就是图中的 read view 框。（注意：这里，我们用的还是事务 C 的逻辑直接提交，而不是事务 C’）

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/ed4b8d03287df67ecca53b5b4830ee6e-1584367389025.png)

图 8 读提交隔离级别下的事务状态图

这时，事务 A 的查询语句的视图数组是在执行这个语句的时候创建的，时序上 (1,2)、(1,3) 的生成时间都在创建这个视图数组的时刻之前。但是，在这个时刻：

- (1,3) 还没提交，属于情况 1，不可见；
- (1,2) 提交了，属于情况 3，可见。

所以，这时候事务 A 查询语句返回的是 k=2。

显然地，事务 B 查询结果 k=3。

#### 小结

InnoDB 的行数据有多个版本，每个数据版本有自己的 row trx_id，每个事务或者语句有自己的一致性视图。普通查询语句是一致性读，一致性读会根据 row trx_id 和一致性视图确定数据版本的可见性。

- 对于可重复读，查询只承认在事务启动前就已经提交完成的数据；
- 对于读提交，查询只承认在语句启动前就已经提交完成的数据；

而当前读，总是读取已经提交完成的最新版本。

你也可以想一下，为什么表结构不支持“可重复读”？这是因为表结构没有对应的行数据，也没有 row trx_id，因此只能遵循当前读的逻辑。

当然，MySQL 8.0 已经可以把表结构放在 InnoDB 字典里了，也许以后会支持表结构的可重复读。

又到思考题时间了。我用下面的表结构和初始化语句作为试验环境，事务隔离级别是可重复读。现在，我要把所有“字段 c 和 id 值相等的行”的 c 值清零，但是却发现了一个“诡异”的、改不掉的情况。请你构造出这种情况，并说明其原理。

```sql
mysql> CREATE TABLE `t` (
  `id` int(11) NOT NULL,
  `c` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB;
insert into t(id, c) values(1,1),(2,2),(3,3),(4,4);
```

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/9b8fe7cf88c9ba40dc12e93e36c3060b-1584367389183.png)复现出来以后，请你再思考一下，在实际的业务开发中有没有可能碰到这种情况？你的应用代码会不会掉进这个“坑”里，你又是怎么解决的呢？

你可以把你的思考和观点写在留言区里，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

我在上一篇文章最后，留给你的问题是：怎么删除表的前 10000 行。比较多的留言都选择了第二种方式，即：在一个连接中循环执行 20 次 delete from T limit 500。

确实是这样的，第二种方式是相对较好的。

第一种方式（即：直接执行 delete from T limit 10000）里面，单个语句占用时间长，锁的时间也比较长；而且大事务还会导致主从延迟。

第三种方式（即：在 20 个连接中同时执行 delete from T limit 500），会人为造成锁冲突。

评论区留言点赞板：

> @Tony Du 的评论，详细而且准确。 @Knight²º¹⁸ 提到了如果可以加上特定条件，将这 10000  行天然分开，可以考虑第三种。是的，实际上在操作的时候我也建议你尽量拿到 ID 再删除。 @荒漠甘泉 提了一个不错的问题，大家需要区分行锁、MDL 锁和表锁的区别。对 InnoDB 表更新一行，可能过了 MDL 关，却被挡在行锁阶段。

### 09 普通索引和唯一索引，应该怎么选择？

今天的正文开始前，我要特意感谢一下评论区几位留下高质量留言的同学。

用户名是 @某、人  的同学，对文章的知识点做了梳理，然后提了关于事务可见性的问题，就是先启动但是后提交的事务，对数据可见性的影响。@夏日雨同学也提到了这个问题，我在置顶评论中回复了，今天的文章末尾也会再展开说明。@Justin 和 @倪大人两位同学提了两个好问题。

对于能够引发更深一步思考的问题，我会在回复的内容中写上“好问题”三个字，方便你搜索，你也可以去看看他们的留言。

非常感谢大家很细致地看文章，并且留下了那么多和很高质量的留言。知道文章有给大家带来一些新理解，对我来说是一个很好的鼓励。同时，也让其他认真看评论区的同学，有机会发现一些自己还没有意识到的、但可能还不清晰的知识点，这也在总体上提高了整个专栏的质量。再次谢谢你们。

好了，现在就回到我们今天的正文内容。

在前面的基础篇文章中，我给你介绍过索引的基本概念，相信你已经了解了唯一索引和普通索引的区别。今天我们就继续来谈谈，在不同的业务场景下，应该选择普通索引，还是唯一索引？

假设你在维护一个市民系统，每个人都有一个唯一的身份证号，而且业务代码已经保证了不会写入两个重复的身份证号。如果市民系统需要按照身份证号查姓名，就会执行类似这样的 SQL 语句：

```csharp
select name from CUser where id_card = 'xxxxxxxyyyyyyzzzzz';
```

所以，你一定会考虑在 id_card 字段上建索引。

由于身份证号字段比较大，我不建议你把身份证号当做主键，那么现在你有两个选择，要么给 id_card 字段创建唯一索引，要么创建一个普通索引。如果业务代码已经保证了不会写入重复的身份证号，那么这两个选择逻辑上都是正确的。

现在我要问你的是，从性能的角度考虑，你选择唯一索引还是普通索引呢？选择的依据是什么呢？

简单起见，我们还是用第 4 篇文章[《深入浅出索引（上）》]中的例子来说明，假设字段 k 上的值都不重复。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/1ed9536031d6698570ea175a7b7f9a46-1584367389192.png)

图 1 InnoDB 的索引组织结构

接下来，我们就从这两种索引对查询语句和更新语句的性能影响来进行分析。

#### 查询过程

假设，执行查询的语句是 select id from T where k=5。这个查询语句在索引树上查找的过程，先是通过 B+ 树从树根开始，按层搜索到叶子节点，也就是图中右下角的这个数据页，然后可以认为数据页内部通过二分法来定位记录。

- 对于普通索引来说，查找到满足条件的第一个记录 (5,500) 后，需要查找下一个记录，直到碰到第一个不满足 k=5 条件的记录。
- 对于唯一索引来说，由于索引定义了唯一性，查找到第一个满足条件的记录后，就会停止继续检索。

那么，这个不同带来的性能差距会有多少呢？答案是，微乎其微。

你知道的，InnoDB 的数据是按数据页为单位来读写的。也就是说，当需要读一条记录的时候，并不是将这个记录本身从磁盘读出来，而是以页为单位，将其整体读入内存。在 InnoDB 中，每个数据页的大小默认是 16KB。

因为引擎是按页读写的，所以说，当找到 k=5 的记录的时候，它所在的数据页就都在内存里了。那么，对于普通索引来说，要多做的那一次“查找和判断下一条记录”的操作，就只需要一次指针寻找和一次计算。

当然，如果 k=5 这个记录刚好是这个数据页的最后一个记录，那么要取下一个记录，必须读取下一个数据页，这个操作会稍微复杂一些。

但是，我们之前计算过，对于整型字段，一个数据页可以放近千个 key，因此出现这种情况的概率会很低。所以，我们计算平均性能差异时，仍可以认为这个操作成本对于现在的 CPU 来说可以忽略不计。

#### 更新过程

为了说明普通索引和唯一索引对更新语句性能的影响这个问题，我需要先跟你介绍一下 change buffer。

当需要更新一个数据页时，如果数据页在内存中就直接更新，而如果这个数据页还没有在内存中的话，在不影响数据一致性的前提下，InooDB  会将这些更新操作缓存在 change buffer  中，这样就不需要从磁盘中读入这个数据页了。在下次查询需要访问这个数据页的时候，将数据页读入内存，然后执行 change buffer  中与这个页有关的操作。通过这种方式就能保证这个数据逻辑的正确性。

需要说明的是，虽然名字叫作 change buffer，实际上它是可以持久化的数据。也就是说，change buffer 在内存中有拷贝，也会被写入到磁盘上。

将 change buffer 中的操作应用到原数据页，得到最新结果的过程称为 merge。除了访问这个数据页会触发 merge 外，系统有后台线程会定期 merge。在数据库正常关闭（shutdown）的过程中，也会执行 merge 操作。

显然，如果能够将更新操作先记录在 change buffer，减少读磁盘，语句的执行速度会得到明显的提升。而且，数据读入内存是需要占用 buffer pool 的，所以这种方式还能够避免占用内存，提高内存利用率。

那么，**什么条件下可以使用 change buffer 呢？**

对于唯一索引来说，所有的更新操作都要先判断这个操作是否违反唯一性约束。比如，要插入 (4,400)  这个记录，就要先判断现在表中是否已经存在 k=4  的记录，而这必须要将数据页读入内存才能判断。如果都已经读入到内存了，那直接更新内存会更快，就没必要使用 change buffer 了。

因此，唯一索引的更新就不能使用 change buffer，实际上也只有普通索引可以使用。

change buffer 用的是 buffer pool 里的内存，因此不能无限增大。change buffer 的大小，可以通过参数  innodb_change_buffer_max_size 来动态设置。这个参数设置为 50 的时候，表示 change buffer  的大小最多只能占用 buffer pool 的 50%。

现在，你已经理解了 change buffer 的机制，那么我们再一起来看看**如果要在这张表中插入一个新记录 (4,400) 的话，InnoDB 的处理流程是怎样的。**

第一种情况是，**这个记录要更新的目标页在内存中**。这时，InnoDB 的处理流程如下：

- 对于唯一索引来说，找到 3 和 5 之间的位置，判断到没有冲突，插入这个值，语句执行结束；
- 对于普通索引来说，找到 3 和 5 之间的位置，插入这个值，语句执行结束。

这样看来，普通索引和唯一索引对更新语句性能影响的差别，只是一个判断，只会耗费微小的 CPU 时间。

但，这不是我们关注的重点。

第二种情况是，**这个记录要更新的目标页不在内存中**。这时，InnoDB 的处理流程如下：

- 对于唯一索引来说，需要将数据页读入内存，判断到没有冲突，插入这个值，语句执行结束；
- 对于普通索引来说，则是将更新记录在 change buffer，语句执行就结束了。

将数据从磁盘读入内存涉及随机 IO 的访问，是数据库里面成本最高的操作之一。change buffer 因为减少了随机磁盘访问，所以对更新性能的提升是会很明显的。

之前我就碰到过一件事儿，有个 DBA 的同学跟我反馈说，他负责的某个业务的库内存命中率突然从 99% 降低到了  75%，整个系统处于阻塞状态，更新语句全部堵住。而探究其原因后，我发现这个业务有大量插入数据的操作，而他在前一天把其中的某个普通索引改成了唯一索引。

#### change buffer 的使用场景

通过上面的分析，你已经清楚了使用 change buffer 对更新过程的加速作用，也清楚了 change buffer  只限于用在普通索引的场景下，而不适用于唯一索引。那么，现在有一个问题就是：普通索引的所有场景，使用 change buffer  都可以起到加速作用吗？

因为 merge 的时候是真正进行数据更新的时刻，而 change buffer 的主要目的就是将记录的变更动作缓存下来，所以在一个数据页做 merge 之前，change buffer 记录的变更越多（也就是这个页面上要更新的次数越多），收益就越大。

因此，对于写多读少的业务来说，页面在写完以后马上被访问到的概率比较小，此时 change buffer 的使用效果最好。这种业务模型常见的就是账单类、日志类的系统。

反过来，假设一个业务的更新模式是写入之后马上会做查询，那么即使满足了条件，将更新先记录在 change  buffer，但之后由于马上要访问这个数据页，会立即触发 merge 过程。这样随机访问 IO 的次数不会减少，反而增加了 change  buffer 的维护代价。所以，对于这种业务模式来说，change buffer 反而起到了副作用。

#### 索引选择和实践

回到我们文章开头的问题，普通索引和唯一索引应该怎么选择。其实，这两类索引在查询能力上是没差别的，主要考虑的是对更新性能的影响。所以，我建议你尽量选择普通索引。

如果所有的更新后面，都马上伴随着对这个记录的查询，那么你应该关闭 change buffer。而在其他情况下，change buffer 都能提升更新性能。

在实际使用中，你会发现，普通索引和 change buffer 的配合使用，对于数据量大的表的更新优化还是很明显的。

特别地，在使用机械硬盘时，change buffer  这个机制的收效是非常显著的。所以，当你有一个类似“历史数据”的库，并且出于成本考虑用的是机械硬盘时，那你应该特别关注这些表里的索引，尽量使用普通索引，然后把 change buffer 尽量开大，以确保这个“历史数据”表的数据写入速度。

change buffer 和 redo log

理解了 change buffer 的原理，你可能会联想到我在前面文章中和你介绍过的 redo log 和 WAL。

在前面文章的评论中，我发现有同学混淆了 redo log 和 change buffer。WAL 提升性能的核心机制，也的确是尽量减少随机读写，这两个概念确实容易混淆。所以，这里我把它们放到了同一个流程里来说明，便于你区分这两个概念。

> 备注：这里，你可以再回顾下第 2 篇文章[《日志系统：一条 SQL 更新语句是如何执行的？》]中的相关内容。

现在，我们要在表上执行这个插入语句：

```scss
mysql> insert into t(id,k) values(id1,k1),(id2,k2);
```

这里，我们假设当前 k 索引树的状态，查找到位置后，k1 所在的数据页在内存 (InnoDB buffer pool) 中，k2 所在的数据页不在内存中。如图 2 所示是带 change buffer 的更新状态图。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/980a2b786f0ea7adabef2e64fb4c4ca3-1584367389287.png)

图 2 带 change buffer 的更新过程

分析这条更新语句，你会发现它涉及了四个部分：内存、redo log（ib_log_fileX）、 数据表空间（t.ibd）、系统表空间（ibdata1）。

这条更新语句做了如下的操作（按照图中的数字顺序）：

1. Page 1 在内存中，直接更新内存；
2. Page 2 没有在内存中，就在内存的 change buffer 区域，记录下“我要往 Page 2 插入一行”这个信息
3. 将上述两个动作记入 redo log 中（图中 3 和 4）。

做完上面这些，事务就可以完成了。所以，你会看到，执行这条更新语句的成本很低，就是写了两处内存，然后写了一处磁盘（两次操作合在一起写了一次磁盘），而且还是顺序写的。

同时，图中的两个虚线箭头，是后台操作，不影响更新的响应时间。

那在这之后的读请求，要怎么处理呢？

比如，我们现在要执行 select * from t where k in (k1, k2)。这里，我画了这两个读请求的流程图。

如果读语句发生在更新语句后不久，内存中的数据都还在，那么此时的这两个读操作就与系统表空间（ibdata1）和 redo log（ib_log_fileX）无关了。所以，我在图中就没画出这两部分。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/6dc743577af1dbcbb8550bddbfc5f98e-1584367389446.png)

图 3 带 change buffer 的读过程

从图中可以看到：

1. 读 Page 1 的时候，直接从内存返回。有几位同学在前面文章的评论中问到，WAL 之后如果读数据，是不是一定要读盘，是不是一定要从  redo log 里面把数据更新以后才可以返回？其实是不用的。你可以看一下图 3  的这个状态，虽然磁盘上还是之前的数据，但是这里直接从内存返回结果，结果是正确的。
2. 要读 Page 2 的时候，需要把 Page 2 从磁盘读入内存中，然后应用 change buffer 里面的操作日志，生成一个正确的版本并返回结果。

可以看到，直到需要读 Page 2 的时候，这个数据页才会被读入内存。

所以，如果要简单地对比这两个机制在提升更新性能上的收益的话，**redo log 主要节省的是随机写磁盘的 IO 消耗（转成顺序写），而 change buffer 主要节省的则是随机读磁盘的 IO 消耗。**

#### 小结

今天，我从普通索引和唯一索引的选择开始，和你分享了数据的查询和更新过程，然后说明了 change buffer 的机制以及应用场景，最后讲到了索引选择的实践。

由于唯一索引用不上 change buffer 的优化机制，因此如果业务可以接受，从性能角度出发我建议你优先考虑非唯一索引。

最后，又到了思考题时间。

通过图 2 你可以看到，change buffer 一开始是写内存的，那么如果这个时候机器掉电重启，会不会导致 change buffer 丢失呢？change buffer 丢失可不是小事儿，再从磁盘读入数据可就没有了 merge 过程，就等于是数据丢失了。会不会出现这种情况呢？

你可以把你的思考和观点写在留言区里，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

**补充：** 评论区大家对“是否使用唯一索引”有比较多的讨论，主要是纠结在“业务可能无法确保”的情况。这里，我再说明一下：

- 首先，业务正确性优先。咱们这篇文章的前提是“业务代码已经保证不会写入重复数据”的情况下，讨论性能问题。如果业务不能保证，或者业务就是要求数据库来做约束，那么没得选，必须创建唯一索引。这种情况下，本篇文章的意义在于，如果碰上了大量插入数据慢、内存命中率低的时候，可以给你多提供一个排查思路。
- 然后，在一些“归档库”的场景，你是可以考虑使用唯一索引的。比如，线上数据只需要保留半年，然后历史数据保存在归档库。这时候，归档数据已经是确保没有唯一键冲突了。要提高归档效率，可以考虑把表里面的唯一索引改成普通索引。

#### 上期问题时间

上期的问题是：如何构造一个“数据无法修改”的场景。评论区里已经有不少同学给出了正确答案，这里我再描述一下。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/be7a4d8af04cdf93aaa11108933559ae-1584367389604.png)这样，session A 看到的就是我截图的效果了。

其实，还有另外一种场景，同学们在留言区都还没有提到。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/e24a0689571337959138d787c408defa-1584367389607.png)

这个操作序列跑出来，session A 看的内容也是能够复现我截图的效果的。这个 session B’启动的事务比 A 要早，其实是上期我们描述事务版本的可见性规则时留的彩蛋，因为规则里还有一个“活跃事务的判断”，我是准备留到这里再补充的。

当我试图在这里讲述完整规则的时候，发现第 8 篇文章[《事务到底是隔离的还是不隔离的？》]中的解释引入了太多的概念，以致于分析起来非常复杂。

因此，我重写了第 8 篇，这样我们人工去判断可见性的时候，才会更方便。【看到这里，我建议你能够再重新打开第 8 篇文章并认真学习一次。如果学习的过程中，有任何问题，也欢迎你给我留言】

用新的方式来分析 session B’的更新为什么对 session A 不可见就是：在 session A 视图数组创建的瞬间，session B’是活跃的，属于“版本未提交，不可见”这种情况。

业务中如果要绕过这类问题，@约书亚提供了一个“乐观锁”的解法，大家可以去上一篇的留言区看一下。

评论区留言点赞板：

> @某、人、@夏日雨、@周巘、@李金刚 等同学提了一个很好的问题，就是我们今天答案的 session B’ 的情况； @justin 提到了提交和未提交版本的区别对待，@倪大人 提到了读提交和当前读的区别，都是经过了思考后提出的好问题，大家可以去留言区看看。

### 10 MySQL为什么有时候会选错索引？

前面我们介绍过索引，你已经知道了在 MySQL 中一张表其实是可以支持多个索引的。但是，你写 SQL 语句的时候，并没有主动指定使用哪个索引。也就是说，使用哪个索引是由 MySQL 来确定的。

不知道你有没有碰到过这种情况，一条本来可以执行得很快的语句，却由于 MySQL 选错了索引，而导致执行速度变得很慢？

我们一起来看一个例子吧。

我们先建一个简单的表，表里有 a、b 两个字段，并分别建上索引：

```go
CREATE TABLE `t` (
  `id` int(11) NOT NULL,
  `a` int(11) DEFAULT NULL,
  `b` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `a` (`a`),
  KEY `b` (`b`)
) ENGINE=InnoDB；
```

然后，我们往表 t 中插入 10 万行记录，取值按整数递增，即：(1,1,1)，(2,2,2)，(3,3,3) 直到 (100000,100000,100000)。

我是用存储过程来插入数据的，这里我贴出来方便你复现：

```sql
delimiter ;;
create procedure idata()
begin
  declare i int;
  set i=1;
  while(i<=100000)do
    insert into t values(i, i, i);
    set i=i+1;
  end while;
end;;
delimiter ;
call idata();
```

接下来，我们分析一条 SQL 语句：

```sql
mysql> select * from t where a between 10000 and 20000;
```

你一定会说，这个语句还用分析吗，很简单呀，a 上有索引，肯定是要使用索引 a 的。

你说得没错，图 1 显示的就是使用 explain 命令看到的这条语句的执行情况。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/2cfce769551c6eac9bfbee0563d48fe3-1584367389610.png)

图 1 使用 explain 命令查看语句执行情况

从图 1 看上去，这条查询语句的执行也确实符合预期，key 这个字段值是’a’，表示优化器选择了索引 a。

不过别急，这个案例不会这么简单。在我们已经准备好的包含了 10 万行数据的表上，我们再做如下操作。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/1e5ba1c2934d3b2c0d96b210a27e1a1e-1584367389613.png)

图 2 session A 和 session B 的执行流程

这里，session A 的操作你已经很熟悉了，它就是开启了一个事务。随后，session B 把数据都删除后，又调用了 idata 这个存储过程，插入了 10 万行数据。

这时候，session B 的查询语句 select * from t where a between 10000 and 20000 就不会再选择索引 a 了。我们可以通过慢查询日志（slow log）来查看一下具体的执行情况。

为了说明优化器选择的结果是否正确，我增加了一个对照，即：使用 force index(a) 来让优化器强制使用索引 a（这部分内容，我还会在这篇文章的后半部分中提到）。

下面的三条 SQL 语句，就是这个实验过程。

```sql
set long_query_time=0;
select * from t where a between 10000 and 20000; /*Q1*/
select * from t force index(a) where a between 10000 and 20000;/*Q2*/
```

- 第一句，是将慢查询日志的阈值设置为 0，表示这个线程接下来的语句都会被记录入慢查询日志中；
- 第二句，Q1 是 session B 原来的查询；
- 第三句，Q2 是加了 force index(a) 来和 session B 原来的查询语句执行情况对比。

如图 3 所示是这三条 SQL 语句执行完成后的慢查询日志。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/7c58b9c71853b8bba1a8ad5e926de1f6-1584367389615.png)

图 3 slow log 结果

可以看到，Q1 扫描了 10 万行，显然是走了全表扫描，执行时间是 40 毫秒。Q2 扫描了 10001 行，执行了 21 毫秒。也就是说，我们在没有使用 force index 的时候，MySQL 用错了索引，导致了更长的执行时间。

这个例子对应的是我们平常不断地删除历史数据和新增数据的场景。这时，MySQL 竟然会选错索引，是不是有点奇怪呢？今天，我们就从这个奇怪的结果说起吧。

#### 优化器的逻辑

在第一篇文章中，我们就提到过，选择索引是优化器的工作。

而优化器选择索引的目的，是找到一个最优的执行方案，并用最小的代价去执行语句。在数据库里面，扫描行数是影响执行代价的因素之一。扫描的行数越少，意味着访问磁盘数据的次数越少，消耗的 CPU 资源越少。

当然，扫描行数并不是唯一的判断标准，优化器还会结合是否使用临时表、是否排序等因素进行综合判断。

我们这个简单的查询语句并没有涉及到临时表和排序，所以 MySQL 选错索引肯定是在判断扫描行数的时候出问题了。

那么，问题就是：**扫描行数是怎么判断的？**

MySQL 在真正开始执行语句之前，并不能精确地知道满足这个条件的记录有多少条，而只能根据统计信息来估算记录数。

这个统计信息就是索引的“区分度”。显然，一个索引上不同的值越多，这个索引的区分度就越好。而一个索引上不同的值的个数，我们称之为“基数”（cardinality）。也就是说，这个基数越大，索引的区分度越好。

我们可以使用 show index 方法，看到一个索引的基数。如图 4 所示，就是表 t 的 show index 的结果 。虽然这个表的每一行的三个字段值都是一样的，但是在统计信息中，这三个索引的基数值并不同，而且其实都不准确。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/16dbf8124ad529fec0066950446079d4-1584367389624.png)

图 4 表 t 的 show index 结果

那么，**MySQL 是怎样得到索引的基数的呢？**这里，我给你简单介绍一下 MySQL 采样统计的方法。

为什么要采样统计呢？因为把整张表取出来一行行统计，虽然可以得到精确的结果，但是代价太高了，所以只能选择“采样统计”。

采样统计的时候，InnoDB 默认会选择 N 个数据页，统计这些页面上的不同值，得到一个平均值，然后乘以这个索引的页面数，就得到了这个索引的基数。

而数据表是会持续更新的，索引统计信息也不会固定不变。所以，当变更的数据行数超过 1/M 的时候，会自动触发重新做一次索引统计。

在 MySQL 中，有两种存储索引统计的方式，可以通过设置参数 innodb_stats_persistent 的值来选择：

- 设置为 on 的时候，表示统计信息会持久化存储。这时，默认的 N 是 20，M 是 10。
- 设置为 off 的时候，表示统计信息只存储在内存中。这时，默认的 N 是 8，M 是 16。

由于是采样统计，所以不管 N 是 20 还是 8，这个基数都是很容易不准的。

但，这还不是全部。

你可以从图 4 中看到，这次的索引统计值（cardinality 列）虽然不够精确，但大体上还是差不多的，选错索引一定还有别的原因。

其实索引统计只是一个输入，对于一个具体的语句来说，优化器还要判断，执行这个语句本身要扫描多少行。

接下来，我们再一起看看优化器预估的，这两个语句的扫描行数是多少。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/e2bc5f120858391d4accff05573e1289-1584367389624.png)

图 5 意外的 explain 结果

rows 这个字段表示的是预计扫描行数。

其中，Q1 的结果还是符合预期的，rows 的值是 104620；但是 Q2 的 rows 值是 37116，偏差就大了。而图 1 中我们用 explain 命令看到的 rows 是只有 10001 行，是这个偏差误导了优化器的判断。

到这里，可能你的第一个疑问不是为什么不准，而是优化器为什么放着扫描 37000 行的执行计划不用，却选择了扫描行数是 100000 的执行计划呢？

这是因为，如果使用索引 a，每次从索引 a 上拿到一个值，都要回到主键索引上查出整行数据，这个代价优化器也要算进去的。

而如果选择扫描 10 万行，是直接在主键索引上扫描的，没有额外的代价。

优化器会估算这两个选择的代价，从结果看来，优化器认为直接扫描主键索引更快。当然，从执行时间看来，这个选择并不是最优的。

使用普通索引需要把回表的代价算进去，在图 1 执行 explain 的时候，也考虑了这个策略的代价 ，但图 1 的选择是对的。也就是说，这个策略并没有问题。

所以冤有头债有主，MySQL 选错索引，这件事儿还得归咎到没能准确地判断出扫描行数。至于为什么会得到错误的扫描行数，这个原因就作为课后问题，留给你去分析了。

既然是统计信息不对，那就修正。analyze table t 命令，可以用来重新统计索引信息。我们来看一下执行效果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/209e9d3514688a3bcabbb75e54e1e49c-1584367389626.png)

图 6 执行 analyze table t 命令恢复的 explain 结果

这回对了。

所以在实践中，如果你发现 explain 的结果预估的 rows 值跟实际情况差距比较大，可以采用这个方法来处理。

其实，如果只是索引统计不准确，通过 analyze 命令可以解决很多问题，但是前面我们说了，优化器可不止是看扫描行数。

依然是基于这个表 t，我们看看另外一个语句：

```sql
mysql> select * from t where (a between 1 and 1000)  and (b between 50000 and 100000) order by b limit 1;
```

从条件上看，这个查询没有符合条件的记录，因此会返回空集合。

在开始执行这条语句之前，你可以先设想一下，如果你来选择索引，会选择哪一个呢？

为了便于分析，我们先来看一下 a、b 这两个索引的结构图。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/1d037f92063e800c3bfff3f4dbf1a2b9-1584367389629.png)

图 7 a、b 索引的结构图

如果使用索引 a 进行查询，那么就是扫描索引 a 的前 1000 个值，然后取到对应的 id，再到主键索引上去查出每一行，然后根据字段 b 来过滤。显然这样需要扫描 1000 行。

如果使用索引 b 进行查询，那么就是扫描索引 b 的最后 50001 个值，与上面的执行过程相同，也是需要回到主键索引上取值再判断，所以需要扫描 50001 行。

所以你一定会想，如果使用索引 a 的话，执行速度明显会快很多。那么，下面我们就来看看到底是不是这么一回事儿。

图 8 是执行 explain 的结果。

```sql
mysql> explain select * from t where (a between 1 and 1000) and (b between 50000 and 100000) order by b limit 1;
```

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/483bcb1ef3bb902844e80d9cbdd73ab8-1584367389789.png)

图 8 使用 explain 方法查看执行计划 2

可以看到，返回结果中 key 字段显示，这次优化器选择了索引 b，而 rows 字段显示需要扫描的行数是 50198。

从这个结果中，你可以得到两个结论：

1. 扫描行数的估计值依然不准确；
2. 这个例子里 MySQL 又选错了索引。

#### 索引选择异常和处理

其实大多数时候优化器都能找到正确的索引，但偶尔你还是会碰到我们上面举例的这两种情况：原本可以执行得很快的 SQL 语句，执行速度却比你预期的慢很多，你应该怎么办呢？

**一种方法是，像我们第一个例子一样，采用 force index 强行选择一个索引。**MySQL  会根据词法解析的结果分析出可能可以使用的索引作为候选项，然后在候选列表中依次判断每个索引需要扫描多少行。如果 force index  指定的索引在候选索引列表中，就直接选择这个索引，不再评估其他索引的执行代价。

我们来看看第二个例子。刚开始分析时，我们认为选择索引 a 会更好。现在，我们就来看看执行效果：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/9582401a6bed6cb8fd803c9555750b54-1584367389790.png)

图 9 使用不同索引的语句执行耗时

可以看到，原本语句需要执行 2.23 秒，而当你使用 force index(a) 的时候，只用了 0.05 秒，比优化器的选择快了 40 多倍。

也就是说，优化器没有选择正确的索引，force index 起到了“矫正”的作用。

不过很多程序员不喜欢使用 force index，一来这么写不优美，二来如果索引改了名字，这个语句也得改，显得很麻烦。而且如果以后迁移到别的数据库的话，这个语法还可能会不兼容。

但其实使用 force index 最主要的问题还是变更的及时性。因为选错索引的情况还是比较少出现的，所以开发的时候通常不会先写上  force index。而是等到线上出现问题的时候，你才会再去修改 SQL 语句、加上 force  index。但是修改之后还要测试和发布，对于生产系统来说，这个过程不够敏捷。

所以，数据库的问题最好还是在数据库内部来解决。那么，在数据库里面该怎样解决呢？

既然优化器放弃了使用索引 a，说明 a 还不够合适，所以**第二种方法就是，我们可以考虑修改语句，引导 MySQL  使用我们期望的索引。**比如，在这个例子里，显然把“order by b limit 1” 改成 “order by b,a limit 1”  ，语义的逻辑是相同的。

我们来看看改之后的效果：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/14cd598e52a2b72dd334a42603e5b894-1584367389796.png)

图 10 order by b,a limit 1 执行结果

之前优化器选择使用索引 b，是因为它认为使用索引 b 可以避免排序（b 本身是索引，已经是有序的了，如果选择索引 b 的话，不需要再做排序，只需要遍历），所以即使扫描行数多，也判定为代价更小。

现在 order by b,a 这种写法，要求按照 b,a 排序，就意味着使用这两个索引都需要排序。因此，扫描行数成了影响决策的主要条件，于是此时优化器选了只需要扫描 1000 行的索引 a。

当然，这种修改并不是通用的优化手段，只是刚好在这个语句里面有 limit 1，因此如果有满足条件的记录， order by b limit 1 和 order by b,a limit 1 都会返回 b 是最小的那一行，逻辑上一致，才可以这么做。

如果你觉得修改语义这件事儿不太好，这里还有一种改法，图 11 是执行效果。

```sql
mysql> select * from  (select * from t where (a between 1 and 1000)  and (b between 50000 and 100000) order by b limit 100)alias limit 1;
```

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/b1a2ad43c78477d7f93dbc692cbaa0d7-1584367389799.png)

图 11 改写 SQL 的 explain

在这个例子里，我们用 limit 100 让优化器意识到，使用 b 索引代价是很高的。其实是我们根据数据特征诱导了一下优化器，也不具备通用性。

**第三种方法是，在有些场景下，我们可以新建一个更合适的索引，来提供给优化器做选择，或删掉误用的索引。**

不过，在这个例子中，我没有找到通过新增索引来改变优化器行为的方法。这种情况其实比较少，尤其是经过 DBA 索引优化过的库，再碰到这个 bug，找到一个更合适的索引一般比较难。

如果我说还有一个方法是删掉索引 b，你可能会觉得好笑。但实际上我碰到过两次这样的例子，最终是 DBA 跟业务开发沟通后，发现这个优化器错误选择的索引其实根本没有必要存在，于是就删掉了这个索引，优化器也就重新选择到了正确的索引。

#### 小结

今天我们一起聊了聊索引统计的更新机制，并提到了优化器存在选错索引的可能性。

对于由于索引统计信息不准确导致的问题，你可以用 analyze table 来解决。

而对于其他优化器误判的情况，你可以在应用端用 force index 来强行指定索引，也可以通过修改语句来引导优化器，还可以通过增加或者删除索引来绕过这个问题。

你可能会说，今天这篇文章后面的几个例子，怎么都没有展开说明其原理。我要告诉你的是，今天的话题，我们面对的是 MySQL 的 bug，每一个展开都必须深入到一行行代码去量化，实在不是我们在这里应该做的事情。

所以，我把我用过的解决方法跟你分享，希望你在碰到类似情况的时候，能够有一些思路。

你平时在处理 MySQL 优化器 bug 的时候有什么别的方法，也发到评论区分享一下吧。

最后，我给你留下一个思考题。前面我们在构造第一个例子的过程中，通过 session A 的配合，让 session B 删除数据后又重新插入了一遍数据，然后就发现 explain 结果中，rows 字段从 10001 变成 37000 多。

而如果没有 session A 的配合，只是单独执行 delete from t 、call idata()、explain 这三句话，会看到 rows 字段其实还是 10000 左右。你可以自己验证一下这个结果。

这是什么原因呢？也请你分析一下吧。

你可以把你的分析结论写在留言区里，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

我在上一篇文章最后留给你的问题是，如果某次写入使用了 change buffer 机制，之后主机异常重启，是否会丢失 change buffer 和数据。

这个问题的答案是不会丢失，留言区的很多同学都回答对了。虽然是只更新内存，但是在事务提交的时候，我们把 change buffer 的操作也记录到 redo log 里了，所以崩溃恢复的时候，change buffer 也能找回来。

在评论区有同学问到，merge 的过程是否会把数据直接写回磁盘，这是个好问题。这里，我再为你分析一下。

merge 的执行流程是这样的：

1. 从磁盘读入数据页到内存（老版本的数据页）；
2. 从 change buffer 里找出这个数据页的 change buffer 记录 (可能有多个），依次应用，得到新版数据页；
3. 写 redo log。这个 redo log 包含了数据的变更和 change buffer 的变更。

到这里 merge 过程就结束了。这时候，数据页和内存中 change buffer 对应的磁盘位置都还没有修改，属于脏页，之后各自刷回自己的物理数据，就是另外一个过程了。

评论区留言点赞板：

> @某、人 把 02 篇的 redo log 更新细节和 change buffer 的更新串了起来； @Ivan 回复了其他同学的问题，并联系到 Checkpoint 机制； @约书亚 问到了 merge 和 redolog 的关系。

### 11 怎么给字符串字段加索引？

现在，几乎所有的系统都支持邮箱登录，如何在邮箱这样的字段上建立合理的索引，是我们今天要讨论的问题。

假设，你现在维护一个支持邮箱登录的系统，用户表是这么定义的：

```sql
mysql> create table SUser(
ID bigint unsigned primary key,
email varchar(64), 
... 
)engine=innodb; 
```

由于要使用邮箱登录，所以业务代码中一定会出现类似于这样的语句：

```csharp
mysql> select f1, f2 from SUser where email='xxx';
```

从第 4 和第 5 篇讲解索引的文章中，我们可以知道，如果 email 这个字段上没有索引，那么这个语句就只能做全表扫描。

同时，MySQL 是支持前缀索引的，也就是说，你可以定义字符串的一部分作为索引。默认地，如果你创建索引的语句不指定前缀长度，那么索引就会包含整个字符串。

比如，这两个在 email 字段上创建索引的语句：

```sql
mysql> alter table SUser add index index1(email);
或
mysql> alter table SUser add index index2(email(6));
```

第一个语句创建的 index1 索引里面，包含了每个记录的整个字符串；而第二个语句创建的 index2 索引里面，对于每个记录都是只取前 6 个字节。

那么，这两种不同的定义在数据结构和存储上有什么区别呢？如图 2 和 3 所示，就是这两个索引的示意图。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/d31da662bee595991862c439a5567eb7-1584367389800.jpg)

图 1 email 索引结构

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/134583875561de914991fc2e192cf842-1584367389802.jpg)

图 2 email(6) 索引结构

从图中你可以看到，由于 email(6) 这个索引结构中每个邮箱字段都只取前 6 个字节（即：zhangs），所以占用的空间会更小，这就是使用前缀索引的优势。

但，这同时带来的损失是，可能会增加额外的记录扫描次数。

接下来，我们再看看下面这个语句，在这两个索引定义下分别是怎么执行的。

```csharp
select id,name,email from SUser where email='zhangssxyz@xxx.com';
```

**如果使用的是 index1**（即 email 整个字符串的索引结构），执行顺序是这样的：

1. 从 index1 索引树找到满足索引值是’zhangssxyz@xxx.com’的这条记录，取得 ID2 的值；
2. 到主键上查到主键值是 ID2 的行，判断 email 的值是正确的，将这行记录加入结果集；
3. 取 index1 索引树上刚刚查到的位置的下一条记录，发现已经不满足 email='zhangssxyz@xxx.com’的条件了，循环结束。

这个过程中，只需要回主键索引取一次数据，所以系统认为只扫描了一行。

**如果使用的是 index2**（即 email(6) 索引结构），执行顺序是这样的：

1. 从 index2 索引树找到满足索引值是’zhangs’的记录，找到的第一个是 ID1；
2. 到主键上查到主键值是 ID1 的行，判断出 email 的值不是’zhangssxyz@xxx.com’，这行记录丢弃；
3. 取 index2 上刚刚查到的位置的下一条记录，发现仍然是’zhangs’，取出 ID2，再到 ID 索引上取整行然后判断，这次值对了，将这行记录加入结果集；
4. 重复上一步，直到在 idxe2 上取到的值不是’zhangs’时，循环结束。

在这个过程中，要回主键索引取 4 次数据，也就是扫描了 4 行。

通过这个对比，你很容易就可以发现，使用前缀索引后，可能会导致查询语句读数据的次数变多。

但是，对于这个查询语句来说，如果你定义的 index2 不是 email(6) 而是 email(7），也就是说取 email 字段的前 7 个字节来构建索引的话，即满足前缀’zhangss’的记录只有一个，也能够直接查到 ID2，只扫描一行就结束了。

也就是说**使用前缀索引，定义好长度，就可以做到既节省空间，又不用额外增加太多的查询成本。**

于是，你就有个问题：当要给字符串创建前缀索引时，有什么方法能够确定我应该使用多长的前缀呢？

实际上，我们在建立索引时关注的是区分度，区分度越高越好。因为区分度越高，意味着重复的键值越少。因此，我们可以通过统计索引上有多少个不同的值来判断要使用多长的前缀。

首先，你可以使用下面这个语句，算出这个列上有多少个不同的值：

```csharp
mysql> select count(distinct email) as L from SUser;
```

然后，依次选取不同长度的前缀来看这个值，比如我们要看一下 4~7 个字节的前缀索引，可以用这个语句：

```sql
mysql> select 
  count(distinct left(email,4)）as L4,
  count(distinct left(email,5)）as L5,
  count(distinct left(email,6)）as L6,
  count(distinct left(email,7)）as L7,
from SUser;
```

当然，使用前缀索引很可能会损失区分度，所以你需要预先设定一个可以接受的损失比例，比如 5%。然后，在返回的 L4~L7 中，找出不小于 L * 95% 的值，假设这里 L6、L7 都满足，你就可以选择前缀长度为 6。

#### 前缀索引对覆盖索引的影响

前面我们说了使用前缀索引可能会增加扫描行数，这会影响到性能。其实，前缀索引的影响不止如此，我们再看一下另外一个场景。

你先来看看这个 SQL 语句：

```csharp
select id,email from SUser where email='zhangssxyz@xxx.com';
```

与前面例子中的 SQL 语句

```csharp
select id,name,email from SUser where email='zhangssxyz@xxx.com';
```

相比，这个语句只要求返回 id 和 email 字段。

所以，如果使用 index1（即 email 整个字符串的索引结构）的话，可以利用覆盖索引，从 index1  查到结果后直接就返回了，不需要回到 ID 索引再去查一次。而如果使用 index2（即 email(6) 索引结构）的话，就不得不回到 ID  索引再去判断 email 字段的值。

即使你将 index2 的定义修改为 email(18) 的前缀索引，这时候虽然 index2 已经包含了所有的信息，但 InnoDB 还是要回到 id 索引再查一下，因为系统并不确定前缀索引的定义是否截断了完整信息。

也就是说，使用前缀索引就用不上覆盖索引对查询性能的优化了，这也是你在选择是否使用前缀索引时需要考虑的一个因素。

#### 其他方式

对于类似于邮箱这样的字段来说，使用前缀索引的效果可能还不错。但是，遇到前缀的区分度不够好的情况时，我们要怎么办呢？

比如，我们国家的身份证号，一共 18 位，其中前 6 位是地址码，所以同一个县的人的身份证号前 6 位一般会是相同的。

假设你维护的数据库是一个市的公民信息系统，这时候如果对身份证号做长度为 6 的前缀索引的话，这个索引的区分度就非常低了。

按照我们前面说的方法，可能你需要创建长度为 12 以上的前缀索引，才能够满足区分度要求。

但是，索引选取的越长，占用的磁盘空间就越大，相同的数据页能放下的索引值就越少，搜索的效率也就会越低。

那么，如果我们能够确定业务需求里面只有按照身份证进行等值查询的需求，还有没有别的处理方法呢？这种方法，既可以占用更小的空间，也能达到相同的查询效率。

答案是，有的。

**第一种方式是使用倒序存储。**如果你存储身份证号的时候把它倒过来存，每次查询的时候，你可以这么写：

```csharp
mysql> select field_list from t where id_card = reverse('input_id_card_string');
```

由于身份证号的最后 6 位没有地址码这样的重复逻辑，所以最后这 6 位很可能就提供了足够的区分度。当然了，实践中你不要忘记使用 count(distinct) 方法去做个验证。

**第二种方式是使用 hash 字段。**你可以在表上再创建一个整数字段，来保存身份证的校验码，同时在这个字段上创建索引。

```sql
mysql> alter table t add id_card_crc int unsigned, add index(id_card_crc);
```

然后每次插入新记录的时候，都同时用 crc32()  这个函数得到校验码填到这个新字段。由于校验码可能存在冲突，也就是说两个不同的身份证号通过 crc32()  函数得到的结果可能是相同的，所以你的查询语句 where 部分要判断 id_card 的值是否精确相同。

```csharp
mysql> select field_list from t where id_card_crc=crc32('input_id_card_string') and id_card='input_id_card_string'
```

这样，索引的长度变成了 4 个字节，比原来小了很多。

接下来，我们再一起看看**使用倒序存储和使用 hash 字段这两种方法的异同点。**

首先，它们的相同点是，都不支持范围查询。倒序存储的字段上创建的索引是按照倒序字符串的方式排序的，已经没有办法利用索引方式查出身份证号码在 [ID_X, ID_Y] 的所有市民了。同样地，hash 字段的方式也只能支持等值查询。

它们的区别，主要体现在以下三个方面：

1. 从占用的额外空间来看，倒序存储方式在主键索引上，不会消耗额外的存储空间，而 hash 字段方法需要增加一个字段。当然，倒序存储方式使用 4 个字节的前缀长度应该是不够的，如果再长一点，这个消耗跟额外这个 hash 字段也差不多抵消了。
2. 在 CPU 消耗方面，倒序方式每次写和读的时候，都需要额外调用一次 reverse 函数，而 hash 字段的方式需要额外调用一次 crc32() 函数。如果只从这两个函数的计算复杂度来看的话，reverse 函数额外消耗的 CPU 资源会更小些。
3. 从查询效率上看，使用 hash 字段方式的查询性能相对更稳定一些。因为 crc32 算出来的值虽然有冲突的概率，但是概率非常小，可以认为每次查询的平均扫描行数接近 1。而倒序存储方式毕竟还是用的前缀索引的方式，也就是说还是会增加扫描行数。

#### 小结

在今天这篇文章中，我跟你聊了聊字符串字段创建索引的场景。我们来回顾一下，你可以使用的方式有：

1. 直接创建完整索引，这样可能比较占用空间；
2. 创建前缀索引，节省空间，但会增加查询扫描次数，并且不能使用覆盖索引；
3. 倒序存储，再创建前缀索引，用于绕过字符串本身前缀的区分度不够的问题；
4. 创建 hash 字段索引，查询性能稳定，有额外的存储和计算消耗，跟第三种方式一样，都不支持范围扫描。

在实际应用中，你要根据业务字段的特点选择使用哪种方式。

好了，又到了最后的问题时间。

如果你在维护一个学校的学生信息数据库，学生登录名的统一格式是”学号 @gmail.com", 而学号的规则是：十五位的数字，其中前三位是所在城市编号、第四到第六位是学校编号、第七位到第十位是入学年份、最后五位是顺序编号。

系统登录的时候都需要学生输入登录名和密码，验证正确后才能继续使用系统。就只考虑登录验证这个行为的话，你会怎么设计这个登录名的索引呢？

你可以把你的分析思路和设计结果写在留言区里，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

上篇文章中的第一个例子，评论区有几位同学说没有复现，大家要检查一下隔离级别是不是 RR（Repeatable Read，可重复读），创建的表 t 是不是 InnoDB 引擎。我把复现过程做成了一个视频，供你参考。

在上一篇文章最后，我给你留的问题是，为什么经过这个操作序列，explain 的结果就不对了？这里，我来为你分析一下原因。

delete 语句删掉了所有的数据，然后再通过 call idata() 插入了 10 万行数据，看上去是覆盖了原来的 10 万行。

但是，session A 开启了事务并没有提交，所以之前插入的 10 万行数据是不能删除的。这样，之前的数据每一行数据都有两个版本，旧版本是 delete 之前的数据，新版本是标记为 deleted 的数据。

这样，索引 a 上的数据其实就有两份。

然后你会说，不对啊，主键上的数据也不能删，那没有使用 force index 的语句，使用 explain 命令看到的扫描行数为什么还是 100000 左右？（潜台词，如果这个也翻倍，也许优化器还会认为选字段 a 作为索引更合适）

是的，不过这个是主键，主键是直接按照表的行数来估计的。而表的行数，优化器直接用的是 show table status 的值。

这个值的计算方法，我会在后面有文章为你详细讲解。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/e0e4c8381f3feae4d87958470760d367-1584367389807.png)评论区留言点赞板：

> @斜面镜子 Bill 的评论最接近答案； @某、人 做了两个很不错的对照试验； @ye7zi  等几位同学很认真的验证，赞态度。大家的机器如果 IO 能力比较差的话，做这个验证的时候，可以把  innodb_flush_log_at_trx_commit 和 sync_binlog 都设置成 0。



### 16 “order by”是怎么工作的？

在你开发应用的时候，一定会经常碰到需要根据指定的字段排序来显示结果的需求。还是以我们前面举例用过的市民表为例，假设你要查询城市是“杭州”的所有人名字，并且按照姓名排序返回前 1000 个人的姓名、年龄。

假设这个表的部分定义是这样的：

```r
CREATE TABLE `t` (
  `id` int(11) NOT NULL,
  `city` varchar(16) NOT NULL,
  `name` varchar(16) NOT NULL,
  `age` int(11) NOT NULL,
  `addr` varchar(128) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `city` (`city`)
) ENGINE=InnoDB;
```

这时，你的 SQL 语句可以这么写：

```csharp
select city,name,age from t where city='杭州' order by name limit 1000  ;
```

这个语句看上去逻辑很清晰，但是你了解它的执行流程吗？今天，我就和你聊聊这个语句是怎么执行的，以及有什么参数会影响执行的行为。

#### 全字段排序

前面我们介绍过索引，所以你现在就很清楚了，为避免全表扫描，我们需要在 city 字段加上索引。

在 city 字段上创建索引之后，我们用 explain 命令来看看这个语句的执行情况。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/826579b63225def812330ef6c344a303-1584367390630.png)

图 1 使用 explain 命令查看语句的执行情况

Extra 这个字段中的“Using filesort”表示的就是需要排序，MySQL 会给每个线程分配一块内存用于排序，称为 sort_buffer。

为了说明这个 SQL 查询语句的执行过程，我们先来看一下 city 这个索引的示意图。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/5334cca9118be14bde95ec94b02f0a3e-1584367390633.png)

图 2 city 字段的索引示意图

从图中可以看到，满足 city='杭州’条件的行，是从 ID_X 到 ID_(X+N) 的这些记录。

通常情况下，这个语句执行流程如下所示 ：

1. 初始化 sort_buffer，确定放入 name、city、age 这三个字段；
2. 从索引 city 找到第一个满足 city='杭州’条件的主键 id，也就是图中的 ID_X；
3. 到主键 id 索引取出整行，取 name、city、age 三个字段的值，存入 sort_buffer 中；
4. 从索引 city 取下一个记录的主键 id；
5. 重复步骤 3、4 直到 city 的值不满足查询条件为止，对应的主键 id 也就是图中的 ID_Y；
6. 对 sort_buffer 中的数据按照字段 name 做快速排序；
7. 按照排序结果取前 1000 行返回给客户端。

我们暂且把这个排序过程，称为全字段排序，执行流程的示意图如下所示，下一篇文章中我们还会用到这个排序。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/6c821828cddf46670f9d56e126e3e772-1584367392861.jpg)

图 3 全字段排序

图中“按 name 排序”这个动作，可能在内存中完成，也可能需要使用外部排序，这取决于排序所需的内存和参数 sort_buffer_size。

sort_buffer_size，就是 MySQL 为排序开辟的内存（sort_buffer）的大小。如果要排序的数据量小于 sort_buffer_size，排序就在内存中完成。但如果排序数据量太大，内存放不下，则不得不利用磁盘临时文件辅助排序。

你可以用下面介绍的方法，来确定一个排序语句是否使用了临时文件。

```sql
/* 打开 optimizer_trace，只对本线程有效 */
SET optimizer_trace='enabled=on';  
/* @a 保存 Innodb_rows_read 的初始值 */
select VARIABLE_VALUE into @a from  performance_schema.session_status where variable_name = 'Innodb_rows_read'; 
/* 执行语句 */
select city, name,age from t where city='杭州' order by name limit 1000;  
/* 查看 OPTIMIZER_TRACE 输出 */
SELECT * FROM `information_schema`.`OPTIMIZER_TRACE`\G 
/* @b 保存 Innodb_rows_read 的当前值 */
select VARIABLE_VALUE into @b from performance_schema.session_status where variable_name = 'Innodb_rows_read'; 
/* 计算 Innodb_rows_read 差值 */
select @b-@a;
```

这个方法是通过查看 OPTIMIZER_TRACE 的结果来确认的，你可以从 number_of_tmp_files 中看到是否使用了临时文件。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/89baf99cdeefe90a22370e1d6f5e6495-1584367392864.png)

图 4 全排序的 OPTIMIZER_TRACE 部分结果

number_of_tmp_files 表示的是，排序过程中使用的临时文件数。你一定奇怪，为什么需要 12 个文件？内存放不下时，就需要使用外部排序，外部排序一般使用归并排序算法。可以这么简单理解，**MySQL 将需要排序的数据分成 12 份，每一份单独排序后存在这些临时文件中。然后把这 12 个有序文件再合并成一个有序的大文件。**

如果 sort_buffer_size 超过了需要排序的数据量的大小，number_of_tmp_files 就是 0，表示排序可以直接在内存中完成。

否则就需要放在临时文件中排序。sort_buffer_size 越小，需要分成的份数越多，number_of_tmp_files 的值就越大。

接下来，我再和你解释一下图 4 中其他两个值的意思。

我们的示例表中有 4000 条满足 city='杭州’的记录，所以你可以看到 examined_rows=4000，表示参与排序的行数是 4000 行。

sort_mode 里面的 packed_additional_fields 的意思是，排序过程对字符串做了“紧凑”处理。即使 name 字段的定义是 varchar(16)，在排序过程中还是要按照实际长度来分配空间的。

同时，最后一个查询语句 select @b-@a 的返回结果是 4000，表示整个执行过程只扫描了 4000 行。

这里需要注意的是，为了避免对结论造成干扰，我把 internal_tmp_disk_storage_engine 设置成 MyISAM。否则，select @b-@a 的结果会显示为 4001。

这是因为查询 OPTIMIZER_TRACE 这个表时，需要用到临时表，而  internal_tmp_disk_storage_engine 的默认值是 InnoDB。如果使用的是 InnoDB  引擎的话，把数据从临时表取出来的时候，会让 Innodb_rows_read 的值加 1。

#### rowid 排序

在上面这个算法过程里面，只对原表的数据读了一遍，剩下的操作都是在 sort_buffer  和临时文件中执行的。但这个算法有一个问题，就是如果查询要返回的字段很多的话，那么 sort_buffer  里面要放的字段数太多，这样内存里能够同时放下的行数很少，要分成很多个临时文件，排序的性能会很差。

所以如果单行很大，这个方法效率不够好。

那么，**如果 MySQL 认为排序的单行长度太大会怎么做呢？**

接下来，我来修改一个参数，让 MySQL 采用另外一种算法。

```java
SET max_length_for_sort_data = 16;
```

max_length_for_sort_data，是 MySQL 中专门控制用于排序的行数据的长度的一个参数。它的意思是，如果单行的长度超过这个值，MySQL 就认为单行太大，要换一个算法。

city、name、age 这三个字段的定义总长度是 36，我把 max_length_for_sort_data 设置为 16，我们再来看看计算过程有什么改变。

新的算法放入 sort_buffer 的字段，只有要排序的列（即 name 字段）和主键 id。

但这时，排序的结果就因为少了 city 和 age 字段的值，不能直接返回了，整个执行流程就变成如下所示的样子：

1. 初始化 sort_buffer，确定放入两个字段，即 name 和 id；
2. 从索引 city 找到第一个满足 city='杭州’条件的主键 id，也就是图中的 ID_X；
3. 到主键 id 索引取出整行，取 name、id 这两个字段，存入 sort_buffer 中；
4. 从索引 city 取下一个记录的主键 id；
5. 重复步骤 3、4 直到不满足 city='杭州’条件为止，也就是图中的 ID_Y；
6. 对 sort_buffer 中的数据按照字段 name 进行排序；
7. 遍历排序结果，取前 1000 行，并按照 id 的值回到原表中取出 city、name 和 age 三个字段返回给客户端。

这个执行流程的示意图如下，我把它称为 rowid 排序。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/dc92b67721171206a302eb679c83e86d-1584367392864.jpg)

图 5 rowid 排序

对比图 3 的全字段排序流程图你会发现，rowid 排序多访问了一次表 t 的主键索引，就是步骤 7。

需要说明的是，最后的“结果集”是一个逻辑概念，实际上 MySQL 服务端从排序后的 sort_buffer 中依次取出 id，然后到原表查到 city、name 和 age 这三个字段的结果，不需要在服务端再耗费内存存储结果，是直接返回给客户端的。

根据这个说明过程和图示，你可以想一下，这个时候执行 select @b-@a，结果会是多少呢？

现在，我们就来看看结果有什么不同。

首先，图中的 examined_rows 的值还是 4000，表示用于排序的数据是 4000 行。但是 select @b-@a 这个语句的值变成 5000 了。

因为这时候除了排序过程外，在排序完成后，还要根据 id 去原表取值。由于语句是 limit 1000，因此会多读 1000 行。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/27f164804d1a4689718291be5d10f89b-1584367392865.png)

图 6 rowid 排序的 OPTIMIZER_TRACE 部分输出

从 OPTIMIZER_TRACE 的结果中，你还能看到另外两个信息也变了。

- sort_mode 变成了 <sort_key, rowid>，表示参与排序的只有 name 和 id 这两个字段。
- number_of_tmp_files 变成 10 了，是因为这时候参与排序的行数虽然仍然是 4000 行，但是每一行都变小了，因此需要排序的总数据量就变小了，需要的临时文件也相应地变少了。

#### 全字段排序 VS rowid 排序

我们来分析一下，从这两个执行流程里，还能得出什么结论。

如果 MySQL 实在是担心排序内存太小，会影响排序效率，才会采用 rowid 排序算法，这样排序过程中一次可以排序更多行，但是需要再回到原表去取数据。

如果 MySQL 认为内存足够大，会优先选择全字段排序，把需要的字段都放到 sort_buffer 中，这样排序后就会直接从内存里面返回查询结果了，不用再回到原表去取数据。

这也就体现了 MySQL 的一个设计思想：**如果内存够，就要多利用内存，尽量减少磁盘访问。**

对于 InnoDB 表来说，rowid 排序会要求回表多造成磁盘读，因此不会被优先选择。

这个结论看上去有点废话的感觉，但是你要记住它，下一篇文章我们就会用到。

看到这里，你就了解了，MySQL 做排序是一个成本比较高的操作。那么你会问，是不是所有的 order by 都需要排序操作呢？如果不排序就能得到正确的结果，那对系统的消耗会小很多，语句的执行时间也会变得更短。

其实，并不是所有的 order by 语句，都需要排序操作的。从上面分析的执行过程，我们可以看到，MySQL 之所以需要生成临时表，并且在临时表上做排序操作，**其原因是原来的数据都是无序的。**

你可以设想下，如果能够保证从 city 这个索引上取出来的行，天然就是按照 name 递增排序的话，是不是就可以不用再排序了呢？

确实是这样的。

所以，我们可以在这个市民表上创建一个 city 和 name 的联合索引，对应的 SQL 语句是：

```sql
alter table t add index city_user(city, name);
```

作为与 city 索引的对比，我们来看看这个索引的示意图。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/f980201372b676893647fb17fac4e2bf-1584367392865.png)

图 7 city 和 name 联合索引示意图

在这个索引里面，我们依然可以用树搜索的方式定位到第一个满足 city='杭州’的记录，并且额外确保了，接下来按顺序取“下一条记录”的遍历过程中，只要 city 的值是杭州，name 的值就一定是有序的。

这样整个查询过程的流程就变成了：

1. 从索引 (city,name) 找到第一个满足 city='杭州’条件的主键 id；
2. 到主键 id 索引取出整行，取 name、city、age 三个字段的值，作为结果集的一部分直接返回；
3. 从索引 (city,name) 取下一个记录主键 id；
4. 重复步骤 2、3，直到查到第 1000 条记录，或者是不满足 city='杭州’条件时循环结束。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/3f590c3a14f9236f2d8e1e2cb9686692-1584367392865.jpg)

图 8 引入 (city,name) 联合索引后，查询语句的执行计划

可以看到，这个查询过程不需要临时表，也不需要排序。接下来，我们用 explain 的结果来印证一下。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/fc53de303811ba3c46d344595743358a-1584367392865.png)

图 9 引入 (city,name) 联合索引后，查询语句的执行计划

从图中可以看到，Extra 字段中没有 Using filesort 了，也就是不需要排序了。而且由于 (city,name)  这个联合索引本身有序，所以这个查询也不用把 4000 行全都读一遍，只要找到满足条件的前 1000  条记录就可以退出了。也就是说，在我们这个例子里，只需要扫描 1000 次。

既然说到这里了，我们再往前讨论，**这个语句的执行流程有没有可能进一步简化呢？**不知道你还记不记得，我在第 5 篇文章[《 深入浅出索引（下）》]中，和你介绍的覆盖索引。

这里我们可以再稍微复习一下。**覆盖索引是指，索引上的信息足够满足查询请求，不需要再回到主键索引上去取数据。**

按照覆盖索引的概念，我们可以再优化一下这个查询语句的执行流程。

针对这个查询，我们可以创建一个 city、name 和 age 的联合索引，对应的 SQL 语句就是：

```sql
alter table t add index city_user_age(city, name, age);
```

这时，对于 city 字段的值相同的行来说，还是按照 name 字段的值递增排序的，此时的查询语句也就不再需要排序了。这样整个查询语句的执行流程就变成了：

1. 从索引 (city,name,age) 找到第一个满足 city='杭州’条件的记录，取出其中的 city、name 和 age 这三个字段的值，作为结果集的一部分直接返回；
2. 从索引 (city,name,age) 取下一个记录，同样取出这三个字段的值，作为结果集的一部分直接返回；
3. 重复执行步骤 2，直到查到第 1000 条记录，或者是不满足 city='杭州’条件时循环结束。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/df4b8e445a59c53df1f2e0f115f02cd6-1584367392865.jpg)

图 10 引入 (city,name,age) 联合索引后，查询语句的执行流程

然后，我们再来看看 explain 的结果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/9e40b7b8f0e3f81126a9171cc22e3423-1584367392866.png)

图 11 引入 (city,name,age) 联合索引后，查询语句的执行计划

可以看到，Extra 字段里面多了“Using index”，表示的就是使用了覆盖索引，性能上会快很多。

当然，这里并不是说要为了每个查询能用上覆盖索引，就要把语句中涉及的字段都建上联合索引，毕竟索引还是有维护代价的。这是一个需要权衡的决定。

#### 小结

今天这篇文章，我和你介绍了 MySQL 里面 order by 语句的几种算法流程。

在开发系统的时候，你总是不可避免地会使用到 order by 语句。你心里要清楚每个语句的排序逻辑是怎么实现的，还要能够分析出在最坏情况下，每个语句的执行对系统资源的消耗，这样才能做到下笔如有神，不犯低级错误。

最后，我给你留下一个思考题吧。

假设你的表里面已经有了 city_name(city, name) 这个联合索引，然后你要查杭州和苏州两个城市中所有的市民的姓名，并且按名字排序，显示前 100 条记录。如果 SQL 查询语句是这么写的 ：

```csharp
mysql> select * from t where city in ('杭州'," 苏州 ") order by name limit 100;
```

那么，这个语句执行的时候会有排序过程吗，为什么？

如果业务端代码由你来开发，需要实现一个在数据库端不需要排序的方案，你会怎么实现呢？

进一步地，如果有分页需求，要显示第 101 页，也就是说语句最后要改成 “limit 10000,100”， 你的实现方法又会是什么呢？

你可以把你的思考和观点写在留言区里，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

上期的问题是，当 MySQL 去更新一行，但是要修改的值跟原来的值是相同的，这时候 MySQL 会真的去执行一次修改吗？还是看到值相同就直接返回呢？

这是第一次我们课后问题的三个选项都有同学选的，所以我要和你需要详细说明一下。

第一个选项是，MySQL 读出数据，发现值与原来相同，不更新，直接返回，执行结束。这里我们可以用一个锁实验来确认。

假设，当前表 t 里的值是 (1,2)。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/6d9d8837560d01b57d252c470157ea90-1584367392866.png)

图 12 锁验证方式

session B 的 update 语句被 blocked 了，加锁这个动作是 InnoDB 才能做的，所以排除选项 1。

第二个选项是，MySQL 调用了 InnoDB 引擎提供的接口，但是引擎发现值与原来相同，不更新，直接返回。有没有这种可能呢？这里我用一个可见性实验来确认。

假设当前表里的值是 (1,2)。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/441682b64a3f5dd50f35b12ca4b87c96-1584367392866.png)

图 13 可见性验证方式

session A 的第二个 select 语句是一致性读（快照读)，它是不能看见 session B 的更新的。

现在它返回的是 (1,3)，表示它看见了某个新的版本，这个版本只能是 session A 自己的 update 语句做更新的时候生成。（如果你对这个逻辑有疑惑的话，可以回顾下第 8 篇文章[《事务到底是隔离的还是不隔离的？》]中的相关内容）

所以，我们上期思考题的答案应该是选项 3，即：InnoDB 认真执行了“把这个值修改成 (1,2)"这个操作，该加锁的加锁，该更新的更新。

然后你会说，MySQL 怎么这么笨，就不会更新前判断一下值是不是相同吗？如果判断一下，不就不用浪费 InnoDB 操作，多去更新一次了？

其实 MySQL 是确认了的。只是在这个语句里面，MySQL 认为读出来的值，只有一个确定的 (id=1), 而要写的是 (a=3)，只从这两个信息是看不出来“不需要修改”的。

作为验证，你可以看一下下面这个例子。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/63dd6df32dacdb827d256e5acb9837c1-1584367392866.png)

图 14 可见性验证方式 -- 对照

**补充说明：**

上面我们的验证结果都是在 binlog_format=statement 格式下进行的。

@didiren 补充了一个 case， 如果是 binlog_format=row 并且 binlog_row_image=FULL 的时候，由于 MySQL 需要在 binlog 里面记录所有的字段，所以在读数据的时候就会把所有数据都读出来了。

根据上面说的规则，“既然读了数据，就会判断”， 因此在这时候，select * from t where id=1，结果就是“返回 (1,2)”。

同理，如果是 binlog_row_image=NOBLOB, 会读出除 blob 外的所有字段，在我们这个例子里，结果还是“返回 (1,2)”。

对应的代码如图 15 所示。这是 MySQL 5.6 版本引入的，在此之前我没有看过。所以，特此说明。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/d413b9235d56c62f9829750a68b06b89-1584367392866.png)

图 15 binlog_row_image=FULL 读字段逻辑

类似的，@mahonebags 同学提到了 timestamp 字段的问题。结论是：如果表中有 timestamp 字段而且设置了自动更新的话，那么更新“别的字段”的时候，MySQL 会读入所有涉及的字段，这样通过判断，就会发现不需要修改。

这两个点我会在后面讲更新性能的文章中再展开。

评论区留言点赞板：

> @Gavin 、@melon、@阿建 等同学提到了锁验证法； @郭江伟 同学提到了两个点，都非常好，有去实际验证。结论是这样的：  第一，hexdump 看出来没改应该是 WAL 机制生效了，要过一会儿，或者把库 shutdown 看看。 第二，binlog 没写是  MySQL Server 层知道行的值没变，所以故意不写的，这个是在 row 格式下的策略。你可以把 binlog_format 改成  statement 再验证下。



### 20 幻读是什么，幻读有什么问题？

在上一篇文章最后，我给你留了一个关于加锁规则的问题。今天，我们就从这个问题说起吧。

为了便于说明问题，这一篇文章，我们就先使用一个小一点儿的表。建表和初始化语句如下（为了便于本期的例子说明，我把上篇文章中用到的表结构做了点儿修改）：

```sql
CREATE TABLE `t` (
  `id` int(11) NOT NULL,
  `c` int(11) DEFAULT NULL,
  `d` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `c` (`c`)
) ENGINE=InnoDB; 
insert into t values(0,0,0),(5,5,5),
(10,10,10),(15,15,15),(20,20,20),(25,25,25);
```

这个表除了主键 id 外，还有一个索引 c，初始化语句在表中插入了 6 行数据。

上期我留给你的问题是，下面的语句序列，是怎么加锁的，加的锁又是什么时候释放的呢？

```sql
begin;
select * from t where d=5 for update;
commit;
```

比较好理解的是，这个语句会命中 d=5 的这一行，对应的主键 id=5，因此在 select 语句执行完成后，id=5 这一行会加一个写锁，而且由于两阶段锁协议，这个写锁会在执行 commit 语句的时候释放。

由于字段 d 上没有索引，因此这条查询语句会做全表扫描。那么，其他被扫描到的，但是不满足条件的 5 行记录上，会不会被加锁呢？

我们知道，InnoDB 的默认事务隔离级别是可重复读，所以本文接下来没有特殊说明的部分，都是设定在可重复读隔离级别下。

#### 幻读是什么？

现在，我们就来分析一下，如果只在 id=5 这一行加锁，而其他行的不加锁的话，会怎么样。

下面先来看一下这个场景（注意：这是我假设的一个场景）：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/5bc506e5884d21844126d26bbe6fa68b-1584367394523.png)

图 1 假设只在 id=5 这一行加行锁

可以看到，session A 里执行了三次查询，分别是 Q1、Q2 和 Q3。它们的 SQL 语句相同，都是 select * from t where d=5 for update。这个语句的意思你应该很清楚了，查所有 d=5  的行，而且使用的是当前读，并且加上写锁。现在，我们来看一下这三条 SQL 语句，分别会返回什么结果。

1. Q1 只返回 id=5 这一行；
2. 在 T2 时刻，session B 把 id=0 这一行的 d 值改成了 5，因此 T3 时刻 Q2 查出来的是 id=0 和 id=5 这两行；
3. 在 T4 时刻，session C 又插入一行（1,1,5），因此 T5 时刻 Q3 查出来的是 id=0、id=1 和 id=5 的这三行。

其中，Q3 读到 id=1 这一行的现象，被称为“幻读”。也就是说，幻读指的是一个事务在前后两次查询同一个范围的时候，后一次查询看到了前一次查询没有看到的行。

这里，我需要对“幻读”做一个说明：

1. 在可重复读隔离级别下，普通的查询是快照读，是不会看到别的事务插入的数据的。因此，幻读在“当前读”下才会出现。
2. 上面 session B 的修改结果，被 session A 之后的 select 语句用“当前读”看到，不能称为幻读。幻读仅专指“新插入的行”。

如果只从第 8 篇文章[《事务到底是隔离的还是不隔离的？》]我们学到的事务可见性规则来分析的话，上面这三条 SQL 语句的返回结果都没有问题。

因为这三个查询都是加了 for update，都是当前读。而当前读的规则，就是要能读到所有已经提交的记录的最新值。并且，session B 和 sessionC 的两条语句，执行后就会提交，所以 Q2 和 Q3  就是应该看到这两个事务的操作效果，而且也看到了，这跟事务的可见性规则并不矛盾。

但是，这是不是真的没问题呢？

不，这里还真就有问题。

#### 幻读有什么问题？

**首先是语义上的。**session A 在 T1 时刻就声明了，“我要把所有 d=5 的行锁住，不准别的事务进行读写操作”。而实际上，这个语义被破坏了。

如果现在这样看感觉还不明显的话，我再往 session B 和 session C 里面分别加一条 SQL 语句，你再看看会出现什么现象。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/7a9ffa90ac3cc78db6a51ff9b9075607-1584367394532.png)

图 2 假设只在 id=5 这一行加行锁 -- 语义被破坏

session B 的第二条语句 update t set c=5 where id=0，语义是“我把 id=0、d=5 这一行的 c 值，改成了 5”。

由于在 T1 时刻，session A 还只是给 id=5 这一行加了行锁， 并没有给 id=0 这行加上锁。因此，session B 在 T2 时刻，是可以执行这两条 update 语句的。这样，就破坏了 session A 里 Q1 语句要锁住所有 d=5 的行的加锁声明。

session C 也是一样的道理，对 id=1 这一行的修改，也是破坏了 Q1 的加锁声明。

**其次，是数据一致性的问题。**

我们知道，锁的设计是为了保证数据的一致性。而这个一致性，不止是数据库内部数据状态在此刻的一致性，还包含了数据和日志在逻辑上的一致性。

为了说明这个问题，我给 session A 在 T1 时刻再加一个更新语句，即：update t set d=100 where d=5。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/dcea7845ff0bdbee2622bf3c67d31d92-1584367394539.png)

图 3 假设只在 id=5 这一行加行锁 -- 数据一致性问题

update 的加锁语义和 select …for update 是一致的，所以这时候加上这条 update 语句也很合理。session A 声明说“要给 d=5 的语句加上锁”，就是为了要更新数据，新加的这条 update 语句就是把它认为加上了锁的这一行的 d 值修改成了  100。

现在，我们来分析一下图 3 执行完成后，数据库里会是什么结果。

1. 经过 T1 时刻，id=5 这一行变成 (5,5,100)，当然这个结果最终是在 T6 时刻正式提交的 ;
2. 经过 T2 时刻，id=0 这一行变成 (0,5,5);
3. 经过 T4 时刻，表里面多了一行 (1,5,5);
4. 其他行跟这个执行序列无关，保持不变。

这样看，这些数据也没啥问题，但是我们再来看看这时候 binlog 里面的内容。

1. T2 时刻，session B 事务提交，写入了两条语句；
2. T4 时刻，session C 事务提交，写入了两条语句；
3. T6 时刻，session A 事务提交，写入了 update t set d=100 where d=5 这条语句。

我统一放到一起的话，就是这样的：

```sql
update t set d=5 where id=0; /*(0,0,5)*/
update t set c=5 where id=0; /*(0,5,5)*/ 
insert into t values(1,1,5); /*(1,1,5)*/
update t set c=5 where id=1; /*(1,5,5)*/ 
update t set d=100 where d=5;/* 所有 d=5 的行，d 改成 100*/
```

好，你应该看出问题了。这个语句序列，不论是拿到备库去执行，还是以后用 binlog 来克隆一个库，这三行的结果，都变成了 (0,5,100)、(1,5,100) 和 (5,5,100)。

也就是说，id=0 和 id=1 这两行，发生了数据不一致。这个问题很严重，是不行的。

到这里，我们再回顾一下，**这个数据不一致到底是怎么引入的？**

我们分析一下可以知道，这是我们假设“select * from t where d=5 for update 这条语句只给 d=5 这一行，也就是 id=5 的这一行加锁”导致的。

所以我们认为，上面的设定不合理，要改。

那怎么改呢？我们把扫描过程中碰到的行，也都加上写锁，再来看看执行效果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/34ad6478281709da833856084a1e3447-1584367394550.png)

图 4 假设扫描到的行都被加上了行锁

由于 session A 把所有的行都加了写锁，所以 session B 在执行第一个 update 语句的时候就被锁住了。需要等到 T6 时刻 session A 提交以后，session B 才能继续执行。

这样对于 id=0 这一行，在数据库里的最终结果还是 (0,5,5)。在 binlog 里面，执行序列是这样的：

```sql
insert into t values(1,1,5); /*(1,1,5)*/
update t set c=5 where id=1; /*(1,5,5)*/ 
update t set d=100 where d=5;/* 所有 d=5 的行，d 改成 100*/ 
update t set d=5 where id=0; /*(0,0,5)*/
update t set c=5 where id=0; /*(0,5,5)*/
```

可以看到，按照日志顺序执行，id=0 这一行的最终结果也是 (0,5,5)。所以，id=0 这一行的问题解决了。

但同时你也可以看到，id=1 这一行，在数据库里面的结果是 (1,5,5)，而根据 binlog 的执行结果是  (1,5,100)，也就是说幻读的问题还是没有解决。为什么我们已经这么“凶残”地，把所有的记录都上了锁，还是阻止不了 id=1  这一行的插入和更新呢？

原因很简单。在 T3 时刻，我们给所有行加锁的时候，id=1 这一行还不存在，不存在也就加不上锁。

**也就是说，即使把所有的记录都加上锁，还是阻止不了新插入的记录，**这也是为什么“幻读”会被单独拿出来解决的原因。

到这里，其实我们刚说明完文章的标题 ：幻读的定义和幻读有什么问题。

接下来，我们再看看 InnoDB 怎么解决幻读的问题。

#### 如何解决幻读？

现在你知道了，产生幻读的原因是，行锁只能锁住行，但是新插入记录这个动作，要更新的是记录之间的“间隙”。因此，为了解决幻读问题，InnoDB 只好引入新的锁，也就是间隙锁 (Gap Lock)。

顾名思义，间隙锁，锁的就是两个值之间的空隙。比如文章开头的表 t，初始化插入了 6 个记录，这就产生了 7 个间隙。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/e7f7ca0d3dab2f48c588d714ee3ac861-1584367394558.png)

图 5 表 t 主键索引上的行锁和间隙锁

这样，当你执行 select * from t where d=5 for update 的时候，就不止是给数据库中已有的 6 个记录加上了行锁，还同时加了 7 个间隙锁。这样就确保了无法再插入新的记录。

也就是说这时候，在一行行扫描的过程中，不仅将给行加上了行锁，还给行两边的空隙，也加上了间隙锁。

现在你知道了，数据行是可以加上锁的实体，数据行之间的间隙，也是可以加上锁的实体。但是间隙锁跟我们之前碰到过的锁都不太一样。

比如行锁，分成读锁和写锁。下图就是这两种类型行锁的冲突关系。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/c435c765556c0f3735a6eda0779ff151-1584367394562.png)

图 6 两种行锁间的冲突关系

也就是说，跟行锁有冲突关系的是“另外一个行锁”。

但是间隙锁不一样，**跟间隙锁存在冲突关系的，是“往这个间隙中插入一个记录”这个操作。**间隙锁之间都不存在冲突关系。

这句话不太好理解，我给你举个例子：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/7c37732d936650f1cda7dbf27daf7498-1584367394590.png)

图 7 间隙锁之间不互锁

这里 session B 并不会被堵住。因为表 t 里并没有 c=7 这个记录，因此 session A 加的是间隙锁 (5,10)。而  session B 也是在这个间隙加的间隙锁。它们有共同的目标，即：保护这个间隙，不允许插入值。但，它们之间是不冲突的。

间隙锁和行锁合称 next-key lock，每个 next-key lock 是前开后闭区间。也就是说，我们的表 t 初始化以后，如果用 select * from t for update 要把整个表所有记录锁起来，就形成了 7 个 next-key lock，分别是  (-∞,0]、(0,5]、(5,10]、(10,15]、(15,20]、(20, 25]、(25, +supremum]。

> 备注：这篇文章中，如果没有特别说明，我们把间隙锁记为开区间，把 next-key lock 记为前开后闭区间。

你可能会问说，这个 supremum 从哪儿来的呢？

这是因为 +∞是开区间。实现上，InnoDB 给每个索引加了一个不存在的最大值 supremum，这样才符合我们前面说的“都是前开后闭区间”。

**间隙锁和 next-key lock 的引入，帮我们解决了幻读的问题，但同时也带来了一些“困扰”。**

在前面的文章中，就有同学提到了这个问题。我把他的问题转述一下，对应到我们这个例子的表来说，业务逻辑这样的：任意锁住一行，如果这一行不存在的话就插入，如果存在这一行就更新它的数据，代码如下：

```sql
begin;
select * from t where id=N for update; 
/* 如果行不存在 */
insert into t values(N,N,N);
/* 如果行存在 */
update t set d=N set id=N; 
commit;
```

可能你会说，这个不是 insert … on duplicate key update 就能解决吗？但其实在有多个唯一键的时候，这个方法是不能满足这位提问同学的需求的。至于为什么，我会在后面的文章中再展开说明。

现在，我们就只讨论这个逻辑。

这个同学碰到的现象是，这个逻辑一旦有并发，就会碰到死锁。你一定也觉得奇怪，这个逻辑每次操作前用 for update 锁起来，已经是最严格的模式了，怎么还会有死锁呢？

这里，我用两个 session 来模拟并发，并假设 N=9。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/df37bf0bb9f85ea59f0540e24eb6bcbe-1584367394594.png)

图 8 间隙锁导致的死锁

你看到了，其实都不需要用到后面的 update 语句，就已经形成死锁了。我们按语句执行顺序来分析一下：

1. session A 执行 select … for update 语句，由于 id=9 这一行并不存在，因此会加上间隙锁 (5,10);
2. session B 执行 select … for update 语句，同样会加上间隙锁 (5,10)，间隙锁之间不会冲突，因此这个语句可以执行成功；
3. session B 试图插入一行 (9,9,9)，被 session A 的间隙锁挡住了，只好进入等待；
4. session A 试图插入一行 (9,9,9)，被 session B 的间隙锁挡住了。

至此，两个 session 进入互相等待状态，形成死锁。当然，InnoDB 的死锁检测马上就发现了这对死锁关系，让 session A 的 insert 语句报错返回了。

你现在知道了，**间隙锁的引入，可能会导致同样的语句锁住更大的范围，这其实是影响了并发度的**。其实，这还只是一个简单的例子，在下一篇文章中我们还会碰到更多、更复杂的例子。

你可能会说，为了解决幻读的问题，我们引入了这么一大串内容，有没有更简单一点的处理方法呢。

我在文章一开始就说过，如果没有特别说明，今天和你分析的问题都是在可重复读隔离级别下的，间隙锁是在可重复读隔离级别下才会生效的。所以，你如果把隔离级别设置为读提交的话，就没有间隙锁了。但同时，你要解决可能出现的数据和日志不一致问题，需要把 binlog 格式设置为 row。这，也是现在不少公司使用的配置组合。

前面文章的评论区有同学留言说，他们公司就使用的是读提交隔离级别加 binlog_format=row 的组合。他曾问他们公司的 DBA 说，你为什么要这么配置。DBA 直接答复说，因为大家都这么用呀。

所以，这个同学在评论区就问说，这个配置到底合不合理。

关于这个问题本身的答案是，如果读提交隔离级别够用，也就是说，业务不需要可重复读的保证，这样考虑到读提交下操作数据的锁范围更小（没有间隙锁），这个选择是合理的。

但其实我想说的是，配置是否合理，跟业务场景有关，需要具体问题具体分析。

但是，如果 DBA 认为之所以这么用的原因是“大家都这么用”，那就有问题了，或者说，迟早会出问题。

比如说，大家都用读提交，可是逻辑备份的时候，mysqldump 为什么要把备份线程设置成可重复读呢？（这个我在前面的文章中已经解释过了，你可以再回顾下第 6 篇文章[《全局锁和表锁 ：给表加个字段怎么有这么多阻碍？》]的内容）

然后，在备份期间，备份线程用的是可重复读，而业务线程用的是读提交。同时存在两种事务隔离级别，会不会有问题？

进一步地，这两个不同的隔离级别现象有什么不一样的，关于我们的业务，“用读提交就够了”这个结论是怎么得到的？

如果业务开发和运维团队这些问题都没有弄清楚，那么“没问题”这个结论，本身就是有问题的。

#### 小结

今天我们从上一篇文章的课后问题说起，提到了全表扫描的加锁方式。我们发现即使给所有的行都加上行锁，仍然无法解决幻读问题，因此引入了间隙锁的概念。

我碰到过很多对数据库有一定了解的业务开发人员，他们在设计数据表结构和业务 SQL 语句的时候，对行锁有很准确的认识，但却很少考虑到间隙锁。最后的结果，就是生产库上会经常出现由于间隙锁导致的死锁现象。

行锁确实比较直观，判断规则也相对简单，间隙锁的引入会影响系统的并发度，也增加了锁分析的复杂度，但也有章可循。下一篇文章，我就会为你讲解 InnoDB 的加锁规则，帮你理顺这其中的“章法”。

作为对下一篇文章的预习，我给你留下一个思考题。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/0d796060073668ca169166a8903fbf3d-1584367394597.png)

图 9 事务进入锁等待状态

如果你之前没有了解过本篇文章的相关内容，一定觉得这三个语句简直是风马牛不相及。但实际上，这里 session B 和 session C 的 insert 语句都会进入锁等待状态。

你可以试着分析一下，出现这种情况的原因是什么？

这里需要说明的是，这其实是我在下一篇文章介绍加锁规则后才能回答的问题，是留给你作为预习的，其中 session C 被锁住这个分析是有点难度的。如果你没有分析出来，也不要气馁，我会在下一篇文章和你详细说明。

你也可以说说，你的线上 MySQL 配置的是什么隔离级别，为什么会这么配置？你有没有碰到什么场景，是必须使用可重复读隔离级别的呢？

你可以把你的碰到的场景和分析写在留言区里，我会在下一篇文章选取有趣的评论跟大家一起分享和分析。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

我们在本文的开头回答了上期问题。有同学的回答中还说明了读提交隔离级别下，在语句执行完成后，是只有行锁的。而且语句执行完成后，InnoDB 就会把不满足条件的行行锁去掉。

当然了，c=5 这一行的行锁，还是会等到 commit 的时候才释放的。

评论区留言点赞板：

> @薛畅 、@张永志同学给出了正确答案。而且提到了在读提交隔离级别下，是只有行锁的。 @帆帆帆帆帆帆帆帆、@欧阳成  对上期的例子做了验证，需要说明一下，需要在启动配置里面增加  performance_schema=on，才能用上这个功能，performance_schema 库里的表才有数据。



### 22 MySQL有哪些“饮鸩止渴”提高性能的方法？

不知道你在实际运维过程中有没有碰到这样的情景：业务高峰期，生产环境的 MySQL 压力太大，没法正常响应，需要短期内、临时性地提升一些性能。

我以前做业务护航的时候，就偶尔会碰上这种场景。用户的开发负责人说，不管你用什么方案，让业务先跑起来再说。

但，如果是无损方案的话，肯定不需要等到这个时候才上场。今天我们就来聊聊这些临时方案，并着重说一说它们可能存在的风险。

#### 短连接风暴

正常的短连接模式就是连接到数据库后，执行很少的 SQL 语句就断开，下次需要的时候再重连。如果使用的是短连接，在业务高峰期的时候，就可能出现连接数突然暴涨的情况。

我在第 1 篇文章[《基础架构：一条 SQL 查询语句是如何执行的？》]中说过，MySQL 建立连接的过程，成本是很高的。除了正常的网络连接三次握手外，还需要做登录权限判断和获得这个连接的数据读写权限。

在数据库压力比较小的时候，这些额外的成本并不明显。

但是，短连接模型存在一个风险，就是一旦数据库处理得慢一些，连接数就会暴涨。max_connections 参数，用来控制一个 MySQL  实例同时存在的连接数的上限，超过这个值，系统就会拒绝接下来的连接请求，并报错提示“Too many  connections”。对于被拒绝连接的请求来说，从业务角度看就是数据库不可用。

在机器负载比较高的时候，处理现有请求的时间变长，每个连接保持的时间也更长。这时，再有新建连接的话，就可能会超过 max_connections 的限制。

碰到这种情况时，一个比较自然的想法，就是调高 max_connections 的值。但这样做是有风险的。因为设计  max_connections 这个参数的目的是想保护  MySQL，如果我们把它改得太大，让更多的连接都可以进来，那么系统的负载可能会进一步加大，大量的资源耗费在权限验证等逻辑上，结果可能是适得其反，已经连接的线程拿不到 CPU 资源去执行业务的 SQL 请求。

那么这种情况下，你还有没有别的建议呢？我这里还有两种方法，但要注意，这些方法都是有损的。

**第一种方法：先处理掉那些占着连接但是不工作的线程。**

max_connections 的计算，不是看谁在 running，是只要连着就占用一个计数位置。对于那些不需要保持的连接，我们可以通过  kill connection 主动踢掉。这个行为跟事先设置 wait_timeout 的效果是一样的。设置 wait_timeout  参数表示的是，一个线程空闲 wait_timeout 这么多秒之后，就会被 MySQL 直接断开连接。

但是需要注意，在 show processlist 的结果里，踢掉显示为 sleep 的线程，可能是有损的。我们来看下面这个例子。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/9091ff280592c8c68665771b1516c62a-1584367394653.png)

图 1 sleep 线程的两种状态

在上面这个例子里，如果断开 session A 的连接，因为这时候 session A 还没有提交，所以 MySQL  只能按照回滚事务来处理；而断开 session B 的连接，就没什么大影响。所以，如果按照优先级来说，你应该优先断开像 session B  这样的事务外空闲的连接。

但是，怎么判断哪些是事务外空闲的呢？session C 在 T 时刻之后的 30 秒执行 show processlist，看到的结果是这样的。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/ae6a9ceecf8517e47f9ebfc565f0f925-1584367394656.png)

图 2 sleep 线程的两种状态，show processlist 结果

图中 id=4 和 id=5 的两个会话都是 Sleep 状态。而要看事务具体状态的话，你可以查 information_schema 库的 innodb_trx 表。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/ca4b455c8eacbf32b98d1fe9ed9876e8-1584367394660.png)

图 3 从 information_schema.innodb_trx 查询事务状态

这个结果里，trx_mysql_thread_id=4，表示 id=4 的线程还处在事务中。

因此，如果是连接数过多，你可以优先断开事务外空闲太久的连接；如果这样还不够，再考虑断开事务内空闲太久的连接。

从服务端断开连接使用的是 kill connection + id 的命令， 一个客户端处于 sleep  状态时，它的连接被服务端主动断开后，这个客户端并不会马上知道。直到客户端在发起下一个请求的时候，才会收到这样的报错“ERROR 2013  (HY000): Lost connection to MySQL server during query”。

从数据库端主动断开连接可能是有损的，尤其是有的应用端收到这个错误后，不重新连接，而是直接用这个已经不能用的句柄重试查询。这会导致从应用端看上去，“MySQL 一直没恢复”。

你可能觉得这是一个冷笑话，但实际上我碰到过不下 10 次。

所以，如果你是一个支持业务的 DBA，不要假设所有的应用代码都会被正确地处理。即使只是一个断开连接的操作，也要确保通知到业务开发团队。

**第二种方法：减少连接过程的消耗。**

有的业务代码会在短时间内先大量申请数据库连接做备用，如果现在数据库确认是被连接行为打挂了，那么一种可能的做法，是让数据库跳过权限验证阶段。

跳过权限验证的方法是：重启数据库，并使用–skip-grant-tables 参数启动。这样，整个 MySQL 会跳过所有的权限验证阶段，包括连接过程和语句执行过程在内。

但是，这种方法特别符合我们标题里说的“饮鸩止渴”，风险极高，是我特别不建议使用的方案。尤其你的库外网可访问的话，就更不能这么做了。

在 MySQL 8.0 版本里，如果你启用–skip-grant-tables 参数，MySQL 会默认把  --skip-networking 参数打开，表示这时候数据库只能被本地的客户端连接。可见，MySQL 官方对  skip-grant-tables 这个参数的安全问题也很重视。

除了短连接数暴增可能会带来性能问题外，实际上，我们在线上碰到更多的是查询或者更新语句导致的性能问题。其中，查询问题比较典型的有两类，一类是由新出现的慢查询导致的，一类是由 QPS（每秒查询数）突增导致的。而关于更新语句导致的性能问题，我会在下一篇文章和你展开说明。

#### 慢查询性能问题

在 MySQL 中，会引发性能问题的慢查询，大体有以下三种可能：

1. 索引没有设计好；
2. SQL 语句没写好；
3. MySQL 选错了索引。

接下来，我们就具体分析一下这三种可能，以及对应的解决方案。

**导致慢查询的第一种可能是，索引没有设计好。**

这种场景一般就是通过紧急创建索引来解决。MySQL 5.6 版本以后，创建索引都支持 Online DDL 了，对于那种高峰期数据库已经被这个语句打挂了的情况，最高效的做法就是直接执行 alter table 语句。

比较理想的是能够在备库先执行。假设你现在的服务是一主一备，主库 A、备库 B，这个方案的大致流程是这样的：

1. 在备库 B 上执行 set sql_log_bin=off，也就是不写 binlog，然后执行 alter table 语句加上索引；
2. 执行主备切换；
3. 这时候主库是 B，备库是 A。在 A 上执行 set sql_log_bin=off，然后执行 alter table 语句加上索引。

这是一个“古老”的 DDL 方案。平时在做变更的时候，你应该考虑类似 gh-ost 这样的方案，更加稳妥。但是在需要紧急处理时，上面这个方案的效率是最高的。

**导致慢查询的第二种可能是，语句没写好。**

比如，我们犯了在第 18 篇文章[《为什么这些 SQL 语句逻辑相同，性能却差异巨大？》]中提到的那些错误，导致语句没有使用上索引。

这时，我们可以通过改写 SQL 语句来处理。MySQL 5.7 提供了 query_rewrite 功能，可以把输入的一种语句改写成另外一种模式。

比如，语句被错误地写成了 select * from t where id + 1 = 10000，你可以通过下面的方式，增加一个语句改写规则。

```sql
mysql> insert into query_rewrite.rewrite_rules(pattern, replacement, pattern_database) values ("select * from t where id + 1 = ?", "select * from t where id = ? - 1", "db1"); 
call query_rewrite.flush_rewrite_rules();
```

这里，call query_rewrite.flush_rewrite_rules() 这个存储过程，是让插入的新规则生效，也就是我们说的“查询重写”。你可以用图 4 中的方法来确认改写规则是否生效。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/47a1002cbc4c05c74841591d20f7388a-1584367394663.png)

图 4 查询重写效果

**导致慢查询的第三种可能，就是碰上了我们在第 10 篇文章**[《MySQL 为什么有时候会选错索引？》]**中提到的情况，MySQL 选错了索引。**

这时候，应急方案就是给这个语句加上 force index。

同样地，使用查询重写功能，给原来的语句加上 force index，也可以解决这个问题。

上面我和你讨论的由慢查询导致性能问题的三种可能情况，实际上出现最多的是前两种，即：索引没设计好和语句没写好。而这两种情况，恰恰是完全可以避免的。比如，通过下面这个过程，我们就可以预先发现问题。

1. 上线前，在测试环境，把慢查询日志（slow log）打开，并且把 long_query_time 设置成 0，确保每个语句都会被记录入慢查询日志；
2. 在测试表里插入模拟线上的数据，做一遍回归测试；
3. 观察慢查询日志里每类语句的输出，特别留意 Rows_examined 字段是否与预期一致。（我们在前面文章中已经多次用到过 Rows_examined 方法了，相信你已经动手尝试过了。如果还有不明白的，欢迎给我留言，我们一起讨论）。

不要吝啬这段花在上线前的“额外”时间，因为这会帮你省下很多故障复盘的时间。

如果新增的 SQL 语句不多，手动跑一下就可以。而如果是新项目的话，或者是修改了原有项目的 表结构设计，全量回归测试都是必要的。这时候，你需要工具帮你检查所有的 SQL 语句的返回结果。比如，你可以使用开源工具 pt-query-digest(https://www.percona.com/doc/percona-toolkit/3.0/pt-query-digest.html)。

#### QPS 突增问题

有时候由于业务突然出现高峰，或者应用程序 bug，导致某个语句的 QPS 突然暴涨，也可能导致 MySQL 压力过大，影响服务。

我之前碰到过一类情况，是由一个新功能的 bug 导致的。当然，最理想的情况是让业务把这个功能下掉，服务自然就会恢复。

而下掉一个功能，如果从数据库端处理的话，对应于不同的背景，有不同的方法可用。我这里再和你展开说明一下。

1. 一种是由全新业务的 bug 导致的。假设你的 DB 运维是比较规范的，也就是说白名单是一个个加的。这种情况下，如果你能够确定业务方会下掉这个功能，只是时间上没那么快，那么就可以从数据库端直接把白名单去掉。
2. 如果这个新功能使用的是单独的数据库用户，可以用管理员账号把这个用户删掉，然后断开现有连接。这样，这个新功能的连接不成功，由它引发的 QPS 就会变成 0。
3. 如果这个新增的功能跟主体功能是部署在一起的，那么我们只能通过处理语句来限制。这时，我们可以使用上面提到的查询重写功能，把压力最大的 SQL 语句直接重写成"select 1"返回。

当然，这个操作的风险很高，需要你特别细致。它可能存在两个副作用：

1. 如果别的功能里面也用到了这个 SQL 语句模板，会有误伤；
2. 很多业务并不是靠这一个语句就能完成逻辑的，所以如果单独把这一个语句以 select 1 的结果返回的话，可能会导致后面的业务逻辑一起失败。

所以，方案 3 是用于止血的，跟前面提到的去掉权限验证一样，应该是你所有选项里优先级最低的一个方案。

同时你会发现，其实方案 1 和 2 都要依赖于规范的运维体系：虚拟化、白名单机制、业务账号分离。由此可见，更多的准备，往往意味着更稳定的系统。

#### 小结

今天这篇文章，我以业务高峰期的性能问题为背景，和你介绍了一些紧急处理的手段。

这些处理手段中，既包括了粗暴地拒绝连接和断开连接，也有通过重写语句来绕过一些坑的方法；既有临时的高危方案，也有未雨绸缪的、相对安全的预案。

在实际开发中，我们也要尽量避免一些低效的方法，比如避免大量地使用短连接。同时，如果你做业务开发的话，要知道，连接异常断开是常有的事，你的代码里要有正确地重连并重试的机制。

DBA 虽然可以通过语句重写来暂时处理问题，但是这本身是一个风险高的操作，做好 SQL 审计可以减少需要这类操作的机会。

其实，你可以看得出来，在这篇文章中我提到的解决方法主要集中在 server 层。在下一篇文章中，我会继续和你讨论一些跟 InnoDB 有关的处理方法。

最后，又到了我们的思考题时间了。

今天，我留给你的课后问题是，你是否碰到过，在业务高峰期需要临时救火的场景？你又是怎么处理的呢？

你可以把你的经历和经验写在留言区，我会在下一篇文章的末尾选取有趣的评论跟大家一起分享和分析。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

前两期我给你留的问题是，下面这个图的执行序列中，为什么 session B 的 insert 语句会被堵住。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/3a7578e104612a188a2d574eaa3bd81e-1550569913824-1584367394667.png)我们用上一篇的加锁规则来分析一下，看看 session A 的 select 语句加了哪些锁：

1. 由于是 order by c desc，第一个要定位的是索引 c 上“最右边的”c=20 的行，所以会加上间隙锁 (20,25) 和 next-key lock (15,20]。
2. 在索引 c 上向左遍历，要扫描到 c=10 才停下来，所以 next-key lock 会加到 (5,10]，这正是阻塞 session B 的 insert 语句的原因。
3. 在扫描过程中，c=20、c=15、c=10 这三行都存在值，由于是 select *，所以会在主键 id 上加三个行锁。

因此，session A 的 select 语句锁的范围就是：

1. 索引 c 上 (5, 25)；
2. 主键索引上 id=15、20 两个行锁。

这里，我再啰嗦下，你会发现我在文章中，每次加锁都会说明是加在“哪个索引上”的。因为，锁就是加在索引上的，这是 InnoDB 的一个基础设定，需要你在分析问题的时候要一直记得。

评论区留言点赞板：

> @HuaMax 给出了正确的解释。

> @Justin 同学提了个好问题，<= 到底是间隙锁还是行锁？其实，这个问题，你要跟“执行过程”配合起来分析。在 InnoDB  要去找“第一个值”的时候，是按照等值去找的，用的是等值判断的规则；找到第一个值以后，要在索引内找“下一个值”，对应于我们规则中说的范围查找。

> @信信 提了一个不错的问题，要知道最终的加锁是根据实际执行情况来的。所以，如果一个 select * from … for update 语句，优化器决定使用全表扫描，那么就会把主键索引上 next-key lock 全加上。

> @nero 同学的问题，提示我需要提醒大家注意，“有行”才会加行锁。如果查询条件没有命中行，那就加 next-key  lock。当然，等值判断的时候，需要加上优化 2（即：索引上的等值查询，向右遍历时且最后一个值不满足等值条件的时候，next-key lock  退化为间隙锁。）。

> @小李子、@发条橙子同学，都提了很好的问题，这期高质量评论很多，你也都可以去看看。

最后，我要为元旦期间还坚持学习的同学们，点个赞 ^_^

### 23 MySQL是怎么保证数据不丢的？

今天这篇文章，我会继续和你介绍在业务高峰期临时提升性能的方法。从文章标题“MySQL 是怎么保证数据不丢的？”，你就可以看出来，今天我和你介绍的方法，跟数据的可靠性有关。

在专栏前面文章和答疑篇中，我都着重介绍了 WAL 机制（你可以再回顾下[第 2 篇]、[第 9 篇]、[第 12 篇]和[第 15  篇]文章中的相关内容），得到的结论是：只要 redo log 和 binlog 保证持久化到磁盘，就能确保 MySQL  异常重启后，数据可以恢复。

评论区有同学又继续追问，redo log 的写入流程是怎么样的，如何保证 redo log 真实地写入了磁盘。那么今天，我们就再一起看看 MySQL 写入 binlog 和 redo log 的流程。

#### binlog 的写入机制

其实，binlog 的写入逻辑比较简单：事务执行过程中，先把日志写到 binlog cache，事务提交的时候，再把 binlog cache 写到 binlog 文件中。

一个事务的 binlog 是不能被拆开的，因此不论这个事务多大，也要确保一次性写入。这就涉及到了 binlog cache 的保存问题。

系统给 binlog cache 分配了一片内存，每个线程一个，参数 binlog_cache_size 用于控制单个线程内 binlog cache 所占内存的大小。如果超过了这个参数规定的大小，就要暂存到磁盘。

事务提交的时候，执行器把 binlog cache 里的完整事务写入到 binlog 中，并清空 binlog cache。状态如图 1 所示。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/9ed86644d5f39efb0efec595abb92e3e-1584367394669.png)

图 1 binlog 写盘状态

可以看到，每个线程有自己 binlog cache，但是共用同一份 binlog 文件。

- 图中的 write，指的就是指把日志写入到文件系统的 page cache，并没有把数据持久化到磁盘，所以速度比较快。
- 图中的 fsync，才是将数据持久化到磁盘的操作。一般情况下，我们认为 fsync 才占磁盘的 IOPS。

write 和 fsync 的时机，是由参数 sync_binlog 控制的：

1. sync_binlog=0 的时候，表示每次提交事务都只 write，不 fsync；
2. sync_binlog=1 的时候，表示每次提交事务都会执行 fsync；
3. sync_binlog=N(N>1) 的时候，表示每次提交事务都 write，但累积 N 个事务后才 fsync。

因此，在出现 IO 瓶颈的场景里，将 sync_binlog 设置成一个比较大的值，可以提升性能。在实际的业务场景中，考虑到丢失日志量的可控性，一般不建议将这个参数设成 0，比较常见的是将其设置为 100~1000 中的某个数值。

但是，将 sync_binlog 设置为 N，对应的风险是：如果主机发生异常重启，会丢失最近 N 个事务的 binlog 日志。

#### redo log 的写入机制

接下来，我们再说说 redo log 的写入机制。

在专栏的[第 15 篇答疑文章]中，我给你介绍了 redo log buffer。事务在执行过程中，生成的 redo log 是要先写到 redo log buffer 的。

然后就有同学问了，redo log buffer 里面的内容，是不是每次生成后都要直接持久化到磁盘呢？

答案是，不需要。

如果事务执行期间 MySQL 发生异常重启，那这部分日志就丢了。由于事务并没有提交，所以这时日志丢了也不会有损失。

那么，另外一个问题是，事务还没提交的时候，redo log buffer 中的部分日志有没有可能被持久化到磁盘呢？

答案是，确实会有。

这个问题，要从 redo log 可能存在的三种状态说起。这三种状态，对应的就是图 2 中的三个颜色块。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/9d057f61d3962407f413deebc80526d4-1584367394787.png)

图 2 MySQL redo log 存储状态

这三种状态分别是：

1. 存在 redo log buffer 中，物理上是在 MySQL 进程内存中，就是图中的红色部分；
2. 写到磁盘 (write)，但是没有持久化（fsync)，物理上是在文件系统的 page cache 里面，也就是图中的黄色部分；
3. 持久化到磁盘，对应的是 hard disk，也就是图中的绿色部分。

日志写到 redo log buffer 是很快的，wirte 到 page cache 也差不多，但是持久化到磁盘的速度就慢多了。

为了控制 redo log 的写入策略，InnoDB 提供了 innodb_flush_log_at_trx_commit 参数，它有三种可能取值：

1. 设置为 0 的时候，表示每次事务提交时都只是把 redo log 留在 redo log buffer 中 ;
2. 设置为 1 的时候，表示每次事务提交时都将 redo log 直接持久化到磁盘；
3. 设置为 2 的时候，表示每次事务提交时都只是把 redo log 写到 page cache。

InnoDB 有一个后台线程，每隔 1 秒，就会把 redo log buffer 中的日志，调用 write 写到文件系统的 page cache，然后调用 fsync 持久化到磁盘。

注意，事务执行中间过程的 redo log 也是直接写在 redo log buffer 中的，这些 redo log 也会被后台线程一起持久化到磁盘。也就是说，一个没有提交的事务的 redo log，也是可能已经持久化到磁盘的。

实际上，除了后台线程每秒一次的轮询操作外，还有两种场景会让一个没有提交的事务的 redo log 写入到磁盘中。

1. **一种是，redo log buffer 占用的空间即将达到 innodb_log_buffer_size  一半的时候，后台线程会主动写盘。**注意，由于这个事务并没有提交，所以这个写盘动作只是 write，而没有调用  fsync，也就是只留在了文件系统的 page cache。
2. **另一种是，并行的事务提交的时候，顺带将这个事务的 redo log buffer 持久化到磁盘。**假设一个事务 A  执行到一半，已经写了一些 redo log 到 buffer 中，这时候有另外一个线程的事务 B 提交，如果  innodb_flush_log_at_trx_commit 设置的是 1，那么按照这个参数的逻辑，事务 B 要把 redo log  buffer 里的日志全部持久化到磁盘。这时候，就会带上事务 A 在 redo log buffer 里的日志一起持久化到磁盘。

这里需要说明的是，我们介绍两阶段提交的时候说过，时序上 redo log 先 prepare， 再写 binlog，最后再把 redo log commit。

如果把 innodb_flush_log_at_trx_commit 设置成 1，那么 redo log 在 prepare  阶段就要持久化一次，因为有一个崩溃恢复逻辑是要依赖于 prepare 的 redo log，再加上 binlog  来恢复的。（如果你印象有点儿模糊了，可以再回顾下[第 15 篇文章]中的相关内容）。

每秒一次后台轮询刷盘，再加上崩溃恢复这个逻辑，InnoDB 就认为 redo log 在 commit 的时候就不需要 fsync 了，只会 write 到文件系统的 page cache 中就够了。

通常我们说 MySQL 的“双 1”配置，指的就是 sync_binlog 和  innodb_flush_log_at_trx_commit 都设置成 1。也就是说，一个事务完整提交前，需要等待两次刷盘，一次是 redo  log（prepare 阶段），一次是 binlog。

这时候，你可能有一个疑问，这意味着我从 MySQL 看到的 TPS 是每秒两万的话，每秒就会写四万次磁盘。但是，我用工具测试出来，磁盘能力也就两万左右，怎么能实现两万的 TPS？

解释这个问题，就要用到组提交（group commit）机制了。

这里，我需要先和你介绍日志逻辑序列号（log sequence number，LSN）的概念。LSN 是单调递增的，用来对应 redo log 的一个个写入点。每次写入长度为 length 的 redo log， LSN 的值就会加上 length。

LSN 也会写到 InnoDB 的数据页中，来确保数据页不会被多次执行重复的 redo log。关于 LSN 和 redo log、checkpoint 的关系，我会在后面的文章中详细展开。

如图 3 所示，是三个并发事务 (trx1, trx2, trx3) 在 prepare 阶段，都写完 redo log buffer，持久化到磁盘的过程，对应的 LSN 分别是 50、120 和 160。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/933fdc052c6339de2aa3bf3f65b188cc-1584367394795.png)

图 3 redo log 组提交

从图中可以看到，

1. trx1 是第一个到达的，会被选为这组的 leader；
2. 等 trx1 要开始写盘的时候，这个组里面已经有了三个事务，这时候 LSN 也变成了 160；
3. trx1 去写盘的时候，带的就是 LSN=160，因此等 trx1 返回时，所有 LSN 小于等于 160 的 redo log，都已经被持久化到磁盘；
4. 这时候 trx2 和 trx3 就可以直接返回了。

所以，一次组提交里面，组员越多，节约磁盘 IOPS 的效果越好。但如果只有单线程压测，那就只能老老实实地一个事务对应一次持久化操作了。

在并发更新场景下，第一个事务写完 redo log buffer 以后，接下来这个 fsync 越晚调用，组员可能越多，节约 IOPS 的效果就越好。

为了让一次 fsync 带的组员更多，MySQL 有一个很有趣的优化：拖时间。在介绍两阶段提交的时候，我曾经给你画了一个图，现在我把它截过来。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/98b3b4ff7b36d6d72e38029b86870551-1584367394832.png)

图 4 两阶段提交

图中，我把“写 binlog”当成一个动作。但实际上，写 binlog 是分成两步的：

1. 先把 binlog 从 binlog cache 中写到磁盘上的 binlog 文件；
2. 调用 fsync 持久化。

MySQL 为了让组提交的效果更好，把 redo log 做 fsync 的时间拖到了步骤 1 之后。也就是说，上面的图变成了这样：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/5ae7d074c34bc5bd55c82781de670c28-1584367394852.png)

图 5 两阶段提交细化

这么一来，binlog 也可以组提交了。在执行图 5 中第 4 步把 binlog fsync 到磁盘时，如果有多个事务的 binlog 已经写完了，也是一起持久化的，这样也可以减少 IOPS 的消耗。

不过通常情况下第 3 步执行得会很快，所以 binlog 的 write 和 fsync 间的间隔时间短，导致能集合到一起持久化的 binlog 比较少，因此 binlog 的组提交的效果通常不如 redo log 的效果那么好。

如果你想提升 binlog 组提交的效果，可以通过设置 binlog_group_commit_sync_delay 和 binlog_group_commit_sync_no_delay_count 来实现。

1. binlog_group_commit_sync_delay 参数，表示延迟多少微秒后才调用 fsync;
2. binlog_group_commit_sync_no_delay_count 参数，表示累积多少次以后才调用 fsync。

这两个条件是或的关系，也就是说只要有一个满足条件就会调用 fsync。

所以，当 binlog_group_commit_sync_delay 设置为 0 的时候，binlog_group_commit_sync_no_delay_count 也无效了。

之前有同学在评论区问到，WAL 机制是减少磁盘写，可是每次提交事务都要写 redo log 和 binlog，这磁盘读写次数也没变少呀？

现在你就能理解了，WAL 机制主要得益于两个方面：

1. redo log 和 binlog 都是顺序写，磁盘的顺序写比随机写速度要快；
2. 组提交机制，可以大幅度降低磁盘的 IOPS 消耗。

分析到这里，我们再来回答这个问题：**如果你的 MySQL 现在出现了性能瓶颈，而且瓶颈在 IO 上，可以通过哪些方法来提升性能呢？**

针对这个问题，可以考虑以下三种方法：

1. 设置 binlog_group_commit_sync_delay 和  binlog_group_commit_sync_no_delay_count 参数，减少 binlog  的写盘次数。这个方法是基于“额外的故意等待”来实现的，因此可能会增加语句的响应时间，但没有丢失数据的风险。
2. 将 sync_binlog 设置为大于 1 的值（比较常见是 100~1000）。这样做的风险是，主机掉电时会丢 binlog 日志。
3. 将 innodb_flush_log_at_trx_commit 设置为 2。这样做的风险是，主机掉电的时候会丢数据。

我不建议你把 innodb_flush_log_at_trx_commit 设置成 0。因为把这个参数设置成 0，表示 redo log  只保存在内存中，这样的话 MySQL 本身异常重启也会丢数据，风险太大。而 redo log 写到文件系统的 page cache  的速度也是很快的，所以将这个参数设置成 2 跟设置成 0 其实性能差不多，但这样做 MySQL 异常重启时就不会丢数据了，相比之下风险会更小。

#### 小结

在专栏的[第 2 篇]和[第 15 篇]文章中，我和你分析了，如果 redo log 和 binlog 是完整的，MySQL 是如何保证  crash-safe 的。今天这篇文章，我着重和你介绍的是 MySQL 是“怎么保证 redo log 和 binlog 是完整的”。

希望这三篇文章串起来的内容，能够让你对 crash-safe 这个概念有更清晰的理解。

之前的第 15 篇答疑文章发布之后，有同学继续留言问到了一些跟日志相关的问题，这里为了方便你回顾、学习，我再集中回答一次这些问题。

**问题 1：**执行一个 update 语句以后，我再去执行 hexdump 命令直接查看 ibd 文件内容，为什么没有看到数据有改变呢？

回答：这可能是因为 WAL 机制的原因。update 语句执行完成后，InnoDB 只保证写完了 redo log、内存，可能还没来得及将数据写到磁盘。

**问题 2：**为什么 binlog cache 是每个线程自己维护的，而 redo log buffer 是全局共用的？

回答：MySQL 这么设计的主要原因是，binlog 是不能“被打断的”。一个事务的 binlog 必须连续写，因此要整个事务完成后，再一起写到文件里。

而 redo log 并没有这个要求，中间有生成的日志可以写到 redo log buffer 中。redo log buffer 中的内容还能“搭便车”，其他事务提交的时候可以被一起写到磁盘中。

**问题 3：**事务执行期间，还没到提交阶段，如果发生 crash 的话，redo log 肯定丢了，这会不会导致主备不一致呢？

回答：不会。因为这时候 binlog 也还在 binlog cache 里，没发给备库。crash 以后 redo log 和 binlog 都没有了，从业务角度看这个事务也没有提交，所以数据是一致的。

**问题 4：**如果 binlog 写完盘以后发生 crash，这时候还没给客户端答复就重启了。等客户端再重连进来，发现事务已经提交成功了，这是不是 bug？

回答：不是。

你可以设想一下更极端的情况，整个事务都提交成功了，redo log commit 完成了，备库也收到 binlog  并执行了。但是主库和客户端网络断开了，导致事务成功的包返回不回去，这时候客户端也会收到“网络断开”的异常。这种也只能算是事务成功的，不能认为是  bug。

实际上数据库的 crash-safe 保证的是：

1. 如果客户端收到事务成功的消息，事务就一定持久化了；
2. 如果客户端收到事务失败（比如主键冲突、回滚等）的消息，事务就一定失败了；
3. 如果客户端收到“执行异常”的消息，应用需要重连后通过查询当前状态来继续后续的逻辑。此时数据库只需要保证内部（数据和日志之间，主库和备库之间）一致就可以了。

最后，又到了课后问题时间。

今天我留给你的思考题是：你的生产库设置的是“双 1”吗？ 如果平时是的话，你有在什么场景下改成过“非双 1”吗？你的这个操作又是基于什么决定的？

另外，我们都知道这些设置可能有损，如果发生了异常，你的止损方案是什么？

你可以把你的理解或者经验写在留言区，我会在下一篇文章的末尾选取有趣的评论和你一起分享和分析。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

我在上篇文章最后，想要你分享的是线上“救火”的经验。

@Long 同学，在留言中提到了几个很好的场景。

- 其中第 3 个问题，“如果一个数据库是被客户端的压力打满导致无法响应的，重启数据库是没用的。”，说明他很好地思考了。 这个问题是因为重启之后，业务请求还会再发。而且由于是重启，buffer pool 被清空，可能会导致语句执行得更慢。
- 他提到的第 4  个问题也很典型。有时候一个表上会出现多个单字段索引（而且往往这是因为运维工程师对索引原理不够清晰做的设计），这样就可能出现优化器选择索引合并算法的现象。但实际上，索引合并算法的效率并不好。而通过将其中的一个索引改成联合索引的方法，是一个很好的应对方案。

还有其他几个同学提到的问题场景，也很好，很值得你一看。

> @Max 同学提到一个很好的例子：客户端程序的连接器，连接完成后会做一些诸如 show columns  的操作，在短连接模式下这个影响就非常大了。 这个提醒我们，在 review 项目的时候，不止要 review 我们自己业务的代码，也要  review 连接器的行为。一般做法就是在测试环境，把 general_log 打开，用业务行为触发连接，然后通过 general log  分析连接器的行为。

> @Manjusaka  同学的留言中，第二点提得非常好：如果你的数据库请求模式直接对应于客户请求，这往往是一个危险的设计。因为客户行为不可控，可能突然因为你们公司的一个运营推广，压力暴增，这样很容易把数据库打挂。 在设计模型里面设计一层，专门负责管理请求和数据库服务资源，对于比较重要和大流量的业务，是一个好的设计方向。

> @Vincent 同学提了一个好问题，用文中提到的 DDL 方案，会导致 binlog 里面少了这个 DDL 语句，后续影响备份恢复的功能。由于需要另一个知识点（主备同步协议），我放在后面的文章中说明。

### 24 MySQL是怎么保证主备一致的？

在前面的文章中，我不止一次地和你提到了 binlog，大家知道 binlog 可以用来归档，也可以用来做主备同步，但它的内容是什么样的呢？为什么备库执行了 binlog 就可以跟主库保持一致了呢？今天我就正式地和你介绍一下它。

毫不夸张地说，MySQL 能够成为现下最流行的开源数据库，binlog 功不可没。

在最开始，MySQL 是以容易学习和方便的高可用架构，被开发人员青睐的。而它的几乎所有的高可用架构，都直接依赖于 binlog。虽然这些高可用架构已经呈现出越来越复杂的趋势，但都是从最基本的一主一备演化过来的。

今天这篇文章我主要为你介绍主备的基本原理。理解了背后的设计原理，你也可以从业务开发的角度，来借鉴这些设计思想。

#### MySQL 主备的基本原理

如图 1 所示就是基本的主备切换流程。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/fd75a2b37ae6ca709b7f16fe060c2c10-1584367395065.png)

图 1 MySQL 主备切换流程

在状态 1 中，客户端的读写都直接访问节点 A，而节点 B 是 A 的备库，只是将 A 的更新都同步过来，到本地执行。这样可以保持节点 B 和 A 的数据是相同的。

当需要切换的时候，就切成状态 2。这时候客户端读写访问的都是节点 B，而节点 A 是 B 的备库。

在状态 1 中，虽然节点 B 没有被直接访问，但是我依然建议你把节点 B（也就是备库）设置成只读（readonly）模式。这样做，有以下几个考虑：

1. 有时候一些运营类的查询语句会被放到备库上去查，设置为只读可以防止误操作；
2. 防止切换逻辑有 bug，比如切换过程中出现双写，造成主备不一致；
3. 可以用 readonly 状态，来判断节点的角色。

你可能会问，我把备库设置成只读了，还怎么跟主库保持同步更新呢？

这个问题，你不用担心。因为 readonly 设置对超级 (super) 权限用户是无效的，而用于同步更新的线程，就拥有超级权限。

接下来，我们再看看**节点 A 到 B 这条线的内部流程是什么样的**。图 2 中画出的就是一个 update 语句在节点 A 执行，然后同步到节点 B 的完整流程图。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/a66c154c1bc51e071dd2cc8c1d6ca6a3-1584367397412.png)

图 2 主备流程图

图 2 中，包含了我在上一篇文章中讲到的 binlog 和 redo log 的写入机制相关的内容，可以看到：主库接收到客户端的更新请求后，执行内部事务的更新逻辑，同时写 binlog。

备库 B 跟主库 A 之间维持了一个长连接。主库 A 内部有一个线程，专门用于服务备库 B 的这个长连接。一个事务日志同步的完整过程是这样的：

1. 在备库 B 上通过 change master 命令，设置主库 A 的 IP、端口、用户名、密码，以及要从哪个位置开始请求 binlog，这个位置包含文件名和日志偏移量。
2. 在备库 B 上执行 start slave 命令，这时候备库会启动两个线程，就是图中的 io_thread 和 sql_thread。其中 io_thread 负责与主库建立连接。
3. 主库 A 校验完用户名、密码后，开始按照备库 B 传过来的位置，从本地读取 binlog，发给 B。
4. 备库 B 拿到 binlog 后，写到本地文件，称为中转日志（relay log）。
5. sql_thread 读取中转日志，解析出日志里的命令，并执行。

这里需要说明，后来由于多线程复制方案的引入，sql_thread 演化成为了多个线程，跟我们今天要介绍的原理没有直接关系，暂且不展开。

分析完了这个长连接的逻辑，我们再来看一个问题：binlog 里面到底是什么内容，为什么备库拿过去可以直接执行。

#### binlog 的三种格式对比

我在[第 15 篇答疑文章]中，和你提到过 binlog 有两种格式，一种是 statement，一种是 row。可能你在其他资料上还会看到有第三种格式，叫作 mixed，其实它就是前两种格式的混合。

为了便于描述 binlog 的这三种格式间的区别，我创建了一个表，并初始化几行数据。

```sql
mysql> CREATE TABLE `t` (
  `id` int(11) NOT NULL,
  `a` int(11) DEFAULT NULL,
  `t_modified` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`),
  KEY `a` (`a`),
  KEY `t_modified`(`t_modified`)
) ENGINE=InnoDB; 
insert into t values(1,1,'2018-11-13');
insert into t values(2,2,'2018-11-12');
insert into t values(3,3,'2018-11-11');
insert into t values(4,4,'2018-11-10');
insert into t values(5,5,'2018-11-09');
```

如果要在表中删除一行数据的话，我们来看看这个 delete 语句的 binlog 是怎么记录的。

注意，下面这个语句包含注释，如果你用 MySQL 客户端来做这个实验的话，要记得加 -c 参数，否则客户端会自动去掉注释。

```sql
mysql> delete from t /*comment*/  where a>=4 and t_modified<='2018-11-10' limit 1;
```

当 binlog_format=statement 时，binlog 里面记录的就是 SQL 语句的原文。你可以用

```shell
mysql> show binlog events in 'master.000001';
```

命令看 binlog 中的内容。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/b9818f73cd7d38a96ddcb75350b52931-1584367397413.png)

图 3 statement 格式 binlog 示例

现在，我们来看一下图 3 的输出结果。

- 第一行 SET @@SESSION.GTID_NEXT='ANONYMOUS’你可以先忽略，后面文章我们会在介绍主备切换的时候再提到；
- 第二行是一个 BEGIN，跟第四行的 commit 对应，表示中间是一个事务；
- 第三行就是真实执行的语句了。可以看到，在真实执行的 delete 命令之前，还有一个“use  ‘test’”命令。这条命令不是我们主动执行的，而是 MySQL  根据当前要操作的表所在的数据库，自行添加的。这样做可以保证日志传到备库去执行的时候，不论当前的工作线程在哪个库里，都能够正确地更新到 test  库的表 t。 use 'test’命令之后的 delete 语句，就是我们输入的 SQL 原文了。可以看到，binlog“忠实”地记录了 SQL 命令，甚至连注释也一并记录了。
- 最后一行是一个 COMMIT。你可以看到里面写着 xid=61。你还记得这个 XID 是做什么用的吗？如果记忆模糊了，可以再回顾一下[第 15 篇文章]中的相关内容。

为了说明 statement 和 row 格式的区别，我们来看一下这条 delete 命令的执行效果图：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/96c2be9c0fcbff66883118526b26652b-1584367397421.png)

图 4 delete 执行 warnings

可以看到，运行这条 delete 命令产生了一个 warning，原因是当前 binlog 设置的是 statement 格式，并且语句中有 limit，所以这个命令可能是 unsafe 的。

为什么这么说呢？这是因为 delete 带 limit，很可能会出现主备数据不一致的情况。比如上面这个例子：

1. 如果 delete 语句使用的是索引 a，那么会根据索引 a 找到第一个满足条件的行，也就是说删除的是 a=4 这一行；
2. 但如果使用的是索引 t_modified，那么删除的就是 t_modified='2018-11-09’也就是 a=5 这一行。

由于 statement 格式下，记录到 binlog 里的是语句原文，因此可能会出现这样一种情况：在主库执行这条 SQL  语句的时候，用的是索引 a；而在备库执行这条 SQL 语句的时候，却使用了索引 t_modified。因此，MySQL 认为这样写是有风险的。

那么，如果我把 binlog 的格式改为 binlog_format=‘row’， 是不是就没有这个问题了呢？我们先来看看这时候 binog 中的内容吧。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/d67a38db154afff610ae3bb64e266826-1584367389320.png)

图 5 row 格式 binlog 示例

可以看到，与 statement 格式的 binlog 相比，前后的 BEGIN 和 COMMIT 是一样的。但是，row 格式的 binlog 里没有了 SQL 语句的原文，而是替换成了两个 event：Table_map 和 Delete_rows。

1. Table_map event，用于说明接下来要操作的表是 test 库的表 t;
2. Delete_rows event，用于定义删除的行为。

其实，我们通过图 5 是看不到详细信息的，还需要借助 mysqlbinlog 工具，用下面这个命令解析和查看 binlog  中的内容。因为图 5 中的信息显示，这个事务的 binlog 是从 8900 这个位置开始的，所以可以用 start-position  参数来指定从这个位置的日志开始解析。

```bash
mysqlbinlog  -vv data/master.000001 --start-position=8900;
```

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/c342cf480d23b05d30a294b114cebfc2-1584367389357.png)

图 6 row 格式 binlog 示例的详细信息

从这个图中，我们可以看到以下几个信息：

- server id 1，表示这个事务是在 server_id=1 的这个库上执行的。
- 每个 event 都有 CRC32 的值，这是因为我把参数 binlog_checksum 设置成了 CRC32。
- Table_map event 跟在图 5 中看到的相同，显示了接下来要打开的表，map 到数字 226。现在我们这条 SQL  语句只操作了一张表，如果要操作多张表呢？每个表都有一个对应的 Table_map event、都会 map  到一个单独的数字，用于区分对不同表的操作。
- 我们在 mysqlbinlog 的命令中，使用了 -vv 参数是为了把内容都解析出来，所以从结果里面可以看到各个字段的值（比如，@1=4、 @2=4 这些值）。
- binlog_row_image 的默认配置是 FULL，因此 Delete_event 里面，包含了删掉的行的所有字段的值。如果把  binlog_row_image 设置为 MINIMAL，则只会记录必要的信息，在这个例子里，就是只会记录 id=4 这个信息。
- 最后的 Xid event，用于表示事务被正确地提交了。

你可以看到，当 binlog_format 使用 row 格式的时候，binlog 里面记录了真实删除行的主键 id，这样 binlog 传到备库去的时候，就肯定会删除 id=4 的行，不会有主备删除不同行的问题。

#### 为什么会有 mixed 格式的 binlog？

基于上面的信息，我们来讨论一个问题：**为什么会有 mixed 这种 binlog 格式的存在场景？**推论过程是这样的：

- 因为有些 statement 格式的 binlog 可能会导致主备不一致，所以要使用 row 格式。
- 但 row 格式的缺点是，很占空间。比如你用一个 delete 语句删掉 10 万行数据，用 statement 的话就是一个 SQL  语句被记录到 binlog 中，占用几十个字节的空间。但如果用 row 格式的 binlog，就要把这 10 万条记录都写到 binlog  中。这样做，不仅会占用更大的空间，同时写 binlog 也要耗费 IO 资源，影响执行速度。
- 所以，MySQL 就取了个折中方案，也就是有了 mixed 格式的 binlog。mixed 格式的意思是，MySQL 自己会判断这条 SQL 语句是否可能引起主备不一致，如果有可能，就用 row 格式，否则就用 statement 格式。

也就是说，mixed 格式可以利用 statment 格式的优点，同时又避免了数据不一致的风险。

因此，如果你的线上 MySQL 设置的 binlog 格式是 statement 的话，那基本上就可以认为这是一个不合理的设置。你至少应该把 binlog 的格式设置为 mixed。

比如我们这个例子，设置为 mixed 后，就会记录为 row 格式；而如果执行的语句去掉 limit 1，就会记录为 statement 格式。

当然我要说的是，现在越来越多的场景要求把 MySQL 的 binlog 格式设置成 row。这么做的理由有很多，我来给你举一个可以直接看出来的好处：**恢复数据**。

接下来，我们就分别从 delete、insert 和 update 这三种 SQL 语句的角度，来看看数据恢复的问题。

通过图 6 你可以看出来，即使我执行的是 delete 语句，row 格式的 binlog  也会把被删掉的行的整行信息保存起来。所以，如果你在执行完一条 delete 语句以后，发现删错数据了，可以直接把 binlog 中记录的  delete 语句转成 insert，把被错删的数据插入回去就可以恢复了。

如果你是执行错了 insert 语句呢？那就更直接了。row 格式下，insert 语句的 binlog  里会记录所有的字段信息，这些信息可以用来精确定位刚刚被插入的那一行。这时，你直接把 insert 语句转成 delete  语句，删除掉这被误插入的一行数据就可以了。

如果执行的是 update 语句的话，binlog 里面会记录修改前整行的数据和修改后的整行数据。所以，如果你误执行了 update 语句的话，只需要把这个 event 前后的两行信息对调一下，再去数据库里面执行，就能恢复这个更新操作了。

其实，由 delete、insert 或者 update 语句导致的数据操作错误，需要恢复到操作之前状态的情况，也时有发生。MariaDB 的[Flashback](https://mariadb.com/kb/en/library/flashback/)工具就是基于上面介绍的原理来回滚数据的。

虽然 mixed 格式的 binlog 现在已经用得不多了，但这里我还是要再借用一下 mixed 格式来说明一个问题，来看一下这条 SQL 语句：

```sql
mysql> insert into t values(10,10, now());
```

如果我们把 binlog 格式设置为 mixed，你觉得 MySQL 会把它记录为 row 格式还是 statement 格式呢？

先不要着急说结果，我们一起来看一下这条语句执行的效果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/0150301698979255a6f27711c35e9eef-1584367389377.png)

图 7 mixed 格式和 now()

可以看到，MySQL 用的居然是 statement 格式。你一定会奇怪，如果这个 binlog 过了 1 分钟才传给备库的话，那主备的数据不就不一致了吗？

接下来，我们再用 mysqlbinlog 工具来看看：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/1ad3a4c4b9a71955edba5195757dd041-1584367389377.png)

图 8 TIMESTAMP 命令

从图中的结果可以看到，原来 binlog 在记录 event 的时候，多记了一条命令：SET TIMESTAMP=1546103491。它用 SET TIMESTAMP 命令约定了接下来的 now() 函数的返回时间。

因此，不论这个 binlog 是 1 分钟之后被备库执行，还是 3 天后用来恢复这个库的备份，这个 insert 语句插入的行，值都是固定的。也就是说，通过这条 SET TIMESTAMP 命令，MySQL 就确保了主备数据的一致性。

我之前看过有人在重放 binlog 数据的时候，是这么做的：用 mysqlbinlog 解析出日志，然后把里面的 statement 语句直接拷贝出来执行。

你现在知道了，这个方法是有风险的。因为有些语句的执行结果是依赖于上下文命令的，直接执行的结果很可能是错误的。

所以，用 binlog 来恢复数据的标准做法是，用 mysqlbinlog 工具解析出来，然后把解析结果整个发给 MySQL 执行。类似下面的命令：

```bash
mysqlbinlog master.000001  --start-position=2738 --stop-position=2973 | mysql -h127.0.0.1 -P13000 -u$user -p$pwd;
```

这个命令的意思是，将 master.000001 文件里面从第 2738 字节到第 2973 字节中间这段内容解析出来，放到 MySQL 去执行。

#### 循环复制问题

通过上面对 MySQL 中 binlog 基本内容的理解，你现在可以知道，binlog 的特性确保了在备库执行相同的 binlog，可以得到与主库相同的状态。

因此，我们可以认为正常情况下主备的数据是一致的。也就是说，图 1 中 A、B 两个节点的内容是一致的。其实，图 1 中我画的是 M-S 结构，但实际生产上使用比较多的是双 M 结构，也就是图 9 所示的主备切换流程。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/20ad4e163115198dc6cf372d5116c956-1584367389406.png)

图 9 MySQL 主备切换流程 -- 双 M 结构

对比图 9 和图 1，你可以发现，双 M 结构和 M-S 结构，其实区别只是多了一条线，即：节点 A 和 B 之间总是互为主备关系。这样在切换的时候就不用再修改主备关系。

但是，双 M 结构还有一个问题需要解决。

业务逻辑在节点 A 上更新了一条语句，然后再把生成的 binlog 发给节点 B，节点 B 执行完这条更新语句后也会生成  binlog。（我建议你把参数 log_slave_updates 设置为 on，表示备库执行 relay log 后生成 binlog）。

那么，如果节点 A 同时是节点 B 的备库，相当于又把节点 B 新生成的 binlog 拿过来执行了一次，然后节点 A 和 B 间，会不断地循环执行这个更新语句，也就是循环复制了。这个要怎么解决呢？

从上面的图 6 中可以看到，MySQL 在 binlog 中记录了这个命令第一次执行时所在实例的 server id。因此，我们可以用下面的逻辑，来解决两个节点间的循环复制的问题：

1. 规定两个库的 server id 必须不同，如果相同，则它们之间不能设定为主备关系；
2. 一个备库接到 binlog 并在重放的过程中，生成与原 binlog 的 server id 相同的新的 binlog；
3. 每个库在收到从自己的主库发过来的日志后，先判断 server id，如果跟自己的相同，表示这个日志是自己生成的，就直接丢弃这个日志。

按照这个逻辑，如果我们设置了双 M 结构，日志的执行流就会变成这样：

1. 从节点 A 更新的事务，binlog 里面记的都是 A 的 server id；
2. 传到节点 B 执行一次以后，节点 B 生成的 binlog 的 server id 也是 A 的 server id；
3. 再传回给节点 A，A 判断到这个 server id 与自己的相同，就不会再处理这个日志。所以，死循环在这里就断掉了。

#### 小结

今天这篇文章，我给你介绍了 MySQL binlog 的格式和一些基本机制，是后面我要介绍的读写分离等系列文章的背景知识，希望你可以认真消化理解。

binlog 在 MySQL 的各种高可用方案上扮演了重要角色。今天介绍的可以说是所有 MySQL 高可用方案的基础。在这之上演化出了诸如多节点、半同步、MySQL group replication 等相对复杂的方案。

我也跟你介绍了 MySQL 不同格式 binlog 的优缺点，和设计者的思考。希望你在做系统开发时候，也能借鉴这些设计思想。

最后，我给你留下一个思考题吧。

说到循环复制问题的时候，我们说 MySQL 通过判断 server id 的方式，断掉死循环。但是，这个机制其实并不完备，在某些场景下，还是有可能出现死循环。

你能构造出一个这样的场景吗？又应该怎么解决呢？

你可以把你的设计和分析写在评论区，我会在下一篇文章跟你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

上期我留给你的问题是，你在什么时候会把线上生产库设置成“非双 1”。我目前知道的场景，有以下这些：

1. 业务高峰期。一般如果有预知的高峰期，DBA 会有预案，把主库设置成“非双 1”。
2. 备库延迟，为了让备库尽快赶上主库。@永恒记忆和 @Second Sight 提到了这个场景。
3. 用备份恢复主库的副本，应用 binlog 的过程，这个跟上一种场景类似。
4. 批量导入数据的时候。

一般情况下，把生产库改成“非双 1”配置，是设置 innodb_flush_logs_at_trx_commit=2、sync_binlog=1000。

评论区留言点赞板：

> @way 同学提到了一个有趣的现象，由于从库设置了 binlog_group_commit_sync_delay 和  binlog_group_commit_sync_no_delay_count 导致一直延迟的情况。我们在主库设置这两个参数，是为了减少  binlog 的写盘压力。备库这么设置，尤其在“快要追上”的时候，就反而会受这两个参数的拖累。一般追主备就用“非双 1”（追上记得改回来）。

> @一大只 同学验证了在 sync_binlog=0 的情况下，设置 sync_delay 和 sync_no_delay_count  的现象，点赞这种发现边界的意识和手动验证的好习惯。是这样的：sync_delay 和 sync_no_delay_count  的逻辑先走，因此该等还是会等。等到满足了这两个条件之一，就进入 sync_binlog 阶段。这时候如果判断  sync_binlog=0，就直接跳过，还是不调 fsync。

> @锅子 同学提到，设置 sync_binlog=0 的时候，还是可以看到 binlog 文件马上做了修改。这个是对的，我们说“写到了 page cache”，就是文件系统的 page cache。而你用 ls 命令看到的就是文件系统返回的结果。

### 25 MySQL是怎么保证高可用的？

在上一篇文章中，我和你介绍了 binlog 的基本内容，在一个主备关系中，每个备库接收主库的 binlog 并执行。

正常情况下，只要主库执行更新生成的所有 binlog，都可以传到备库并被正确地执行，备库就能达到跟主库一致的状态，这就是最终一致性。

但是，MySQL 要提供高可用能力，只有最终一致性是不够的。为什么这么说呢？今天我就着重和你分析一下。

这里，我再放一次上一篇文章中讲到的双 M 结构的主备切换流程图。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/89290bbcf454ff9a3dc5de42a85a69cc-1584367397421.png)

图 1 MySQL 主备切换流程 -- 双 M 结构

#### 主备延迟

主备切换可能是一个主动运维动作，比如软件升级、主库所在机器按计划下线等，也可能是被动操作，比如主库所在机器掉电。

接下来，我们先一起看看主动切换的场景。

在介绍主动切换流程的详细步骤之前，我要先跟你说明一个概念，即“同步延迟”。与数据同步有关的时间点主要包括以下三个：

1. 主库 A 执行完成一个事务，写入 binlog，我们把这个时刻记为 T1;
2. 之后传给备库 B，我们把备库 B 接收完这个 binlog 的时刻记为 T2;
3. 备库 B 执行完成这个事务，我们把这个时刻记为 T3。

所谓主备延迟，就是同一个事务，在备库执行完成的时间和主库执行完成的时间之间的差值，也就是 T3-T1。

你可以在备库上执行 show slave status 命令，它的返回结果里面会显示 seconds_behind_master，用于表示当前备库延迟了多少秒。

seconds_behind_master 的计算方法是这样的：

1. 每个事务的 binlog 里面都有一个时间字段，用于记录主库上写入的时间；
2. 备库取出当前正在执行的事务的时间字段的值，计算它与当前系统时间的差值，得到 seconds_behind_master。

可以看到，其实 seconds_behind_master 这个参数计算的就是 T3-T1。所以，我们可以用 seconds_behind_master 来作为主备延迟的值，这个值的时间精度是秒。

你可能会问，如果主备库机器的系统时间设置不一致，会不会导致主备延迟的值不准？

其实不会的。因为，备库连接到主库的时候，会通过执行 SELECT UNIX_TIMESTAMP()  函数来获得当前主库的系统时间。如果这时候发现主库的系统时间与自己不一致，备库在执行 seconds_behind_master  计算的时候会自动扣掉这个差值。

需要说明的是，在网络正常的时候，日志从主库传给备库所需的时间是很短的，即 T2-T1 的值是非常小的。也就是说，网络正常情况下，主备延迟的主要来源是备库接收完 binlog 和执行完这个事务之间的时间差。

所以说，主备延迟最直接的表现是，备库消费中转日志（relay log）的速度，比主库生产 binlog 的速度要慢。接下来，我就和你一起分析下，这可能是由哪些原因导致的。

#### 主备延迟的来源

**首先，有些部署条件下，备库所在机器的性能要比主库所在的机器性能差。**

一般情况下，有人这么部署时的想法是，反正备库没有请求，所以可以用差一点儿的机器。或者，他们会把 20 个主库放在 4 台机器上，而把备库集中在一台机器上。

其实我们都知道，更新请求对 IOPS 的压力，在主库和备库上是无差别的。所以，做这种部署时，一般都会将备库设置为“非双 1”的模式。

但实际上，更新过程中也会触发大量的读操作。所以，当备库主机上的多个备库都在争抢资源的时候，就可能会导致主备延迟了。

当然，这种部署现在比较少了。因为主备可能发生切换，备库随时可能变成主库，所以主备库选用相同规格的机器，并且做对称部署，是现在比较常见的情况。

追问 1：但是，做了对称部署以后，还可能会有延迟。这是为什么呢？

这就是**第二种常见的可能了，即备库的压力大**。一般的想法是，主库既然提供了写能力，那么备库可以提供一些读能力。或者一些运营后台需要的分析语句，不能影响正常业务，所以只能在备库上跑。

我真就见过不少这样的情况。由于主库直接影响业务，大家使用起来会比较克制，反而忽视了备库的压力控制。结果就是，备库上的查询耗费了大量的 CPU 资源，影响了同步速度，造成主备延迟。

这种情况，我们一般可以这么处理：

1. 一主多从。除了备库外，可以多接几个从库，让这些从库来分担读的压力。
2. 通过 binlog 输出到外部系统，比如 Hadoop 这类系统，让外部系统提供统计类查询的能力。

其中，一主多从的方式大都会被采用。因为作为数据库系统，还必须保证有定期全量备份的能力。而从库，就很适合用来做备份。

> 备注：这里需要说明一下，从库和备库在概念上其实差不多。在我们这个专栏里，为了方便描述，我把会在 HA 过程中被选成新主库的，称为备库，其他的称为从库。

追问 2：采用了一主多从，保证备库的压力不会超过主库，还有什么情况可能导致主备延迟吗？

**这就是第三种可能了，即大事务。**

大事务这种情况很好理解。因为主库上必须等事务执行完成才会写入 binlog，再传给备库。所以，如果一个主库上的语句执行 10 分钟，那这个事务很可能就会导致从库延迟 10 分钟。

不知道你所在公司的 DBA 有没有跟你这么说过：不要**一次性地用 delete 语句删除太多数据**。其实，这就是一个典型的大事务场景。

比如，一些归档类的数据，平时没有注意删除历史数据，等到空间快满了，业务开发人员要一次性地删掉大量历史数据。同时，又因为要避免在高峰期操作会影响业务（至少有这个意识还是很不错的），所以会在晚上执行这些大量数据的删除操作。

结果，负责的 DBA 同学半夜就会收到延迟报警。然后，DBA 团队就要求你后续再删除数据的时候，要控制每个事务删除的数据量，分成多次删除。

**另一种典型的大事务场景，就是大表 DDL。**这个场景，我在前面的文章中介绍过。处理方案就是，计划内的 DDL，建议使用 gh-ost 方案（这里，你可以再回顾下第 13 篇文章[《为什么表数据删掉一半，表文件大小不变？》]中的相关内容）。

追问 3：如果主库上也不做大事务了，还有什么原因会导致主备延迟吗？

造成主备延迟还有一个大方向的原因，就是**备库的并行复制能力**。这个话题，我会留在下一篇文章再和你详细介绍。

其实还是有不少其他情况会导致主备延迟，如果你还碰到过其他场景，欢迎你在评论区给我留言，我来和你一起分析、讨论。

由于主备延迟的存在，所以在主备切换的时候，就相应的有不同的策略。

#### 可靠性优先策略

在图 1 的双 M 结构下，从状态 1 到状态 2 切换的详细过程是这样的：

1. 判断备库 B 现在的 seconds_behind_master，如果小于某个值（比如 5 秒）继续下一步，否则持续重试这一步；
2. 把主库 A 改成只读状态，即把 readonly 设置为 true；
3. 判断备库 B 的 seconds_behind_master 的值，直到这个值变成 0 为止；
4. 把备库 B 改成可读写状态，也就是把 readonly 设置为 false；
5. 把业务请求切到备库 B。

这个切换流程，一般是由专门的 HA 系统来完成的，我们暂时称之为可靠性优先流程。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/54f4c7c31e6f0f807c2ab77f78c8844a-1584367397422.png)

图 2 MySQL 可靠性优先主备切换流程

备注：图中的 SBM，是 seconds_behind_master 参数的简写。

可以看到，这个切换流程中是有不可用时间的。因为在步骤 2 之后，主库 A 和备库 B 都处于 readonly 状态，也就是说这时系统处于不可写状态，直到步骤 5 完成后才能恢复。

在这个不可用状态中，比较耗费时间的是步骤 3，可能需要耗费好几秒的时间。这也是为什么需要在步骤 1 先做判断，确保 seconds_behind_master 的值足够小。

试想如果一开始主备延迟就长达 30 分钟，而不先做判断直接切换的话，系统的不可用时间就会长达 30 分钟，这种情况一般业务都是不可接受的。

当然，系统的不可用时间，是由这个数据可靠性优先的策略决定的。你也可以选择可用性优先的策略，来把这个不可用时间几乎降为 0。

#### 可用性优先策略

如果我强行把步骤 4、5 调整到最开始执行，也就是说不等主备数据同步，直接把连接切到备库 B，并且让备库 B 可以读写，那么系统几乎就没有不可用时间了。

我们把这个切换流程，暂时称作可用性优先流程。这个切换流程的代价，就是可能出现数据不一致的情况。

接下来，我就和你分享一个可用性优先流程产生数据不一致的例子。假设有一个表 t：

```sql
mysql> CREATE TABLE `t` (
  `id` int(11) unsigned NOT NULL AUTO_INCREMENT,
  `c` int(11) unsigned DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB; 
insert into t(c) values(1),(2),(3);
```

这个表定义了一个自增主键 id，初始化数据后，主库和备库上都是 3 行数据。接下来，业务人员要继续在表 t 上执行两条插入语句的命令，依次是：

```scss
insert into t(c) values(4);
insert into t(c) values(5);
```

假设，现在主库上其他的数据表有大量的更新，导致主备延迟达到 5 秒。在插入一条 c=4 的语句后，发起了主备切换。

图 3 是**可用性优先策略，且 binlog_format=mixed**时的切换流程和数据结果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/3786bd6ad37faa34aca25bf1a1d8af3a-1584367397423.png)

图 3 可用性优先策略，且 binlog_format=mixed

现在，我们一起分析下这个切换流程：

1. 步骤 2 中，主库 A 执行完 insert 语句，插入了一行数据（4,4），之后开始进行主备切换。
2. 步骤 3 中，由于主备之间有 5 秒的延迟，所以备库 B 还没来得及应用“插入 c=4”这个中转日志，就开始接收客户端“插入 c=5”的命令。
3. 步骤 4 中，备库 B 插入了一行数据（4,5），并且把这个 binlog 发给主库 A。
4. 步骤 5 中，备库 B 执行“插入 c=4”这个中转日志，插入了一行数据（5,4）。而直接在备库 B 执行的“插入 c=5”这个语句，传到主库 A，就插入了一行新数据（5,5）。

最后的结果就是，主库 A 和备库 B 上出现了两行不一致的数据。可以看到，这个数据不一致，是由可用性优先流程导致的。

那么，如果我还是用**可用性优先策略，但设置 binlog_format=row**，情况又会怎样呢？

因为 row 格式在记录 binlog  的时候，会记录新插入的行的所有字段值，所以最后只会有一行不一致。而且，两边的主备同步的应用线程会报错 duplicate key error  并停止。也就是说，这种情况下，备库 B 的 (5,4) 和主库 A 的 (5,5) 这两行数据，都不会被对方执行。

图 4 中我画出了详细过程，你可以自己再分析一下。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/b8d2229b2b40dd087fd3b111d1bdda43-1584367397424.png)

图 4 可用性优先策略，且 binlog_format=row

从上面的分析中，你可以看到一些结论：

1. 使用 row 格式的 binlog 时，数据不一致的问题更容易被发现。而使用 mixed 或者 statement 格式的 binlog 时，数据很可能悄悄地就不一致了。如果你过了很久才发现数据不一致的问题，很可能这时的数据不一致已经不可查，或者连带造成了更多的数据逻辑不一致。
2. 主备切换的可用性优先策略会导致数据不一致。因此，大多数情况下，我都建议你使用可靠性优先策略。毕竟对数据服务来说的话，数据的可靠性一般还是要优于可用性的。

但事无绝对，**有没有哪种情况数据的可用性优先级更高呢？**

答案是，有的。

我曾经碰到过这样的一个场景：

- 有一个库的作用是记录操作日志。这时候，如果数据不一致可以通过 binlog 来修补，而这个短暂的不一致也不会引发业务问题。
- 同时，业务系统依赖于这个日志写入逻辑，如果这个库不可写，会导致线上的业务操作无法执行。

这时候，你可能就需要选择先强行切换，事后再补数据的策略。

当然，事后复盘的时候，我们想到了一个改进措施就是，让业务逻辑不要依赖于这类日志的写入。也就是说，日志写入这个逻辑模块应该可以降级，比如写到本地文件，或者写到另外一个临时库里面。

这样的话，这种场景就又可以使用可靠性优先策略了。

接下来我们再看看，**按照可靠性优先的思路，异常切换会是什么效果？**

假设，主库 A 和备库 B 间的主备延迟是 30 分钟，这时候主库 A 掉电了，HA 系统要切换 B 作为主库。我们在主动切换的时候，可以等到主备延迟小于 5 秒的时候再启动切换，但这时候已经别无选择了。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/553b7fc2d0dce3ec78bb595e1806eb8b-1584367397425.png)

图 5 可靠性优先策略，主库不可用

采用可靠性优先策略的话，你就必须得等到备库 B 的 seconds_behind_master=0  之后，才能切换。但现在的情况比刚刚更严重，并不是系统只读、不可写的问题了，而是系统处于完全不可用的状态。因为，主库 A  掉电后，我们的连接还没有切到备库 B。

你可能会问，那能不能直接切换到备库 B，但是保持 B 只读呢？

这样也不行。

因为，这段时间内，中转日志还没有应用完成，如果直接发起主备切换，客户端查询看不到之前执行完成的事务，会认为有“数据丢失”。

虽然随着中转日志的继续应用，这些数据会恢复回来，但是对于一些业务来说，查询到“暂时丢失数据的状态”也是不能被接受的。

聊到这里你就知道了，在满足数据可靠性的前提下，MySQL 高可用系统的可用性，是依赖于主备延迟的。延迟的时间越小，在主库故障的时候，服务恢复需要的时间就越短，可用性就越高。

#### 小结

今天这篇文章，我先和你介绍了 MySQL 高可用系统的基础，就是主备切换逻辑。紧接着，我又和你讨论了几种会导致主备延迟的情况，以及相应的改进方向。

然后，由于主备延迟的存在，切换策略就有不同的选择。所以，我又和你一起分析了可靠性优先和可用性优先策略的区别。

在实际的应用中，我更建议使用可靠性优先的策略。毕竟保证数据准确，应该是数据库服务的底线。在这个基础上，通过减少主备延迟，提升系统的可用性。

最后，我给你留下一个思考题吧。

一般现在的数据库运维系统都有备库延迟监控，其实就是在备库上执行 show slave status，采集 seconds_behind_master 的值。

假设，现在你看到你维护的一个备库，它的延迟监控的图像类似图 6，是一个 45°斜向上的线段，你觉得可能是什么原因导致呢？你又会怎么去确认这个原因呢？

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/cf5ea52aa3b26ef56c567125197fa171-1584367398739.png)

图 6 备库延迟

你可以把你的分析写在评论区，我会在下一篇文章的末尾跟你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

上期我留给你的问题是，什么情况下双 M 结构会出现循环复制。

一种场景是，在一个主库更新事务后，用命令 set global server_id=x 修改了 server_id。等日志再传回来的时候，发现 server_id 跟自己的 server_id 不同，就只能执行了。

另一种场景是，有三个节点的时候，如图 7 所示，trx1 是在节点 B 执行的，因此 binlog 上的 server_id 就是 B，binlog 传给节点 A，然后 A 和 A’搭建了双 M 结构，就会出现循环复制。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/f968192ce2f436c939dd702b8f409771-1584367398746.png)

图 7 三节点循环复制

这种三节点复制的场景，做数据库迁移的时候会出现。

如果出现了循环复制，可以在 A 或者 A’上，执行如下命令：

```vbnet
stop slave；
CHANGE MASTER TO IGNORE_SERVER_IDS=(server_id_of_B);
start slave;
```

这样这个节点收到日志后就不会再执行。过一段时间后，再执行下面的命令把这个值改回来。

```vbnet
stop slave；
CHANGE MASTER TO IGNORE_SERVER_IDS=();
start slave;
```

评论区留言点赞板：

> @一大只、@HuaMax 同学提到了第一个复现方法；

> @Jonh 同学提到了 IGNORE_SERVER_IDS 这个解决方法；

> @React 提到，如果主备设置不同的步长，备库是不是可以设置为可读写。我的建议是，只要这个节点设计内就不会有业务直接在上面执行更新，就建议设置为 readonly。



### 27 主库出问题了，从库怎么办？

在前面的第[24]、[25]和[26]篇文章中，我和你介绍了 MySQL 主备复制的基础结构，但这些都是一主一备的结构。

大多数的互联网应用场景都是读多写少，因此你负责的业务，在发展过程中很可能先会遇到读性能的问题。而在数据库层解决读性能问题，就要涉及到接下来两篇文章要讨论的架构：一主多从。

今天这篇文章，我们就先聊聊一主多从的切换正确性。然后，我们在下一篇文章中再聊聊解决一主多从的查询逻辑正确性的方法。

如图 1 所示，就是一个基本的一主多从结构。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/aadb3b956d1ffc13ac46515a7d619e79-1584367399405.png)

图 1 一主多从基本结构

图中，虚线箭头表示的是主备关系，也就是 A 和 A’互为主备， 从库 B、C、D 指向的是主库 A。一主多从的设置，一般用于读写分离，主库负责所有的写入和一部分读，其他的读请求则由从库分担。

今天我们要讨论的就是，在一主多从架构下，主库故障后的主备切换问题。

如图 2 所示，就是主库发生故障，主备切换后的结果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/0014f97423bd75235a9187f492fb2453-1584367399531.png)

图 2 一主多从基本结构 -- 主备切换

相比于一主一备的切换流程，一主多从结构在切换完成后，A’会成为新的主库，从库 B、C、D 也要改接到 A’。正是由于多了从库 B、C、D 重新指向的这个过程，所以主备切换的复杂性也相应增加了。

接下来，我们再一起看看一个切换系统会怎么完成一主多从的主备切换过程。

#### 基于位点的主备切换

这里，我们需要先来回顾一个知识点。

当我们把节点 B 设置成节点 A’的从库的时候，需要执行一条 change master 命令：

```bash
CHANGE MASTER TO 
MASTER_HOST=$host_name 
MASTER_PORT=$port 
MASTER_USER=$user_name 
MASTER_PASSWORD=$password 
MASTER_LOG_FILE=$master_log_name 
MASTER_LOG_POS=$master_log_pos  
```

这条命令有这么 6 个参数：

- MASTER_HOST、MASTER_PORT、MASTER_USER 和 MASTER_PASSWORD 四个参数，分别代表了主库 A’的 IP、端口、用户名和密码。
- 最后两个参数 MASTER_LOG_FILE 和 MASTER_LOG_POS 表示，要从主库的 master_log_name 文件的 master_log_pos 这个位置的日志继续同步。而这个位置就是我们所说的同步位点，也就是主库对应的文件名和日志偏移量。

那么，这里就有一个问题了，节点 B 要设置成 A’的从库，就要执行 change master 命令，就不可避免地要设置位点的这两个参数，但是这两个参数到底应该怎么设置呢？

原来节点 B 是 A 的从库，本地记录的也是 A 的位点。但是相同的日志，A 的位点和 A’的位点是不同的。因此，从库 B 要切换的时候，就需要先经过“找同步位点”这个逻辑。

这个位点很难精确取到，只能取一个大概位置。为什么这么说呢？

我来和你分析一下看看这个位点一般是怎么获取到的，你就清楚其中不精确的原因了。

考虑到切换过程中不能丢数据，所以我们找位点的时候，总是要找一个“稍微往前”的，然后再通过判断跳过那些在从库 B 上已经执行过的事务。

一种取同步位点的方法是这样的：

1. 等待新主库 A’把中转日志（relay log）全部同步完成；
2. 在 A’上执行 show master status 命令，得到当前 A’上最新的 File 和 Position；
3. 取原主库 A 故障的时刻 T；
4. 用 mysqlbinlog 工具解析 A’的 File，得到 T 时刻的位点。

```r
mysqlbinlog File --stop-datetime=T --start-datetime=T
```

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/3471dfe4aebcccfaec0523a08cdd0ddd-1584367399747.png)

图 3 mysqlbinlog 部分输出结果

图中，end_log_pos 后面的值“123”，表示的就是 A’这个实例，在 T 时刻写入新的 binlog 的位置。然后，我们就可以把 123 这个值作为 $master_log_pos ，用在节点 B 的 change master 命令里。

当然这个值并不精确。为什么呢？

你可以设想有这么一种情况，假设在 T 这个时刻，主库 A 已经执行完成了一个 insert 语句插入了一行数据 R，并且已经将 binlog 传给了 A’和 B，然后在传完的瞬间主库 A 的主机就掉电了。

那么，这时候系统的状态是这样的：

1. 在从库 B 上，由于同步了 binlog， R 这一行已经存在；
2. 在新主库 A’上， R 这一行也已经存在，日志是写在 123 这个位置之后的；
3. 我们在从库 B 上执行 change master 命令，指向 A’的 File 文件的 123 位置，就会把插入 R 这一行数据的 binlog 又同步到从库 B 去执行。

这时候，从库 B 的同步线程就会报告 Duplicate entry ‘id_of_R’ for key ‘PRIMARY’ 错误，提示出现了主键冲突，然后停止同步。

所以，**通常情况下，我们在切换任务的时候，要先主动跳过这些错误，有两种常用的方法。**

**一种做法是**，主动跳过一个事务。跳过命令的写法是：

```sql
set global sql_slave_skip_counter=1;
start slave;
```

因为切换过程中，可能会不止重复执行一个事务，所以我们需要在从库 B 刚开始接到新主库 A’时，持续观察，每次碰到这些错误就停下来，执行一次跳过命令，直到不再出现停下来的情况，以此来跳过可能涉及的所有事务。

**另外一种方式是，**通过设置 slave_skip_errors 参数，直接设置跳过指定的错误。

在执行主备切换时，有这么两类错误，是经常会遇到的：

- 1062 错误是插入数据时唯一键冲突；
- 1032 错误是删除数据时找不到行。

因此，我们可以把 slave_skip_errors 设置为 “1032,1062”，这样中间碰到这两个错误时就直接跳过。

这里需要注意的是，这种直接跳过指定错误的方法，针对的是主备切换时，由于找不到精确的同步位点，所以只能采用这种方法来创建从库和新主库的主备关系。

这个背景是，我们很清楚在主备切换过程中，直接跳过 1032 和 1062 这两类错误是无损的，所以才可以这么设置  slave_skip_errors  参数。等到主备间的同步关系建立完成，并稳定执行一段时间之后，我们还需要把这个参数设置为空，以免之后真的出现了主从数据不一致，也跳过了。

#### GTID

通过 sql_slave_skip_counter 跳过事务和通过 slave_skip_errors  忽略错误的方法，虽然都最终可以建立从库 B 和新主库 A’的主备关系，但这两种操作都很复杂，而且容易出错。所以，MySQL 5.6 版本引入了  GTID，彻底解决了这个困难。

那么，GTID 到底是什么意思，又是如何解决找同步位点这个问题呢？现在，我就和你简单介绍一下。

GTID 的全称是 Global Transaction Identifier，也就是全局事务 ID，是一个事务在提交的时候生成的，是这个事务的唯一标识。它由两部分组成，格式是：

```ini
GTID=server_uuid:gno
```

其中：

- server_uuid 是一个实例第一次启动时自动生成的，是一个全局唯一的值；
- gno 是一个整数，初始值是 1，每次提交事务的时候分配给这个事务，并加 1。

这里我需要和你说明一下，在 MySQL 的官方文档里，GTID 格式是这么定义的：

```ini
GTID=source_id:transaction_id
```

这里的 source_id 就是 server_uuid；而后面的这个 transaction_id，我觉得容易造成误导，所以我改成了 gno。为什么说使用 transaction_id 容易造成误解呢？

因为，在 MySQL 里面我们说 transaction_id 就是指事务 id，事务 id 是在事务执行过程中分配的，如果这个事务回滚了，事务 id 也会递增，而 gno 是在事务提交的时候才会分配。

从效果上看，GTID 往往是连续的，因此我们用 gno 来表示更容易理解。

GTID 模式的启动也很简单，我们只需要在启动一个 MySQL 实例的时候，加上参数 gtid_mode=on 和 enforce_gtid_consistency=on 就可以了。

在 GTID 模式下，每个事务都会跟一个 GTID 一一对应。这个 GTID 有两种生成方式，而使用哪种方式取决于 session 变量 gtid_next 的值。

1. 如果 gtid_next=automatic，代表使用默认值。这时，MySQL 就会把 server_uuid:gno 分配给这个事务。 a. 记录 binlog 的时候，先记录一行 SET @@SESSION.GTID_NEXT=‘server_uuid:gno’; b.  把这个 GTID 加入本实例的 GTID 集合。
2. 如果 gtid_next 是一个指定的 GTID 的值，比如通过 set gtid_next='current_gtid’指定为  current_gtid，那么就有两种可能： a. 如果 current_gtid 已经存在于实例的 GTID  集合中，接下来执行的这个事务会直接被系统忽略； b. 如果 current_gtid 没有存在于实例的 GTID 集合中，就将这个  current_gtid 分配给接下来要执行的事务，也就是说系统不需要给这个事务生成新的 GTID，因此 gno 也不用加 1。

注意，一个 current_gtid 只能给一个事务使用。这个事务提交后，如果要执行下一个事务，就要执行 set 命令，把 gtid_next 设置成另外一个 gtid 或者 automatic。

这样，每个 MySQL 实例都维护了一个 GTID 集合，用来对应“这个实例执行过的所有事务”。

这样看上去不太容易理解，接下来我就用一个简单的例子，来和你说明 GTID 的基本用法。

我们在实例 X 中创建一个表 t。

```sql
CREATE TABLE `t` (
  `id` int(11) NOT NULL,
  `c` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB; 
insert into t values(1,1);
```

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/28a5cab0079fb12fd5abecd92b3324c2-1584367399789.png)

图 4 初始化数据的 binlog

可以看到，事务的 BEGIN 之前有一条 SET @@SESSION.GTID_NEXT 命令。这时，如果实例 X 有从库，那么将  CREATE TABLE 和 insert 语句的 binlog 同步过去执行的话，执行事务之前就会先执行这两个 SET 命令，  这样被加入从库的 GTID 集合的，就是图中的这两个 GTID。

假设，现在这个实例 X 是另外一个实例 Y 的从库，并且此时在实例 Y 上执行了下面这条插入语句：

```sql
insert into t values(1,1);
```

并且，这条语句在实例 Y 上的 GTID 是 “aaaaaaaa-cccc-dddd-eeee-ffffffffffff:10”。

那么，实例 X 作为 Y 的从库，就要同步这个事务过来执行，显然会出现主键冲突，导致实例 X 的同步线程停止。这时，我们应该怎么处理呢？

处理方法就是，你可以执行下面的这个语句序列：

```sql
set gtid_next='aaaaaaaa-cccc-dddd-eeee-ffffffffffff:10';
begin;
commit;
set gtid_next=automatic;
start slave;
```

其中，前三条语句的作用，是通过提交一个空事务，把这个 GTID 加到实例 X 的 GTID 集合中。如图 5 所示，就是执行完这个空事务之后的 show master status 的结果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/c8d3299ece7d583a3ecd1557851ed157-1584367399827.png)

图 5 show master status 结果

可以看到实例 X 的 Executed_Gtid_set 里面，已经加入了这个 GTID。

这样，我再执行 start slave 命令让同步线程执行起来的时候，虽然实例 X 上还是会继续执行实例 Y  传过来的事务，但是由于“aaaaaaaa-cccc-dddd-eeee-ffffffffffff:10”已经存在于实例 X 的 GTID  集合中了，所以实例 X 就会直接跳过这个事务，也就不会再出现主键冲突的错误。

在上面的这个语句序列中，start slave 命令之前还有一句 set gtid_next=automatic。这句话的作用是“恢复 GTID 的默认分配行为”，也就是说如果之后有新的事务再执行，就还是按照原来的分配方式，继续分配 gno=3。

#### 基于 GTID 的主备切换

现在，我们已经理解 GTID 的概念，再一起来看看基于 GTID 的主备复制的用法。

在 GTID 模式下，备库 B 要设置为新主库 A’的从库的语法如下：

```makefile
CHANGE MASTER TO 
MASTER_HOST=$host_name 
MASTER_PORT=$port 
MASTER_USER=$user_name 
MASTER_PASSWORD=$password 
master_auto_position=1 
```

其中，master_auto_position=1 就表示这个主备关系使用的是 GTID 协议。可以看到，前面让我们头疼不已的 MASTER_LOG_FILE 和 MASTER_LOG_POS 参数，已经不需要指定了。

我们把现在这个时刻，实例 A’的 GTID 集合记为 set_a，实例 B 的 GTID 集合记为 set_b。接下来，我们就看看现在的主备切换逻辑。

我们在实例 B 上执行 start slave 命令，取 binlog 的逻辑是这样的：

1. 实例 B 指定主库 A’，基于主备协议建立连接。
2. 实例 B 把 set_b 发给主库 A’。
3. 实例 A’算出 set_a 与 set_b 的差集，也就是所有存在于 set_a，但是不存在于 set_b 的 GITD 的集合，判断  A’本地是否包含了这个差集需要的所有 binlog 事务。 a. 如果不包含，表示 A’已经把实例 B 需要的 binlog  给删掉了，直接返回错误； b. 如果确认全部包含，A’从自己的 binlog 文件里面，找出第一个不在 set_b 的事务，发给 B；
4. 之后就从这个事务开始，往后读文件，按顺序取 binlog 发给 B 去执行。

其实，这个逻辑里面包含了一个设计思想：在基于 GTID 的主备关系里，系统认为只要建立主备关系，就必须保证主库发给备库的日志是完整的。因此，如果实例 B 需要的日志已经不存在，A’就拒绝把日志发给 B。

这跟基于位点的主备协议不同。基于位点的协议，是由备库决定的，备库指定哪个位点，主库就发哪个位点，不做日志的完整性判断。

基于上面的介绍，我们再来看看引入 GTID 后，一主多从的切换场景下，主备切换是如何实现的。

由于不需要找位点了，所以从库 B、C、D 只需要分别执行 change master 命令指向实例 A’即可。

其实，严谨地说，主备切换不是不需要找位点了，而是找位点这个工作，在实例 A’内部就已经自动完成了。但由于这个工作是自动的，所以对 HA 系统的开发人员来说，非常友好。

之后这个系统就由新主库 A’写入，主库 A’的自己生成的 binlog 中的 GTID 集合格式是：server_uuid_of_A’:1-M。

如果之前从库 B 的 GTID 集合格式是 server_uuid_of_A:1-N， 那么切换之后 GTID 集合的格式就变成了 server_uuid_of_A:1-N, server_uuid_of_A’:1-M。

当然，主库 A’之前也是 A 的备库，因此主库 A’和从库 B 的 GTID 集合是一样的。这就达到了我们预期。

#### GTID 和在线 DDL

接下来，我再举个例子帮你理解 GTID。

之前在第 22 篇文章[《MySQL  有哪些“饮鸩止渴”提高性能的方法？》]中，我和你提到业务高峰期的慢查询性能问题时，分析到如果是由于索引缺失引起的性能问题，我们可以通过在线加索引来解决。但是，考虑到要避免新增索引对主库性能造成的影响，我们可以先在备库加索引，然后再切换。

当时我说，在双 M 结构下，备库执行的 DDL 语句也会传给主库，为了避免传回后对主库造成影响，要通过 set sql_log_bin=off 关掉 binlog。

评论区有位同学提出了一个问题：这样操作的话，数据库里面是加了索引，但是 binlog 并没有记录下这一个更新，是不是会导致数据和日志不一致？

这个问题提得非常好。当时，我在留言的回复中就引用了 GTID 来说明。今天，我再和你展开说明一下。

假设，这两个互为主备关系的库还是实例 X 和实例 Y，且当前主库是 X，并且都打开了 GTID 模式。这时的主备切换流程可以变成下面这样：

- 在实例 X 上执行 stop slave。
- 在实例 Y 上执行 DDL 语句。注意，这里并不需要关闭 binlog。
- 执行完成后，查出这个 DDL 语句对应的 GTID，并记为 server_uuid_of_Y:gno。
- 到实例 X 上执行以下语句序列：

```sql
set GTID_NEXT="server_uuid_of_Y:gno";
begin;
commit;
set gtid_next=automatic;
start slave;
```

这样做的目的在于，既可以让实例 Y 的更新有 binlog 记录，同时也可以确保不会在实例 X 上执行这条更新。

- 接下来，执行完主备切换，然后照着上述流程再执行一遍即可。

#### 小结

在今天这篇文章中，我先和你介绍了一主多从的主备切换流程。在这个过程中，从库找新主库的位点是一个痛点。由此，我们引出了 MySQL 5.6 版本引入的 GTID 模式，介绍了 GTID 的基本概念和用法。

可以看到，在 GTID 模式下，一主多从切换就非常方便了。

因此，如果你使用的 MySQL 版本支持 GTID 的话，我都建议你尽量使用 GTID 模式来做一主多从的切换。

在下一篇文章中，我们还能看到 GTID 模式在读写分离场景的应用。

最后，又到了我们的思考题时间。

你在 GTID 模式下设置主从关系的时候，从库执行 start slave 命令后，主库发现需要的 binlog 已经被删除掉了，导致主备创建不成功。这种情况下，你觉得可以怎么处理呢？

你可以把你的方法写在留言区，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

上一篇文章最后，我给你留的问题是，如果主库都是单线程压力模式，在从库追主库的过程中，binlog-transaction-dependency-tracking 应该选用什么参数？

这个问题的答案是，应该将这个参数设置为 WRITESET。

由于主库是单线程压力模式，所以每个事务的 commit_id 都不同，那么设置为 COMMIT_ORDER 模式的话，从库也只能单线程执行。

同样地，由于 WRITESET_SESSION 模式要求在备库应用日志的时候，同一个线程的日志必须与主库上执行的先后顺序相同，也会导致主库单线程压力模式下退化成单线程复制。

所以，应该将 binlog-transaction-dependency-tracking 设置为 WRITESET。

**评论区留言点赞板：**

> @慧鑫 coming 问了一个好问题，对同一行作更新的几个事务，如果 commit_id  相同，是不是在备库并行执行的时候会导致数据不一致？这个问题的答案是更新同一行的事务是不可能同时进入 commit 状态的。 @老杨同志  对这个问题给出了更详细的回答，大家可以去看一下。

### 28 读写分离有哪些坑？

在上一篇文章中，我和你介绍了一主多从的结构以及切换流程。今天我们就继续聊聊一主多从架构的应用场景：读写分离，以及怎么处理主备延迟导致的读写分离问题。

我们在上一篇文章中提到的一主多从的结构，其实就是读写分离的基本结构了。这里，我再把这张图贴过来，方便你理解。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/1334b9c08b8fd837832fdb2d82e6b0aa-1584367399834.png)

图 1 读写分离基本结构

读写分离的主要目标就是分摊主库的压力。图 1 中的结构是客户端（client）主动做负载均衡，这种模式下一般会把数据库的连接信息放在客户端的连接层。也就是说，由客户端来选择后端数据库进行查询。

还有一种架构是，在 MySQL 和客户端之间有一个中间代理层 proxy，客户端只连接 proxy， 由 proxy 根据请求类型和上下文决定请求的分发路由。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/065ef246c59019effc8384967d774318-1584367399845.png)

图 2 带 proxy 的读写分离架构

接下来，我们就看一下客户端直连和带 proxy 的读写分离架构，各有哪些特点。

1. 客户端直连方案，因为少了一层 proxy  转发，所以查询性能稍微好一点儿，并且整体架构简单，排查问题更方便。但是这种方案，由于要了解后端部署细节，所以在出现主备切换、库迁移等操作的时候，客户端都会感知到，并且需要调整数据库连接信息。 你可能会觉得这样客户端也太麻烦了，信息大量冗余，架构很丑。其实也未必，一般采用这样的架构，一定会伴随一个负责管理后端的组件，比如  Zookeeper，尽量让业务端只专注于业务逻辑开发。
2. 带 proxy 的架构，对客户端比较友好。客户端不需要关注后端细节，连接维护、后端信息维护等工作，都是由 proxy 完成的。但这样的话，对后端维护团队的要求会更高。而且，proxy 也需要有高可用架构。因此，带 proxy 架构的整体就相对比较复杂。

理解了这两种方案的优劣，具体选择哪个方案就取决于数据库团队提供的能力了。但目前看，趋势是往带 proxy 的架构方向发展的。

但是，不论使用哪种架构，你都会碰到我们今天要讨论的问题：由于主从可能存在延迟，客户端执行完一个更新事务后马上发起查询，如果查询选择的是从库的话，就有可能读到刚刚的事务更新之前的状态。

**这种“在从库上会读到系统的一个过期状态”的现象，在这篇文章里，我们暂且称之为“过期读”。**

前面我们说过了几种可能导致主备延迟的原因，以及对应的优化策略，但是主从延迟还是不能 100% 避免的。

不论哪种结构，客户端都希望查询从库的数据结果，跟查主库的数据结果是一样的。

接下来，我们就来讨论怎么处理过期读问题。

这里，我先把文章中涉及到的处理过期读的方案汇总在这里，以帮助你更好地理解和掌握全文的知识脉络。这些方案包括：

- 强制走主库方案；
- sleep 方案；
- 判断主备无延迟方案；
- 配合 semi-sync 方案；
- 等主库位点方案；
- 等 GTID 方案。

#### 强制走主库方案

强制走主库方案其实就是，将查询请求做分类。通常情况下，我们可以将查询请求分为这么两类：

1. 对于必须要拿到最新结果的请求，强制将其发到主库上。比如，在一个交易平台上，卖家发布商品以后，马上要返回主页面，看商品是否发布成功。那么，这个请求需要拿到最新的结果，就必须走主库。
2. 对于可以读到旧数据的请求，才将其发到从库上。在这个交易平台上，买家来逛商铺页面，就算晚几秒看到最新发布的商品，也是可以接受的。那么，这类请求就可以走从库。

你可能会说，这个方案是不是有点畏难和取巧的意思，但其实这个方案是用得最多的。

当然，这个方案最大的问题在于，有时候你会碰到“所有查询都不能是过期读”的需求，比如一些金融类的业务。这样的话，你就要放弃读写分离，所有读写压力都在主库，等同于放弃了扩展性。

因此接下来，我们来讨论的话题是：可以支持读写分离的场景下，有哪些解决过期读的方案，并分析各个方案的优缺点。

#### Sleep 方案

主库更新后，读从库之前先 sleep 一下。具体的方案就是，类似于执行一条 select sleep(1) 命令。

这个方案的假设是，大多数情况下主备延迟在 1 秒之内，做一个 sleep 可以有很大概率拿到最新的数据。

这个方案给你的第一感觉，很可能是不靠谱儿，应该不会有人用吧？并且，你还可能会说，直接在发起查询时先执行一条 sleep 语句，用户体验很不友好啊。

但，这个思路确实可以在一定程度上解决问题。为了看起来更靠谱儿，我们可以换一种方式。

以卖家发布商品为例，商品发布后，用 Ajax（Asynchronous JavaScript + XML，异步 JavaScript 和 XML）直接把客户端输入的内容作为“新的商品”显示在页面上，而不是真正地去数据库做查询。

这样，卖家就可以通过这个显示，来确认产品已经发布成功了。等到卖家再刷新页面，去查看商品的时候，其实已经过了一段时间，也就达到了 sleep 的目的，进而也就解决了过期读的问题。

也就是说，这个 sleep 方案确实解决了类似场景下的过期读问题。但，从严格意义上来说，这个方案存在的问题就是不精确。这个不精确包含了两层意思：

1. 如果这个查询请求本来 0.5 秒就可以在从库上拿到正确结果，也会等 1 秒；
2. 如果延迟超过 1 秒，还是会出现过期读。

看到这里，你是不是有一种“你是不是在逗我”的感觉，这个改进方案虽然可以解决类似 Ajax 场景下的过期读问题，但还是怎么看都不靠谱儿。别着急，接下来我就和你介绍一些更准确的方案。

#### 判断主备无延迟方案

要确保备库无延迟，通常有三种做法。

通过前面的[第 25 篇]文章，我们知道 show slave status 结果里的 seconds_behind_master 参数的值，可以用来衡量主备延迟时间的长短。

所以**第一种确保主备无延迟的方法是，**每次从库执行查询请求前，先判断 seconds_behind_master 是否已经等于 0。如果还不等于 0 ，那就必须等到这个参数变为 0 才能执行查询请求。

seconds_behind_master 的单位是秒，如果你觉得精度不够的话，还可以采用对比位点和 GTID 的方法来确保主备无延迟，也就是我们接下来要说的第二和第三种方法。

如图 3 所示，是一个 show slave status 结果的部分截图。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/00110923007513e865d7f43a124887c1-1584367399854.png)

图 3 show slave status 结果

现在，我们就通过这个结果，来看看具体如何通过对比位点和 GTID 来确保主备无延迟。

**第二种方法，**对比位点确保主备无延迟：

- Master_Log_File 和 Read_Master_Log_Pos，表示的是读到的主库的最新位点；
- Relay_Master_Log_File 和 Exec_Master_Log_Pos，表示的是备库执行的最新位点。

如果 Master_Log_File 和 Relay_Master_Log_File、Read_Master_Log_Pos 和 Exec_Master_Log_Pos 这两组值完全相同，就表示接收到的日志已经同步完成。

**第三种方法，**对比 GTID 集合确保主备无延迟：

- Auto_Position=1 ，表示这对主备关系使用了 GTID 协议。
- Retrieved_Gtid_Set，是备库收到的所有日志的 GTID 集合；
- Executed_Gtid_Set，是备库所有已经执行完成的 GTID 集合。

如果这两个集合相同，也表示备库接收到的日志都已经同步完成。

可见，对比位点和对比 GTID 这两种方法，都要比判断 seconds_behind_master 是否为 0 更准确。

在执行查询请求之前，先判断从库是否同步完成的方法，相比于 sleep 方案，准确度确实提升了不少，但还是没有达到“精确”的程度。为什么这么说呢？

我们现在一起来回顾下，一个事务的 binlog 在主备库之间的状态：

1. 主库执行完成，写入 binlog，并反馈给客户端；
2. binlog 被从主库发送给备库，备库收到；
3. 在备库执行 binlog 完成。

我们上面判断主备无延迟的逻辑，是“备库收到的日志都执行完成了”。但是，从 binlog 在主备之间状态的分析中，不难看出还有一部分日志，处于客户端已经收到提交确认，而备库还没收到日志的状态。

如图 4 所示就是这样的一个状态。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/557445207b57d6c0f2747509d7d6619e-1584367399858.png)

图 4 备库还没收到 trx3

这时，主库上执行完成了三个事务 trx1、trx2 和 trx3，其中：

1. trx1 和 trx2 已经传到从库，并且已经执行完成了；
2. trx3 在主库执行完成，并且已经回复给客户端，但是还没有传到从库中。

如果这时候你在从库 B 上执行查询请求，按照我们上面的逻辑，从库认为已经没有同步延迟，但还是查不到 trx3 的。严格地说，就是出现了过期读。

那么，这个问题有没有办法解决呢？

#### 配合 semi-sync

要解决这个问题，就要引入半同步复制，也就是 semi-sync replication。

semi-sync 做了这样的设计：

1. 事务提交的时候，主库把 binlog 发给从库；
2. 从库收到 binlog 以后，发回给主库一个 ack，表示收到了；
3. 主库收到这个 ack 以后，才能给客户端返回“事务完成”的确认。

也就是说，如果启用了 semi-sync，就表示所有给客户端发送过确认的事务，都确保了备库已经收到了这个日志。

在[第 25 篇文章]的评论区，有同学问到：如果主库掉电的时候，有些 binlog 还来不及发给从库，会不会导致系统数据丢失？

答案是，如果使用的是普通的异步复制模式，就可能会丢失，但 semi-sync 就可以解决这个问题。

这样，semi-sync 配合前面关于位点的判断，就能够确定在从库上执行的查询请求，可以避免过期读。

但是，semi-sync+ 位点判断的方案，只对一主一备的场景是成立的。在一主多从场景中，主库只要等到一个从库的 ack，就开始给客户端返回确认。这时，在从库上执行查询请求，就有两种情况：

1. 如果查询是落在这个响应了 ack 的从库上，是能够确保读到最新数据；
2. 但如果是查询落到其他从库上，它们可能还没有收到最新的日志，就会产生过期读的问题。

其实，判断同步位点的方案还有另外一个潜在的问题，即：如果在业务更新的高峰期，主库的位点或者 GTID 集合更新很快，那么上面的两个位点等值判断就会一直不成立，很可能出现从库上迟迟无法响应查询请求的情况。

实际上，回到我们最初的业务逻辑里，当发起一个查询请求以后，我们要得到准确的结果，其实并不需要等到“主备完全同步”。

为什么这么说呢？我们来看一下这个时序图。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/9cf54f3e91dc8f7b8947d7d8e384aa09-1584367399864.png)

图 5 主备持续延迟一个事务

图 5 所示，就是等待位点方案的一个 bad case。图中备库 B 下的虚线框，分别表示 relaylog 和 binlog 中的事务。可以看到，图 5 中从状态 1 到状态 4，一直处于延迟一个事务的状态。

备库 B 一直到状态 4 都和主库 A 存在延迟，如果用上面必须等到无延迟才能查询的方案，select 语句直到状态 4 都不能被执行。

但是，其实客户端是在发完 trx1 更新后发起的 select 语句，我们只需要确保 trx1 已经执行完成就可以执行 select 语句了。也就是说，如果在状态 3 执行查询请求，得到的就是预期结果了。

到这里，我们小结一下，semi-sync 配合判断主备无延迟的方案，存在两个问题：

1. 一主多从的时候，在某些从库执行查询请求会存在过期读的现象；
2. 在持续延迟的情况下，可能出现过度等待的问题。

接下来，我要和你介绍的等主库位点方案，就可以解决这两个问题。

#### 等主库位点方案

要理解等主库位点方案，我需要先和你介绍一条命令：

```csharp
select master_pos_wait(file, pos[, timeout]);
```

这条命令的逻辑如下：

1. 它是在从库执行的；
2. 参数 file 和 pos 指的是主库上的文件名和位置；
3. timeout 可选，设置为正整数 N 表示这个函数最多等待 N 秒。

这个命令正常返回的结果是一个正整数 M，表示从命令开始执行，到应用完 file 和 pos 表示的 binlog 位置，执行了多少事务。

当然，除了正常返回一个正整数 M 外，这条命令还会返回一些其他结果，包括：

1. 如果执行期间，备库同步线程发生异常，则返回 NULL；
2. 如果等待超过 N 秒，就返回 -1；
3. 如果刚开始执行的时候，就发现已经执行过这个位置了，则返回 0。

对于图 5 中先执行 trx1，再执行一个查询请求的逻辑，要保证能够查到正确的数据，我们可以使用这个逻辑：

1. trx1 事务更新完成后，马上执行 show master status 得到当前主库执行到的 File 和 Position；
2. 选定一个从库执行查询语句；
3. 在从库上执行 select master_pos_wait(File, Position, 1)；
4. 如果返回值是 >=0 的正整数，则在这个从库执行查询语句；
5. 否则，到主库执行查询语句。

我把上面这个流程画出来。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/b20ae91ea46803df1b63ed683e1de357-1584367399926.png)

图 6 master_pos_wait 方案

这里我们假设，这条 select 查询最多在从库上等待 1 秒。那么，如果 1 秒内 master_pos_wait 返回一个大于等于 0 的整数，就确保了从库上执行的这个查询结果一定包含了 trx1 的数据。

步骤 5 到主库执行查询语句，是这类方案常用的退化机制。因为从库的延迟时间不可控，不能无限等待，所以如果等待超时，就应该放弃，然后到主库去查。

你可能会说，如果所有的从库都延迟超过 1 秒了，那查询压力不就都跑到主库上了吗？确实是这样。

但是，按照我们设定不允许过期读的要求，就只有两种选择，一种是超时放弃，一种是转到主库查询。具体怎么选择，就需要业务开发同学做好限流策略了。

#### GTID 方案

如果你的数据库开启了 GTID 模式，对应的也有等待 GTID 的方案。

MySQL 中同样提供了一个类似的命令：

```csharp
 select wait_for_executed_gtid_set(gtid_set, 1);
```

这条命令的逻辑是：

1. 等待，直到这个库执行的事务中包含传入的 gtid_set，返回 0；
2. 超时返回 1。

在前面等位点的方案中，我们执行完事务后，还要主动去主库执行 show master status。而 MySQL 5.7.6 版本开始，允许在执行完更新类事务后，把这个事务的 GTID 返回给客户端，这样等 GTID 的方案就可以减少一次查询。

这时，等 GTID 的执行流程就变成了：

1. trx1 事务更新完成后，从返回包直接获取这个事务的 GTID，记为 gtid1；
2. 选定一个从库执行查询语句；
3. 在从库上执行 select wait_for_executed_gtid_set(gtid1, 1)；
4. 如果返回值是 0，则在这个从库执行查询语句；
5. 否则，到主库执行查询语句。

跟等主库位点的方案一样，等待超时后是否直接到主库查询，需要业务开发同学来做限流考虑。

我把这个流程图画出来。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/d521de8017297aff59db2f68170ee739-1584367399972.png)

图 7 wait_for_executed_gtid_set 方案

在上面的第一步中，trx1 事务更新完成后，从返回包直接获取这个事务的 GTID。问题是，怎么能够让 MySQL 在执行事务后，返回包中带上 GTID 呢？

你只需要将参数 session_track_gtids 设置为 OWN_GTID，然后通过 API 接口 mysql_session_track_get_first 从返回包解析出 GTID 的值即可。

在专栏的[第一篇文章]中，我介绍 mysql_reset_connection 的时候，评论区有同学留言问这类接口应该怎么使用。

这里我再回答一下。其实，MySQL 并没有提供这类接口的 SQL 用法，是提供给程序的 API(https://dev.mysql.com/doc/refman/5.7/en/c-api-functions.html)。

比如，为了让客户端在事务提交后，返回的 GITD 能够在客户端显示出来，我对 MySQL 客户端代码做了点修改，如下所示：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/973bdd8741f830acebe005cbf37a7663-1584367400038.png)

图 8 显示更新事务的 GTID-- 代码

这样，就可以看到语句执行完成，显示出 GITD 的值。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/253106d31d9d97aaa2846b2015f593fe-1584367400043.png)

图 9 显示更新事务的 GTID-- 效果

当然了，这只是一个例子。你要使用这个方案的时候，还是应该在你的客户端代码中调用 mysql_session_track_get_first 这个函数。

#### 小结

在今天这篇文章中，我跟你介绍了一主多从做读写分离时，可能碰到过期读的原因，以及几种应对的方案。

这几种方案中，有的方案看上去是做了妥协，有的方案看上去不那么靠谱儿，但都是有实际应用场景的，你需要根据业务需求选择。

即使是最后等待位点和等待 GTID 这两个方案，虽然看上去比较靠谱儿，但仍然存在需要权衡的情况。如果所有的从库都延迟，那么请求就会全部落到主库上，这时候会不会由于压力突然增大，把主库打挂了呢？

其实，在实际应用中，这几个方案是可以混合使用的。

比如，先在客户端对请求做分类，区分哪些请求可以接受过期读，而哪些请求完全不能接受过期读；然后，对于不能接受过期读的语句，再使用等 GTID 或等位点的方案。

但话说回来，过期读在本质上是由一写多读导致的。在实际应用中，可能会有别的不需要等待就可以水平扩展的数据库方案，但这往往是用牺牲写性能换来的，也就是需要在读性能和写性能中取权衡。

最后 ，我给你留下一个问题吧。

假设你的系统采用了我们文中介绍的最后一个方案，也就是等 GTID 的方案，现在你要对主库的一张大表做 DDL，可能会出现什么情况呢？为了避免这种情况，你会怎么做呢？

你可以把你的分析和方案设计写在评论区，我会在下一篇文章跟你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

上期给你留的问题是，在 GTID 模式下，如果一个新的从库接上主库，但是需要的 binlog 已经没了，要怎么做？

@某、人同学给了很详细的分析，我把他的回答略做修改贴过来。

1. 如果业务允许主从不一致的情况，那么可以在主库上先执行 show global variables like  ‘gtid_purged’，得到主库已经删除的 GTID 集合，假设是 gtid_purged1；然后先在从库上执行 reset  master，再执行 set global gtid_purged =‘gtid_purged1’；最后执行 start  slave，就会从主库现存的 binlog 开始同步。binlog 缺失的那一部分，数据在从库上就可能会有丢失，造成主从不一致。
2. 如果需要主从数据一致的话，最好还是通过重新搭建从库来做。
3. 如果有其他的从库保留有全量的 binlog 的话，可以把新的从库先接到这个保留了全量 binlog 的从库，追上日志以后，如果有需要，再接回主库。
4. 如果 binlog 有备份的情况，可以先在从库上应用缺失的 binlog，然后再执行 start slave。

评论区留言点赞板：

> @悟空 同学级联实验，验证了 seconds_behind_master 的计算逻辑。

> @_CountingStars 问了一个好问题：MySQL 是怎么快速定位 binlog 里面的某一个 GTID 位置的？答案是，在 binlog 文件头部的 Previous_gtids 可以解决这个问题。

> @王朋飞 同学问了一个好问题，sql_slave_skip_counter 跳过的是一个 event，由于 MySQL  总不能执行一半的事务，所以既然跳过了一个 event，就会跳到这个事务的末尾，因此 set global  sql_slave_skip_counter=1;start slave 是可以跳过整个事务的。

### 29 如何判断一个数据库是不是出问题了？

我在第[25]和[27]篇文章中，和你介绍了主备切换流程。通过这些内容的讲解，你应该已经很清楚了：在一主一备的双 M 架构里，主备切换只需要把客户端流量切到备库；而在一主多从架构里，主备切换除了要把客户端流量切到备库外，还需要把从库接到新主库上。

主备切换有两种场景，一种是主动切换，一种是被动切换。而其中被动切换，往往是因为主库出问题了，由 HA 系统发起的。

这也就引出了我们今天要讨论的问题：怎么判断一个主库出问题了？

你一定会说，这很简单啊，连上 MySQL，执行个 select 1 就好了。但是 select 1 成功返回了，就表示主库没问题吗？

#### select 1 判断

实际上，select 1 成功返回，只能说明这个库的进程还在，并不能说明主库没问题。现在，我们来看一下这个场景。

```sql
set global innodb_thread_concurrency=3; 
CREATE TABLE `t` (
  `id` int(11) NOT NULL,
  `c` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB; 
 insert into t values(1,1)
```

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/35076dd3d0a0d44d22b76d2a29885255-1584367400048.png)

图 1 查询 blocked

我们设置 innodb_thread_concurrency 参数的目的是，控制 InnoDB 的并发线程上限。也就是说，一旦并发线程数达到这个值，InnoDB 在接收到新请求的时候，就会进入等待状态，直到有线程退出。

这里，我把 innodb_thread_concurrency 设置成 3，表示 InnoDB 只允许 3 个线程并行执行。而在我们的例子中，前三个 session 中的 sleep(100)，使得这三个语句都处于“执行”状态，以此来模拟大查询。

你看到了， session D 里面，select 1 是能执行成功的，但是查询表 t 的语句会被堵住。也就是说，如果这时候我们用 select 1 来检测实例是否正常的话，是检测不出问题的。

在 InnoDB 中，innodb_thread_concurrency 这个参数的默认值是 0，表示不限制并发线程数量。但是，不限制并发线程数肯定是不行的。因为，一个机器的 CPU 核数有限，线程全冲进来，上下文切换的成本就会太高。

所以，通常情况下，我们建议把 innodb_thread_concurrency 设置为 64~128 之间的值。这时，你一定会有疑问，并发线程上限数设置为 128 够干啥，线上的并发连接数动不动就上千了。

产生这个疑问的原因，是搞混了**并发连接和并发查询。**

并发连接和并发查询，并不是同一个概念。你在 show processlist 的结果里，看到的几千个连接，指的就是并发连接。而“当前正在执行”的语句，才是我们所说的并发查询。

并发连接数达到几千个影响并不大，就是多占一些内存而已。我们应该关注的是并发查询，因为并发查询太高才是 CPU 杀手。这也是为什么我们需要设置 innodb_thread_concurrency 参数的原因。

然后，你可能还会想起我们在[第 7 篇文章]中讲到的热点更新和死锁检测的时候，如果把 innodb_thread_concurrency 设置为 128 的话，那么出现同一行热点更新的问题时，是不是很快就把 128 消耗完了，这样整个系统是不是就挂了呢？

实际上，**在线程进入锁等待以后，并发线程的计数会减一**，也就是说等行锁（也包括间隙锁）的线程是不算在 128 里面的。

MySQL 这样设计是非常有意义的。因为，进入锁等待的线程已经不吃 CPU 了；更重要的是，必须这么设计，才能避免整个系统锁死。

为什么呢？假设处于锁等待的线程也占并发线程的计数，你可以设想一下这个场景：

1. 线程 1 执行 begin; update t set c=c+1 where id=1, 启动了事务 trx1， 然后保持这个状态。这时候，线程处于空闲状态，不算在并发线程里面。
2. 线程 2 到线程 129 都执行 update t set c=c+1 where id=1; 由于等行锁，进入等待状态。这样就有 128 个线程处于等待状态；
3. 如果处于锁等待状态的线程计数不减一，InnoDB 就会认为线程数用满了，会阻止其他语句进入引擎执行，这样线程 1 不能提交事务。而另外的 128 个线程又处于锁等待状态，整个系统就堵住了。

下图 2 显示的就是这个状态。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/3206ea18b8a24b546515b1b95dc4a11d-1584367400052.png)

图 2 系统锁死状态（假设等行锁的语句占用并发计数）

这时候 InnoDB 不能响应任何请求，整个系统被锁死。而且，由于所有线程都处于等待状态，此时占用的 CPU 却是 0，而这明显不合理。所以，我们说 InnoDB 在设计时，遇到进程进入锁等待的情况时，将并发线程的计数减 1 的设计，是合理而且是必要的。

虽然说等锁的线程不算在并发线程计数里，但如果它在真正地执行查询，就比如我们上面例子中前三个事务中的 select sleep(100) from t，还是要算进并发线程的计数的。

在这个例子中，同时在执行的语句超过了设置的 innodb_thread_concurrency 的值，这时候系统其实已经不行了，但是通过 select 1 来检测系统，会认为系统还是正常的。

因此，我们使用 select 1 的判断逻辑要修改一下。

#### 查表判断

为了能够检测 InnoDB 并发线程数过多导致的系统不可用情况，我们需要找一个访问 InnoDB 的场景。一般的做法是，在系统库（mysql 库）里创建一个表，比如命名为 health_check，里面只放一行数据，然后定期执行：

```csharp
mysql> select * from mysql.health_check; 
```

使用这个方法，我们可以检测出由于并发线程过多导致的数据库不可用的情况。

但是，我们马上还会碰到下一个问题，即：空间满了以后，这种方法又会变得不好使。

我们知道，更新事务要写 binlog，而一旦 binlog 所在磁盘的空间占用率达到 100%，那么所有的更新语句和事务提交的 commit 语句就都会被堵住。但是，系统这时候还是可以正常读数据的。

因此，我们还是把这条监控语句再改进一下。接下来，我们就看看把查询语句改成更新语句后的效果。

#### 更新判断

既然要更新，就要放个有意义的字段，常见做法是放一个 timestamp 字段，用来表示最后一次执行检测的时间。这条更新语句类似于：

```shell
mysql> update mysql.health_check set t_modified=now();
```

节点可用性的检测都应该包含主库和备库。如果用更新来检测主库的话，那么备库也要进行更新检测。

但，备库的检测也是要写 binlog 的。由于我们一般会把数据库 A 和 B 的主备关系设计为双 M 结构，所以在备库 B 上执行的检测命令，也要发回给主库 A。

但是，如果主库 A 和备库 B 都用相同的更新命令，就可能出现行冲突，也就是可能会导致主备同步停止。所以，现在看来 mysql.health_check 这个表就不能只有一行数据了。

为了让主备之间的更新不产生冲突，我们可以在 mysql.health_check 表上存入多行数据，并用 A、B 的 server_id 做主键。

```sql
mysql> CREATE TABLE `health_check` (
  `id` int(11) NOT NULL,
  `t_modified` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB; 
/* 检测命令 */
insert into mysql.health_check(id, t_modified) values (@@server_id, now()) on duplicate key update t_modified=now();
```

由于 MySQL 规定了主库和备库的 server_id 必须不同（否则创建主备关系的时候就会报错），这样就可以保证主、备库各自的检测命令不会发生冲突。

更新判断是一个相对比较常用的方案了，不过依然存在一些问题。其中，“判定慢”一直是让 DBA 头疼的问题。

你一定会疑惑，**更新语句，如果失败或者超时，就可以发起主备切换了，为什么还会有判定慢的问题呢？**

其实，这里涉及到的是服务器 IO 资源分配的问题。

首先，所有的检测逻辑都需要一个超时时间 N。执行一条 update 语句，超过 N 秒后还不返回，就认为系统不可用。

你可以设想一个日志盘的 IO 利用率已经是 100% 的场景。这时候，整个系统响应非常慢，已经需要做主备切换了。

但是你要知道，IO 利用率 100% 表示系统的 IO 是在工作的，每个请求都有机会获得 IO 资源，执行自己的任务。而我们的检测使用的  update 命令，需要的资源很少，所以可能在拿到 IO 资源的时候就可以提交成功，并且在超时时间 N 秒未到达之前就返回给了检测系统。

检测系统一看，update 命令没有超时，于是就得到了“系统正常”的结论。

也就是说，这时候在业务系统上正常的 SQL 语句已经执行得很慢了，但是 DBA 上去一看，HA 系统还在正常工作，并且认为主库现在处于可用状态。

之所以会出现这个现象，根本原因是我们上面说的所有方法，都是基于外部检测的。外部检测天然有一个问题，就是随机性。

因为，外部检测都需要定时轮询，所以系统可能已经出问题了，但是却需要等到下一个检测发起执行语句的时候，我们才有可能发现问题。而且，如果你的运气不够好的话，可能第一次轮询还不能发现，这就会导致切换慢的问题。

所以，接下来我要再和你介绍一种在 MySQL 内部发现数据库问题的方法。

#### 内部统计

针对磁盘利用率这个问题，如果 MySQL 可以告诉我们，内部每一次 IO 请求的时间，那我们判断数据库是否出问题的方法就可靠得多了。

其实，MySQL 5.6 版本以后提供的 performance_schema 库，就在 file_summary_by_event_name 表里统计了每次 IO 请求的时间。

file_summary_by_event_name 表里有很多行数据，我们先来看看 event_name='wait/io/file/innodb/innodb_log_file’这一行。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/752ccfe43b4eab155be17401838c62dd-1584367400232.png)

图 3 performance_schema.file_summary_by_event_name 的一行

图中这一行表示统计的是 redo log 的写入时间，第一列 EVENT_NAME 表示统计的类型。

接下来的三组数据，显示的是 redo log 操作的时间统计。

第一组五列，是所有 IO 类型的统计。其中，COUNT_STAR 是所有 IO 的总次数，接下来四列是具体的统计项， 单位是皮秒；前缀 SUM、MIN、AVG、MAX，顾名思义指的就是总和、最小值、平均值和最大值。

第二组六列，是读操作的统计。最后一列 SUM_NUMBER_OF_BYTES_READ 统计的是，总共从 redo log 里读了多少个字节。

第三组六列，统计的是写操作。

最后的第四组数据，是对其他类型数据的统计。在 redo log 里，你可以认为它们就是对 fsync 的统计。

在 performance_schema 库的 file_summary_by_event_name 表里，binlog 对应的是  event_name = "wait/io/file/sql/binlog"这一行。各个字段的统计逻辑，与 redo log  的各个字段完全相同。这里，我就不再赘述了。

因为我们每一次操作数据库，performance_schema 都需要额外地统计这些信息，所以我们打开这个统计功能是有性能损耗的。

我的测试结果是，如果打开所有的 performance_schema 项，性能大概会下降 10% 左右。所以，我建议你只打开自己需要的项进行统计。你可以通过下面的方法打开或者关闭某个具体项的统计。

如果要打开 redo log 的时间监控，你可以执行这个语句：

```sql
mysql> update setup_instruments set ENABLED='YES', Timed='YES' where name like '%wait/io/file/innodb/innodb_log_file%';
```

假设，现在你已经开启了 redo log 和 binlog 这两个统计信息，那要怎么把这个信息用在实例状态诊断上呢？

很简单，你可以通过 MAX_TIMER 的值来判断数据库是否出问题了。比如，你可以设定阈值，单次 IO 请求时间超过 200 毫秒属于异常，然后使用类似下面这条语句作为检测逻辑。

```csharp
mysql> select event_name,MAX_TIMER_WAIT  FROM performance_schema.file_summary_by_event_name where event_name in ('wait/io/file/innodb/innodb_log_file','wait/io/file/sql/binlog') and MAX_TIMER_WAIT>200*1000000000;
```

发现异常后，取到你需要的信息，再通过下面这条语句：

```shell
mysql> truncate table performance_schema.file_summary_by_event_name;
```

把之前的统计信息清空。这样如果后面的监控中，再次出现这个异常，就可以加入监控累积值了。

#### 小结

今天，我和你介绍了检测一个 MySQL 实例健康状态的几种方法，以及各种方法存在的问题和演进的逻辑。

你看完后可能会觉得，select 1 这样的方法是不是已经被淘汰了呢，但实际上使用非常广泛的 MHA（Master High Availability），默认使用的就是这个方法。

MHA 中的另一个可选方法是只做连接，就是 “如果连接成功就认为主库没问题”。不过据我所知，选择这个方法的很少。

其实，每个改进的方案，都会增加额外损耗，并不能用“对错”做直接判断，需要你根据业务实际情况去做权衡。

我个人比较倾向的方案，是优先考虑 update 系统表，然后再配合增加检测 performance_schema 的信息。

最后，又到了我们的思考题时间。

今天，我想问你的是：业务系统一般也有高可用的需求，在你开发和维护过的服务中，你是怎么判断服务有没有出问题的呢？

你可以把你用到的方法和分析写在留言区，我会在下一篇文章中选取有趣的方案一起来分享和分析。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

上期的问题是，如果使用 GTID 等位点的方案做读写分离，在对大表做 DDL 的时候会怎么样。

假设，这条语句在主库上要执行 10 分钟，提交后传到备库就要 10 分钟（典型的大事务）。那么，在主库 DDL 之后再提交的事务的 GTID，去备库查的时候，就会等 10 分钟才出现。

这样，这个读写分离机制在这 10 分钟之内都会超时，然后走主库。

这种预期内的操作，应该在业务低峰期的时候，确保主库能够支持所有业务查询，然后把读请求都切到主库，再在主库上做 DDL。等备库延迟追上以后，再把读请求切回备库。

通过这个思考题，我主要想让关注的是，大事务对等位点方案的影响。

当然了，使用 gh-ost 方案来解决这个问题也是不错的选择。

评论区留言点赞板：

> @曾剑、@max 同学提到的备库先做，再切主库的方法也是可以的。

### 33 我查这么多数据，会不会把数据库内存打爆？

我经常会被问到这样一个问题：我的主机内存只有 100G，现在要对一个 200G 的大表做全表扫描，会不会把数据库主机的内存用光了？

这个问题确实值得担心，被系统 OOM（out of memory）可不是闹着玩的。但是，反过来想想，逻辑备份的时候，可不就是做整库扫描吗？如果这样就会把内存吃光，逻辑备份不是早就挂了？

所以说，对大表做全表扫描，看来应该是没问题的。但是，这个流程到底是怎么样的呢？

#### 全表扫描对 server 层的影响

假设，我们现在要对一个 200G 的 InnoDB 表 db1. t，执行一个全表扫描。当然，你要把扫描结果保存在客户端，会使用类似这样的命令：

```bash
mysql -h$host -P$port -u$user -p$pwd -e "select * from db1.t" > $target_file
```

你已经知道了，InnoDB 的数据是保存在主键索引上的，所以全表扫描实际上是直接扫描表 t 的主键索引。这条查询语句由于没有其他的判断条件，所以查到的每一行都可以直接放到结果集里面，然后返回给客户端。

那么，这个“结果集”存在哪里呢？

实际上，服务端并不需要保存一个完整的结果集。取数据和发数据的流程是这样的：

1. 获取一行，写到 net_buffer 中。这块内存的大小是由参数 net_buffer_length 定义的，默认是 16k。
2. 重复获取行，直到 net_buffer 写满，调用网络接口发出去。
3. 如果发送成功，就清空 net_buffer，然后继续取下一行，并写入 net_buffer。
4. 如果发送函数返回 EAGAIN 或 WSAEWOULDBLOCK，就表示本地网络栈（socket send buffer）写满了，进入等待。直到网络栈重新可写，再继续发送。

这个过程对应的流程图如下所示。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/a027c300d7dde8cea4fad8f34b670ebd-1584367400340.jpg)

图 1 查询结果发送流程

从这个流程中，你可以看到：

1. 一个查询在发送过程中，占用的 MySQL 内部的内存最大就是 net_buffer_length 这么大，并不会达到 200G；
2. socket send buffer 也不可能达到 200G（默认定义 /proc/sys/net/core/wmem_default），如果 socket send buffer 被写满，就会暂停读数据的流程。

也就是说，**MySQL 是“边读边发的”**，这个概念很重要。这就意味着，如果客户端接收得慢，会导致 MySQL 服务端由于结果发不出去，这个事务的执行时间变长。

比如下面这个状态，就是我故意让客户端不去读 socket receive buffer 中的内容，然后在服务端 show processlist 看到的结果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/183a704d4495bebbc13c524695b5b6c3-1584367400345.png)

图 2 服务端发送阻塞

如果你看到 State 的值一直处于**“Sending to client”**，就表示服务器端的网络栈写满了。

我在上一篇文章中曾提到，如果客户端使用–quick 参数，会使用 mysql_use_result  方法。这个方法是读一行处理一行。你可以想象一下，假设有一个业务的逻辑比较复杂，每读一行数据以后要处理的逻辑如果很慢，就会导致客户端要过很久才会去取下一行数据，可能就会出现如图 2 所示的这种情况。

因此，**对于正常的线上业务来说，如果一个查询的返回结果不会很多的话，我都建议你使用 mysql_store_result 这个接口，直接把查询结果保存到本地内存。**

当然前提是查询返回结果不多。在[第 30 篇文章]评论区，有同学说到自己因为执行了一个大查询导致客户端占用内存近 20G，这种情况下就需要改用 mysql_use_result 接口了。

另一方面，如果你在自己负责维护的 MySQL 里看到很多个线程都处于“Sending to client”这个状态，就意味着你要让业务开发同学优化查询结果，并评估这么多的返回结果是否合理。

而如果要快速减少处于这个状态的线程的话，将 net_buffer_length 参数设置为一个更大的值是一个可选方案。

与“Sending to client”长相很类似的一个状态是**“Sending  data”**，这是一个经常被误会的问题。有同学问我说，在自己维护的实例上看到很多查询语句的状态是“Sending  data”，但查看网络也没什么问题啊，为什么 Sending data 要这么久？

实际上，一个查询语句的状态变化是这样的（注意：这里，我略去了其他无关的状态）：

- MySQL 查询语句进入执行阶段后，首先把状态设置成“Sending data”；
- 然后，发送执行结果的列相关的信息（meta data) 给客户端；
- 再继续执行语句的流程；
- 执行完成后，把状态设置成空字符串。

也就是说，“Sending data”并不一定是指“正在发送数据”，而可能是处于执行器过程中的任意阶段。比如，你可以构造一个锁等待的场景，就能看到 Sending data 状态。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/7640b0d82965bf8b305514f30425424b-1584367400348.png)

图 3 读全表被锁

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/84533515cf36be65582309fbb85e13c0-1584367400352.png)

图 4 Sending data 状态

可以看到，session B 明显是在等锁，状态显示为 Sending data。

也就是说，仅当一个线程处于“等待客户端接收结果”的状态，才会显示"Sending to client"；而如果显示成“Sending data”，它的意思只是“正在执行”。

现在你知道了，查询的结果是分段发给客户端的，因此扫描全表，查询返回大量的数据，并不会把内存打爆。

在 server 层的处理逻辑我们都清楚了，在 InnoDB 引擎里面又是怎么处理的呢？ 扫描全表会不会对引擎系统造成影响呢？

#### 全表扫描对 InnoDB 的影响

在[第 2]和[第 15 篇]文章中，我介绍 WAL 机制的时候，和你分析了 InnoDB 内存的一个作用，是保存更新的结果，再配合 redo log，就避免了随机写盘。

内存的数据页是在 Buffer Pool (BP) 中管理的，在 WAL 里 Buffer Pool 起到了加速更新的作用。而实际上，Buffer Pool 还有一个更重要的作用，就是加速查询。

在第 2 篇文章的评论区有同学问道，由于有 WAL 机制，当事务提交的时候，磁盘上的数据页是旧的，那如果这时候马上有一个查询要来读这个数据页，是不是要马上把 redo log 应用到数据页呢？

答案是不需要。因为这时候内存数据页的结果是最新的，直接读内存页就可以了。你看，这时候查询根本不需要读磁盘，直接从内存拿结果，速度是很快的。所以说，Buffer Pool 还有加速查询的作用。

而 Buffer Pool 对查询的加速效果，依赖于一个重要的指标，即：**内存命中率**。

你可以在 show engine innodb status 结果中，查看一个系统当前的 BP 命中率。一般情况下，一个稳定服务的线上系统，要保证响应时间符合要求的话，内存命中率要在 99% 以上。

执行 show engine innodb status ，可以看到“Buffer pool hit rate”字样，显示的就是当前的命中率。比如图 5 这个命中率，就是 99.0%。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/c70a95ee99826812c292c46de508982e-1584367400354.png)

图 5 show engine innodb status 显示内存命中率

如果所有查询需要的数据页都能够直接从内存得到，那是最好的，对应的命中率就是 100%。但，这在实际生产上是很难做到的。

InnoDB Buffer Pool 的大小是由参数 innodb_buffer_pool_size 确定的，一般建议设置成可用物理内存的 60%~80%。

在大约十年前，单机的数据量是上百个 G，而物理内存是几个 G；现在虽然很多服务器都能有 128G 甚至更高的内存，但是单机的数据量却达到了 T 级别。

所以，innodb_buffer_pool_size 小于磁盘的数据量是很常见的。如果一个 Buffer Pool 满了，而又要从磁盘读入一个数据页，那肯定是要淘汰一个旧数据页的。

InnoDB 内存管理用的是最近最少使用 (Least Recently Used, LRU) 算法，这个算法的核心就是淘汰最久未使用的数据。

下图是一个 LRU 算法的基本模型。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/e0ac92febac50a5d881f1188ea5bfd65-1584367400359.jpg)

图 6 基本 LRU 算法

InnoDB 管理 Buffer Pool 的 LRU 算法，是用链表来实现的。

1. 在图 6 的状态 1 里，链表头部是 P1，表示 P1 是最近刚刚被访问过的数据页；假设内存里只能放下这么多数据页；
2. 这时候有一个读请求访问 P3，因此变成状态 2，P3 被移到最前面；
3. 状态 3 表示，这次访问的数据页是不存在于链表中的，所以需要在 Buffer Pool 中新申请一个数据页 Px，加到链表头部。但是由于内存已经满了，不能申请新的内存。于是，会清空链表末尾 Pm 这个数据页的内存，存入 Px 的内容，然后放到链表头部。
4. 从效果上看，就是最久没有被访问的数据页 Pm，被淘汰了。

这个算法乍一看上去没什么问题，但是如果考虑到要做一个全表扫描，会不会有问题呢？

假设按照这个算法，我们要扫描一个 200G 的表，而这个表是一个历史数据表，平时没有业务访问它。

那么，按照这个算法扫描的话，就会把当前的 Buffer Pool 里的数据全部淘汰掉，存入扫描过程中访问到的数据页的内容。也就是说 Buffer Pool 里面主要放的是这个历史数据表的数据。

对于一个正在做业务服务的库，这可不妙。你会看到，Buffer Pool 的内存命中率急剧下降，磁盘压力增加，SQL 语句响应变慢。

所以，InnoDB 不能直接使用这个 LRU 算法。实际上，InnoDB 对 LRU 算法做了改进。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/25e18920dd204cf99eec2d62755fe99e-1584367400443.png)

图 7 改进的 LRU 算法

在 InnoDB 实现上，按照 5:3 的比例把整个 LRU 链表分成了 young 区域和 old 区域。图中 LRU_old  指向的就是 old 区域的第一个位置，是整个链表的 5/8 处。也就是说，靠近链表头部的 5/8 是 young 区域，靠近链表尾部的 3/8 是 old 区域。

改进后的 LRU 算法执行流程变成了下面这样。

1. 图 7 中状态 1，要访问数据页 P3，由于 P3 在 young 区域，因此和优化前的 LRU 算法一样，将其移到链表头部，变成状态 2。
2. 之后要访问一个新的不存在于当前链表的数据页，这时候依然是淘汰掉数据页 Pm，但是新插入的数据页 Px，是放在 LRU_old 处。
3. 处于 old 区域的数据页，每次被访问的时候都要做下面这个判断：
   - 若这个数据页在 LRU 链表中存在的时间超过了 1 秒，就把它移动到链表头部；
   - 如果这个数据页在 LRU 链表中存在的时间短于 1 秒，位置保持不变。1 秒这个时间，是由参数 innodb_old_blocks_time 控制的。其默认值是 1000，单位毫秒。

这个策略，就是为了处理类似全表扫描的操作量身定制的。还是以刚刚的扫描 200G 的历史数据表为例，我们看看改进后的 LRU 算法的操作逻辑：

1. 扫描过程中，需要新插入的数据页，都被放到 old 区域 ;
2. 一个数据页里面有多条记录，这个数据页会被多次访问到，但由于是顺序扫描，这个数据页第一次被访问和最后一次被访问的时间间隔不会超过 1 秒，因此还是会被保留在 old 区域；
3. 再继续扫描后续的数据，之前的这个数据页之后也不会再被访问到，于是始终没有机会移到链表头部（也就是 young 区域），很快就会被淘汰出去。

可以看到，这个策略最大的收益，就是在扫描这个大表的过程中，虽然也用到了 Buffer Pool，但是对 young 区域完全没有影响，从而保证了 Buffer Pool 响应正常业务的查询命中率。

#### 小结

今天，我用“大查询会不会把内存用光”这个问题，和你介绍了 MySQL 的查询结果，发送给客户端的过程。

由于 MySQL 采用的是边算边发的逻辑，因此对于数据量很大的查询结果来说，不会在 server 端保存完整的结果集。所以，如果客户端读结果不及时，会堵住 MySQL 的查询过程，但是不会把内存打爆。

而对于 InnoDB 引擎内部，由于有淘汰策略，大查询也不会导致内存暴涨。并且，由于 InnoDB 对 LRU 算法做了改进，冷数据的全表扫描，对 Buffer Pool 的影响也能做到可控。

当然，我们前面文章有说过，全表扫描还是比较耗费 IO 资源的，所以业务高峰期还是不能直接在线上主库执行全表扫描的。

最后，我给你留一个思考题吧。

我在文章中说到，如果由于客户端压力太大，迟迟不能接收结果，会导致 MySQL 无法发送结果而影响语句执行。但，这还不是最糟糕的情况。

你可以设想出由于客户端的性能问题，对数据库影响更严重的例子吗？或者你是否经历过这样的场景？你又是怎么优化的？

你可以把你的经验和分析写在留言区，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

上期的问题是，如果一个事务被 kill 之后，持续处于回滚状态，从恢复速度的角度看，你是应该重启等它执行结束，还是应该强行重启整个 MySQL 进程。

因为重启之后该做的回滚动作还是不能少的，所以从恢复速度的角度来说，应该让它自己结束。

当然，如果这个语句可能会占用别的锁，或者由于占用 IO 资源过多，从而影响到了别的语句执行的话，就需要先做主备切换，切到新主库提供服务。

切换之后别的线程都断开了连接，自动停止执行。接下来还是等它自己执行完成。这个操作属于我们在文章中说到的，减少系统压力，加速终止逻辑。

评论区留言点赞板：

> @HuaMax 的回答中提到了对其他线程的影响； @夹心面包 @Ryoma @曾剑 同学提到了重启后依然继续做回滚操作的逻辑。

### 34 到底可不可以使用join？

在实际生产中，关于 join 语句使用的问题，一般会集中在以下两类：

1. 我们 DBA 不让使用 join，使用 join 有什么问题呢？
2. 如果有两个大小不同的表做 join，应该用哪个表做驱动表呢？

今天这篇文章，我就先跟你说说 join 语句到底是怎么执行的，然后再来回答这两个问题。

为了便于量化分析，我还是创建两个表 t1 和 t2 来和你说明。

```sql
CREATE TABLE `t2` (
  `id` int(11) NOT NULL,
  `a` int(11) DEFAULT NULL,
  `b` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `a` (`a`)
) ENGINE=InnoDB; 
drop procedure idata;
delimiter ;;
create procedure idata()
begin
  declare i int;
  set i=1;
  while(i<=1000)do
    insert into t2 values(i, i, i);
    set i=i+1;
  end while;
end;;
delimiter ;
call idata(); 
create table t1 like t2;
insert into t1 (select * from t2 where id<=100)
```

可以看到，这两个表都有一个主键索引 id 和一个索引 a，字段 b 上无索引。存储过程 idata() 往表 t2 里插入了 1000 行数据，在表 t1 里插入的是 100 行数据。

#### Index Nested-Loop Join

我们来看一下这个语句：

```csharp
select * from t1 straight_join t2 on (t1.a=t2.a);
```

如果直接使用 join 语句，MySQL 优化器可能会选择表 t1 或 t2 作为驱动表，这样会影响我们分析 SQL  语句的执行过程。所以，为了便于分析执行过程中的性能问题，我改用 straight_join 让 MySQL  使用固定的连接方式执行查询，这样优化器只会按照我们指定的方式去 join。在这个语句里，t1 是驱动表，t2 是被驱动表。

现在，我们来看一下这条语句的 explain 结果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/4b9cb0e0b83618e01c9bfde44a0ea990-1584367400492.png)

图 1 使用索引字段 join 的 explain 结果

可以看到，在这条语句里，被驱动表 t2 的字段 a 上有索引，join 过程用上了这个索引，因此这个语句的执行流程是这样的：

1. 从表 t1 中读入一行数据 R；
2. 从数据行 R 中，取出 a 字段到表 t2 里去查找；
3. 取出表 t2 中满足条件的行，跟 R 组成一行，作为结果集的一部分；
4. 重复执行步骤 1 到 3，直到表 t1 的末尾循环结束。

这个过程是先遍历表 t1，然后根据从表 t1 中取出的每行数据中的 a 值，去表 t2  中查找满足条件的记录。在形式上，这个过程就跟我们写程序时的嵌套查询类似，并且可以用上被驱动表的索引，所以我们称之为“Index  Nested-Loop Join”，简称 NLJ。

它对应的流程图如下所示：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/d83ad1cbd6118603be795b26d38f8df6-1584367400497.jpg)

图 2 Index Nested-Loop Join 算法的执行流程

在这个流程里：

1. 对驱动表 t1 做了全表扫描，这个过程需要扫描 100 行；
2. 而对于每一行 R，根据 a 字段去表 t2 查找，走的是树搜索过程。由于我们构造的数据都是一一对应的，因此每次的搜索过程都只扫描一行，也是总共扫描 100 行；
3. 所以，整个执行流程，总扫描行数是 200。

现在我们知道了这个过程，再试着回答一下文章开头的两个问题。

先看第一个问题：**能不能使用 join?**

假设不使用 join，那我们就只能用单表查询。我们看看上面这条语句的需求，用单表查询怎么实现。

1. 执行`select * from t1`，查出表 t1 的所有数据，这里有 100 行；
2. 循环遍历这 100 行数据：
   - 从每一行 R 取出字段 a 的值 $R.a；
   - 执行`select * from t2 where a=$R.a`；
   - 把返回的结果和 R 构成结果集的一行。

可以看到，在这个查询过程，也是扫描了 200 行，但是总共执行了 101 条语句，比直接 join 多了 100 次交互。除此之外，客户端还要自己拼接 SQL 语句和结果。

显然，这么做还不如直接 join 好。

我们再来看看第二个问题：**怎么选择驱动表？**

在这个 join 语句执行过程中，驱动表是走全表扫描，而被驱动表是走树搜索。

假设被驱动表的行数是 M。每次在被驱动表查一行数据，要先搜索索引 a，再搜索主键索引。每次搜索一棵树近似复杂度是以 2 为底的 M 的对数，记为 log2M，所以在被驱动表上查一行的时间复杂度是 2*log2M。

假设驱动表的行数是 N，执行过程就要扫描驱动表 N 行，然后对于每一行，到被驱动表上匹配一次。

因此整个执行过程，近似复杂度是 N + N*2*log2M。

显然，N 对扫描行数的影响更大，因此应该让小表来做驱动表。

> 如果你没觉得这个影响有那么“显然”， 可以这么理解：N 扩大 1000 倍的话，扫描行数就会扩大 1000 倍；而 M 扩大 1000 倍，扫描行数扩大不到 10 倍。

到这里小结一下，通过上面的分析我们得到了两个结论：

1. 使用 join 语句，性能比强行拆成多个单表执行 SQL 语句的性能要好；
2. 如果使用 join 语句的话，需要让小表做驱动表。

但是，你需要注意，这个结论的前提是“可以使用被驱动表的索引”。

接下来，我们再看看被驱动表用不上索引的情况。

#### Simple Nested-Loop Join

现在，我们把 SQL 语句改成这样：

```csharp
select * from t1 straight_join t2 on (t1.a=t2.b);
```

由于表 t2 的字段 b 上没有索引，因此再用图 2 的执行流程时，每次到 t2 去匹配的时候，就要做一次全表扫描。

你可以先设想一下这个问题，继续使用图 2 的算法，是不是可以得到正确的结果呢？如果只看结果的话，这个算法是正确的，而且这个算法也有一个名字，叫做“Simple Nested-Loop Join”。

但是，这样算来，这个 SQL 请求就要扫描表 t2 多达 100 次，总共扫描 100*1000=10 万行。

这还只是两个小表，如果 t1 和 t2 都是 10 万行的表（当然了，这也还是属于小表的范围），就要扫描 100 亿行，这个算法看上去太“笨重”了。

当然，MySQL 也没有使用这个 Simple Nested-Loop Join 算法，而是使用了另一个叫作“Block Nested-Loop Join”的算法，简称 BNL。

#### Block Nested-Loop Join

这时候，被驱动表上没有可用的索引，算法的流程是这样的：

1. 把表 t1 的数据读入线程内存 join_buffer 中，由于我们这个语句中写的是 select *，因此是把整个表 t1 放入了内存；
2. 扫描表 t2，把表 t2 中的每一行取出来，跟 join_buffer 中的数据做对比，满足 join 条件的，作为结果集的一部分返回。

这个过程的流程图如下：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/15ae4f17c46bf71e8349a8f2ef70d573-1584367400733.jpg)

图 3 Block Nested-Loop Join 算法的执行流程

对应地，这条 SQL 语句的 explain 结果如下所示：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/676921fa0883e9463dd34fb2bc5e87e1-1584367400742.png)

图 4 不使用索引字段 join 的 explain 结果

可以看到，在这个过程中，对表 t1 和 t2 都做了一次全表扫描，因此总的扫描行数是 1100。由于 join_buffer  是以无序数组的方式组织的，因此对表 t2 中的每一行，都要做 100 次判断，总共需要在内存中做的判断次数是：100*1000=10 万次。

前面我们说过，如果使用 Simple Nested-Loop Join 算法进行查询，扫描行数也是 10  万行。因此，从时间复杂度上来说，这两个算法是一样的。但是，Block Nested-Loop Join 算法的这 10  万次判断是内存操作，速度上会快很多，性能也更好。

接下来，我们来看一下，在这种情况下，应该选择哪个表做驱动表。

假设小表的行数是 N，大表的行数是 M，那么在这个算法里：

1. 两个表都做一次全表扫描，所以总的扫描行数是 M+N；
2. 内存中的判断次数是 M*N。

可以看到，调换这两个算式中的 M 和 N 没差别，因此这时候选择大表还是小表做驱动表，执行耗时是一样的。

然后，你可能马上就会问了，这个例子里表 t1 才 100 行，要是表 t1 是一个大表，join_buffer 放不下怎么办呢？

join_buffer 的大小是由参数 join_buffer_size 设定的，默认值是 256k。**如果放不下表 t1 的所有数据话，策略很简单，就是分段放。**我把 join_buffer_size 改成 1200，再执行：

```csharp
select * from t1 straight_join t2 on (t1.a=t2.b);
```

执行过程就变成了：

1. 扫描表 t1，顺序读取数据行放入 join_buffer 中，放完第 88 行 join_buffer 满了，继续第 2 步；
2. 扫描表 t2，把 t2 中的每一行取出来，跟 join_buffer 中的数据做对比，满足 join 条件的，作为结果集的一部分返回；
3. 清空 join_buffer；
4. 继续扫描表 t1，顺序读取最后的 12 行数据放入 join_buffer 中，继续执行第 2 步。

执行流程图也就变成这样：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/695adf810fcdb07e393467bcfd2f6ac4-1584367400746.jpg)

图 5 Block Nested-Loop Join -- 两段

图中的步骤 4 和 5，表示清空 join_buffer 再复用。

这个流程才体现出了这个算法名字中“Block”的由来，表示“分块去 join”。

可以看到，这时候由于表 t1 被分成了两次放入 join_buffer 中，导致表 t2 会被扫描两次。虽然分成两次放入 join_buffer，但是判断等值条件的次数还是不变的，依然是 (88+12)*1000=10 万次。

我们再来看下，在这种情况下驱动表的选择问题。

假设，驱动表的数据行数是 N，需要分 K 段才能完成算法流程，被驱动表的数据行数是 M。

注意，这里的 K 不是常数，N 越大 K 就会越大，因此把 K 表示为λ*N，显然λ的取值范围是 (0,1)。

所以，在这个算法的执行过程中：

1. 扫描行数是 N+λ*N*M；
2. 内存判断 N*M 次。

显然，内存判断次数是不受选择哪个表作为驱动表影响的。而考虑到扫描行数，在 M 和 N 大小确定的情况下，N 小一些，整个算式的结果会更小。

所以结论是，应该让小表当驱动表。

当然，你会发现，在 N+λ*N*M 这个式子里，λ才是影响扫描行数的关键因素，这个值越小越好。

刚刚我们说了 N 越大，分段数 K 越大。那么，N 固定的时候，什么参数会影响 K 的大小呢？（也就是λ的大小）答案是  join_buffer_size。join_buffer_size  越大，一次可以放入的行越多，分成的段数也就越少，对被驱动表的全表扫描次数就越少。

这就是为什么，你可能会看到一些建议告诉你，如果你的 join 语句很慢，就把 join_buffer_size 改大。

理解了 MySQL 执行 join 的两种算法，现在我们再来试着**回答文章开头的两个问题**。

第一个问题：能不能使用 join 语句？

1. 如果可以使用 Index Nested-Loop Join 算法，也就是说可以用上被驱动表上的索引，其实是没问题的；
2. 如果使用 Block Nested-Loop Join 算法，扫描行数就会过多。尤其是在大表上的 join 操作，这样可能要扫描被驱动表很多次，会占用大量的系统资源。所以这种 join 尽量不要用。

所以你在判断要不要使用 join 语句时，就是看 explain 结果里面，Extra 字段里面有没有出现“Block Nested Loop”字样。

第二个问题是：如果要使用 join，应该选择大表做驱动表还是选择小表做驱动表？

1. 如果是 Index Nested-Loop Join 算法，应该选择小表做驱动表；
2. 如果是 Block Nested-Loop Join 算法：
   - 在 join_buffer_size 足够大的时候，是一样的；
   - 在 join_buffer_size 不够大的时候（这种情况更常见），应该选择小表做驱动表。

所以，这个问题的结论就是，总是应该使用小表做驱动表。

当然了，这里我需要说明下，**什么叫作“小表”**。

我们前面的例子是没有加条件的。如果我在语句的 where 条件加上 t2.id<=50 这个限定条件，再来看下这两条语句：

```csharp
select * from t1 straight_join t2 on (t1.b=t2.b) where t2.id<=50;
select * from t2 straight_join t1 on (t1.b=t2.b) where t2.id<=50;
```

注意，为了让两条语句的被驱动表都用不上索引，所以 join 字段都使用了没有索引的字段 b。

但如果是用第二个语句的话，join_buffer 只需要放入 t2 的前 50 行，显然是更好的。所以这里，“t2 的前 50 行”是那个相对小的表，也就是“小表”。

我们再来看另外一组例子：

```csharp
select t1.b,t2.* from  t1  straight_join t2 on (t1.b=t2.b) where t2.id<=100;
select t1.b,t2.* from  t2  straight_join t1 on (t1.b=t2.b) where t2.id<=100;
```

这个例子里，表 t1 和 t2 都是只有 100 行参加 join。但是，这两条语句每次查询放入 join_buffer 中的数据是不一样的：

- 表 t1 只查字段 b，因此如果把 t1 放到 join_buffer 中，则 join_buffer 中只需要放入 b 的值；
- 表 t2 需要查所有的字段，因此如果把表 t2 放到 join_buffer 中的话，就需要放入三个字段 id、a 和 b。

这里，我们应该选择表 t1 作为驱动表。也就是说在这个例子里，“只需要一列参与 join 的表 t1”是那个相对小的表。

所以，更准确地说，**在决定哪个表做驱动表的时候，应该是两个表按照各自的条件过滤，过滤完成之后，计算参与 join 的各个字段的总数据量，数据量小的那个表，就是“小表”，应该作为驱动表。**

#### 小结

今天，我和你介绍了 MySQL 执行 join 语句的两种可能算法，这两种算法是由能否使用被驱动表的索引决定的。而能否用上被驱动表的索引，对 join 语句的性能影响很大。

通过对 Index Nested-Loop Join 和 Block Nested-Loop Join 两个算法执行过程的分析，我们也得到了文章开头两个问题的答案：

1. 如果可以使用被驱动表的索引，join 语句还是有其优势的；
2. 不能使用被驱动表的索引，只能使用 Block Nested-Loop Join 算法，这样的语句就尽量不要使用；
3. 在使用 join 的时候，应该让小表做驱动表。

最后，又到了今天的问题时间。

我们在上文说到，使用 Block Nested-Loop Join 算法，可能会因为 join_buffer 不够大，需要对被驱动表做多次全表扫描。

我的问题是，如果被驱动表是一个大表，并且是一个冷数据表，除了查询过程中可能会导致 IO 压力大以外，你觉得对这个 MySQL 服务还有什么更严重的影响吗？（这个问题需要结合上一篇文章的知识点）

你可以把你的结论和分析写在留言区，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

我在上一篇文章最后留下的问题是，如果客户端由于压力过大，迟迟不能接收数据，会对服务端造成什么严重的影响。

这个问题的核心是，造成了“长事务”。

至于长事务的影响，就要结合我们前面文章中提到的锁、MVCC 的知识点了。

- 如果前面的语句有更新，意味着它们在占用着行锁，会导致别的语句更新被锁住；
- 当然读的事务也有问题，就是会导致 undo log 不能被回收，导致回滚段空间膨胀。

评论区留言点赞板：

> @老杨同志 提到了更新之间会互相等锁的问题。同一个事务，更新之后要尽快提交，不要做没必要的查询，尤其是不要执行需要返回大量数据的查询； @长杰 同学提到了 undo 表空间变大，db 服务堵塞，服务端磁盘空间不足的例子。

### 35 join语句怎么优化？

在上一篇文章中，我和你介绍了 join 语句的两种算法，分别是 Index Nested-Loop Join(NLJ) 和 Block Nested-Loop Join(BNL)。

我们发现在使用 NLJ 算法的时候，其实效果还是不错的，比通过应用层拆分成多个语句然后再拼接查询结果更方便，而且性能也不会差。

但是，BNL 算法在大表 join 的时候性能就差多了，比较次数等于两个表参与 join 的行数的乘积，很消耗 CPU 资源。

当然了，这两个算法都还有继续优化的空间，我们今天就来聊聊这个话题。

为了便于分析，我还是创建两个表 t1、t2 来和你展开今天的问题。

```sql
create table t1(id int primary key, a int, b int, index(a));
create table t2 like t1;
drop procedure idata;
delimiter ;;
create procedure idata()
begin
  declare i int;
  set i=1;
  while(i<=1000)do
    insert into t1 values(i, 1001-i, i);
    set i=i+1;
  end while;
  
  set i=1;
  while(i<=1000000)do
    insert into t2 values(i, i, i);
    set i=i+1;
  end while; 
end;;
delimiter ;
call idata();
```

为了便于后面量化说明，我在表 t1 里，插入了 1000 行数据，每一行的 a=1001-id 的值。也就是说，表 t1 中字段 a 是逆序的。同时，我在表 t2 中插入了 100 万行数据。

#### Multi-Range Read 优化

在介绍 join 语句的优化方案之前，我需要先和你介绍一个知识点，即：Multi-Range Read 优化 (MRR)。这个优化的主要目的是尽量使用顺序读盘。

在[第 4 篇文章]中，我和你介绍 InnoDB 的索引结构时，提到了“回表”的概念。我们先来回顾一下这个概念。回表是指，InnoDB 在普通索引 a 上查到主键 id 的值后，再根据一个个主键 id 的值到主键索引上去查整行数据的过程。

然后，有同学在留言区问到，回表过程是一行行地查数据，还是批量地查数据？

我们先来看看这个问题。假设，我执行这个语句：

```csharp
select * from t1 where a>=1 and a<=100;
```

主键索引是一棵 B+ 树，在这棵树上，每次只能根据一个主键 id 查到一行数据。因此，回表肯定是一行行搜索主键索引的，基本流程如图 1 所示。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/1761edbd7734276ae0a213af3cdd3311-1584367401565.jpg)

图 1 基本回表流程

如果随着 a 的值递增顺序查询的话，id 的值就变成随机的，那么就会出现随机访问，性能相对较差。虽然“按行查”这个机制不能改，但是调整查询的顺序，还是能够加速的。

**因为大多数的数据都是按照主键递增顺序插入得到的，所以我们可以认为，如果按照主键的递增顺序查询的话，对磁盘的读比较接近顺序读，能够提升读性能。**

这，就是 MRR 优化的设计思路。此时，语句的执行流程变成了这样：

1. 根据索引 a，定位到满足条件的记录，将 id 值放入 read_rnd_buffer 中 ;
2. 将 read_rnd_buffer 中的 id 进行递增排序；
3. 排序后的 id 数组，依次到主键 id 索引中查记录，并作为结果返回。

这里，read_rnd_buffer 的大小是由 read_rnd_buffer_size 参数控制的。如果步骤 1  中，read_rnd_buffer 放满了，就会先执行完步骤 2 和 3，然后清空 read_rnd_buffer。之后继续找索引 a  的下个记录，并继续循环。

另外需要说明的是，如果你想要稳定地使用 MRR 优化的话，需要设置`set optimizer_switch="mrr_cost_based=off"`。（官方文档的说法，是现在的优化器策略，判断消耗的时候，会更倾向于不使用 MRR，把 mrr_cost_based 设置为 off，就是固定使用 MRR 了。）

下面两幅图就是使用了 MRR 优化后的执行流程和 explain 结果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/d502fbaea7cac6f815c626b078da86c7-1584367401571.jpg)

图 2 MRR 执行流程

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/a513d07ebaf1ae044d44391c89bc6432-1584367401988.png)

图 3 MRR 执行流程的 explain 结果

从图 3 的 explain 结果中，我们可以看到 Extra 字段多了 Using MRR，表示的是用上了 MRR  优化。而且，由于我们在 read_rnd_buffer 中按照 id 做了排序，所以最后得到的结果集也是按照主键 id 递增顺序的，也就是与图 1 结果集中行的顺序相反。

到这里，我们小结一下。

**MRR 能够提升性能的核心**在于，这条查询语句在索引 a 上做的是一个范围查询（也就是说，这是一个多值查询），可以得到足够多的主键 id。这样通过排序以后，再去主键索引查数据，才能体现出“顺序性”的优势。

#### Batched Key Access

理解了 MRR 性能提升的原理，我们就能理解 MySQL 在 5.6 版本后开始引入的 Batched Key Acess(BKA) 算法了。这个 BKA 算法，其实就是对 NLJ 算法的优化。

我们再来看看上一篇文章中用到的 NLJ 算法的流程图：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/10e14e8b9691ac6337d457172b641a3d-1584367401994.jpg)

图 4 Index Nested-Loop Join 流程图

NLJ 算法执行的逻辑是：从驱动表 t1，一行行地取出 a 的值，再到被驱动表 t2 去做 join。也就是说，对于表 t2 来说，每次都是匹配一个值。这时，MRR 的优势就用不上了。

那怎么才能一次性地多传些值给表 t2 呢？方法就是，从表 t1 里一次性地多拿些行出来，一起传给表 t2。

既然如此，我们就把表 t1 的数据取出来一部分，先放到一个临时内存。这个临时内存不是别人，就是 join_buffer。

通过上一篇文章，我们知道 join_buffer 在 BNL 算法里的作用，是暂存驱动表的数据。但是在 NLJ 算法里并没有用。那么，我们刚好就可以复用 join_buffer 到 BKA 算法中。

如图 5 所示，是上面的 NLJ 算法优化后的 BKA 算法的流程。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/31d85666542b9cb0b47a447a8593a47e-1584367402099.jpg)

图 5 Batched Key Acess 流程

图中，我在 join_buffer 中放入的数据是 P1~P100，表示的是只会取查询需要的字段。当然，如果 join buffer 放不下 P1~P100 的所有数据，就会把这 100 行数据分成多段执行上图的流程。

那么，这个 BKA 算法到底要怎么启用呢？

如果要使用 BKA 优化算法的话，你需要在执行 SQL 语句之前，先设置

```bash
set optimizer_switch='mrr=on,mrr_cost_based=off,batched_key_access=on';
```

其中，前两个参数的作用是要启用 MRR。这么做的原因是，BKA 算法的优化要依赖于 MRR。

#### BNL 算法的性能问题

说完了 NLJ 算法的优化，我们再来看 BNL 算法的优化。

我在上一篇文章末尾，给你留下的思考题是，使用 Block Nested-Loop Join(BNL) 算法时，可能会对被驱动表做多次扫描。如果这个被驱动表是一个大的冷数据表，除了会导致 IO 压力大以外，还会对系统有什么影响呢？

在[第 33 篇文章]中，我们说到 InnoDB 的 LRU 算法的时候提到，由于 InnoDB 对 Bufffer Pool 的 LRU 算法做了优化，即：第一次从磁盘读入内存的数据页，会先放在 old 区域。如果 1 秒之后这个数据页不再被访问了，就不会被移动到 LRU  链表头部，这样对 Buffer Pool 的命中率影响就不大。

但是，如果一个使用 BNL 算法的 join 语句，多次扫描一个冷表，而且这个语句执行时间超过 1 秒，就会在再次扫描冷表的时候，把冷表的数据页移到 LRU 链表头部。

这种情况对应的，是冷表的数据量小于整个 Buffer Pool 的 3/8，能够完全放入 old 区域的情况。

如果这个冷表很大，就会出现另外一种情况：业务正常访问的数据页，没有机会进入 young 区域。

由于优化机制的存在，一个正常访问的数据页，要进入 young 区域，需要隔 1 秒后再次被访问到。但是，由于我们的 join  语句在循环读磁盘和淘汰内存页，进入 old 区域的数据页，很可能在 1 秒之内就被淘汰了。这样，就会导致这个 MySQL 实例的 Buffer  Pool 在这段时间内，young 区域的数据页没有被合理地淘汰。

也就是说，这两种情况都会影响 Buffer Pool 的正常运作。

**大表 join 操作虽然对 IO 有影响，但是在语句执行结束后，对 IO 的影响也就结束了。但是，对 Buffer Pool 的影响就是持续性的，需要依靠后续的查询请求慢慢恢复内存命中率。**

为了减少这种影响，你可以考虑增大 join_buffer_size 的值，减少对被驱动表的扫描次数。

也就是说，BNL 算法对系统的影响主要包括三个方面：

1. 可能会多次扫描被驱动表，占用磁盘 IO 资源；
2. 判断 join 条件需要执行 M*N 次对比（M、N 分别是两张表的行数），如果是大表就会占用非常多的 CPU 资源；
3. 可能会导致 Buffer Pool 的热数据被淘汰，影响内存命中率。

我们执行语句之前，需要通过理论分析和查看 explain 结果的方式，确认是否要使用 BNL 算法。如果确认优化器会使用 BNL 算法，就需要做优化。优化的常见做法是，给被驱动表的 join 字段加上索引，把 BNL 算法转成 BKA 算法。

接下来，我们就具体看看，这个优化怎么做？

#### BNL 转 BKA

一些情况下，我们可以直接在被驱动表上建索引，这时就可以直接转成 BKA 算法了。

但是，有时候你确实会碰到一些不适合在被驱动表上建索引的情况。比如下面这个语句：

```csharp
select * from t1 join t2 on (t1.b=t2.b) where t2.b>=1 and t2.b<=2000;
```

我们在文章开始的时候，在表 t2 中插入了 100 万行数据，但是经过 where 条件过滤后，需要参与 join 的只有 2000 行数据。如果这条语句同时是一个低频的 SQL 语句，那么再为这个语句在表 t2 的字段 b 上创建一个索引就很浪费了。

但是，如果使用 BNL 算法来 join 的话，这个语句的执行流程是这样的：

1. 把表 t1 的所有字段取出来，存入 join_buffer 中。这个表只有 1000 行，join_buffer_size 默认值是 256k，可以完全存入。
2. 扫描表 t2，取出每一行数据跟 join_buffer 中的数据进行对比，
   - 如果不满足 t1.b=t2.b，则跳过；
   - 如果满足 t1.b=t2.b, 再判断其他条件，也就是是否满足 t2.b 处于 [1,2000] 的条件，如果是，就作为结果集的一部分返回，否则跳过。

我在上一篇文章中说过，对于表 t2 的每一行，判断 join 是否满足的时候，都需要遍历 join_buffer 中的所有行。因此判断等值条件的次数是 1000*100 万 =10 亿次，这个判断的工作量很大。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/92fbdbfc35da3040396401250cb33f60-1584367402648.png)

图 6 explain 结果

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/d862bc3e88305688df2c354a4b26809c-1584367402652.png)

图 7 语句执行时间

可以看到，explain 结果里 Extra 字段显示使用了 BNL 算法。在我的测试环境里，这条语句需要执行 1 分 11 秒。

在表 t2 的字段 b 上创建索引会浪费资源，但是不创建索引的话这个语句的等值条件要判断 10 亿次，想想也是浪费。那么，有没有两全其美的办法呢？

这时候，我们可以考虑使用临时表。使用临时表的大致思路是：

1. 把表 t2 中满足条件的数据放在临时表 tmp_t 中；
2. 为了让 join 使用 BKA 算法，给临时表 tmp_t 的字段 b 加上索引；
3. 让表 t1 和 tmp_t 做 join 操作。

此时，对应的 SQL 语句的写法如下：

```sql
create temporary table temp_t(id int primary key, a int, b int, index(b))engine=innodb;
insert into temp_t select * from t2 where b>=1 and b<=2000;
select * from t1 join temp_t on (t1.b=temp_t.b);
```

图 8 就是这个语句序列的执行效果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/a80cdffe8173fa0fd8969ed976ac6ac7-1584367402655.png)

图 8 使用临时表的执行效果

可以看到，整个过程 3 个语句执行时间的总和还不到 1 秒，相比于前面的 1 分 11 秒，性能得到了大幅提升。接下来，我们一起看一下这个过程的消耗：

1. 执行 insert 语句构造 temp_t 表并插入数据的过程中，对表 t2 做了全表扫描，这里扫描行数是 100 万。
2. 之后的 join 语句，扫描表 t1，这里的扫描行数是 1000；join 比较过程中，做了 1000 次带索引的查询。相比于优化前的 join 语句需要做 10 亿次条件判断来说，这个优化效果还是很明显的。

总体来看，不论是在原表上加索引，还是用有索引的临时表，我们的思路都是让 join 语句能够用上被驱动表上的索引，来触发 BKA 算法，提升查询性能。

#### 扩展 -hash join

看到这里你可能发现了，其实上面计算 10 亿次那个操作，看上去有点儿傻。如果 join_buffer 里面维护的不是一个无序数组，而是一个哈希表的话，那么就不是 10 亿次判断，而是 100 万次 hash 查找。这样的话，整条语句的执行速度就快多了吧？

确实如此。

这，也正是 MySQL 的优化器和执行器一直被诟病的一个原因：不支持哈希 join。并且，MySQL 官方的 roadmap，也是迟迟没有把这个优化排上议程。

实际上，这个优化思路，我们可以自己实现在业务端。实现流程大致如下：

1. `select * from t1;`取得表 t1 的全部 1000 行数据，在业务端存入一个 hash 结构，比如 C++ 里的 set、PHP 的 dict 这样的数据结构。
2. `select * from t2 where b>=1 and b<=2000;` 获取表 t2 中满足条件的 2000 行数据。
3. 把这 2000 行数据，一行一行地取到业务端，到 hash 结构的数据表中寻找匹配的数据。满足匹配的条件的这行数据，就作为结果集的一行。

理论上，这个过程会比临时表方案的执行速度还要快一些。如果你感兴趣的话，可以自己验证一下。

#### 小结

今天，我和你分享了 Index Nested-Loop Join（NLJ）和 Block Nested-Loop Join（BNL）的优化方法。

在这些优化方法中：

1. BKA 优化是 MySQL 已经内置支持的，建议你默认使用；
2. BNL 算法效率低，建议你都尽量转成 BKA 算法。优化的方向就是给被驱动表的关联字段加上索引；
3. 基于临时表的改进方案，对于能够提前过滤出小数据的 join 语句来说，效果还是很好的；
4. MySQL 目前的版本还不支持 hash join，但你可以配合应用端自己模拟出来，理论上效果要好于临时表的方案。

最后，我给你留下一道思考题吧。

我们在讲 join 语句的这两篇文章中，都只涉及到了两个表的 join。那么，现在有一个三个表 join 的需求，假设这三个表的表结构如下：

```sql
CREATE TABLE `t1` (
 `id` int(11) NOT NULL,
 `a` int(11) DEFAULT NULL,
 `b` int(11) DEFAULT NULL,
 `c` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB; 
create table t2 like t1;
create table t3 like t2;
insert into ... // 初始化三张表的数据
```

语句的需求实现如下的 join 逻辑：

```vbnet
select * from t1 join t2 on(t1.a=t2.a) join t3 on (t2.b=t3.b) where t1.c>=X and t2.c>=Y and t3.c>=Z;
```

现在为了得到最快的执行速度，如果让你来设计表 t1、t2、t3 上的索引，来支持这个 join 语句，你会加哪些索引呢？

同时，如果我希望你用 straight_join 来重写这个语句，配合你创建的索引，你就需要安排连接顺序，你主要考虑的因素是什么呢？

你可以把你的方案和分析写在留言区，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

我在上篇文章最后留给你的问题，已经在本篇文章中解答了。

这里我再根据评论区留言的情况，简单总结下。根据数据量的大小，有这么两种情况：

- @长杰 和 @老杨同志 提到了数据量小于 old 区域内存的情况；
- @Zzz 同学，很认真地看了其他同学的评论，并且提了一个很深的问题。对被驱动表数据量大于 Buffer Pool 的场景，做了很细致的推演和分析。

给这些同学点赞，非常好的思考和讨论。



### 38 都说InnoDB好，那还要不要使用Memory引擎？

我在上一篇文章末尾留给你的问题是：两个 group by 语句都用了 order by null，为什么使用内存临时表得到的语句结果里，0 这个值在最后一行；而使用磁盘临时表得到的结果里，0 这个值在第一行？

今天我们就来看看，出现这个问题的原因吧。

#### 内存表的数据组织结构

为了便于分析，我来把这个问题简化一下，假设有以下的两张表 t1 和 t2，其中表 t1 使用 Memory 引擎， 表 t2 使用 InnoDB 引擎。

```sql
create table t1(id int primary key, c int) engine=Memory;
create table t2(id int primary key, c int) engine=innodb;
insert into t1 values(1,1),(2,2),(3,3),(4,4),(5,5),(6,6),(7,7),(8,8),(9,9),(0,0);
insert into t2 values(1,1),(2,2),(3,3),(4,4),(5,5),(6,6),(7,7),(8,8),(9,9),(0,0);
```

然后，我分别执行 select * from t1 和 select * from t2。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/3fb1100b6e3390357d4efff0ba4765e6-1584367406946.png)

图 1 两个查询结果 -0 的位置

可以看到，内存表 t1 的返回结果里面 0 在最后一行，而 InnoDB 表 t2 的返回结果里 0 在第一行。

出现这个区别的原因，要从这两个引擎的主键索引的组织方式说起。

表 t2 用的是 InnoDB 引擎，它的主键索引 id 的组织方式，你已经很熟悉了：InnoDB 表的数据就放在主键索引树上，主键索引是 B+ 树。所以表 t2 的数据组织方式如下图所示：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/4e29e4f9db55ace6ab09161c68ad8c8d-1584367406946.jpg)

图 2 表 t2 的数据组织

主键索引上的值是有序存储的。在执行 select * 的时候，就会按照叶子节点从左到右扫描，所以得到的结果里，0 就出现在第一行。

与 InnoDB 引擎不同，Memory 引擎的数据和索引是分开的。我们来看一下表 t1 中的数据内容。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/dde03e92074cecba4154d30cd16a9684-1584367406946.jpg)

图 3 表 t1 的数据组织

可以看到，内存表的数据部分以数组的方式单独存放，而主键 id 索引里，存的是每个数据的位置。主键 id 是 hash 索引，可以看到索引上的 key 并不是有序的。

在内存表 t1 中，当我执行 select * 的时候，走的是全表扫描，也就是顺序扫描这个数组。因此，0 就是最后一个被读到，并放入结果集的数据。

可见，InnoDB 和 Memory 引擎的数据组织方式是不同的：

- InnoDB 引擎把数据放在主键索引上，其他索引上保存的是主键 id。这种方式，我们称之为**索引组织表**（Index Organizied Table）。
- 而 Memory 引擎采用的是把数据单独存放，索引上保存数据位置的数据组织形式，我们称之为**堆组织表**（Heap Organizied Table）。

从中我们可以看出，这两个引擎的一些典型不同：

1. InnoDB 表的数据总是有序存放的，而内存表的数据就是按照写入顺序存放的；
2. 当数据文件有空洞的时候，InnoDB 表在插入新数据的时候，为了保证数据有序性，只能在固定的位置写入新值，而内存表找到空位就可以插入新值；
3. 数据位置发生变化的时候，InnoDB 表只需要修改主键索引，而内存表需要修改所有索引；
4. InnoDB 表用主键索引查询时需要走一次索引查找，用普通索引查询的时候，需要走两次索引查找。而内存表没有这个区别，所有索引的“地位”都是相同的。
5. InnoDB 支持变长数据类型，不同记录的长度可能不同；内存表不支持 Blob 和 Text 字段，并且即使定义了 varchar(N)，实际也当作 char(N)，也就是固定长度字符串来存储，因此内存表的每行数据长度相同。

由于内存表的这些特性，每个数据行被删除以后，空出的这个位置都可以被接下来要插入的数据复用。比如，如果要在表 t1 中执行：

```sql
delete from t1 where id=5;
insert into t1 values(10,10);
select * from t1;
```

就会看到返回结果里，id=10 这一行出现在 id=4 之后，也就是原来 id=5 这行数据的位置。

需要指出的是，表 t1 的这个主键索引是哈希索引，因此如果执行范围查询，比如

```csharp
select * from t1 where id<5;
```

是用不上主键索引的，需要走全表扫描。你可以借此再回顾下[第 4 篇文章]的内容。那如果要让内存表支持范围扫描，应该怎么办呢 ？

#### hash 索引和 B-Tree 索引

实际上，内存表也是支 B-Tree 索引的。在 id 列上创建一个 B-Tree 索引，SQL 语句可以这么写：

```sql
alter table t1 add index a_btree_index using btree (id);
```

这时，表 t1 的数据组织形式就变成了这样：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/1788deca56cb83c114d8353c92e3bde3-1584367406946.jpg)

图 4 表 t1 的数据组织 -- 增加 B-Tree 索引

新增的这个 B-Tree 索引你看着就眼熟了，这跟 InnoDB 的 b+ 树索引组织形式类似。

作为对比，你可以看一下这下面这两个语句的输出：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/a85808fcccab24911d257d720550328a-1584367406947.png)

图 5 使用 B-Tree 和 hash 索引查询返回结果对比

可以看到，执行 select * from t1 where id<5 的时候，优化器会选择 B-Tree 索引，所以返回结果是 0 到 4。 使用 force index 强行使用主键 id 这个索引，id=0 这一行就在结果集的最末尾了。

其实，一般在我们的印象中，内存表的优势是速度快，其中的一个原因就是 Memory 引擎支持 hash 索引。当然，更重要的原因是，内存表的所有数据都保存在内存，而内存的读写速度总是比磁盘快。

但是，接下来我要跟你说明，为什么我不建议你在生产环境上使用内存表。这里的原因主要包括两个方面：

1. 锁粒度问题；
2. 数据持久化问题。

#### 内存表的锁

我们先来说说内存表的锁粒度问题。

内存表不支持行锁，只支持表锁。因此，一张表只要有更新，就会堵住其他所有在这个表上的读写操作。

需要注意的是，这里的表锁跟之前我们介绍过的 MDL 锁不同，但都是表级的锁。接下来，我通过下面这个场景，跟你模拟一下内存表的表级锁。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/f216e2d707559ed2ca98fbe21e509f29-1584367406948.png)

图 6 内存表的表锁 -- 复现步骤

在这个执行序列里，session A 的 update 语句要执行 50 秒，在这个语句执行期间 session B 的查询会进入锁等待状态。session C 的 show processlist 结果输出如下：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/14d88076dad6db573f0b66f2c17df916-1584367406948.png)

图 7 内存表的表锁 -- 结果

跟行锁比起来，表锁对并发访问的支持不够好。所以，内存表的锁粒度问题，决定了它在处理并发事务的时候，性能也不会太好。

#### 数据持久性问题

接下来，我们再看看数据持久性的问题。

数据放在内存中，是内存表的优势，但也是一个劣势。因为，数据库重启的时候，所有的内存表都会被清空。

你可能会说，如果数据库异常重启，内存表被清空也就清空了，不会有什么问题啊。但是，在高可用架构下，内存表的这个特点简直可以当做 bug 来看待了。为什么这么说呢？

**我们先看看 M-S 架构下，使用内存表存在的问题。**

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/5b910e4c0f1afa219aeecd1f291c95e9-1584367406948.jpg)

图 8 M-S 基本架构

我们来看一下下面这个时序：

1. 业务正常访问主库；
2. 备库硬件升级，备库重启，内存表 t1 内容被清空；
3. 备库重启后，客户端发送一条 update 语句，修改表 t1 的数据行，这时备库应用线程就会报错“找不到要更新的行”。

这样就会导致主备同步停止。当然，如果这时候发生主备切换的话，客户端会看到，表 t1 的数据“丢失”了。

在图 8 中这种有 proxy 的架构里，大家默认主备切换的逻辑是由数据库系统自己维护的。这样对客户端来说，就是“网络断开，重连之后，发现内存表数据丢失了”。

你可能说这还好啊，毕竟主备发生切换，连接会断开，业务端能够感知到异常。

但是，接下来内存表的这个特性就会让使用现象显得更“诡异”了。由于 MySQL  知道重启之后，内存表的数据会丢失。所以，担心主库重启之后，出现主备不一致，MySQL 在实现上做了这样一件事儿：在数据库重启之后，往  binlog 里面写入一行 DELETE FROM t1。

**如果你使用是如图 9 所示的双 M 结构的话：**

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/4089c9c1f92ce61d2ed779fd0932ba57-1584367406948.jpg)

图 9 双 M 结构

在备库重启的时候，备库 binlog 里的 delete 语句就会传到主库，然后把主库内存表的内容删除。这样你在使用的时候就会发现，主库的内存表数据突然被清空了。

基于上面的分析，你可以看到，内存表并不适合在生产环境上作为普通数据表使用。

有同学会说，但是内存表执行速度快呀。这个问题，其实你可以这么分析：

1. 如果你的表更新量大，那么并发度是一个很重要的参考指标，InnoDB 支持行锁，并发度比内存表好；
2. 能放到内存表的数据量都不大。如果你考虑的是读的性能，一个读 QPS 很高并且数据量不大的表，即使是使用 InnoDB，数据也是都会缓存在 InnoDB Buffer Pool 里的。因此，使用 InnoDB 表的读性能也不会差。

所以，**我建议你把普通内存表都用 InnoDB 表来代替。**但是，有一个场景却是例外的。

这个场景就是，我们在第 35 和 36 篇说到的用户临时表。在数据量可控，不会耗费过多内存的情况下，你可以考虑使用内存表。

内存临时表刚好可以无视内存表的两个不足，主要是下面的三个原因：

1. 临时表不会被其他线程访问，没有并发性的问题；
2. 临时表重启后也是需要删除的，清空数据这个问题不存在；
3. 备库的临时表也不会影响主库的用户线程。

现在，我们回过头再看一下第 35 篇 join 语句优化的例子，当时我建议的是创建一个 InnoDB 临时表，使用的语句序列是：

```sql
create temporary table temp_t(id int primary key, a int, b int, index(b))engine=innodb;
insert into temp_t select * from t2 where b>=1 and b<=2000;
select * from t1 join temp_t on (t1.b=temp_t.b);
```

了解了内存表的特性，你就知道了， 其实这里使用内存临时表的效果更好，原因有三个：

1. 相比于 InnoDB 表，使用内存表不需要写磁盘，往表 temp_t 的写数据的速度更快；
2. 索引 b 使用 hash 索引，查找的速度比 B-Tree 索引快；
3. 临时表数据只有 2000 行，占用的内存有限。

因此，你可以对[第 35 篇文章]的语句序列做一个改写，将临时表 t1 改成内存临时表，并且在字段 b 上创建一个 hash 索引。

```sql
create temporary table temp_t(id int primary key, a int, b int, index (b))engine=memory;
insert into temp_t select * from t2 where b>=1 and b<=2000;
select * from t1 join temp_t on (t1.b=temp_t.b);
```

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/a468ba6d14ea225623074b6255b99f92-1584367406948.png)

图 10 使用内存临时表的执行效果

可以看到，不论是导入数据的时间，还是执行 join 的时间，使用内存临时表的速度都比使用 InnoDB 临时表要更快一些。

#### 小结

今天这篇文章，我从“要不要使用内存表”这个问题展开，和你介绍了 Memory 引擎的几个特性。

可以看到，由于重启会丢数据，如果一个备库重启，会导致主备同步线程停止；如果主库跟这个备库是双 M 架构，还可能导致主库的内存表数据被删掉。

因此，在生产上，我不建议你使用普通内存表。

如果你是 DBA，可以在建表的审核系统中增加这类规则，要求业务改用 InnoDB 表。我们在文中也分析了，其实 InnoDB 表性能还不错，而且数据安全也有保障。而内存表由于不支持行锁，更新语句会阻塞查询，性能也未必就如想象中那么好。

基于内存表的特性，我们还分析了它的一个适用场景，就是内存临时表。内存表支持 hash 索引，这个特性利用起来，对复杂查询的加速效果还是很不错的。

最后，我给你留一个问题吧。

假设你刚刚接手的一个数据库上，真的发现了一个内存表。备库重启之后肯定是会导致备库的内存表数据被清空，进而导致主备同步停止。这时，最好的做法是将它修改成 InnoDB 引擎表。

假设当时的业务场景暂时不允许你修改引擎，你可以加上什么自动化逻辑，来避免主备同步停止呢？

你可以把你的思考和分析写在评论区，我会在下一篇文章的末尾跟你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

今天文章的正文内容，已经回答了我们上期的问题，这里就不再赘述了。

评论区留言点赞板：

> @老杨同志、@poppy、@长杰 这三位同学给出了正确答案，春节期间还持续保持跟进学习，给你们点赞。

### 39 自增主键为什么不是连续的？

在[第 4 篇文章]中，我们提到过自增主键，由于自增主键可以让主键索引尽量地保持递增顺序插入，避免了页分裂，因此索引更紧凑。

之前我见过有的业务设计依赖于自增主键的连续性，也就是说，这个设计假设自增主键是连续的。但实际上，这样的假设是错的，因为自增主键不能保证连续递增。

今天这篇文章，我们就来说说这个问题，看看什么情况下自增主键会出现 “空洞”？

为了便于说明，我们创建一个表 t，其中 id 是自增主键字段、c 是唯一索引。

```sql
CREATE TABLE `t` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `c` int(11) DEFAULT NULL,
  `d` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `c` (`c`)
) ENGINE=InnoDB;
```

#### 自增值保存在哪儿？

在这个空表 t 里面执行 insert into t values(null, 1, 1); 插入一行数据，再执行 show create table 命令，就可以看到如下图所示的结果：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/cb2637cada0201b18650f56875e94fff-1584367406950.png)

图 1 自动生成的 AUTO_INCREMENT 值

可以看到，表定义里面出现了一个 AUTO_INCREMENT=2，表示下一次插入数据时，如果需要自动生成自增值，会生成 id=2。

其实，这个输出结果容易引起这样的误解：自增值是保存在表结构定义里的。实际上，**表的结构定义存放在后缀名为.frm 的文件中，但是并不会保存自增值。**

不同的引擎对于自增值的保存策略不同。

- MyISAM 引擎的自增值保存在数据文件中。
- InnoDB 引擎的自增值，其实是保存在了内存里，并且到了 MySQL 8.0 版本后，才有了“自增值持久化”的能力，也就是才实现了“如果发生重启，表的自增值可以恢复为 MySQL 重启前的值”，具体情况是：
  - 在 MySQL 5.7 及之前的版本，自增值保存在内存里，并没有持久化。每次重启后，第一次打开表的时候，都会去找自增值的最大值  max(id)，然后将 max(id)+1 作为这个表当前的自增值。﻿ 举例来说，如果一个表当前数据行里最大的 id 是  10，AUTO_INCREMENT=11。这时候，我们删除 id=10 的行，AUTO_INCREMENT 还是  11。但如果马上重启实例，重启后这个表的 AUTO_INCREMENT 就会变成 10。﻿ 也就是说，MySQL 重启可能会修改一个表的  AUTO_INCREMENT 的值。
  - 在 MySQL 8.0 版本，将自增值的变更记录在了 redo log 中，重启的时候依靠 redo log 恢复重启之前的值。

理解了 MySQL 对自增值的保存策略以后，我们再看看自增值修改机制。

#### 自增值修改机制

在 MySQL 里面，如果字段 id 被定义为 AUTO_INCREMENT，在插入一行数据的时候，自增值的行为如下：

1. 如果插入数据时 id 字段指定为 0、null 或未指定值，那么就把这个表当前的 AUTO_INCREMENT 值填到自增字段；
2. 如果插入数据时 id 字段指定了具体的值，就直接使用语句里指定的值。

根据要插入的值和当前自增值的大小关系，自增值的变更结果也会有所不同。假设，某次要插入的值是 X，当前的自增值是 Y。

1. 如果 X<Y，那么这个表的自增值不变；
2. 如果 X≥Y，就需要把当前自增值修改为新的自增值。

**新的自增值生成算法是**：从 auto_increment_offset 开始，以 auto_increment_increment 为步长，持续叠加，直到找到第一个大于 X 的值，作为新的自增值。

其中，auto_increment_offset 和 auto_increment_increment 是两个系统参数，分别用来表示自增的初始值和步长，默认值都是 1。

> 备注：在一些场景下，使用的就不全是默认值。比如，双 M 的主备结构里要求双写的时候，我们就可能会设置成 auto_increment_increment=2，让一个库的自增 id 都是奇数，另一个库的自增 id 都是偶数，避免两个库生成的主键发生冲突。

当 auto_increment_offset 和 auto_increment_increment 都是 1 的时候，新的自增值生成逻辑很简单，就是：

1. 如果准备插入的值 >= 当前自增值，新的自增值就是“准备插入的值 +1”；
2. 否则，自增值不变。

这就引入了我们文章开头提到的问题，在这两个参数都设置为 1 的时候，自增主键 id 却不能保证是连续的，这是什么原因呢？

#### 自增值的修改时机

要回答这个问题，我们就要看一下自增值的修改时机。

假设，表 t 里面已经有了 (1,1,1) 这条记录，这时我再执行一条插入数据命令：

```sql
insert into t values(null, 1, 1); 
```

这个语句的执行流程就是：

1. 执行器调用 InnoDB 引擎接口写入一行，传入的这一行的值是 (0,1,1);
2. InnoDB 发现用户没有指定自增 id 的值，获取表 t 当前的自增值 2；
3. 将传入的行的值改成 (2,1,1);
4. 将表的自增值改成 3；
5. 继续执行插入数据操作，由于已经存在 c=1 的记录，所以报 Duplicate key error，语句返回。

对应的执行流程图如下：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/f16d89a6e7ad6e2cde13b32bb2292dd3-1584367406951.jpg)

图 2 insert(null, 1,1) 唯一键冲突

可以看到，这个表的自增值改成 3，是在真正执行插入数据的操作之前。这个语句真正执行的时候，因为碰到唯一键 c 冲突，所以 id=2 这一行并没有插入成功，但也没有将自增值再改回去。

所以，在这之后，再插入新的数据行时，拿到的自增 id 就是 3。也就是说，出现了自增主键不连续的情况。

如图 3 所示就是完整的演示结果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/77b87820b649692a555f19b562d5d926-1584367406952.png)

图 3 一个自增主键 id 不连续的复现步骤

可以看到，这个操作序列复现了一个自增主键 id 不连续的现场 (没有 id=2 的行）。可见，**唯一键冲突是导致自增主键 id 不连续的第一种原因。**

同样地，事务**回滚也会产生类似的现象，这就是第二种原因。**

下面这个语句序列就可以构造不连续的自增 id，你可以自己验证一下。

```sql
insert into t values(null,1,1);
begin;
insert into t values(null,2,2);
rollback;
insert into t values(null,2,2);
// 插入的行是 (3,2,2)
```

你可能会问，为什么在出现唯一键冲突或者回滚的时候，MySQL 没有把表 t 的自增值改回去呢？如果把表 t 的当前自增值从 3 改回 2，再插入新数据的时候，不就可以生成 id=2 的一行数据了吗？

其实，MySQL 这么设计是为了提升性能。接下来，我就跟你分析一下这个设计思路，看看**自增值为什么不能回退。**

假设有两个并行执行的事务，在申请自增值的时候，为了避免两个事务申请到相同的自增 id，肯定要加锁，然后顺序申请。

1. 假设事务 A 申请到了 id=2， 事务 B 申请到 id=3，那么这时候表 t 的自增值是 4，之后继续执行。
2. 事务 B 正确提交了，但事务 A 出现了唯一键冲突。
3. 如果允许事务 A 把自增 id 回退，也就是把表 t 的当前自增值改回 2，那么就会出现这样的情况：表里面已经有 id=3 的行，而当前的自增 id 值是 2。
4. 接下来，继续执行的其他事务就会申请到 id=2，然后再申请到 id=3。这时，就会出现插入语句报错“主键冲突”。

而为了解决这个主键冲突，有两种方法：

1. 每次申请 id 之前，先判断表里面是否已经存在这个 id。如果存在，就跳过这个 id。但是，这个方法的成本很高。因为，本来申请 id 是一个很快的操作，现在还要再去主键索引树上判断 id 是否存在。
2. 把自增 id 的锁范围扩大，必须等到一个事务执行完成并提交，下一个事务才能再申请自增 id。这个方法的问题，就是锁的粒度太大，系统并发能力大大下降。

可见，这两个方法都会导致性能问题。造成这些麻烦的罪魁祸首，就是我们假设的这个“允许自增 id 回退”的前提导致的。

因此，InnoDB 放弃了这个设计，语句执行失败也不回退自增 id。也正是因为这样，所以才只保证了自增 id 是递增的，但不保证是连续的。

#### 自增锁的优化

可以看到，自增 id 锁并不是一个事务锁，而是每次申请完就马上释放，以便允许别的事务再申请。其实，在 MySQL 5.1 版本之前，并不是这样的。

接下来，我会先给你介绍下自增锁设计的历史，这样有助于你分析接下来的一个问题。

在 MySQL 5.0 版本的时候，自增锁的范围是语句级别。也就是说，如果一个语句申请了一个表自增锁，这个锁会等语句执行结束以后才释放。显然，这样设计会影响并发度。

MySQL 5.1.22 版本引入了一个新策略，新增参数 innodb_autoinc_lock_mode，默认值是 1。

1. 这个参数的值被设置为 0 时，表示采用之前 MySQL 5.0 版本的策略，即语句执行结束后才释放锁；
2. 这个参数的值被设置为 1 时：
   - 普通 insert 语句，自增锁在申请之后就马上释放；
   - 类似 insert … select 这样的批量插入数据的语句，自增锁还是要等语句结束后才被释放；
3. 这个参数的值被设置为 2 时，所有的申请自增主键的动作都是申请后就释放锁。

你一定有两个疑问：**为什么默认设置下，insert … select 要使用语句级的锁？为什么这个参数的默认值不是 2？**

答案是，这么设计还是为了数据的一致性。

我们一起来看一下这个场景：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/e0a69e151277de54a8262657e4ec89df-1584367406952.png)

图 4 批量插入数据的自增锁

在这个例子里，我往表 t1 中插入了 4 行数据，然后创建了一个相同结构的表 t2，然后两个 session 同时执行向表 t2 中插入数据的操作。

你可以设想一下，如果 session B 是申请了自增值以后马上就释放自增锁，那么就可能出现这样的情况：

- session B 先插入了两个记录，(1,1,1)、(2,2,2)；
- 然后，session A 来申请自增 id 得到 id=3，插入了（3,5,5)；
- 之后，session B 继续执行，插入两条记录 (4,3,3)、 (5,4,4)。

你可能会说，这也没关系吧，毕竟 session B 的语义本身就没有要求表 t2 的所有行的数据都跟 session A 相同。

是的，从数据逻辑上看是对的。但是，如果我们现在的 binlog_format=statement，你可以设想下，binlog 会怎么记录呢？

由于两个 session 是同时执行插入数据命令的，所以 binlog 里面对表 t2 的更新日志只有两种情况：要么先记 session A 的，要么先记 session B 的。

但不论是哪一种，这个 binlog 拿去从库执行，或者用来恢复临时实例，备库和临时实例里面，session B 这个语句执行出来，生成的结果里面，id 都是连续的。这时，这个库就发生了数据不一致。

你可以分析一下，出现这个问题的原因是什么？

其实，这是因为原库 session B 的 insert 语句，生成的 id 不连续。这个不连续的 id，用 statement 格式的 binlog 来串行执行，是执行不出来的。

而要解决这个问题，有两种思路：

1. 一种思路是，让原库的批量插入数据语句，固定生成连续的 id 值。所以，自增锁直到语句执行结束才释放，就是为了达到这个目的。
2. 另一种思路是，在 binlog 里面把插入数据的操作都如实记录进来，到备库执行的时候，不再依赖于自增主键去生成。这种情况，其实就是 innodb_autoinc_lock_mode 设置为 2，同时 binlog_format 设置为 row。

因此，**在生产上，尤其是有 insert … select 这种批量插入数据的场景时，从并发插入数据性能的角度考虑，我建议你这样设置：innodb_autoinc_lock_mode=2 ，并且 binlog_format=row**. 这样做，既能提升并发性，又不会出现数据一致性问题。

需要注意的是，我这里说的**批量插入数据，包含的语句类型是 insert … select、replace … select 和 load data 语句。**

但是，在普通的 insert 语句里面包含多个 value 值的情况下，即使 innodb_autoinc_lock_mode 设置为  1，也不会等语句执行完成才释放锁。因为这类语句在申请自增 id 的时候，是可以精确计算出需要多少个 id  的，然后一次性申请，申请完成后锁就可以释放了。

也就是说，批量插入数据的语句，之所以需要这么设置，是因为“不知道要预先申请多少个 id”。

既然预先不知道要申请多少个自增 id，那么一种直接的想法就是需要一个时申请一个。但如果一个 select … insert 语句要插入  10 万行数据，按照这个逻辑的话就要申请 10 万次。显然，这种申请自增 id  的策略，在大批量插入数据的情况下，不但速度慢，还会影响并发插入的性能。

因此，对于批量插入数据的语句，MySQL 有一个批量申请自增 id 的策略：

1. 语句执行过程中，第一次申请自增 id，会分配 1 个；
2. 1 个用完以后，这个语句第二次申请自增 id，会分配 2 个；
3. 2 个用完以后，还是这个语句，第三次申请自增 id，会分配 4 个；
4. 依此类推，同一个语句去申请自增 id，每次申请到的自增 id 个数都是上一次的两倍。

举个例子，我们一起看看下面的这个语句序列：

```sql
insert into t values(null, 1,1);
insert into t values(null, 2,2);
insert into t values(null, 3,3);
insert into t values(null, 4,4);
create table t2 like t;
insert into t2(c,d) select c,d from t;
insert into t2 values(null, 5,5);
```

insert…select，实际上往表 t2 中插入了 4 行数据。但是，这四行数据是分三次申请的自增 id，第一次申请到了 id=1，第二次被分配了 id=2 和 id=3， 第三次被分配到 id=4 到 id=7。

由于这条语句实际只用上了 4 个 id，所以 id=5 到 id=7 就被浪费掉了。之后，再执行 insert into t2 values(null, 5,5)，实际上插入的数据就是（8,5,5)。

**这是主键 id 出现自增 id 不连续的第三种原因。**

#### 小结

今天，我们从“自增主键为什么会出现不连续的值”这个问题开始，首先讨论了自增值的存储。

在 MyISAM 引擎里面，自增值是被写在数据文件上的。而在 InnoDB 中，自增值是被记录在内存的。MySQL 直到 8.0 版本，才给 InnoDB 表的自增值加上了持久化的能力，确保重启前后一个表的自增值不变。

然后，我和你分享了在一个语句执行过程中，自增值改变的时机，分析了为什么 MySQL 在事务回滚的时候不能回收自增 id。

MySQL 5.1.22 版本开始引入的参数  innodb_autoinc_lock_mode，控制了自增值申请时的锁范围。从并发性能的角度考虑，我建议你将其设置为 2，同时将  binlog_format 设置为 row。我在前面的文章中其实多次提到，binlog_format 设置为  row，是很有必要的。今天的例子给这个结论多了一个理由。

最后，我给你留一个思考题吧。

在最后一个例子中，执行 insert into t2(c,d) select c,d from t;  这个语句的时候，如果隔离级别是可重复读（repeatable read），binlog_format=statement。这个语句会对表 t  的所有记录和间隙加锁。

你觉得为什么需要这么做呢？

你可以把你的思考和分析写在评论区，我会在下一篇文章和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

上期的问题是，如果你维护的 MySQL 系统里有内存表，怎么避免内存表突然丢数据，然后导致主备同步停止的情况。

我们假设的是主库暂时不能修改引擎，那么就把备库的内存表引擎先都改成 InnoDB。对于每个内存表，执行

```sql
set sql_log_bin=off;
alter table tbl_name engine=innodb;
```

这样就能避免备库重启的时候，数据丢失的问题。

由于主库重启后，会往 binlog 里面写“delete from tbl_name”，这个命令传到备库，备库的同名的表数据也会被清空。

因此，就不会出现主备同步停止的问题。

如果由于主库异常重启，触发了 HA，这时候我们之前修改过引擎的备库变成了主库。而原来的主库变成了新备库，在新备库上把所有的内存表（这时候表里没数据）都改成 InnoDB 表。

所以，如果我们不能直接修改主库上的表引擎，可以配置一个自动巡检的工具，在备库上发现内存表就把引擎改了。

同时，跟业务开发同学约定好建表规则，避免创建新的内存表。

评论区留言点赞板：

> 大家在春节期间还坚持看专栏，并且深入地思考和回复，给大家点赞。 @长杰 同学提到的将数据保存到 InnoDB  表用来持久化，也是一个方法。不过，我还是建议釜底抽薪，直接修改备库的内存表的引擎。 @老杨同志  提到的是主库异常重启的场景，这时候是不会报主备不一致的，因为主库重启的时候写了 delete from tbl_name，主备的内存表都清空了。

### 40 insert语句的锁为什么这么多？

在上一篇文章中，我提到 MySQL 对自增主键锁做了优化，尽量在申请到自增 id 以后，就释放自增锁。

因此，insert 语句是一个很轻量的操作。不过，这个结论对于“普通的 insert 语句”才有效。也就是说，还有些 insert 语句是属于“特殊情况”的，在执行过程中需要给其他资源加锁，或者无法在申请到自增 id 以后就立马释放自增锁。

那么，今天这篇文章，我们就一起来聊聊这个话题。

#### insert … select 语句

我们先从昨天的问题说起吧。表 t 和 t2 的表结构、初始化数据语句如下，今天的例子我们还是针对这两个表展开。

```sql
CREATE TABLE `t` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `c` int(11) DEFAULT NULL,
  `d` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `c` (`c`)
) ENGINE=InnoDB; 
insert into t values(null, 1,1);
insert into t values(null, 2,2);
insert into t values(null, 3,3);
insert into t values(null, 4,4); 
create table t2 like t
```

现在，我们一起来看看为什么在可重复读隔离级别下，binlog_format=statement 时执行：

```csharp
insert into t2(c,d) select c,d from t;
```

这个语句时，需要对表 t 的所有行和间隙加锁呢？

其实，这个问题我们需要考虑的还是日志和数据的一致性。我们看下这个执行序列：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/33e513ee55d5700dc67f32bcdafb9386-1584367406953.png)

图 1 并发 insert 场景

实际的执行效果是，如果 session B 先执行，由于这个语句对表 t 主键索引加了 (-∞,1] 这个 next-key lock，会在语句执行完成后，才允许 session A 的 insert 语句执行。

但如果没有锁的话，就可能出现 session B 的 insert 语句先执行，但是后写入 binlog 的情况。于是，在 binlog_format=statement 的情况下，binlog 里面就记录了这样的语句序列：

```sql
insert into t values(-1,-1,-1);
insert into t2(c,d) select c,d from t;
```

这个语句到了备库执行，就会把 id=-1 这一行也写到表 t2 中，出现主备不一致。

#### insert 循环写入

当然了，执行 insert … select 的时候，对目标表也不是锁全表，而是只锁住需要访问的资源。

如果现在有这么一个需求：要往表 t2 中插入一行数据，这一行的 c 值是表 t 中 c 值的最大值加 1。

此时，我们可以这么写这条 SQL 语句 ：

```sql
insert into t2(c,d)  (select c+1, d from t force index(c) order by c desc limit 1);
```

这个语句的加锁范围，就是表 t 索引 c 上的 (3,4] 和 (4,supremum] 这两个 next-key lock，以及主键索引上 id=4 这一行。

它的执行流程也比较简单，从表 t 中按照索引 c 倒序，扫描第一行，拿到结果写入到表 t2 中。

因此整条语句的扫描行数是 1。

这个语句执行的慢查询日志（slow log），如下图所示：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/3efdf8256309a44e23d93089459eda74-1584367406953.png)

图 2 慢查询日志 -- 将数据插入表 t2

通过这个慢查询日志，我们看到 Rows_examined=1，正好验证了执行这条语句的扫描行数为 1。

那么，如果我们是要把这样的一行数据插入到表 t 中的话：

```sql
insert into t(c,d)  (select c+1, d from t force index(c) order by c desc limit 1);
```

语句的执行流程是怎样的？扫描行数又是多少呢？

这时候，我们再看慢查询日志就会发现不对了。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/6f90b04c09188bff11dae6e788abb918-1584367406953.png)

图 3 慢查询日志 -- 将数据插入表 t

可以看到，这时候的 Rows_examined 的值是 5。

我在前面的文章中提到过，希望你都能够学会用 explain 的结果来“脑补”整条语句的执行过程。今天，我们就来一起试试。

如图 4 所示就是这条语句的 explain 结果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/d7270781ee3f216325b73bd53999b82a-1584367406953.png)

图 4 explain 结果

从 Extra 字段可以看到“Using temporary”字样，表示这个语句用到了临时表。也就是说，执行过程中，需要把表 t 的内容读出来，写入临时表。

图中 rows 显示的是 1，我们不妨先对这个语句的执行流程做一个猜测：如果说是把子查询的结果读出来（扫描 1 行），写入临时表，然后再从临时表读出来（扫描 1 行），写回表 t 中。那么，这个语句的扫描行数就应该是 2，而不是 5。

所以，这个猜测不对。实际上，Explain 结果里的 rows=1 是因为受到了 limit 1 的影响。

从另一个角度考虑的话，我们可以看看 InnoDB 扫描了多少行。如图 5 所示，是在执行这个语句前后查看 Innodb_rows_read 的结果。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/489281d8029e8f60979cb7c4494010d7-1584367406953.png)

图 5 查看 Innodb_rows_read 变化

可以看到，这个语句执行前后，Innodb_rows_read 的值增加了 4。因为默认临时表是使用 Memory 引擎的，所以这 4 行查的都是表 t，也就是说对表 t 做了全表扫描。

这样，我们就把整个执行过程理清楚了：

1. 创建临时表，表里有两个字段 c 和 d。
2. 按照索引 c 扫描表 t，依次取 c=4、3、2、1，然后回表，读到 c 和 d 的值写入临时表。这时，Rows_examined=4。
3. 由于语义里面有 limit 1，所以只取了临时表的第一行，再插入到表 t 中。这时，Rows_examined 的值加 1，变成了 5。

也就是说，这个语句会导致在表 t 上做全表扫描，并且会给索引 c 上的所有间隙都加上共享的 next-key lock。所以，这个语句执行期间，其他事务不能在这个表上插入数据。

至于这个语句的执行为什么需要临时表，原因是这类一边遍历数据，一边更新数据的情况，如果读出来的数据直接写回原表，就可能在遍历过程中，读到刚刚插入的记录，新插入的记录如果参与计算逻辑，就跟语义不符。

由于实现上这个语句没有在子查询中就直接使用 limit 1，从而导致了这个语句的执行需要遍历整个表  t。它的优化方法也比较简单，就是用前面介绍的方法，先 insert into 到临时表 temp_t，这样就只需要扫描一行；然后再从表  temp_t 里面取出这行数据插入表 t1。

当然，由于这个语句涉及的数据量很小，你可以考虑使用内存临时表来做这个优化。使用内存临时表优化时，语句序列的写法如下：

```sql
create temporary table temp_t(c int,d int) engine=memory;
insert into temp_t  (select c+1, d from t force index(c) order by c desc limit 1);
insert into t select * from temp_t;
drop table temp_t;
```

#### insert 唯一键冲突

前面的两个例子是使用 insert … select 的情况，接下来我要介绍的这个例子就是最常见的 insert 语句出现唯一键冲突的情况。

对于有唯一键的表，插入数据时出现唯一键冲突也是常见的情况了。我先给你举一个简单的唯一键冲突的例子。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/83fb2d877932941b230d6b5be8cca6ca-1584367406954.png)

图 6 唯一键冲突加锁

这个例子也是在可重复读（repeatable read）隔离级别下执行的。可以看到，session B 要执行的 insert 语句进入了锁等待状态。

也就是说，session A 执行的 insert  语句，发生唯一键冲突的时候，并不只是简单地报错返回，还在冲突的索引上加了锁。我们前面说过，一个 next-key lock  就是由它右边界的值定义的。这时候，session A 持有索引 c 上的 (5,10] 共享 next-key lock（读锁）。

至于为什么要加这个读锁，其实我也没有找到合理的解释。从作用上来看，这样做可以避免这一行被别的事务删掉。

这里[官方文档](https://dev.mysql.com/doc/refman/8.0/en/innodb-locks-set.html)有一个描述错误，认为如果冲突的是主键索引，就加记录锁，唯一索引才加 next-key lock。但实际上，这两类索引冲突加的都是 next-key lock。

> 备注：这个 bug，是我在写这篇文章查阅文档时发现的，已经[发给官方](https://bugs.mysql.com/bug.php?id=93806)并被 verified 了。

有同学在前面文章的评论区问到，在有多个唯一索引的表中并发插入数据时，会出现死锁。但是，由于他没有提供复现方法或者现场，我也无法做分析。所以，我建议你在评论区发问题的时候，尽量同时附上复现方法，或者现场信息，这样我才好和你一起分析问题。

这里，我就先和你分享一个经典的死锁场景，如果你还遇到过其他唯一键冲突导致的死锁场景，也欢迎给我留言。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/63658eb26e7a03b49f123fceed94cd2d-1584367406954.png)

图 7 唯一键冲突 -- 死锁

在 session A 执行 rollback 语句回滚的时候，session C 几乎同时发现死锁并返回。

这个死锁产生的逻辑是这样的：

1. 在 T1 时刻，启动 session A，并执行 insert 语句，此时在索引 c 的 c=5 上加了记录锁。注意，这个索引是唯一索引，因此退化为记录锁（如果你的印象模糊了，可以回顾下[第 21 篇文章]介绍的加锁规则）。
2. 在 T2 时刻，session B 要执行相同的 insert 语句，发现了唯一键冲突，加上读锁；同样地，session C 也在索引 c 上，c=5 这一个记录上，加了读锁。
3. T3 时刻，session A 回滚。这时候，session B 和 session C 都试图继续执行插入操作，都要加上写锁。两个 session 都要等待对方的行锁，所以就出现了死锁。

这个流程的状态变化图如下所示。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/3e0bf1a1241931c14360e73fd10032b8-1584367406954.jpg)

图 8 状态变化图 -- 死锁

#### insert into … on duplicate key update

上面这个例子是主键冲突后直接报错，如果是改写成

```sql
insert into t values(11,10,10) on duplicate key update d=100; 
```

的话，就会给索引 c 上 (5,10] 加一个排他的 next-key lock（写锁）。

**insert into … on duplicate key update 这个语义的逻辑是，插入一行数据，如果碰到唯一键约束，就执行后面的更新语句。**

注意，如果有多个列违反了唯一性约束，就会按照索引的顺序，修改跟第一个索引冲突的行。

现在表 t 里面已经有了 (1,1,1) 和 (2,2,2) 这两行，我们再来看看下面这个语句执行的效果：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/5f384d6671c87a60e1ec7e490447d702-1584367407242.png)

图 9 两个唯一键同时冲突

可以看到，主键 id 是先判断的，MySQL 认为这个语句跟 id=2 这一行冲突，所以修改的是 id=2 的行。

需要注意的是，执行这条语句的 affected rows 返回的是 2，很容易造成误解。实际上，真正更新的只有一行，只是在代码实现上，insert 和 update 都认为自己成功了，update 计数加了 1， insert 计数也加了 1。

#### 小结

今天这篇文章，我和你介绍了几种特殊情况下的 insert 语句。

insert … select 是很常见的在两个表之间拷贝数据的方法。你需要注意，在可重复读隔离级别下，这个语句会给 select 的表里扫描到的记录和间隙加读锁。

而如果 insert 和 select 的对象是同一个表，则有可能会造成循环写入。这种情况下，我们需要引入用户临时表来做优化。

insert 语句如果出现唯一键冲突，会在冲突的唯一值上加共享的 next-key lock(S 锁)。因此，碰到由于唯一键约束导致报错后，要尽快提交或回滚事务，避免加锁时间过长。

最后，我给你留一个问题吧。

你平时在两个表之间拷贝数据用的是什么方法，有什么注意事项吗？在你的应用场景里，这个方法，相较于其他方法的优势是什么呢？

你可以把你的经验和分析写在评论区，我会在下一篇文章的末尾选取有趣的评论来和你一起分析。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

我们已经在文章中回答了上期问题。

有同学提到，如果在 insert … select 执行期间有其他线程操作原表，会导致逻辑错误。其实，这是不会的，如果不加锁，就是快照读。

一条语句执行期间，它的一致性视图是不会修改的，所以即使有其他事务修改了原表的数据，也不会影响这条语句看到的数据。

评论区留言点赞板：

> @长杰 同学回答得非常准确。

### 41 怎么最快地复制一张表？

我在上一篇文章最后，给你留下的问题是怎么在两张表中拷贝数据。如果可以控制对源表的扫描行数和加锁范围很小的话，我们简单地使用 insert … select 语句即可实现。

当然，为了避免对源表加读锁，更稳妥的方案是先将数据写到外部文本文件，然后再写回目标表。这时，有两种常用的方法。接下来的内容，我会和你详细展开一下这两种方法。

为了便于说明，我还是先创建一个表 db1.t，并插入 1000 行数据，同时创建一个相同结构的表 db2.t。

```sql
create database db1;
use db1; 
create table t(id int primary key, a int, b int, index(a))engine=innodb;
delimiter ;;
  create procedure idata()
  begin
    declare i int;
    set i=1;
    while(i<=1000)do
      insert into t values(i,i,i);
      set i=i+1;
    end while;
  end;;
delimiter ;
call idata(); 
create database db2;
create table db2.t like db1.t
```

假设，我们要把 db1.t 里面 a>900 的数据行导出来，插入到 db2.t 中。

#### mysqldump 方法

一种方法是，使用 mysqldump 命令将数据导出成一组 INSERT 语句。你可以使用下面的命令：

```bash
mysqldump -h$host -P$port -u$user --add-locks=0 --no-create-info --single-transaction  --set-gtid-purged=OFF db1 t --where="a>900" --result-file=/client_tmp/t.sql
```

把结果输出到临时文件。

这条命令中，主要参数含义如下：

1. –single-transaction 的作用是，在导出数据的时候不需要对表 db1.t 加表锁，而是使用 START TRANSACTION WITH CONSISTENT SNAPSHOT 的方法；
2. –add-locks 设置为 0，表示在输出的文件结果里，不增加" LOCK TABLES `t` WRITE;" ；
3. –no-create-info 的意思是，不需要导出表结构；
4. –set-gtid-purged=off 表示的是，不输出跟 GTID 相关的信息；
5. –result-file 指定了输出文件的路径，其中 client 表示生成的文件是在客户端机器上的。

通过这条 mysqldump 命令生成的 t.sql 文件中就包含了如图 1 所示的 INSERT 语句。

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/8acdcefcaf5c9940570bf7e8f73dbdde-1584367407247.png)

图 1 mysqldump 输出文件的部分结果

可以看到，一条 INSERT 语句里面会包含多个 value 对，这是为了后续用这个文件来写入数据的时候，执行速度可以更快。

如果你希望生成的文件中一条 INSERT 语句只插入一行数据的话，可以在执行 mysqldump 命令时，加上参数–skip-extended-insert。

然后，你可以通过下面这条命令，将这些 INSERT 语句放到 db2 库里去执行。

```bash
mysql -h127.0.0.1 -P13000  -uroot db2 -e "source /client_tmp/t.sql"
```

需要说明的是，source 并不是一条 SQL 语句，而是一个客户端命令。mysql 客户端执行这个命令的流程是这样的：

1. 打开文件，默认以分号为结尾读取一条条的 SQL 语句；
2. 将 SQL 语句发送到服务端执行。

也就是说，服务端执行的并不是这个“source t.sql"语句，而是 INSERT 语句。所以，不论是在慢查询日志（slow log），还是在 binlog，记录的都是这些要被真正执行的 INSERT 语句。

#### 导出 CSV 文件

另一种方法是直接将结果导出成.csv 文件。MySQL 提供了下面的语法，用来将查询结果导出到服务端本地目录：

```csharp
select * from db1.t where a>900 into outfile '/server_tmp/t.csv';
```

我们在使用这条语句时，需要注意如下几点。

1. 这条语句会将结果保存在服务端。如果你执行命令的客户端和 MySQL 服务端不在同一个机器上，客户端机器的临时目录下是不会生成 t.csv 文件的。
2. into outfile 指定了文件的生成位置（/server_tmp/），这个位置必须受参数 secure_file_priv 的限制。参数 secure_file_priv 的可选值和作用分别是：
   - 如果设置为 empty，表示不限制文件生成的位置，这是不安全的设置；
   - 如果设置为一个表示路径的字符串，就要求生成的文件只能放在这个指定的目录，或者它的子目录；
   - 如果设置为 NULL，就表示禁止在这个 MySQL 实例上执行 select … into outfile 操作。
3. 这条命令不会帮你覆盖文件，因此你需要确保 /server_tmp/t.csv 这个文件不存在，否则执行语句时就会因为有同名文件的存在而报错。
4. 这条命令生成的文本文件中，原则上一个数据行对应文本文件的一行。但是，如果字段中包含换行符，在生成的文本中也会有换行符。不过类似换行符、制表符这类符号，前面都会跟上“\”这个转义符，这样就可以跟字段之间、数据行之间的分隔符区分开。

得到.csv 导出文件后，你就可以用下面的 load data 命令将数据导入到目标表 db2.t 中。

```lua
load data infile '/server_tmp/t.csv' into table db2.t;
```

这条语句的执行流程如下所示。

1. 打开文件 /server_tmp/t.csv，以制表符 (\t) 作为字段间的分隔符，以换行符（\n）作为记录之间的分隔符，进行数据读取；
2. 启动事务。
3. 判断每一行的字段数与表 db2.t 是否相同：
   - 若不相同，则直接报错，事务回滚；
   - 若相同，则构造成一行，调用 InnoDB 引擎接口，写入到表中。
4. 重复步骤 3，直到 /server_tmp/t.csv 整个文件读入完成，提交事务。

你可能有一个疑问，**如果 binlog_format=statement，这个 load 语句记录到 binlog 里以后，怎么在备库重放呢？**

由于 /server_tmp/t.csv 文件只保存在主库所在的主机上，如果只是把这条语句原文写到 binlog 中，在备库执行的时候，备库的本地机器上没有这个文件，就会导致主备同步停止。

所以，这条语句执行的完整流程，其实是下面这样的。

1. 主库执行完成后，将 /server_tmp/t.csv 文件的内容直接写到 binlog 文件中。
2. 往 binlog 文件中写入语句 load data local infile ‘/tmp/SQL_LOAD_MB-1-0’ INTO TABLE `db2`.`t`。
3. 把这个 binlog 日志传到备库。
4. 备库的 apply 线程在执行这个事务日志时： a. 先将 binlog 中 t.csv 文件的内容读出来，写入到本地临时目录  /tmp/SQL_LOAD_MB-1-0 中； b. 再执行 load data 语句，往备库的 db2.t 表中插入跟主库相同的数据。

执行流程如图 2 所示：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/3a6790bc933af5ac45a75deba0f52cfd-1584367390347.jpg)

图 2 load data 的同步流程

注意，这里备库执行的 load data 语句里面，多了一个“local”。它的意思是“将执行这条命令的客户端所在机器的本地文件 /tmp/SQL_LOAD_MB-1-0 的内容，加载到目标表 db2.t 中”。

也就是说，**load data 命令有两种用法**：

1. 不加“local”，是读取服务端的文件，这个文件必须在 secure_file_priv 指定的目录或子目录下；
2. 加上“local”，读取的是客户端的文件，只要 mysql 客户端有访问这个文件的权限即可。这时候，MySQL 客户端会先把本地文件传给服务端，然后执行上述的 load data 流程。

另外需要注意的是，**select …into outfile 方法不会生成表结构文件**, 所以我们导数据时还需要单独的命令得到表结构定义。mysqldump 提供了一个–tab 参数，可以同时导出表结构定义文件和 csv 数据文件。这条命令的使用方法如下：

```swift
mysqldump -h$host -P$port -u$user ---single-transaction  --set-gtid-purged=OFF db1 t --where="a>900" --tab=$secure_file_priv
```

这条命令会在 $secure_file_priv 定义的目录下，创建一个 t.sql 文件保存建表语句，同时创建一个 t.txt 文件保存 CSV 数据。

#### 物理拷贝方法

前面我们提到的 mysqldump 方法和导出 CSV 文件的方法，都是逻辑导数据的方法，也就是将数据从表 db1.t 中读出来，生成文本，然后再写入目标表 db2.t 中。

你可能会问，有物理导数据的方法吗？比如，直接把 db1.t 表的.frm 文件和.ibd 文件拷贝到 db2 目录下，是否可行呢？

答案是不行的。

因为，一个 InnoDB 表，除了包含这两个物理文件外，还需要在数据字典中注册。直接拷贝这两个文件的话，因为数据字典中没有 db2.t 这个表，系统是不会识别和接受它们的。

不过，在 MySQL 5.6 版本引入了**可传输表空间**(transportable tablespace) 的方法，可以通过导出 + 导入表空间的方式，实现物理拷贝表的功能。

假设我们现在的目标是在 db1 库下，复制一个跟表 t 相同的表 r，具体的执行步骤如下：

1. 执行 create table r like t，创建一个相同表结构的空表；
2. 执行 alter table r discard tablespace，这时候 r.ibd 文件会被删除；
3. 执行 flush table t for export，这时候 db1 目录下会生成一个 t.cfg 文件；
4. 在 db1 目录下执行 cp t.cfg r.cfg; cp t.ibd r.ibd；这两个命令（这里需要注意的是，拷贝得到的两个文件，MySQL 进程要有读写权限）；
5. 执行 unlock tables，这时候 t.cfg 文件会被删除；
6. 执行 alter table r import tablespace，将这个 r.ibd 文件作为表 r 的新的表空间，由于这个文件的数据内容和 t.ibd 是相同的，所以表 r 中就有了和表 t 相同的数据。

至此，拷贝表数据的操作就完成了。这个流程的执行过程图如下：

![img](http://learn.lianglianglee.com/%E6%9E%81%E5%AE%A2%E6%97%B6%E9%97%B4/assets/ba1ced43eed4a55d49435c062fee21a7-1584367390359.jpg)

图 3 物理拷贝表

关于拷贝表的这个流程，有以下几个注意点：

1. 在第 3 步执行完 flsuh table 命令之后，db1.t 整个表处于只读状态，直到执行 unlock tables 命令后才释放读锁；
2. 在执行 import tablespace 的时候，为了让文件里的表空间 id 和数据字典中的一致，会修改 r.ibd 的表空间  id。而这个表空间 id 存在于每一个数据页中。因此，如果是一个很大的文件（比如 TB 级别），每个数据页都需要修改，所以你会看到这个  import 语句的执行是需要一些时间的。当然，如果是相比于逻辑导入的方法，import 语句的耗时是非常短的。

#### 小结

今天这篇文章，我和你介绍了三种将一个表的数据导入到另外一个表中的方法。

我们来对比一下这三种方法的优缺点。

1. 物理拷贝的方式速度最快，尤其对于大表拷贝来说是最快的方法。如果出现误删表的情况，用备份恢复出误删之前的临时库，然后再把临时库中的表拷贝到生产库上，是恢复数据最快的方法。但是，这种方法的使用也有一定的局限性：
   - 必须是全表拷贝，不能只拷贝部分数据；
   - 需要到服务器上拷贝数据，在用户无法登录数据库主机的场景下无法使用；
   - 由于是通过拷贝物理文件实现的，源表和目标表都是使用 InnoDB 引擎时才能使用。
2. 用 mysqldump 生成包含 INSERT 语句文件的方法，可以在 where 参数增加过滤条件，来实现只导出部分数据。这个方式的不足之一是，不能使用 join 这种比较复杂的 where 条件写法。
3. 用 select … into outfile 的方法是最灵活的，支持所有的 SQL 写法。但，这个方法的缺点之一就是，每次只能导出一张表的数据，而且表结构也需要另外的语句单独备份。

后两种方式都是逻辑备份方式，是可以跨引擎使用的。

最后，我给你留下一个思考题吧。

我们前面介绍 binlog_format=statement 的时候，binlog 记录的 load data 命令是带 local  的。既然这条命令是发送到备库去执行的，那么备库执行的时候也是本地执行，为什么需要这个 local 呢？如果写到 binlog 中的命令不带  local，又会出现什么问题呢？

你可以把你的分析写在评论区，我会在下一篇文章的末尾和你讨论这个问题。感谢你的收听，也欢迎你把这篇文章分享给更多的朋友一起阅读。

#### 上期问题时间

我在上篇文章最后给你留下的思考题，已经在今天这篇文章的正文部分做了回答。

上篇文章的评论区有几个非常好的留言，我在这里和你分享一下。

@huolang 同学提了一个问题：如果 sessionA 拿到 c=5 的记录锁是写锁，那为什么 sessionB 和 sessionC 还能加 c=5 的读锁呢？

这是因为 next-key lock 是先加间隙锁，再加记录锁的。加间隙锁成功了，加记录锁就会被堵住。如果你对这个过程有疑问的话，可以再复习一下[第 30 篇文章]中的相关内容。

@一大只 同学做了一个实验，验证了主键冲突以后，insert 语句加间隙锁的效果。比我在上篇文章正文中提的那个回滚导致死锁的例子更直观，体现了他对这个知识点非常好的理解和思考，很赞。

@roaming 同学验证了在 MySQL 8.0 版本中，已经能够用临时表处理 insert … select 写入原表的语句了。

@老杨同志 的回答提到了我们本文中说到的几个方法。



# MySQL数据库设计规范

https://github.com/guanguans/notes/blob/master/MySQL/MySQL%E6%95%B0%E6%8D%AE%E5%BA%93%E8%AE%BE%E8%AE%A1%E8%A7%84%E8%8C%83.md

## 1. 规范背景与目的

MySQL 数据库与 Oracle、 SQL Server 等数据库相比，有其内核上的优势与劣势。我们在使用 MySQL 数据库的时候需要遵循一定规范，扬长避短。本规范旨在帮助或指导 RD、QA、OP 等技术人员做出适合线上业务的数据库设计。在数据库变更和处理流程、数据库表设计、SQL 编写等方面予以规范，从而为公司业务系统稳定、健康地运行提供保障。

## 2. 设计规范

### 2.1 数据库设计

以下所有规范会按照【高危】、【强制】、【建议】三个级别进行标注，遵守优先级从高到低。

对于不满足【高危】和【强制】两个级别的设计，DBA 会强制打回要求修改。

#### 2.1.1 一般命名规则

1. 【强制】使用小写，有助于提高打字速度，避免因大小写敏感而导致的错误。
2. 【强制】没有空格，使用下划线代替。
3. 【强制】名称中没有数字，只有英文字母。
4. 【强制】有效的可理解的名称。
5. 【强制】名称应该是自我解释的。
6. 【强制】名称不应超过 32 个字符。
7. 【强制】避免使用前缀。

#### 2.1.2 库

1. 【强制】遵守以上全部一般命名规则。

2. 【强制】使用单数。

3. 【强制】库的名称格式：业务系统名称_子系统名。

4. 【强制】一般分库名称命名格式是`库通配名_编号`，编号从 0 开始递增，比如 `northwind_001`，以时间进行分库的名称格式是`库通配名_时间`。

5. 【强制】创建数据库时必须显式指定字符集，并且字符集只能是 utf8 或者 utf8mb4。创建数据库 SQL 举例：

   ```sql
   create database db_name default character set utf8;
   ```

#### 2.1.3 表

1. 【强制】遵守以上全部一般命名规则。
2. 【强制】使用单数。
3. 【强制】相关模块的表名与表名之间尽量体现 join 的关系，如 `user` 表和 `user_login` 表。
4. 【强制】创建表时必须显式指定字符集为 utf8 或 utf8mb4。
5. 【强制】创建表时必须显式指定表存储引擎类型，如无特殊需求，一律为 InnoDB。当需要使用除 InnoDB/MyISAM/Memory 以外的存储引擎时，必须通过 DBA 审核才能在生产环境中使用。因为 InnoDB 表支持事务、行锁、宕机恢复、MVCC 等关系型数据库重要特性，为业界使用最多的 MySQL 存储引擎。而这是其它大多数存储引擎不具备的，因此首推 InnoDB。
6. 【强制】建表必须有 comment。
7. 【强制】关于主键：(1) 命名为 `id`，类型为 int 或 bigint，且为 `auto_increment`；(2) 标识表里每一行主体的字段不要设为主键，建议设为其它字段如 `user_id`，`order_id`等，并建立 `unique key` 索引。因为如果设为主键且主键值为随机插入，则会导致 InnoDB 内部 page 分裂和大量随机 I/O，性能下降。
8. 【建议】核心表（如用户表，金钱相关的表）必须有行数据的创建时间字段 `create_time` 和最后更新时间字段 `update_time`，便于排查问题。
9. 【建议】表中所有字段必须都是 `NOT NULL` 属性，业务可以根据需要定义 `DEFAULT` 值。因为使用 `NULL` 值会存在每一行都会占用额外存储空间、数据迁移容易出错、聚合函数计算结果偏差等问题。
10. 【建议】建议对表里的 `blob`、`text` 等大字段，垂直拆分到其它表里，仅在需要读这些对象的时候才去 select。
11. 【建议】反范式设计：把经常需要 join 查询的字段，在其它表里冗余一份。如 `username` 属性在 `user_account`，`user_login_log` 等表里冗余一份，减少 join 查询。
12. 【强制】中间表用于保留中间结果集，名称必须以 `tmp_` 开头。备份表用于备份或抓取源表快照，名称必须以 `bak_` 开头。中间表和备份表定期清理。
13. 【强制】对于超过 100W 行的大表进行 `alter table`，必须经过 DBA 审核，并在业务低峰期执行。因为 `alter table` 会产生表锁，期间阻塞对于该表的所有写入，对于业务可能会产生极大影响。

#### 2.1.4 字段

1. 【强制】遵守以上全部一般命名规则。
2. 【建议】尽可能选择短的或一两个单词。
3. 【强制】避免使用保留字作为字段名称：`order`，`date`，`name` 是数据库的保留字，避免使用它。可以为这些名称添加前缀使其易于理解，如 `user_name`，`signup_date` 等。
4. 【强制】避免使用与表名相同的字段名，这会在编写查询时造成混淆。
5. 【强制】在数据库模式上定义外键。
6. 【强制】避免使用缩写或基于首字母缩写词的名称。
7. 【强制】外键列必须具有表名及其主键，例如：`blog_id` 表示来自表博客的外键 id。

#### 2.1.5 字段数据类型优化

1. 【建议】表中的自增列（`auto_increment` 属性），推荐使用 `bigint` 类型。因为无符号 `int` 存储范围为 `0~4,294,967,295`（不到 43 亿），溢出后会导致报错。

2. 【建议】业务中选择性很少的状态 `status`、类型 `type` 等字段推荐使用 `tinytint` 或者 `smallint` 类型节省存储空间。

3. 【建议】业务中 IP 地址字段推荐使用 `int` 类型，不推荐用 `char(15)`。因为 `int` 只占 4 字节，可以用如下函数相互转换，而 `char(15)` 占用至少 15 字节。

   SQL:

   ```sql
   select inet_aton('192.168.2.12');
   select inet_ntoa(3232236044); 
   ```

   PHP:

   ```php
   ip2long('192.168.2.12'); 
   long2ip(3530427185);
   ```

   Java:

   ```java
   public static long ipToLong(String addr)
   {
       String[] addrArray = addr.split("\\.");
   
       long num = 0;
       for (int i = 0; i < addrArray.length; i++)
       {
           int power = 3 - i;
           num += ((Integer.parseInt(addrArray[i]) % 256 * Math.pow(256, power)));
       }
   
       return num;
   }
   
   public static String longToIp(long i)
   {
       return ((i >> 24) & 0xFF) + "." +
              ((i >> 16) & 0xFF) + "." +
              ((i >> 8) & 0xFF) + "." +
              (i & 0xFF);
   }
   ```

4. 【建议】不推荐使用 `enum`，`set`。 因为它们浪费空间，且枚举值写死了，变更不方便。推荐使用 `tinyint` 或 `smallint`。

5. 【建议】不推荐使用 `blob`，`text` 等类型。它们都比较浪费硬盘和内存空间。在加载表数据时，会读取大字段到内存里从而浪费内存空间，影响系统性能。建议和 PM、RD 沟通，是否真的需要这么大字段。InnoDB 中当一行记录超过 8098 字节时，会将该记录中选取最长的一个字段将其 768 字节放在原始 page 里，该字段余下内容放在 `overflow-page` 里。不幸的是在 `compact` 行格式下，原始 `page` 和 `overflow-page` 都会加载。

6. 【建议】存储金钱的字段，建议用 `int` 以分为单位存储，最大数值约 4290 万，程序端乘以 100 和除以 100 进行存取。因为 `int` 占用 4 字节，而 `double` 占用 8 字节，空间浪费。

7. 【建议】文本数据尽量用 `varchar` 存储。因为 `varchar` 是变长存储，比 `char` 更省空间。MySQL server 层规定一行所有文本最多存 65535 字节，因此在 utf8 字符集下最多存 21844 个字符，超过会自动转换为 `mediumtext` 字段。而 `text` 在 utf8 字符集下最多存 21844 个字符，`mediumtext` 最多存 2^24/3 个字符，`longtext` 最多存 2^32 个字符。一般建议用 `varchar` 类型，字符数不要超过 2700。

8. 【建议】时间类型尽量选取 `timestamp`。因为 `datetime` 占用 8 字节，`timestamp` 仅占用 4 字节，但是范围为 `1970-01-01 00:00:01` 到 `2038-01-01 00:00:00`。更为高阶的方法，选用 `int` 来存储时间，使用 SQL 函数 `unix_timestamp()` 和 `from_unixtime()` 来进行转换。

* 详细存储大小参考下图：

  | 类型（同义词）                              | 存储长度(BYTES) | 最小值(SIGNED/UNSIGNED) | 最大值(SIGNED/UNSIGNED)   |
  | ------------------------------------------- | --------------- | ----------------------- | ------------------------- |
  | *整形数字*                                  |                 |                         |                           |
  | TINYINT                                     | 1               | -128/0                  | 127/255                   |
  | SMALLINT                                    | 2               | -32,768/0               | 32767/65,535              |
  | MEDIUMINT                                   | 3               | -8,388,608/0            | 8388607/16,777,215/       |
  | INT(INTEGER)                                | 4               | -2,14,7483,648/0        | 2147483647/4,294,967,295/ |
  | BIGINT                                      | 8               | -2^63/0                 | 2^63-1/2^64-1             |
  | *小数支持*                                  |                 |                         |                           |
  | FLOAT[(M[,D])]                              | 4 or 8          | -                       |                           |
  | DOUBLE[(M[,D])]<br>(REAL, DOUBLE PRECISION) | 8               | -                       |                           |
  | *时间类型*                                  |                 |                         |                           |
  | DATETIME                                    | 8               | 1001-01-01 00:00:00     | 9999-12-31 23:59:59       |
  | DATE                                        | 3               | 1001-01-01              | 9999-12-31                |
  | TIME                                        | 3               | 00:00:00                | 23:59:59                  |
  | YEAR                                        | 1               | 1001                    | 9999                      |
  | TIMESTAMP                                   | 4               | 1970-01-01 00:00:00     |                           |


#### 2.1.6 索引设计

1. 【强制】InnoDB 表必须主键为 `id int/bigint auto_increment`，且主键值禁止被更新。
2. 【建议】主键的名称以 `pk_` 开头，唯一键以 `uk_` 开头，普通索引以 `ix_` 开头，一律使用小写格式，以表名/字段的名称或缩写作为后缀。
3. 【强制】InnoDB 和 MyISAM 存储引擎表，索引类型必须为 `BTREE`；MEMORY 表可以根据需要选择 `HASH` 或者 `BTREE` 类型索引。
4. 【强制】单个索引中每个索引记录的长度不能超过 64KB。
5. 【建议】单个表上的索引个数不能超过 7 个。
6. 【建议】在建立索引时，多考虑建立联合索引，并把区分度最高的字段放在最前面。如列 `user_id` 的区分度可由 `select count(distinct user_id)` 计算出来。
7. 【建议】在多表 join 的 SQL 里，保证被驱动表的连接列上有索引，这样 join 执行效率最高。
8. 【建议】建表或加索引时，保证表里互相不存在冗余索引。对于 MySQL 来说，如果表里已经存在 `key(a, b)`，则 `key(a)` 为冗余索引，需要删除。
9. 【建议】如果选择性超过 20%，那么全表扫描比使用索引性能更优，即没有设置索引的必要。

#### 2.1.7 分库分表、分区表

1. 【强制】分区表的分区字段（`partition-key`）必须有索引，或者是组合索引的首列。
2. 【强制】单个分区表中的分区（包括子分区）个数不能超过 1024。
3. 【强制】上线前 RD 或者 DBA 必须指定分区表的创建、清理策略。
4. 【强制】访问分区表的 SQL 必须包含分区键。
5. 【建议】单个分区文件不超过 2G，总大小不超过 50G。建议总分区数不超过 20 个。
6. 【强制】对于分区表执行 `alter table` 操作，必须在业务低峰期执行。
7. 【强制】采用分库策略的，库的数量不能超过 1024。
8. 【强制】采用分表策略的，表的数量不能超过 4096。
9. 【建议】单个分表不超过 500W 行，ibd 文件大小不超过 2G，这样才能让数据分布式变得性能更佳。
10. 【建议】水平分表尽量用取模方式，日志、报表类数据建议采用日期进行分表。

#### 2.1.8 字符集

1. 【强制】数据库本身库、表、列所有字符集必须保持一致，为 `utf8` 或 `utf8mb4`。
2. 【强制】前端程序字符集或者环境变量中的字符集，与数据库、表的字符集必须一致，统一为 `utf8`。

#### 2.1.9 程序层 DAO 设计建议

1. 【建议】新的代码不要用 model，推荐使用手动拼 SQL + 绑定变量传入参数的方式。因为 model 虽然可以使用面向对象的方式操作 db，但是其使用不当很容易造成生成的 SQL 非常复杂，且 model 层自己做的强制类型转换性能较差，最终导致数据库性能下降。
2. 【建议】前端程序连接 MySQL 或者 Redis，必须要有连接超时和失败重连机制，且失败重试必须有间隔时间。
3. 【建议】前端程序报错里尽量能够提示 MySQL 或 Redis 原生态的报错信息，便于排查错误。
4. 【建议】对于有连接池的前端程序，必须根据业务需要配置初始、最小、最大连接数，超时时间以及连接回收机制，否则会耗尽数据库连接资源，造成线上事故。
5. 【建议】对于 `log` 或 `history` 类型的表，随时间增长容易越来越大，因此上线前 RD 或者 DBA 必须建立表数据清理或归档方案。
6. 【建议】在应用程序设计阶段，RD 必须考虑并规避数据库中主从延迟对于业务的影响。尽量避免从库短时延迟（20 秒以内）对业务造成影响，建议强制一致性的读开启事务走主库，或更新后过一段时间再去读从库。
7. 【建议】多个并发业务逻辑访问同一块数据（InnoDB 表）时，会在数据库端产生行锁甚至表锁导致并发下降，因此建议更新类 SQL 尽量基于主键去更新。
8. 【建议】业务逻辑之间加锁顺序尽量保持一致，否则会导致死锁。
9. 【建议】对于单表读写比大于 10:1 的数据行或单个列，可以将热点数据放在缓存里（如 Memcached 或 Redis），加快访问速度，降低 MySQL 压力。

#### 2.1.10 一个规范的建表语句示例

- 一个较为规范的建表语句为：

  ```sql
  create table user 
  ( 
      `id`            bigint(11) not null auto_increment, 
      `user_id`       bigint(11) not null comment '用户 ID', 
      `username`      varchar(45) not null comment '登录名', 
      `email`         varchar(30) not null comment '邮箱', 
      `nickname`      varchar(45) not null comment '昵称', 
      `avatar`        int(11) not null comment '头像', 
      `birthday`      date not null comment '生日', 
      `gender`        tinyint(4) default '0' comment '性别', 
      `intro`         varchar(150) default null comment '简介', 
      `resume_url`    varchar(300) not null comment '简历存放地址', 
      `register_ip`   int not null comment '用户注册时的源 IP', 
      `review_status` tinyint not null comment '审核状态，1-通过，2-审核中，3-未通过，4-尚未提交审核', 
      `create_time`   timestamp not null comment '记录创建的时间', 
      `update_time`   timestamp not null comment '资料修改的时间', 
      
      primary key (`id`), 
      unique `idx_user_id` (`user_id`), 
      key `idx_username`(`username`), 
      key `idx_create_time`(`create_time`, `review_status`) 
  ) 
  engine = InnoDB
  default charset = utf8 
  comment = '用户基本信息'; 
  ```

### 2.2 SQL 编写

#### 2.2.1 DML 语句

1. 【强制】select 语句必须指定具体字段名称，禁止写成 `*`。因为 `select *` 会将不该读的数据也从 MySQL 里读出来，造成网卡压力。
2. 【强制】insert 语句指定具体字段名称，不要写成 `insert into t1 values(…)`，道理同上。
3. 【建议】`insert into … values(xx),(xx),(xx)…`，这里 xx 的值不要超过 5000 个。值过多虽然上线很快，但会引起主从同步延迟。
4. 【建议】select 语句不要使用 `union`，推荐使用 `union all`，并且 `union` 子句个数限制在 5 个以内。因为 `union all` 不需要去重，节省数据库资源，提高性能。
5. 【建议】in 值列表限制在 500 以内。例如 `select … where user_id in(…500 个以内…)`，这么做是为了减少底层扫描，减轻数据库压力从而加速查询。
6. 【建议】事务里批量更新数据需要控制数量，进行必要的 sleep，做到少量多次。
7. 【强制】事务涉及的表必须全部是 InnoDB 表。否则一旦失败不会全部回滚，且易造成主从库同步终端。
8. 【强制】写入和事务发往主库，只读 SQL 发往从库。
9. 【强制】除静态表或小表（100 行以内），dml 语句必须有 where 条件，且使用索引查找。
10. 【强制】生产环境禁止使用 `hint`，如 `sql_no_cache`，`force index`，`ignore key`，`straight join` 等。因为 `hint` 是用来强制 sql 按照某个执行计划来执行，但随着数据量变化我们无法保证自己当初的预判是正确的，因此我们要相信 MySQL 优化器。
11. 【强制】where 条件里等号左右字段类型必须一致，否则无法利用索引。
12. 【建议】`select|update|delete|replace` 要有 where 子句，且 where 子句的条件必需使用索引查找。
13. 【强制】生产数据库中强烈不推荐大表上发生全表扫描，但对于 100 行以下的静态表可以全表扫描。查询数据量不要超过表行数的 25%，否则不会利用索引。
14. 【强制】where 子句中禁止只使用全模糊的 like 条件进行查找，必须有其它等值或范围查询条件，否则无法利用索引。
15. 【建议】索引列不要使用函数或表达式，否则无法利用索引。如 `where length(name) = 'admin'` 或 `where user_id + 2 = 10023`。
16. 【建议】减少使用 or 语句，可将 or 语句优化为 union，然后在各个 where 条件上建立索引。如 `where a = 1 or b = 2` 优化为 `where a = 1 … union … where b = 2, key(a), key(b)`。
17. 【建议】分页查询，当 `limit` 起点较高时，可先用过滤条件进行过滤。如 `select a, b, c from t1 limit 10000, 20;` 优化为: `select a, b, c from t1 where id > 10000 limit 20;`。

#### 2.2.2 多表连接

1. 【强制】禁止跨 DB 的 join 语句。因为这样可以减少模块间耦合，为数据库拆分奠定坚实基础。
2. 【强制】禁止在业务的更新类 SQL 语句中使用 join，比如 `update t1 join t2 …`。
3. 【建议】不建议使用子查询，建议将子查询 SQL 拆开结合程序多次查询，或使用 join 来代替子查询。
4. 【建议】线上环境，多表 join 不要超过 3 个表。
5. 【建议】多表连接查询推荐使用别名，且 select 列表中要用别名引用字段，数据库.表格式，如 `select a from db1.table1 alias1 where …`。
6. 【建议】在多表 join 中，尽量选取结果集较小的表作为驱动表，来 join 其它表。

#### 2.2.3 事务

1. 【建议】事务中 `insert|update|delete|replace` 语句操作的行数控制在 2000 以内，以及 where 子句中 in 列表的传参个数控制在 500 以内。
2. 【建议】批量操作数据时，需要控制事务处理间隔时间，进行必要的 sleep，一般建议值 5-10 秒。
3. 【建议】对于有 `auto_increment` 属性字段的表的插入操作，并发需要控制在 200 以内。
4. 【强制】程序设计必须考虑“数据库事务隔离级别”带来的影响，包括脏读、不可重复读和幻读。线上建议事务隔离级别为 `repeatable-read`。
5. 【建议】事务里包含 SQL 不超过 5 个（支付业务除外）。因为过长的事务会导致锁数据较久，MySQL 内部缓存、连接消耗过多等雪崩问题。
6. 【建议】事务里更新语句尽量基于主键或 `unique key`，如 `update … where id = XX;`，否则会产生间隙锁，内部扩大锁定范围，导致系统性能下降，产生死锁。
7. 【建议】尽量把一些典型外部调用移出事务，如调用 Web Service，访问文件存储等，从而避免事务过长。
8. 【建议】对于 MySQL 主从延迟严格敏感的 select 语句，请开启事务强制访问主库。

#### 2.2.4 排序和分组

1. 【建议】减少使用 `order by`，和业务沟通能不排序就不排序，或将排序放到程序端去做。`order by`、`group by`、`distinct` 这些语句较为耗费 CPU，数据库的 CPU 资源是极其宝贵的。
2. 【建议】`order by`、`group by`、`distinct` 这些 SQL 尽量利用索引直接检索出排序好的数据。如 `where a = 1 order by` 可以利用 `key(a, b)`。
3. 【建议】包含了 `order by`、`group by`、`distinct` 这些查询的语句，where 条件过滤出来的结果集请保持在 1000 行以内，否则 SQL 会很慢。

#### 2.2.5 线上禁止使用的 SQL 语句

1. 【高危】禁用 `update|delete t1 … where a = XX limit XX;` 这种带 limit 的更新语句。因为会导致主从不一致，导致数据错乱。建议加上 `order by PK`。
2. 【高危】禁止使用关联子查询，如 `update t1 set … where name in(select name from user where …);`，效率极其低下。
3. 【强制】禁用 procedure、function、trigger、views、event、外键约束。因为他们消耗数据库资源，降低数据库实例可扩展性。推荐都在程序端实现。
4. 【强制】禁用 `insert into … on duplicate key update …` 在高并发环境下，会造成主从不一致。
5. 【强制】禁止联表更新语句，如 `update t1, t2 where t1.id = t2.id …`。



# Mysql  Advanced

## 逻辑架构

![image-20230201105202736](/images/image-20230201105202736.png)

​																									**InnoDB(Storage Engines) Architecture**

![image-20230201133131813](/images/image-20230201133131813.png)



![image-20230201105921902](/images/image-20230201105921902.png)



## MySQL三大日志

`MySQL` 日志 主要包括错误日志、查询日志、慢查询日志、事务日志、二进制日志几大类。

其中，比较重要的还要属

- `binlog`（归档日志）`MySQL`数据库的**数据备份、主备、主主、主从**都离不开`binlog`，需要依靠`binlog`来同步数据，保证数据一致性。

- `redo log`（重做日志） **InnoDB 特有的**让`MySQL`拥有了**崩溃恢复能力**`MySQL` 实例宕机了，重启时，`InnoDB`存储引擎使用`redo log`恢复数据，  保证数据的持久性与完整性。

- `undo log`（回滚日志）。`MySQL`执行过程中遇到异常的话，我们直接利用 **回滚日志** 中的信息将数据回滚到修改之前的样子即可！事务进行修改前都会先记录到这个回滚日志中

### redo log

`redo log`（重做日志）是`InnoDB`存储引擎独有的，它让`MySQL`拥有了崩溃恢复能力。

比如 `MySQL` 实例挂了或宕机了，重启时，`InnoDB`存储引擎会使用`redo log`恢复数据，保证数据的持久性与完整性。

![image-20230201162750599](/images/image-20230201162750599.png)

`MySQL` 中数据是以页为单位，你查询一条记录，会从硬盘把一页的数据加载出来，加载出来的数据叫数据页，会放入到 `Buffer Pool` 中。

后续的查询都是先从 `Buffer Pool` 中找，没有命中再去硬盘加载，减少硬盘 `IO` 开销，提升性能。

更新表数据的时候，也是如此，发现 `Buffer Pool` 里存在要更新的数据，就直接在 `Buffer Pool` 里更新。

然后会把“在某个数据页上做了什么修改”记录到重做日志缓存（`redo log buffer`）里，接着刷盘到 `redo log` 文件里。

![image-20230201162830131](/images/image-20230201162830131.png)

> 图片笔误提示：第 4 步 “清空 redo log buffe 刷盘到 redo 日志中”这句话中的 buffe 应该是 buffer。

理想情况，事务一提交就会进行刷盘操作，但实际上，刷盘的时机是根据策略来进行的。

> 小贴士：每条 redo 记录由“表空间号+数据页号+偏移量+修改数据长度+具体修改的数据”组成

**刷盘时机**

`InnoDB` 存储引擎为 `redo log` 的刷盘策略提供了 `innodb_flush_log_at_trx_commit` 参数，它支持三种策略：

- **0** ：设置为 0 的时候，表示每次事务提交时不进行刷盘操作
- **1** ：设置为 1 的时候，表示每次事务提交时都将进行刷盘操作（默认值）
- **2** ：设置为 2 的时候，表示每次事务提交时都只把 redo log buffer 内容写入 page cache

`innodb_flush_log_at_trx_commit` 参数默认为 1 ，也就是说当事务提交时会调用 `fsync` 对 redo log 进行刷盘

另外，`InnoDB` 存储引擎有一个后台线程，每隔`1` 秒，就会把 `redo log buffer` 中的内容写到文件系统缓存（`page cache`），然后调用 `fsync` 刷盘。

![image-20230201162843799](/images/image-20230201162843799.png)

也就是说，一个没有提交事务的 `redo log` 记录，也可能会刷盘。

**为什么呢？**

因为在事务执行过程 `redo log` 记录是会写入`redo log buffer` 中，这些 `redo log` 记录会被后台线程刷盘。

![image-20230201162856200](/images/image-20230201162856200.png)

除了后台线程每秒`1`次的轮询操作，还有一种情况，当 `redo log buffer` 占用的空间即将达到 `innodb_log_buffer_size` 一半的时候，后台线程会主动刷盘。

下面是不同刷盘策略的流程图。

**innodb_flush_log_at_trx_commit=0**

![image-20230201162915440](/images/image-20230201162915440.png)

为`0`时，如果`MySQL`挂了或宕机可能会有`1`秒数据的丢失。

**innodb_flush_log_at_trx_commit=1**

![image-20230201162928627](/images/image-20230201162928627.png)

为`1`时， 只要事务提交成功，`redo log`记录就一定在硬盘里，不会有任何数据丢失。

如果事务执行期间`MySQL`挂了或宕机，这部分日志丢了，但是事务并没有提交，所以日志丢了也不会有损失。

 **innodb_flush_log_at_trx_commit=2**

![image-20230201162939325](/images/image-20230201162939325.png)

为`2`时， 只要事务提交成功，`redo log buffer`中的内容只写入文件系统缓存（`page cache`）。

如果仅仅只是`MySQL`挂了不会有任何数据丢失，但是宕机可能会有`1`秒数据的丢失。

**日志文件组**

硬盘上存储的 `redo log` 日志文件不只一个，而是以一个**日志文件组**的形式出现的，每个的`redo`日志文件大小都是一样的。

比如可以配置为一组`4`个文件，每个文件的大小是 `1GB`，整个 `redo log` 日志文件组可以记录`4G`的内容。

它采用的是环形数组形式，从头开始写，写到末尾又回到头循环写，如下图所示。

![image-20230201163003913](/images/image-20230201163003913.png)

在个**日志文件组**中还有两个重要的属性，分别是 `write pos、checkpoint`

- **write pos** 是当前记录的位置，一边写一边后移
- **checkpoint** 是当前要擦除的位置，也是往后推移

每次刷盘 `redo log` 记录到**日志文件组**中，`write pos` 位置就会后移更新。

每次 `MySQL` 加载**日志文件组**恢复数据时，会清空加载过的 `redo log` 记录，并把 `checkpoint` 后移更新。

`write pos` 和 `checkpoint` 之间的还空着的部分可以用来写入新的 `redo log` 记录。

![image-20230201163014042](/images/image-20230201163014042.png)

如果 `write pos` 追上 `checkpoint` ，表示**日志文件组**满了，这时候不能再写入新的 `redo log` 记录，`MySQL` 得停下来，清空一些记录，把 `checkpoint` 推进一下。

![image-20230201163023927](/images/image-20230201163023927.png)

**redo log 小结**

相信大家都知道 `redo log` 的作用和它的刷盘时机、存储形式。

现在我们来思考一个问题： **只要每次把修改后的数据页直接刷盘不就好了，还有 `redo log` 什么事？**

它们不都是刷盘么？差别在哪里？



```java
1 Byte = 8bit
1 KB = 1024 Byte
1 MB = 1024 KB
1 GB = 1024 MB
1 TB = 1024 GB
```

实际上，数据页大小是`16KB`，刷盘比较耗时，可能就修改了数据页里的几 `Byte` 数据，有必要把完整的数据页刷盘吗？

而且数据页刷盘是随机写，因为一个数据页对应的位置可能在硬盘文件的随机位置，所以性能是很差。

如果是写 `redo log`，一行记录可能就占几十 `Byte`，只包含表空间号、数据页号、磁盘文件偏移 量、更新值，再加上是顺序写，所以刷盘速度很快。

所以用 `redo log` 形式记录修改内容，性能会远远超过刷数据页的方式，这也让数据库的并发能力更强。

> 其实内存的数据页在一定时机也会刷盘，我们把这称为页合并，讲 `Buffer Pool`的时候会对这块细说

### binlog

`redo log` 它是物理日志，记录内容是“在某个数据页上做了什么修改”，属于 `InnoDB` 存储引擎。

而 `binlog` 是逻辑日志，记录内容是语句的原始逻辑，类似于“给 ID=2 这一行的 c 字段加 1”，属于`MySQL Server` 层。

不管用什么存储引擎，只要发生了表数据更新，都会产生 `binlog` 日志。

那 `binlog` 到底是用来干嘛的？

可以说`MySQL`数据库的**数据备份、主备、主主、主从**都离不开`binlog`，需要依靠`binlog`来同步数据，保证数据一致性。

![image-20230201163038287](/images/image-20230201163038287.png)

`binlog`会记录所有涉及更新数据的逻辑操作，并且是顺序写。

**记录格式**

`binlog` 日志有三种格式，可以通过`binlog_format`参数指定。

- **statement**
- **row**
- **mixed**

指定`statement`，记录的内容是`SQL`语句原文，比如执行一条`update T set update_time=now() where id=1`，记录的内容如下。

![image-20230201163049621](/images/image-20230201163049621.png)

同步数据时，会执行记录的`SQL`语句，但是有个问题，`update_time=now()`这里会获取当前系统时间，直接执行会导致与原库的数据不一致。

为了解决这种问题，我们需要指定为`row`，记录的内容不再是简单的`SQL`语句了，还包含操作的具体数据，记录内容如下。

![image-20230201163058562](/images/image-20230201163058562.png)

`row`格式记录的内容看不到详细信息，要通过`mysqlbinlog`工具解析出来。

`update_time=now()`变成了具体的时间`update_time=1627112756247`，条件后面的@1、@2、@3 都是该行数据第 1 个~3 个字段的原始值（**假设这张表只有 3 个字段**）。

这样就能保证同步数据的一致性，通常情况下都是指定为`row`，这样可以为数据库的恢复与同步带来更好的可靠性。

但是这种格式，需要更大的容量来记录，比较占用空间，恢复与同步时会更消耗`IO`资源，影响执行速度。

所以就有了一种折中的方案，指定为`mixed`，记录的内容是前两者的混合。

`MySQL`会判断这条`SQL`语句是否可能引起数据不一致，如果是，就用`row`格式，否则就用`statement`格式。

**写入机制**

`binlog`的写入时机也非常简单，事务执行过程中，先把日志写到`binlog cache`，事务提交的时候，再把`binlog cache`写到`binlog`文件中。

因为一个事务的`binlog`不能被拆开，无论这个事务多大，也要确保一次性写入，所以系统会给每个线程分配一个块内存作为`binlog cache`。

我们可以通过`binlog_cache_size`参数控制单个线程 binlog cache 大小，如果存储内容超过了这个参数，就要暂存到磁盘（`Swap`）。

`binlog`日志刷盘流程如下

![image-20230201163113791](/images/image-20230201163113791.png)

- **上图的 write，是指把日志写入到文件系统的 page cache，并没有把数据持久化到磁盘，所以速度比较快**
- **上图的 fsync，才是将数据持久化到磁盘的操作**

`write`和`fsync`的时机，可以由参数`sync_binlog`控制，默认是`0`。

为`0`的时候，表示每次提交事务都只`write`，由系统自行判断什么时候执行`fsync`。

![image-20230201163126115](/images/image-20230201163126115.png)

虽然性能得到提升，但是机器宕机，`page cache`里面的 binlog 会丢失。

为了安全起见，可以设置为`1`，表示每次提交事务都会执行`fsync`，就如同 **redo log 日志刷盘流程** 一样。

最后还有一种折中方式，可以设置为`N(N>1)`，表示每次提交事务都`write`，但累积`N`个事务后才`fsync`。

![image-20230201163136927](/images/image-20230201163136927.png)

在出现`IO`瓶颈的场景里，将`sync_binlog`设置成一个比较大的值，可以提升性能。

同样的，如果机器宕机，会丢失最近`N`个事务的`binlog`日志。

### 两阶段提交

`redo log`（重做日志）让`InnoDB`存储引擎拥有了崩溃恢复能力。

`binlog`（归档日志）保证了`MySQL`集群架构的数据一致性。

虽然它们都属于持久化的保证，但是侧重点不同。

在执行更新语句过程，会记录`redo log`与`binlog`两块日志，以基本的事务为单位，`redo log`在事务执行过程中可以不断写入，而`binlog`只有在提交事务时才写入，所以`redo log`与`binlog`的写入时机不一样。

![image-20230201163148486](/images/image-20230201163148486.png)

回到正题，`redo log`与`binlog`两份日志之间的逻辑不一致，会出现什么问题？

我们以`update`语句为例，假设`id=2`的记录，字段`c`值是`0`，把字段`c`值更新成`1`，`SQL`语句为`update T set c=1 where id=2`。

假设执行过程中写完`redo log`日志后，`binlog`日志写期间发生了异常，会出现什么情况呢？

![image-20230201163157321](/images/image-20230201163157321.png)

由于`binlog`没写完就异常，这时候`binlog`里面没有对应的修改记录。因此，之后用`binlog`日志恢复数据时，就会少这一次更新，恢复出来的这一行`c`值是`0`，而原库因为`redo log`日志恢复，这一行`c`值是`1`，最终数据不一致。

![image-20230201163209142](/images/image-20230201163209142.png)

为了解决两份日志之间的逻辑一致问题，`InnoDB`存储引擎使用**两阶段提交**方案。

原理很简单，将`redo log`的写入拆成了两个步骤`prepare`和`commit`，这就是**两阶段提交**。

![image-20230201163220118](/images/image-20230201163220118.png)

使用**两阶段提交**后，写入`binlog`时发生异常也不会有影响，因为`MySQL`根据`redo log`日志恢复数据时，发现`redo log`还处于`prepare`阶段，并且没有对应`binlog`日志，就会回滚该事务。

![image-20230201163233344](/images/image-20230201163233344.png)

再看一个场景，`redo log`设置`commit`阶段发生异常，那会不会回滚事务呢？

![image-20230201163243923](/images/image-20230201163243923.png)

并不会回滚事务，它会执行上图框住的逻辑，虽然`redo log`是处于`prepare`阶段，但是能通过事务`id`找到对应的`binlog`日志，所以`MySQL`认为是完整的，就会提交事务恢复数据。

### undo log

> 这部分内容为 JavaGuide 的补充：

我们知道如果想要保证事务的原子性，就需要在异常发生时，对已经执行的操作进行**回滚**，在 MySQL 中，恢复机制是通过 **回滚日志（undo log）** 实现的，所有事务进行的修改都会先记录到这个回滚日志中，然后再执行相关的操作。如果执行过程中遇到异常的话，我们直接利用 **回滚日志** 中的信息将数据回滚到修改之前的样子即可！并且，回滚日志会先于数据持久化到磁盘上。这样就保证了即使遇到数据库突然宕机等情况，当用户再次启动数据库的时候，数据库还能够通过查询回滚日志来回滚将之前未完成的事务。

另外，`MVCC` 的实现依赖于：**隐藏字段、Read View、undo log**。在内部实现中，`InnoDB` 通过数据行的 `DB_TRX_ID` 和 `Read View` 来判断数据的可见性，如不可见，则通过数据行的 `DB_ROLL_PTR` 找到 `undo log` 中的历史版本。每个事务读到的数据版本可能是不一样的，在同一个事务中，用户只能看到该事务创建 `Read View` 之前已经提交的修改和该事务本身做的修改

## Mysql中的SQL语句的执行流程

MySQL 主要分为**连接层** **Server 层**和**引擎层**，Server 层主要包括**连接器**、**查询缓存**、**分析器**、**优化器**、**执行器**，

同时还涉及到**日志模块（undolog/ redolog/ binlog）**，**redolog(存储引擎层面的log) 只有 InnoDB 有**。



引擎层是插件式的，目前主要包括，MyISAM,**InnoDB**,Memory 等。



- **查询语句**的执行流程如下：权限校验（如果命中缓存）--->查询缓存--->分析器--->优化器--->权限校验--->执行器--->引擎
- **更新语句**执行流程如下：分析器---->权限校验---->执行器--->引擎---redo log(prepare 状态)--->binlog--->redo log(commit状态)



### 查询语句

- 先**检查该语句是否有权限**，如果没有权限，直接返回错误信息，如果有权限，**在 MySQL8.0 版本以前，会先查询缓存**，以这条 SQL 语句为 key 在内存中查询是否有结果，如果有直接缓存直接返回缓存的结果，如果没有，执行下一步。
- 通过**分析器**，分析出一个**语法树**，提取 SQL 语句的关键元素，比如提取上面这个语句是查询 select，提取需要查询的表名为 tb_student，需要查询所有的列，查询条件是这个表的 id='1'。然后判断这个 SQL 语句是否有**语法&词法**错误，比如**关键词**是否正确等等，如果检查没问题就执行下一步。
- 接下来就是**优化器**进行确定执行方案，上面的 SQL 语句，可以有两种执行方案：

```
  a.先查询学生表中姓名为“张三”的学生，然后判断是否年龄是 18。
  b.先找出学生中年龄 18 岁的学生，然后再查询姓名为“张三”的学生。
```

​	那么优化器根据自己的优化算法进行选择执行效率最好的一个方案（优化器认为，有时候不一定最好）。那么确认了执行计划后就准备开始执行了。

- 进行**权限校验**，如果没有权限就会返回错误信息，如果**有权限就会调用数据库引擎接口，返回引擎的执行结果**

### 更新语句

```text
update tb_student A set A.age='19' where A.name=' 张三 ';
```

我们来给张三修改下年龄，在实际数据库肯定不会设置年龄这个字段的，不然要被技术负责人打的。其实这条语句也基本上会沿着上一个查询的流程走，只不过执行更新的时候肯定要记录日志啦，这就会引入日志模块了，MySQL 自带的日志模块是 **binlog（归档日志）** ，所有的存储引擎都可以使用，

**undolog （回滚日志）**日志文件：**记录数据被修改前的样子**；我们常用的 InnoDB 引擎还自带了一个日志模块 **redo log（重做日志）**，我们就以 InnoDB 模式下来探讨这个语句的执行流程。



**流程如下**：

- 先查询到张三这一条数据，如果有缓存，也是会用到缓存。
- 拿到查询到的原始数据；将这条数据的**原始记录保存到 undo 日志文件中**
- 然后拿到查询的语句，把 age 改为 19，然后调用引擎 API 接口，写入这一行数据，InnoDB 引擎**把数据保存在内存中（Buffer Pool）**，
- **同时记录 redo log**，此时 **redo log 进入 prepare 状态(双阶段提交)**，然后告诉执行器，执行完成了，随时可以提交。
- 执行器收到通知后**记录 binlog**，然后调用引擎接口，
- **提交 redo log 为commit状态(双阶段提交)**。
- 更新完成。

**为什么要用两个日志模块，用一个日志模块不行吗?**

这是因为最开始 MySQL 并没有 InnoDB 引擎（InnoDB 引擎是其他公司以插件形式插入 MySQL 的），MySQL 自带的引擎是 MyISAM，但是我们知道 redo log 是 InnoDB 引擎特有的，其他存储引擎都没有，这就导致会没有 crash-safe 的能力(crash-safe 的能力即使数据库发生异常重启，之前提交的记录都不会丢失)，binlog 日志只能用来归档。

并不是说只用一个日志模块不可以，只是 InnoDB 引擎就是通过 redo log 来支持事务的。那么，又会有同学问，我用两个日志模块，但是不要这么复杂行不行，为什么 redo log 要引入 prepare 预提交状态？这里我们用反证法来说明下为什么要这么做？

- **先写 redo log 直接提交，然后写 binlog**，假设写完 redo log 后，机器挂了，binlog 日志没有被写入，那么机器重启后，这台机器会通过 redo log 恢复数据，但是这个时候 binlog 并没有记录该数据，后续进行机器备份的时候，就会丢失这一条数据，同时主从同步也会丢失这一条数据。
- **先写 binlog，然后写 redo log**，假设写完了 binlog，机器异常重启了，由于没有 redo log，本机是无法恢复这一条记录的，但是 binlog 又有记录，那么和上面同样的道理，就会产生数据不一致的情况。

如果采用 redo log 两阶段提交的方式就不一样了，写完 binlog 后，然后再提交 redo log 就会防止出现上述的问题，从而保证了数据的一致性。那么问题来了，有没有一个极端的情况呢？假设 redo log 处于预提交状态，binlog 也已经写完了，这个时候发生了异常重启会怎么样呢？ 这个就要依赖于 MySQL 的处理机制了，MySQL 的处理过程如下：

- 判断 redo log 是否完整，如果判断是完整的，就立即提交。
- 如果 redo log 只是预提交但不是 commit 状态，这个时候就会去判断 binlog 是否完整，如果完整就提交 redo log, 不完整就回滚事务。

![image-20230201160837989](/images/image-20230201160837989.png)

![image-20221105144640601](/images/image-20221105144640601.png)

![image-20221021194721702](/images/image-20221021194721702.png)

![image-20221021192418947](/images/image-20221021192418947.png)



**查询缓存**在**8.0之后被废弃**了 

原因是**查询缓存实际上十分鸡肋** （命中率太低）要求查询的key要完全一样才能成功匹配到缓存的value

总之查询缓存弊大于利 查询缓存失效十分频繁 

可以手动进行配置是否开启 query-catch-type=0表示off=1表示on

query-catch-type=2表示设置为按需使用

```mysql
select SQL_CACHE * from user;
#SQL-CACHE表示要过一遍查询缓存
select SQL_NO_CACHE * from user;
#SQL_NO_CACHE表示不要过查询缓存
```

建议大家使用**静态表**使用查询缓存 

**静态表即为 极少更新的表**

比如系统配置 字典表

## InnoDB存储引擎对MVCC的实现

### MVCC

*MVCC，全称**Multi-Version Concurrency Control**，即多版本并发控制。MVCC是一种并发控制的方法，一般在数据库管理系统中，实现对数据库的并发访问，在编程语言中实现事务内存。*



**MVCC works only with** the **REPEATABLE READ** and **READ COMMITTED** isolation levels. 

READ UNCOMMITTED isn’t MVCC-compatible because queries don’t read the row version
that’s appropriate for their transaction version; they read the newest version, no matter what. 

SERIALIZABLE isn’t MVCC - compatible because reads lock every row they return



MVCC在MySQL **InnoDB中的实现**主要是为了**提高数据库并发性能**，用更好的方式去处理读-写冲突，做到**即使有读写冲突**时，也**能做到不加锁**，**非阻塞并发读**



多版本并发控制（MVCC）是一种用来**解决读-写冲突的无锁并发控制**，也就是**为事务分配单向增长的时间戳**，**为每个修改保存一个版本**，**版本与事务时间戳关联**，**读操作只读该事务开始前的数据库的快照**。 所以MVCC可以为数据库解决以下问题

在**并发读写数据库时**，可以做到在**读操作时不用阻塞写操作**，**写操作也不用阻塞读操作**，**提高**了数据库**并发读写的性能** 同时还**可以解决脏读，幻读，不可重复读**等事务隔离问题，**但不能解决更新丢失问题**





**数据库并发场景**

- **读-读**：不存在任何问题，也不需要并发控制

- **读-写**：有线程安全问题，可能会造成事务隔离性问题，可能遇到脏读，幻读，不可重复读

- **写-写**：有线程安全问题，可能会存在更新丢失问题，比如第一类更新丢失，第二类更新丢失



**小结一下**

MVCC就是因为大牛们，不满意只让数据库采用悲观锁这样性能不佳的形式去解决读-写冲突问题，而提出的解决方案，所以在数据库中，因为有了MVCC，所以我们可以形成两个组合：

- **MVCC + 悲观锁** MVCC解决读写冲突，悲观锁解决写写冲突
- **MVCC + 乐观锁** MVCC解决读写冲突，乐观锁解决写写冲突



```sql
/** The MVCC read view manager */
class MVCC {
 private:
  view_list_t m_free;    /* 空闲即可以被重复使用的 Read View 的链表 */

  view_list_t m_views;   /* 活跃或者已经关闭的 Read View 的链表 */
};
```

### 一致性非锁定读和锁定读

#### 一致性非锁定读

**快照读**

对于 [**一致性非锁定读（Consistent Nonlocking Reads）** open in new window](https://dev.mysql.com/doc/refman/5.7/en/innodb-consistent-read.html)的实现，通常做法是加一个版本号或者时间戳字段，在更新数据的同时版本号 + 1 或者更新时间戳。查询时，将当前可见的版本号与对应记录的版本号进行比对，如果记录的版本小于可见版本，则表示该记录可见

在 `InnoDB` 存储引擎中，[多版本控制 (multi versioning)open in new window](https://dev.mysql.com/doc/refman/5.7/en/innodb-multi-versioning.html) 就是对非锁定读的实现。如果读取的行正在执行 `DELETE` 或 `UPDATE` 操作，这时读取操作不会去等待行上锁的释放。相反地，`InnoDB` 存储引擎会去读取行的一个快照数据，对于这种读取历史数据的方式，我们叫它快照读 (snapshot read)

在 `Repeatable Read` 和 `Read Committed` 两个隔离级别下，如果是执行普通的 `select` 语句（不包括 `select ... lock in share mode` ,`select ... for update`）则会使用 `一致性非锁定读（MVCC）`。并且在 `Repeatable Read` 下 `MVCC` 实现了可重复读和防止部分幻读

#### 锁定读

**当前读**

如果执行的是下列语句，就是 [**锁定读（Locking Reads）**open in new window](https://dev.mysql.com/doc/refman/5.7/en/innodb-locking-reads.html)

- `select ... lock in share mode`
- `select ... for update`
- `insert`、`update`、`delete` 操作

在锁定读下，读取的是数据的最新版本，这种读也被称为 `当前读（current read）`。锁定读会对读取到的记录加锁：

- `select ... lock in share mode`：对记录加 `S` 锁，其它事务也可以加`S`锁，如果加 `x` 锁则会被阻塞
- `select ... for update`、`insert`、`update`、`delete`：对记录加 `X` 锁，且其它事务不能加任何锁

在一致性非锁定读下，即使读取的记录已被其它事务加上 `X` 锁，这时记录也是可以被读取的，即读取的快照数据。上面说了，在 `Repeatable Read` 下 `MVCC` 防止了部分幻读，这边的 “部分” 是指在 `一致性非锁定读` 情况下，只能读取到第一次查询之前所插入的数据（根据 Read View 判断数据可见性，Read View 在第一次查询时生成）。但是！如果是 `当前读` ，每次读取的都是最新数据，这时如果两次查询中间有其它事务插入数据，就会产生幻读。所以， **`InnoDB` 在实现`Repeatable Read` 时，如果执行的是当前读，则会对读取的记录使用 `Next-key Lock` ，来防止其它事务在间隙间插入数据**

### InnoDB 对 MVCC 的实现

`MVCC` 的实现依赖于：**隐藏字段、Read View、undo log**。在内部实现中，`InnoDB` 通过数据行的 `DB_TRX_ID` 和 `Read View` 来判断数据的可见性，如不可见，则通过数据行的 `DB_ROLL_PTR` 找到 `undo log` 中的历史版本。每个事务读到的数据版本可能是不一样的，在同一个事务中，用户只能看到该事务创建 `Read View` 之前已经提交的修改和该事务本身做的修改

#### 隐藏字段

在内部，`InnoDB` 存储引擎为每行数据添加了三个 [隐藏字段open in new window](https://dev.mysql.com/doc/refman/5.7/en/innodb-multi-versioning.html)：

- `DB_TRX_ID（6字节）`：表示最后一次插入或更新该行的事务 id。（**最近修改(修改/插入)事务ID**）
- `DELETED_BIT (1byte)`, 记录被更新或删除并不代表真的删除，而是删除flag变了(**类似逻辑删除**)
- `DB_ROLL_PTR（7字节）` **回滚指针**，指向该行的 `undo log` 。如果该行未被更新，则为空
- `DB_ROW_ID（6字节）`：如果没有设置主键且该表没有唯一非空索引时，`InnoDB` 会使用该 id 来生成聚簇索引(**隐藏的主键**)

![image-20230201165150965](/images/image-20230201165150965.png)

#### ReadView



```sql
class ReadView {
  /* ... */
private:
  trx_id_t m_low_limit_id;      /* 大于等于这个 ID 的事务均不可见 */

  trx_id_t m_up_limit_id;       /* 小于这个 ID 的事务均可见 */

  trx_id_t m_creator_trx_id;    /* 创建该 Read View 的事务ID */

  trx_id_t m_low_limit_no;      /* 事务 Number, 小于该 Number 的 Undo Logs 均可以被 Purge */

  ids_t m_ids;                  /* 创建 Read View 时的活跃事务列表 */

  m_closed;                     /* 标记 Read View 是否 close */
}
```

[`Read View`open in new window](https://github.com/facebook/mysql-8.0/blob/8.0/storage/innobase/include/read0types.h#L298) 主要是用来做可见性判断，里面保存了 “当前对本事务不可见的其他活跃事务”

主要有以下字段：

- `m_low_limit_id`：目前出现过的最大的事务 ID+1，即下一个将被分配的事务 ID。大于等于这个 ID 的数据版本均不可见
- `m_up_limit_id`：活跃事务列表 `m_ids` 中最小的事务 ID，如果 `m_ids` 为空，则 `m_up_limit_id` 为 `m_low_limit_id`。小于这个 ID 的数据版本均可见
- `m_ids`：`Read View` 创建时其他未提交的活跃事务 ID 列表。创建 `Read View`时，将当前未提交事务 ID 记录下来，后续即使它们修改了记录行的值，对于当前事务也是不可见的。`m_ids` 不包括当前事务自己和已提交的事务（正在内存中）
- `m_creator_trx_id`：创建该 `Read View` 的事务 ID

**事务可见性示意图**：

![image-20230201165955609](/images/image-20230201165955609.png)

#### undo-log

`undo log` 主要有两个作用：

- 当事务回滚时用于将数据恢复到修改前的样子
- 另一个作用是 `MVCC` ，当读取记录时，若该记录被其他事务占用或当前版本对该事务不可见，则可以通过 `undo log` 读取之前的版本数据，以此实现非锁定读

**在 `InnoDB` 存储引擎中 `undo log` 分为：

**Insert undo log** ：插入一条记录时，至少要把这条记录的主键值记下来，之后回滚的时候只需要把这个主键值对应的记录删掉就好了。

**Update undo log**：修改一条记录时，至少要把修改这条记录前的旧值都记录下来，这样之后回滚时再把这条记录更新为旧值就好了。

**Delete undo log**：删除一条记录时，至少要把这条记录中的内容都记下来，这样之后回滚时再把由这些内容组成的记录插入到表中就好了。 

- 删除操作都只是设置一下老记录的DELETED_BIT，并不真正将过时的记录删除。
- 为了节省磁盘空间，InnoDB有专门的purge线程来清理DELETED_BIT为true的记录。为了不影响MVCC的正常工作，purge线程自己也维护了一个read view（这个read view相当于系统中最老活跃事务的read view）;如果某个记录的DELETED_BIT为true，并且DB_TRX_ID相对于purge线程的read view可见，那么这条记录一定是可以被安全清除的。

##### **`insert undo log`** ：

指在 `insert` 操作中产生的 `undo log`。因为 `insert` 操作的记录只对事务本身可见，对其他事务不可见，故该 `undo log` 可以在事务提交后直接删除。不需要进行 `purge` 操作

**`insert` 时的数据初始状态：**

![image-20230201165514158](/images/image-20230201165514158.png)

##### **`update undo log`** ：

`update` 或 `delete` 操作中产生的 `undo log`。该 `undo log`可能需要提供 `MVCC` 机制，因此不能在事务提交时就进行删除。提交时放入 `undo log` 链表，等待 `purge线程` 进行最后的删除

**数据第一次被修改时：**

1. 在事务1修改该行(记录)数据时，数据库会先对该行加排他锁
2. 然后把该行数据拷贝到undo log中，作为旧记录，即在undo log中有当前行的拷贝副本
3. 拷贝完毕后，修改该行name为Tom，并且修改隐藏字段的事务ID为当前事务1的ID, 我们默认从1开始，之后递增，回滚指针指向拷贝到undo log的副本记录，即表示我的上一个版本就是它
4. 事务提交后，释放锁

![image-20230201165536433](/images/image-20230201165536433.png)

**数据第二次被修改时：**

1. 在事务2修改该行数据时，数据库也先为该行加锁
2. 然后把该行数据拷贝到undo log中，作为旧记录，发现该行记录已经有undo log了，那么最新的旧数据作为链表的表头，插在该行记录的undo log最前面
3. 修改该行age为30岁，并且修改隐藏字段的事务ID为当前事务2的ID, 那就是2，回滚指针指向刚刚拷贝到undo log的副本记录
4. 事务提交，释放锁

![image-20230201165644000](/images/image-20230201165644000.png)

不同事务或者相同事务的对同一记录行的修改，会使该记录行的 `undo log` 成为一条链表，**链首就是最新的记录**，**链尾就是最早的旧记录**。

该**undo log的节点可能是会purge线程清除掉**，例子中的第一条insert undo log，其实在事务提交之后可能就被删除丢失了

#### 数据可见性算法

在 `InnoDB` 存储引擎中，创建一个新事务后，执行每个 `select` 语句前，都会创建一个快照（Read View），**快照中保存了当前数据库系统中正处于活跃（没有 commit）的事务的 ID 号**。其实简单的说保存的是系统中当前不应该被本事务看到的其他事务 ID 列表（即 m_ids）。当用户在这个事务中要读取某个记录行的时候，`InnoDB` 会将该记录行的 `DB_TRX_ID` 与 `Read View` 中的一些变量及当前事务 ID 进行比较，判断是否满足可见性条件

具体的比较算法如下

```sql
/* storage/innobase/include/read0types.h */

bool changes_visible(trx_id_t id, const table_name_t &name) const
      MY_ATTRIBUTE((warn_unused_result)) {
    ut_ad(id > 0);
		
    /* 假如 trx_id 小于 Read View 限制的最小活跃事务ID m_up_limit_id 或者等于正在创建的事务ID
     * m_creator_trx_id 即满足事务的可见性. */
    if (id < m_up_limit_id || id == m_creator_trx_id) {
      /* 可见. */
      return (true);
    }

    /* 检查 trx_id 是否有效. */
    check_trx_id_sanity(id, name);
		
    if (id >= m_low_limit_id) {
      /* 假如 trx_id 大于等于最大活跃的事务ID m_low_limit_id, 即不可见. */
      return (false);
    } else if (m_ids.empty()) {
      /* 假如目前不存在活跃的事务，即可见. */
      return (true);
    }

    const ids_t::value_type *p = m_ids.data();

    /* 利用二分查找搜索活跃事务列表, 当 trx_id 在 m_up_limit_id 和 m_low_limit_id 之间
     * 如果 id 在 m_ids 数组中, 表明 ReadView 创建时候，事务处于活跃状态，因此记录不可见. */
    return (!std::binary_search(p, p + m_ids.size(), id));
  }
```

1. 如果记录 DB_TRX_ID < m_up_limit_id，那么表明最新修改该行的事务（DB_TRX_ID）在当前事务创建快照之前就提交了，所以该记录行的值对当前事务是可见的
2. 如果 DB_TRX_ID >= m_low_limit_id，那么表明最新修改该行的事务（DB_TRX_ID）在当前事务创建快照之后才修改该行，所以该记录行的值对当前事务不可见。跳到步骤 5
3. m_ids 为空，则表明在当前事务创建快照之前，修改该行的事务就已经提交了，所以该记录行的值对当前事务是可见的
4. 如果 m_up_limit_id <= DB_TRX_ID < m_low_limit_id，表明最新修改该行的事务（DB_TRX_ID）在当前事务创建快照的时候可能处于“活动状态”或者“已提交状态”；所以就要对活跃事务列表 m_ids 进行查找（源码中是用的二分查找，因为是有序的）
   - 如果在活跃事务列表 m_ids 中能找到 DB_TRX_ID，表明：① 在当前事务创建快照前，该记录行的值被事务 ID 为 DB_TRX_ID 的事务修改了，但没有提交；或者 ② 在当前事务创建快照后，该记录行的值被事务 ID 为 DB_TRX_ID 的事务修改了。这些情况下，这个记录行的值对当前事务都是不可见的。跳到步骤 5
   - 在活跃事务列表中找不到，则表明“id 为 trx_id 的事务”在修改“该记录行的值”后，在“当前事务”创建快照前就已经提交了，所以记录行对当前事务可见
5. 在该记录行的 DB_ROLL_PTR 指针所指向的 `undo log` 取出快照记录，用快照记录的 DB_TRX_ID 跳到步骤 1 重新开始判断，直到找到满足的快照版本或返回空

### RC 和 RR 隔离级别下 MVCC 的差异

在事务隔离级别 `RC` 和 `RR` （InnoDB 存储引擎的默认事务隔离级别）下，`InnoDB` 存储引擎使用 `MVCC`（非锁定一致性读），但它们生成 `Read View` 的时机却不同

- 在 RC 隔离级别下的 **`每次select`** 查询前都生成一个`Read View` (m_ids 列表)
- 在 RR 隔离级别下只在事务开始后 **`第一次select`** 数据前生成一个`Read View`（m_ids 列表）

### MVCC 解决不可重复读问题

虽然 RC 和 RR 都通过 `MVCC` 来读取快照数据，但由于 **生成 Read View 时机不同**，从而在 RR 级别下实现可重复读

举个例子：

![image-20230201170357019](/images/image-20230201170357019.png)

#### 在 RC 下 ReadView 生成情况

**1. 假设时间线来到 T4 ，那么此时数据行 id = 1 的版本链为：**

![image-20230201170459727](/images/image-20230201170459727.png)

由于 RC 级别下每次查询都会生成`Read View` ，并且事务 101、102 并未提交，此时 `103` 事务生成的 `Read View` 中活跃的事务 **`m_ids` 为：[101,102]** ，`m_low_limit_id`为：104，`m_up_limit_id`为：101，`m_creator_trx_id` 为：103

- 此时最新记录的 `DB_TRX_ID` 为 101，m_up_limit_id <= 101 < m_low_limit_id，所以要在 `m_ids` 列表中查找，发现 `DB_TRX_ID` 存在列表中，那么这个记录不可见
- 根据 `DB_ROLL_PTR` 找到 `undo log` 中的上一版本记录，上一条记录的 `DB_TRX_ID` 还是 101，不可见
- 继续找上一条 `DB_TRX_ID`为 1，满足 1 < m_up_limit_id，可见，所以事务 103 查询到数据为 `name = 菜花`

**2. 时间线来到 T6 ，数据的版本链为：**

![image-20230201170511755](/images/image-20230201170511755.png)

因为在 RC 级别下，重新生成 `Read View`，这时事务 101 已经提交，102 并未提交，所以此时 `Read View` 中活跃的事务 **`m_ids`：[102]** ，`m_low_limit_id`为：104，`m_up_limit_id`为：102，`m_creator_trx_id`为：103

- 此时最新记录的 `DB_TRX_ID` 为 102，m_up_limit_id <= 102 < m_low_limit_id，所以要在 `m_ids` 列表中查找，发现 `DB_TRX_ID` 存在列表中，那么这个记录不可见
- 根据 `DB_ROLL_PTR` 找到 `undo log` 中的上一版本记录，上一条记录的 `DB_TRX_ID` 为 101，满足 101 < m_up_limit_id，记录可见，所以在 `T6` 时间点查询到数据为 `name = 李四`，与时间 T4 查询到的结果不一致，不可重复读！

**3. 时间线来到 T9 ，数据的版本链为：**

![image-20230201170524310](/images/image-20230201170524310.png)

重新生成 `Read View`， 这时事务 101 和 102 都已经提交，所以 **m_ids** 为空，则 m_up_limit_id = m_low_limit_id = 104，最新版本事务 ID 为 102，满足 102 < m_low_limit_id，可见，查询结果为 `name = 赵六`

> **总结：** **在 RC 隔离级别下，事务在每次查询开始时都会生成并设置新的 Read View，所以导致不可重复读**

#### 在 RR 下 ReadView 生成情况

在可重复读级别下，只会在事务开始后第一次读取数据时生成一个 Read View（m_ids 列表）

**1. 在 T4 情况下的版本链为：**

![image-20230201170539755](/images/image-20230201170539755.png)

在当前执行 `select` 语句时生成一个 `Read View`，此时 **`m_ids`：[101,102]** ，`m_low_limit_id`为：104，`m_up_limit_id`为：101，`m_creator_trx_id` 为：103

此时和 RC 级别下一样：

- 最新记录的 `DB_TRX_ID` 为 101，m_up_limit_id <= 101 < m_low_limit_id，所以要在 `m_ids` 列表中查找，发现 `DB_TRX_ID` 存在列表中，那么这个记录不可见
- 根据 `DB_ROLL_PTR` 找到 `undo log` 中的上一版本记录，上一条记录的 `DB_TRX_ID` 还是 101，不可见
- 继续找上一条 `DB_TRX_ID`为 1，满足 1 < m_up_limit_id，可见，所以事务 103 查询到数据为 `name = 菜花`

**2. 时间点 T6 情况下：**

![image-20230201170549490](/images/image-20230201170549490.png)

在 RR 级别下只会生成一次`Read View`，所以此时依然沿用 **`m_ids` ：[101,102]** ，`m_low_limit_id`为：104，`m_up_limit_id`为：101，`m_creator_trx_id` 为：103

- 最新记录的 `DB_TRX_ID` 为 102，m_up_limit_id <= 102 < m_low_limit_id，所以要在 `m_ids` 列表中查找，发现 `DB_TRX_ID` 存在列表中，那么这个记录不可见
- 根据 `DB_ROLL_PTR` 找到 `undo log` 中的上一版本记录，上一条记录的 `DB_TRX_ID` 为 101，不可见
- 继续根据 `DB_ROLL_PTR` 找到 `undo log` 中的上一版本记录，上一条记录的 `DB_TRX_ID` 还是 101，不可见
- 继续找上一条 `DB_TRX_ID`为 1，满足 1 < m_up_limit_id，可见，所以事务 103 查询到数据为 `name = 菜花`

**3. 时间点 T9 情况下：**

![image-20230201170601467](/images/image-20230201170601467.png)

此时情况跟 T6 完全一样，由于已经生成了 `Read View`，此时依然沿用 **`m_ids` ：[101,102]** ，所以查询结果依然是 `name = 菜花`

### MVCC➕Next-key-Lock 防止幻读

`InnoDB`存储引擎在 RR 级别下通过 `MVCC`和 `Next-key Lock` 来解决幻读问题：

**1、执行普通 `select`，此时会以 `MVCC` 快照读的方式读取数据**

在快照读的情况下，RR 隔离级别只会在事务开启后的第一次查询生成 `Read View` ，并使用至事务提交。所以在生成 `Read View` 之后其它事务所做的更新、插入记录版本对当前事务并不可见，实现了可重复读和防止快照读下的 “幻读”

**2、执行 select...for update/lock in share mode、insert、update、delete 等当前读**

在当前读下，读取的都是最新的数据，如果其它事务有插入新的记录，并且刚好在当前事务查询范围内，就会产生幻读！`InnoDB` 使用 [Next-key Lockopen in new window](https://dev.mysql.com/doc/refman/5.7/en/innodb-locking.html#innodb-next-key-locks) 来防止这种情况。当执行当前读时，会锁定读取到的记录的同时，锁定它们的间隙，防止其它事务在查询范围内插入数据。只要我不让你插入，就不会发生幻读

## 存储引擎

### InnoDB

具备**外键**支持功能的**事务**存储引擎

![image-20221105151036572](/images/image-20221105151036572.png)

### MyISAM

![image-20221105151306925](/images/image-20221105151306925.png)

### 二者对比

![image-20221105151331261](/images/image-20221105151331261.png)

## 索引

索引是帮助MySQL高效获取数据的数据结构（**Innodb存储引擎默认使用B+Tree索引结构**）

B+树的页（大小默认为16kb）

![image-20221117165712218](/images/image-20221117165712218.png)、

B Tree 指的是 Balance Tree，也就是平衡树。平衡树是一颗查找树，并且所有叶子节点位于同一层。

B+ Tree 是基于 B Tree 和叶子节点顺序访问指针进行实现，它具有 B Tree 的平衡性，并且通过顺序访问指针来提高区间查询的性能。

在 B+ Tree 中，一个节点中的 key 从左到右非递减排列，如果某个指针的左右相邻 key 分别是 keyi 和 keyi+1，且不为 null，则该指针指向节点的所有 key 大于等于 keyi 且小于等于 keyi+1。

B+Tree的**高度决定IO的次数** **一次IO会读取一个页的数据**

B+Tree的特点是树**高度很低**（IO的次数少） 叶子节点出度很大（储存数据）

(一)**更少的查找次数**

平衡树查找操作的时间复杂度等于树高 h，而树高大致为 O(h)=O(logdN)，其中 d 为每个节点的出度。

红黑树的出度为 2，而 B+ Tree 的出度一般都非常大，所以红黑树的树高 h 很明显比 B+ Tree 大非常多，检索的次数也就更多。

(二)**利用计算机预读特性**

**为了减少磁盘 I/O**，**磁盘往往不是严格按需读取**，而是每次都会**预读**。预读过程中，磁盘进行顺序读取，**顺序读取不需要进行磁盘寻道**，并且只需要很短的旋转时间，因此速度会非常快。

操作系统一般将内存和磁盘分割成固态大小的块，每一块称为一页，**内存与磁盘以页为单位交换数据**。数据库系统将**索引的一个节点的大小设置为页的大小**，使得**一次 I/O 就能完全载入一个节点**，并且可以利用预读特性，相邻的节点也能够被预先载入。

### 使用索引的优缺点

![image-20221117162845235](/images/image-20221117162845235.png)

![image-20221117163101308](/images/image-20221117163101308.png)



### Innodb存储引擎的索引结构

![image-20221117170234277](/images/image-20221117170234277.png)

B+Tree

![image-20221117163321223](/images/image-20221117163321223.png)

#### 聚簇索引

![image-20221117163934390](/images/image-20221117163934390.png)

![image-20221117164008929](/images/image-20221117164008929.png)

![image-20221117164029693](/images/image-20221117164029693.png)



![image-20221117163321223](/images/image-20221117163321223.png)

![image-20221117164107226](/images/image-20221117164107226.png)

![image-20221117164127755](/images/image-20221117164127755.png)

![image-20221117164148732](/images/image-20221117164148732.png)



#### 非聚簇索引

![image-20221117164209647](/images/image-20221117164209647.png)

![image-20221117164522759](/images/image-20221117164522759.png)

![image-20221117164227073](/images/image-20221117164227073.png)

##### 二级索引

![image-20221117164451667](/images/image-20221117164451667.png)

##### 联合索引

![image-20221117164654190](/images/image-20221117164654190.png)

![image-20221117164639245](/images/image-20221117164639245.png)

##### 回表

**![image-20221117164405616](/images/image-20221117164405616.png)**

### Innodb引擎索引的注意事项

#### 根页面万年不动

当索引创建的时候是从根节点出发的

#### 内节点中目录项记录的唯一性

非聚簇索引中 也就是**非主键索引中** 可能创建的索引会出现相同的情况 因此**为了保证目录项的唯一性** 使用**主键+页号**的方式构成

![image-20221117165315387](/images/image-20221117165315387.png)

![image-20221117165446585](/images/image-20221117165446585.png)

#### 一个页面最少储存2条记录

### 哈希|二叉树|AVLTree|B-Tree|红黑树|B+Tree

##### 哈希索引

哈希索引能以 O(1) 时间进行查找，但是失去了有序性，它具有以下限制:

- **无法用于排序与分组**；
- 只支持精确查找，**无法用于部分查找和范围查找**。

**InnoDB 存储引擎**有一个特殊的功能叫“**自适应哈希索引**”，**当某个索引值被使用的非常频繁时**，会**在 B+Tree 索引之上再创建一个哈希索引**，这样就让 B+Tree 索引具有哈希索引的一些优点，比如快速的哈希查找。

##### 二叉树

树高度会过高

极端情况下会退化成链表

##### AVLTree

平衡二叉搜索树

树过高



![image-20221117171231544](/images/image-20221117171231544.png)

##### B-Tree

叶子节点与非叶子节点都会存放数据 当对数据进行增删操作时 为了保证树的平衡性 会对非叶子节点进行调节（性能消耗）

插入删除操作记录会破坏平衡树的平衡性，因此在插入删除操作之后，**需要对树进行一个分裂、合并、旋转等操作来维护平衡性**

相较于B+Tree将数据全部放在叶子节点 非叶子节点不存放数据 并且对叶子节点进行双向链表关联起来

![image-20221117171630686](/images/image-20221117171630686.png)

![image-20221117171402867](/images/image-20221117171402867.png)

##### B+Tree

![image-20221117171926475](/images/image-20221117171926475.png)

![image-20221117171848398](/images/image-20221117171848398.png)

![image-20221117172015738](/images/image-20221117172015738.png)

##### 红黑树

![image-20221117172111742](/images/image-20221117172111742.png)

## 存储结构

[一文理解 MySQL 中的 page 页 - 腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1818381)

InnoDB存储引擎的逻辑结构

所有数据都被逻辑地存放在一个空间内，称为**表空间(tablespace)**，而表空间由**段（sengment）**、**区（extent）**、**页（page）**组成。在一些文档中extend又称块（block）

![image-20221120143010692](/images/image-20221120143010692.png)

![image-20221120150923778](/images/image-20221120150923778.png)

![image-20221120151016776](/images/image-20221120151016776.png)

### 页结构

[MySQL 页完全指南——浅入深出页的原理 - detectiveHLH - 博客园 (cnblogs.com)](https://www.cnblogs.com/detectiveHLH/p/14907405.html)[MySQL 页完全指南——浅入深出页的原理 - detectiveHLH - 博客园 (cnblogs.com)](https://www.cnblogs.com/detectiveHLH/p/14907405.html)

![image-20221120143604048](/images/image-20221120143604048.png)

**页**是InnoDB存储引擎**磁盘管理的最小单位**，**每个页默认16KB**；InnoDB存储引擎从1.2.x版本开始，可以通过参数innodb_page_size将页的大小设置为4K、8K、16K。若设置完成，则所有表中页的大小都为innodb_page_size，不可以再次对其进行修改，除非通过mysqldump导入和导出操作来产生新的库。

**页对应B+Tree的一个叶**

**每个页使用双向链表连接起来**

![image-20221120143440603](/images/image-20221120143440603.png)

![image-20221120143652834](/images/image-20221120143652834.png)

innoDB存储引擎中，常见的页类型有：

**\1. 数据页（B-tree Node)**

\2. undo页（undo Log Page）

\3. 系统页 （System Page）

\4. 事物数据页 （Transaction System Page）

\5. 插入缓冲位图页（Insert Buffer Bitmap）

\6. 插入缓冲空闲列表页（Insert Buffer Free List）

\7. 未压缩的二进制大对象页（Uncompressed BLOB Page）

\8. 压缩的二进制大对象页 （compressed BLOB Page）

### 区，段，碎片区与表空间结构

## 索引的创建与设计原则

### 索引的分类

**逻辑上划分**：普通索引(INDEX)，唯一索引(UNIQUE INDEX)，主键索引，全文索引（FULLTEXT INDEX）

**物理实现上划分**：聚簇索引，非聚簇索引

**作用字段个数划分**：单列索引，联合索引

### 索引的创建

**创建表的时候**指定索引

在声明 primary key， unique，foreign key的字段上会自动添加相关索引

未指定索引名称 默认为字段名

```mysql
CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
UNIQUE (P_Id)
)
```

**全文索引**

![image-20221120155332353](/images/image-20221120155332353.png)

![image-20221120155104741](/images/image-20221120155104741.png)

**使用了全文索引的查询**

不使用like '%查询的text%';

```mysql
select * from papers where match(title,content) against (‘查询的text’)；
```

**创建表后添加**索引
ALTER TABLE

ADD

```mysql
#ALTER TABLE 时的 SQL UNIQUE 约束
当表已被创建时，如需在 "P_Id" 列创建 UNIQUE 约束，请使用下面的 SQL：

MySQL / SQL Server / Oracle / MS Access：

ALTER TABLE Persons
ADD UNIQUE (P_Id)
如需命名 UNIQUE 约束，并定义多个列的 UNIQUE 约束，请使用下面的 SQL 语法：

MySQL / SQL Server / Oracle / MS Access：

ALTER TABLE Persons
ADD CONSTRAINT uc_PersonID UNIQUE (P_Id,LastName)
```

CREATE INDEX [indexname] ON [table (file,file,...)]

```mysql
CREATE INDEX index_uname ON table_user (username);
```



### 索引的删除

**实战经验：当需要进行大量的增删改操作前将索引删除掉 完成增删改操作后再添加上索引（效率优化）**

```mysql
删除索引的语法
DROP INDEX [indexName] ON mytable;

ALTER TABLE [tablename] DROP INDEX [indexname];
```

**AUTO_INCREMENT自增长的字段的UNIQUE唯一约束（索引）不能被删除**

![image-20221120160614653](/images/image-20221120160614653.png)

### MySQL8.0支持降序索引

之前的索引都是升序的 若我们order by 字段 desc 使用降序排序时要进行反向扫描 效率较低

8.0之后支持降序索引 索引可以降序 因此避免了上诉反向扫描的情况 效率不受影响

![image-20221120160838423](/images/image-20221120160838423.png)

```mysql
CREATE INDEX index_name_age ON table_user (username ASC,age DESC);
```

```mysql
create index index_name_major on table_user (username asc,major desc);

mysql> show create table table_user\G;
*************************** 1. row ***************************
       Table: table_user
Create Table: CREATE TABLE `table_user` (
  `id` int NOT NULL AUTO_INCREMENT,
  `username` varchar(15) COLLATE utf8mb3_bin NOT NULL DEFAULT '',
  `password` varchar(35) COLLATE utf8mb3_bin NOT NULL DEFAULT '',
  `major` varchar(35) COLLATE utf8mb3_bin NOT NULL DEFAULT '',
  `email` varchar(35) COLLATE utf8mb3_bin NOT NULL DEFAULT '',
  PRIMARY KEY (`id`),
  KEY `index_name_major` (`username`,`major` DESC)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8mb3 COLLATE=utf8mb3_bin
1 row in set (0.00 sec)
```

![image-20221120161632602](/images/image-20221120161632602.png)

### MySQL8.0支持隐藏索引

避免删除后发现数据出现错误还要把索引再添加回来的情况（资源消耗）

**隐藏(invisible)索引**：

**先将索引隐藏**实现**索引失效**的效果 **发现数据无错误**后**再确定将所有进行删除**

**可以用来检测索对当前数据起到的效率（查询性能提升幅度）**可以**将索引设置为invisible先** 再**通过explain进行性能监控** 而**不是直接删除索引 再创建回索引**

![image-20221120162740795](/images/image-20221120162740795.png)

![image-20221120163518013](/images/image-20221120163518013.png)

```mysql
CREATE INDEX index_uname ON table_user (username) INVISIBLE;
```

```mysql
CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
UNIQUE (P_Id) INVISIBLE
)
```

#### 修改索引的可见性

```mysql
ALTER TABLE table_user ALTER INDEX [indexname] VISIBLE/INVISIBLE;
```

### 索引的设计原则

索引是把双刃剑

提高查询效率

同时影响增删改的效率并且占用磁盘空间

#### 适合创建索引的情况

**1）字段的数值有唯一性约束**

**2）频繁作为where查询条件的字段**

**3）经常group by和order by的列**

```markdown
如果同时要使用到group by 和 order by 可以考虑建立联合索引 注意先group by 后order by

（执行顺序是先group by --> order by）
```

**4）update，delete和where条件列**

```markdown
我们需要先根据where条件列检索出记录 然后进行更新或删除操作

因此在进行更新或删除操作时对where字段创建了索引能大幅提高效率

对于查询而言 有索引 会极大的提高查询的效率 

对于更新或删除而言 有索引则需要对索引进行再次维护 （更新的是非索引字段则效率更高）
```

**5）distinct字段需要创建索引**

**6）多表join连接操作时**

```markdown
连接**表的数量不要超过3** 数量级剧增 影响效率

对于**where条件创建索引** where作为数据的过滤

对于**连接的字段创建索引** 对于**连接的字段**多张表中的**数据类型必须一致
```

**7）使用列的类型小的创建索引**

```markdown
数据类型越小 **查询速度越快**

数据类型越小 索引**占用的空间越小** **数据页中可以放下更多的记录** 减少I/O带来的性能损耗 **可以将更多的页缓存在内存中** 加快读写速度

**主键数据类型尽可能的小**（聚簇索引和非聚簇索引都是会存储主键值的）
```

**8）使用字符串前缀创建索引**

![image-20221207095347562](/images/image-20221207095347562.png)

```markdown
字符串越长 占用的空间越大

字符串越长 比较时花费的时间更长

使用**前缀索引**（截取字符串前面的部分作为索引）节约空间的同时 减少字符串比较所花费的时间

create table shop (address varchar(150) not null default '');

alter table shop add index (address(12));

计算应当截取多少合适
公式 区别度计算 
count(distinct left(column,index_length)) / count(*);
截取前多少个字符的选择度计算 越接近1越好
```

![image-20221207095527112](/images/image-20221207095527112.png)

**9）区分度高（散列性高）的列适合作为索引**

```markdown
使用计算区分度的公式：select count(distinct column) / count(*) from table
越接近1越好 一半超过33%算比较高效的索引

联合索引要把区分度高的（散列性高的）列放在前面
```

**10）使用最频繁的列放到联合索引的左侧**

**11）在多个字段都需要创建索引的时候，联合索引优于单个值索引**

#### 限制索引的数目

单表索引数量**不要超过6个**

1）索引会**占用磁盘空间**

2）索引**影响insert delete update 等操作的性能** 数据做修改时 **需要对索引进行维护**

3）**优化器**进行优化查询时 使**用索引来进行评估**以生成最好的执行计划 **索引过多** 会**影响优化器的执行效率** 从而影响整个执行过程的性能

#### 不适合创建索引的情况

1）在where group by order by 中未使用到的字段

2）数据量小的表最好不要创建索引

3）有大量重复数据的列上不要创建索引（区分度不高/散列性不高的列）

4）避免对经常更新（增删改）的表创建过多的索引 每次更新都需要对索引进行维护

5）不建议使用无序的值作为索引

6）删除不再使用或很少使用的索引

7）不要定义冗余或者重复的索引 （联合索引可以做到单列索引的工作时 不要单独再建立单列索引了）（主键即代表了唯一索引 因此不要再创建主键为唯一索引或普通索引）



## MySQL 索引失效场景

### 1.联合索引不满足最左匹配原则

### 2.使用了select *

### 3.索引列参与运算

### 4.索引列参使用了函数

### 5.模糊查询时(like语句)，模糊匹配的占位符%位于条件的首部

### 6.类型隐式转换

### 7.使用or关键字，其中一个字段没有创建索引;or两边为“>”和“<”范围查询

### 8.两列做比较

### 9.当查询条件为字符串时，使用”<>“或”!=“作为条件查询，有可能不走索引

### 10.is not null

### 11.使用not in时，字段不是主键;使用not exists时

### 12.使用order by时，字段不是主键;查询条件涉及到order  by、limit等条件时，情况比较复杂（使用explain）

### 13.Mysql发现通过索引扫描的行记录数超过全表的10%-30%时，优化器可能会放弃走索引（使用explain）

## 性能分析

对数据库进行调优：目标是：**响应时间快，吞吐量大；**

利用宏观的**监控工具**和微观的**日志分析**可以快速找到调优的思路和方法

![image-20221207114919876](/images/image-20221207114919876.png)

### 数据库服务器优化的步骤

观察分析（Show status） 以及 行动（Action）

![image-20221207114840144](/images/image-20221207114840144.png)



### 查看系统性能参数

![image-20221207115000574](/images/image-20221207115000574.png)

```sql
mysql> show status like 'connections';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| Connections   | 10    |
+---------------+-------+
1 row in set (0.02 sec)
```

### 统计sql查询成本（cost）

```sql
show status like 'last_query_cost';

mysql> show status like 'last_query_cost';
+-----------------+-----------+
| Variable_name   | Value     |
+-----------------+-----------+
| Last_query_cost | 10.249000 |
+-----------------+-----------+
1 row in set (0.01 sec)

# value 代表当前需要加载到的数据页页数
```

![image-20221207120001163](/images/image-20221207120001163.png)

### 慢查询日志

**定位执行慢的sql:**

用来记录在MySQL中响应时间超过阈值（**long_query_time**值）的语句，会将其记录在慢查询日志中。

**long_query_time**默认值为**10s**（运行时间超过10s）

**默认情况下不开启慢查询日志**（影响平时运行效率），**调优时**可以**手动进行开启**

慢查询日志将日志记录写入文件

```sql
#查看慢查询参数
mysql> show variables like '%slow_query_log';
+----------------+-------+
| Variable_name  | Value |
+----------------+-------+
| slow_query_log | OFF   |
+----------------+-------+
1 row in set (0.00 sec)

mysql> 

#开启慢查询
mysql> set global slow_query_log = on;
Query OK, 0 rows affected (0.01 sec)

mysql> 

#查看慢查询日志文件
mysql> show variables like '%slow_query_log%';
+---------------------+---------------------------------------+
| Variable_name       | Value                                 |
+---------------------+---------------------------------------+
| slow_query_log      | ON                                    |
| slow_query_log_file | /usr/local/mysql/mysqldb/192-slow.log |
+---------------------+---------------------------------------+
2 rows in set (0.00 sec)

mysql> 

#查看慢查询阈值long_query_time（默认10s）
mysql> show variables like '%long_query_time%';
+-----------------+-----------+
| Variable_name   | Value     |
+-----------------+-----------+
| long_query_time | 10.000000 |
+-----------------+-----------+
1 row in set (0.00 sec)

#设置慢查询阈值(注意设置的是global变量还是session变量)
mysql> set global long_query_time = 1;
Query OK, 0 rows affected (0.00 sec)

mysql> show variables like '%long_query_time%';
+-----------------+-----------+
| Variable_name   | Value     |
+-----------------+-----------+
| long_query_time | 10.000000 |
+-----------------+-----------+
1 row in set (0.00 sec)

mysql> set global long_query_time = 1;
Query OK, 0 rows affected (0.00 sec)

mysql> show global variables like '%long_query_time%';
+-----------------+----------+
| Variable_name   | Value    |
+-----------------+----------+
| long_query_time | 1.000000 |
+-----------------+----------+
1 row in set (0.01 sec)

mysql> set long_query_time = 1;
Query OK, 0 rows affected (0.00 sec)

mysql> show variables like '%long_query_time%';
+-----------------+----------+
| Variable_name   | Value    |
+-----------------+----------+
| long_query_time | 1.000000 |
+-----------------+----------+
1 row in set (0.00 sec)

```

**永久配置则需要在配置文件中进行配置**

my.cnf

```
[root@192 bin]# find / -name my.cnf
/etc/my.cnf
[root@192 bin]# 
```

![image-20221207141647697](/images/image-20221207141647697.png)

**mysqldumpslow查看慢查询日志**

```sql
[root@192 bin]# ./mysqldumpslow -s t -t 5 /usr/local/mysql/mysqldb/192-slow.log
								#sort 排序方式 t更加查询时间降序 -t 显示top多少条数据 
Reading mysql slow query log from /usr/local/mysql/mysqldb/192-slow.log
Count: 1  Time=1.13s (1s)  Lock=0.00s (0s)  Rows=1000000.0 (1000000), root[root]@localhost
  select * from students

Died at ./mysqldumpslow line 162, <> chunk 1.
[root@192 bin]# 
```

**删除/重置慢查询日志文件**

```sql
[root@192 bin]# ./mysqladmin -u root -p flush-logs slow #重置慢查询日志文件
Enter password: 
[root@192 bin]# 

#删除慢查询日志文件
[root@192 mysqldb]# rm 192-slow.log 
rm: remove regular file ‘192-slow.log’? y
[root@192 mysqldb]# 
```

### show profile

![image-20221207152038538](/images/image-20221207152038538.png)

```sql
mysql> show variables like 'profiling';#查看profiling是否开启状态 （默认是关闭的）
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| profiling     | OFF    |
+---------------+-------+
1 row in set (0.00 sec)

mysql> set profiling = 'ON';#设置profiling为开启
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysql> show profiles;
+----------+------------+---------------------------------+
| Query_ID | Duration   | Query                           |
+----------+------------+---------------------------------+
|        1 | 0.00173125 | show variables like 'profiling' |
|        2 | 0.00087875 | select * from student           |
|        3 | 1.07819950 | select * from students          |
|        4 | 0.00205300 | show variables like 'profiling' |
|        5 | 0.00016450 | set profiling = 'ON'            |
+----------+------------+---------------------------------+
5 rows in set, 1 warning (0.00 sec)

mysql> show profile
    -> ;
+----------------+----------+
| Status         | Duration |
+----------------+----------+
| starting       | 0.000085 |
| Opening tables | 0.000035 |
| query end      | 0.000010 |
| closing tables | 0.000005 |
| freeing items  | 0.000016 |
| cleaning up    | 0.000014 |
+----------------+----------+
6 rows in set, 1 warning (0.00 sec)

mysql> show profile for query 3
    -> ;
+--------------------------------+----------+
| Status                         | Duration |
+--------------------------------+----------+
| starting                       | 0.000091 |
| Executing hook on transaction  | 0.000011 |
| starting                       | 0.000013 |
| checking permissions           | 0.000010 |
| Opening tables                 | 0.000055 |
| init                           | 0.000014 |
| System lock                    | 0.000017 |
| optimizing                     | 0.000007 |
| statistics                     | 0.000016 |
| preparing                      | 0.000019 |
| executing                      | 1.077882 |
| end                            | 0.000018 |
| query end                      | 0.000005 |
| waiting for handler commit     | 0.000012 |
| closing tables                 | 0.000011 |
| freeing items                  | 0.000011 |
| cleaning up                    | 0.000012 |
+--------------------------------+----------+
17 rows in set, 1 warning (0.00 sec)

mysql> show profile cpu,block io for query 3;
+--------------------------------+----------+----------+------------+--------------+---------------+
| Status                         | Duration | CPU_user | CPU_system | Block_ops_in | Block_ops_out |
+--------------------------------+----------+----------+------------+--------------+---------------+
| starting                       | 0.000091 | 0.000050 |   0.000034 |            0 |             0 |
| Executing hook on transaction  | 0.000011 | 0.000005 |   0.000004 |            0 |             0 |
| starting                       | 0.000013 | 0.000008 |   0.000005 |            0 |             0 |
| checking permissions           | 0.000010 | 0.000006 |   0.000004 |            0 |             0 |
| Opening tables                 | 0.000055 | 0.000033 |   0.000023 |            0 |             0 |
| init                           | 0.000014 | 0.000008 |   0.000005 |            0 |             0 |
| System lock                    | 0.000017 | 0.000009 |   0.000007 |            0 |             0 |
| optimizing                     | 0.000007 | 0.000003 |   0.000002 |            0 |             0 |
| statistics                     | 0.000016 | 0.000010 |   0.000007 |            0 |             0 |
| preparing                      | 0.000019 | 0.000011 |   0.000007 |            0 |             0 |
| executing                      | 1.077882 | 0.831914 |   0.000000 |            0 |             0 |
| end                            | 0.000018 | 0.000011 |   0.000000 |            0 |             0 |
| query end                      | 0.000005 | 0.000005 |   0.000000 |            0 |             0 |
| waiting for handler commit     | 0.000012 | 0.000011 |   0.000000 |            0 |             0 |
| closing tables                 | 0.000011 | 0.000012 |   0.000000 |            0 |             0 |
| freeing items                  | 0.000011 | 0.000011 |   0.000000 |            0 |             0 |
| cleaning up                    | 0.000012 | 0.000012 |   0.000000 |            0 |             0 |
+--------------------------------+----------+----------+------------+--------------+---------------+
17 rows in set, 1 warning (0.00 sec)
```

### EXPLAIN★

定位了执行慢的查询语句后（通过慢查询日志查看）；使用**EXPLAIN**分析/DESCRIBEF分析查看**执行计划**；针对性的对sql语句进行分析

![image-20221207152547152](/images/image-20221207152547152.png)

目前5.7版本以来的EXPLAIN可以应用在select ，update 以及delete语句

```sql
explain select * from students;
explain update students set `name` = 'eddie' where id = 1;
explain delete from students where id = 1;
```

**涉及到几张表就会有几条记录**

**前面的表**称之为**驱动表** **后边的表**称之为**被驱动表**

![image-20221207153656988](/images/image-20221207153656988.png)

![image-20221207153248476](/images/image-20221207153248476.png)

## Mysql主从复制

![image-20230108082244019](/images/image-20230108082244019.png)

![image-20230108082309588](/images/image-20230108082309588.png)

### 主从复制原理

![image-20230108082403130](/images/image-20230108082403130.png)

MySQL binlog(**binary log 即二进制日志文件**) 主要记录了 MySQL 数据库中数据的所有变化(数据库执行的所有 DDL 和 DML 语句)。因此，我们根据主库的 MySQL binlog 日志就能够将主库的数据同步到从库中。

1) 主库将数据库中数据的变化写入到 binlog

2) 从库连接主库

3) 从库会创建一个 I/O 线程向主库请求更新的 binlog

4) 主库会创建一个 binlog dump 线程来发送 binlog ，从库中的 I/O 线程负责接收

5) 从库的 I/O 线程将接收的 binlog 写入到 relay log 中。

6) 从库的 SQL 线程读取 relay log 同步数据本地（也就是再执行一遍 SQL ）。

### 主从数据库环境搭建

**1）准备两台Linux服务器 分别安装Mysql 搭建一主一从**

tip:若是clone的Linux服务器 记得将其中一个的MySQL的UUID 进行修改

![image-20230108093125043](/images/image-20230108093125043.png)

**2）分别配置两个MySQL的my.cnf（MySQL的配置文件）**

配置文件修改后重启MySQL服务

![image-20230108094024340](/images/image-20230108094024340.png)

**从服务器更完整的配置**

```
## 设置server_id,注意要唯一
server-id=101  
## 开启二进制日志功能，以备Slave作为其它Slave的Master时使用
log-bin=slave-bin   
## relay_log配置中继日志
relay_log=/var/lib/mysql/relay.log  
read_only=1  ## 设置为只读,该项如果不设置，表示slave可读可写
```

**3）配置并开启主从复制**

master

在Master数据库创建数据同步用户，授予用户 slave REPLICATION SLAVE权限和REPLICATION CLIENT权限，用于在主从库之间同步数据。

```mysql
CREATE USER 'slave'@'%' IDENTIFIED WITH mysql_native_password BY 'slave';
GRANT REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'slave'@'%';

show master status;
```

slave

```mysql
change master to master_host='192.168.199.181',
 master_user='slave', 
 master_password='slave', 
 master_port=3306, 
 master_log_file='mysql-bin.000003', 
 master_log_pos=1239, 
 master_connect_retry=30;
 
 
 start slave;
 stop slave;
 
 show slave status;
```

![image-20230108095447271](/images/image-20230108095447271.png)

**4）查看主从状态**

![image-20230108095705696](/images/image-20230108095705696.png)

### Sharding-JDBC

1）引入maven坐标

```xml
<!--TODO sharding-jdbc整合springboot框架 实现mysql 主从复制 读写分离-->
        <dependency>
            <groupId>org.inurl.shardingsphere</groupId>
            <artifactId>sharding-jdbc-spring-boot-starter</artifactId>
            <version>4.1.0</version>
        </dependency>
```

2）配置yml

```yml
spring:
  application:
    name: reggie_takeout
  # TODO 配置ShardingSphere 实现MySQL主从复制
  shardingsphere:
    datasource:
      names: master,slave
      # 主数据源
      master:
        type: com.alibaba.druid.pool.DruidDataSource
        driver-class-name: com.mysql.cj.jdbc.Driver
        url: jdbc:mysql://192.168.199.181:3306/reggie?serverTimezone=Asia/Shanghai&useUnicode=true&characterEncoding=utf-8&zeroDateTimeBehavior=convertToNull&useSSL=false&allowPublicKeyRetrieval=true
        username: root
        password: root
      # 从数据源
      slave:
        type: com.alibaba.druid.pool.DruidDataSource
        driver-class-name: com.mysql.cj.jdbc.Driver
        url: jdbc:mysql://192.168.199.180:3306/reggie?serverTimezone=Asia/Shanghai&useUnicode=true&characterEncoding=utf-8&zeroDateTimeBehavior=convertToNull&useSSL=false&allowPublicKeyRetrieval=true
        username: root
        password: root
    masterslave:
      # 读写分离配置
      load-balance-algorithm-type: round_robin #轮询
      # 最终的数据源名称
      name: dataSource
      # 主库数据源名称
      master-data-source-name: master
      # 从库数据源名称列表，多个逗号分隔
      slave-data-source-names: slave
    props:
      sql:
        show: true #开启SQL显示，默认false
  main:
    allow-bean-definition-overriding: true #允许bean覆盖 druid数据源和sharding都会床架datasource数据 为了避免报错 允许后一个覆盖前一个
```

3）启动

![image-20230108100222147](/images/image-20230108100222147.png)

![image-20230108100552837](/images/image-20230108100552837.png)

![image-20230108100608705](/images/image-20230108100608705.png)


