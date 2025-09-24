# SQL

### 数据库分类

关系型数据库

- MySQL

非关系型数据库

- mongoDB
- Redis

应用 <--> 数据库软件 --> 数据库

- 应用和关系型数据库软件间，使用 SQL 进行操作
  > 非关系型数据库使用专有语言进行操作

### table 和 key

数据库中存在表(table)，表中存在键(key)和数据(data)

键(key)

- 主键(primary key)：每一条数据的唯一标识，可以通过复合主键达到同样的效果
- 外键(foreign key)：对应其它表的主键，相互关联

### 建库语句

> 使用``将库名和关键字进行区分

- CREATE DATABASE 表名
- DROP DATABASE 表名
- USE 表名

### 建表语句

- CREATE TABLE 表名( 'student\*id' INT PRIMARY KEY AUTO_INCREMENT )
  > 创建名为 student 的表，并包含 student_id 的自增主键，数据类型为 int
- ALTER TABLE 表名 ADD 'name' VARCHAR(20)
- ALTER TABLE 表名 DROP COLUMN 'name'
- DROP TABLE 表名
- DESCRIBE 表名

SQL 中的数据类型限制

- INT 整数
- DECIMAL(m, n) 浮点数，宽度为 m，小数位数为 n
- VARCHAR(n) 长度为 n 的字符串
- BLOB 图片、影像、档案等
- DATE 日期
- TIMESTAMP 时间戳

SQL 对于 key 的限制

- NOT NULL
- AUTO_INCREMENT

**外键**

设置外键

- FOREIGN KEY ( manager_id ) REFERENCES employee ( emp_id ) ON DELETE SET NULL
- FOREIGN KEY ( client_id ) REFERENCES client ( client_id ) ON DELETE CASCADE

修改表

- ALTER TABLE employee ADD FOREIGN KEY ( branch_id ) REFERENCES branch ( branch_id ) ON DELETE SET NULL;

ON DELETE SET NULL

- 当对应表数据被删除时，表中数据设置为 null

ON DELETE CASCADE

- 当对应表数据被删除时，表中数据同步删除

### 写入、修改、删除数据语句

- INSERT INTO 表名('name') VALUES(''小米'')
- UPDATE 表名 SET 'name' = '小明' WHERE 'name' = '小米' OR 'name' = '小黄'
- DELETE FROM 表名 WHERE 'name' IN('小米', '小黄')

### 数据查询语句 DQL

- SELETE \* FROM 表名

  > \*为全查，也可以使用'key', 'key'的形式，查取指定的 key

  - WHERE ’key‘ = ’xx‘
  - WHERE 'key' LIKE '%335'
    - % 多个字符
    - 单个字符
  - LIMIT 3
  - ORDER BY 'key' DESC
    > 默认升序 ASC
  - DISTINCT 去重
    - 聚合函数
    - COUNT(\_)
    - AVG(key)
    - SUM(\_)
    - MAX()
    - MIN()
  - 多表联查
    - union 连集：将两个表的查询结果拼接
    - join 连接
      ```sql
      SELECT *
      FROM `employee`JOIN`branch`
      ON`emp_id`=`manager_id`;
      ```
    - 左连接
      - 不管条件是否成立，返回所有左侧表格内容。不成立回传 null

- 高级查询
  - 根据一个查询的结果，进行新的查询
    ```sql
    SELECT `name`FROM`employee`WHERE`emp_id`IN (
    SELECT`emp_id`FROM`works_with`WHERE`total_sales` >= 50000
    )
    ```
