# **SQLearn**
repository for learning SQL


什么是SQL？简单地说，**SQL就是访问和处理关系数据库的计算机标准语言**。也就是说，无论用什么编程语言（Java、Python、C++……）编写程序，只要涉及到操作关系数据库，比如，一个电商网站需要把用户和商品信息存入数据库，或者一个手机游戏需要把用户的道具、通关信息存入数据库，都**必须**通过`SQL`来完成。

NoSQL数据库作为SQL数据库的补充，两者不再是二选一的问题，而是主从关系。
# 关系数据库概述
## 为什么需要数据库？
因为应用程序需要保存用户的数据，比如Word需要把用户文档保存起来，以便下次继续编辑或者拷贝到另一台电脑。

但是，随着应用程序的功能越来越复杂，数据量越来越大，如何管理这些数据就成了大问题：
- 读写文件并解析出数据需要大量重复代码；
- 从成千上万的数据中快速查询出指定数据需要复杂的逻辑。

所以，数据库作为一种专门管理数据的软件就出现了，应用数据库之后，应用程序不再关心数据的存储，只需要把数据存储和读写的问题留给数据库程序。

## 数据模型
主流为关系模型，或者说矩阵模型。

数据又可以储存为不同的数据类型，也就是整形`(INT)`，长整型`(BIGINT)`，浮点型`(REAL/DOUBLE)`，定长字符串`(CHAR(N))`，变长字符串`(VARCHAR(R))`等等。

## SQL
什么是SQL？SQL是**结构化查询语言的缩写**（`Structured Query Language`），用来访问和操作数据库系统。SQL语句既可以查询数据库中的数据，也可以添加、更新和删除数据库中的数据，还可以对数据库进行管理和维护操作。不同的数据库，都支持SQL，这样，我们通过学习SQL这一种语言，就可以操作各种不同的数据库。

然而现实情况是，如果我们只使用标准SQL的核心功能，那么所有数据库通常都可以执行。不常用的SQL功能，不同的数据库支持的程度都不一样。而各个数据库支持的各自扩展的功能，通常我们把它们称之为“`方言`”。

总的来说，SQL语言定义了这么几种操作数据库的能力：
- DDL：Data Definition Language  
  DDL允许用户定义数据，也就是创建表、删除表、修改表结构这些操作。通常，DDL由数据库管理员执行。

- DML：Data Manipulation Language
  DML为用户提供添加、删除、更新数据的能力，这些是应用程序对数据库的日常操作。

- DQL：Data Query Language
  DQL允许用户查询数据，这也是通常最频繁的数据库日常操作。

## 语法特点
SQL语言关键字不区分大小写！！！但是，针对不同的数据库，对于表名和列名，有的数据库区分大小写，有的数据库不区分大小写。同一个数据库，有的在Linux上区分大小写，有的在Windows上不区分大小写。

# 安装MySQL

## MySQL 介绍
MySQL是目前应用最广泛的开源关系数据库。

和其他关系数据库有所不同的是，MySQL本身实际上只是一个SQL接口，它的内部还包含了多种数据引擎，常用的包括：
- InnoDB：由Innobase Oy公司开发的一款支持事务的数据库引擎，2006年被Oracle收购；
- MyISAM：MySQL早期集成的默认数据库引擎，不支持事务。
  
MySQL接口和数据库引擎的关系就好比某某浏览器和浏览器引擎。切换MySQL引擎不影响自己写的应用程序使用MySQL的接口。使用MySQL时，不同的表还可以使用不同的数据库引擎。如果你不知道应该采用哪种引擎，记住总是选择`InnoDB`就好了。

## MySQL 安装
* 前往[官方网站](https://dev.mysql.com/downloads/mysql/)下载安装
* 账号：njukl@foxmail.com
* root : Kl842518425X
* 在安装过程中，MySQL会自动创建一个root用户，并提示输入root口令。
* MySQL安装后会自动在后台运行。为了验证MySQL安装是否正确，我们需要通过mysql这个命令行程序来连接MySQL服务器。
  * 在命令提示符下输入`mysql -u root -p`，然后输入口令，
  * 如果一切正确，就会连接到MySQL服务器，同时提示符变为`mysql>`。
  * 输入`exit`退出MySQL命令行。
  * **注意**，MySQL服务器仍在后台运行。

# 关系模型

SQL采用关系模型，可以认为是多个关联的二维表格。

表的每一行称为记录（Record），记录是一个逻辑意义上的数据。

表的每一列称为字段（Column），同一个表的每一行记录都拥有相同的若干字段。

字段定义了数据类型（整型、浮点型、字符串、日期等），以及是否允许为`NULL`。

**注意**`NULL`表示字段数据不存在。一个整型字段如果为`NULL`不表示它的值为`0`，同样的，一个字符串型字段为`NULL`也不表示它的值为空串`''`。

关系数据库的表和表之间需要建立“`一对多`”，“`多对一`”和“`一对一`”的关系，这样才能够按照应用程序的逻辑来组织和存储数据。
- 一对多： 班级列表罗列班级，每一条班级ID对应多个学生ID
- 多对一： 学生列表中，每一个学生ID都指向一个班级，许多个同一个班级的学生对应于一个班级(ID)
- 一对一： 假如建立以工号为ID的班主任表以及以班级号为ID的班级表，则每一条班级表对应一个班主任ID

在关系数据库中，关系是通过`[主键]`和`[外键]`来维护的。

## 主键

数据关系列表中，我们需要一个永远不会重复的字段来标记每一条记录，从而可以通过这个字段来区分整条记录。我们称这个字段为`主键`。
- **对主键的关键要求**：记录一旦插入到表中，主键最好不要再修改；
- 选取主键的一个基本原则是：不使用任何业务相关的字段作为主键；
- 作为主键最好是完全业务无关的字段，我们一般把这个字段命名为`id`。常见的可作为`id`字段的类型有：
  - 自增整数类型：数据库会在插入数据时自动为每一条记录分配一个自增整数，这样我们就完全不用担心主键重复，也不用自己预先生成主键；
  - 全局唯一GUID类型：使用一种全局唯一的字符串作为主键，类似`8f55d96b-8acc-4636-8cb8-76bf8abc2f57`。GUID算法通过网卡MAC地址、时间戳和随机数保证任意计算机在任意时间生成的字符串都是不同的，大部分编程语言都内置了GUID算法，可以自己预算出主键。
- _对于大部分应用来说，通常自增类型的主键就能满足需求。_

## 联合主键
关系数据库实际上还允许通过多个字段唯一标识记录，即两个或更多的字段都设置为主键，这种主键被称为联合主键。

比如对于客户记录，可以记录`id-type`和对应`id-num`,则此两者共同构成一个`联合主键`来独立此条记录。

## 外键
### 1. 外键约束
通过外键，我们可以把不同的表关联起来。实现外键需要定义**外键约束**。

外键也具有一个ID，通过`外键约束`，我们可以知道，这个外键ID对应于数据库中：
- 哪一张表
- 的哪条信息
- `外键约束`是定义一种对应关系。
  
### 2. 外键举例
在`students`表中，通过`class_id`的字段，可以把数据与另一张表关联起来。
- classes sheet

  id |  name | others...
  ----|----|----
  1| 一班 | ...
  2| 二班 | ...
  3| 三班 | ...
- students sheet
  id | class_id | name | score| others...
  ----|----|----|----|---
  1|  1  | 小明 | 85|...
  2|  1  | 小红 | 98|...
  5|  2  | 小白 | 94|...

- 定义外键约束  
  
      ALTER TABLE students
      ADD CONSTRAINT fk_class_id
      FOREIGN KEY (class_id)
      REFERENCES classes (id);
- 其中，外键约束的名称`fk_class_id`可以任意，`FOREIGN KEY (class_id)`指定了`class_id`作为外键，`REFERENCES classes (id)`指定了这个外键将关联到`classes`表的`id`列（即`classes`表的主键）。
- 通过定义外键约束，关系数据库可以保证无法插入无效的数据。即如果`classes`表不存在`id=99`的记录，`students`表就无法插入`class_id=99`的记录。

### 3. 删除外键约束
- 要删除一个外键约束，也是通过ALTER TABLE实现的：

      ALTER TABLE students
      DROP FOREIGN KEY fk_class_id;
- **注意**：删除外键约束并没有删除外键这一列。删除列是通过`DROP COLUMN ...`实现的。

### 4. 多对多
要实现多对多，通常需要定义一个`中间表`来关联两个一对多关系。比如说，记录应聘者和应聘岗位的关系。一个岗位对应多个应聘者，每个应聘者也对应多个岗位。这样，应聘者id和岗位id的数对关系，就可以构成一个中间表。
- 中间表 应聘者 & 岗位
  id  |  candidat_id  |  job_id
  ---|---|---
  1|1|1
  2|1|2
  3|2|1
  4|2|2
  5|3|1
  6|4|2
  ...|...|...
- 由这个中间表实现的多对多关系告诉我们，`candidats`表中ID为1的`应聘者1`同时申请了`jogs`表中ID分别为1和2的`岗位1`和`岗位2`
- 同时，也告诉我们`jogs`表中ID为1的`岗位1`有`candidats`表中ID为1，2和3的`应聘者1`，`应聘者2`和`应聘者3`的应聘者。

### 5. 一对一
一对一关系是指，一个表的记录对应到另一个表的唯一一个记录。
  
如果业务允许，完全可以把两个表合为一个表。

还有一些应用会把一个大表拆成两个一对一的表，目的是把经常读取和不经常读取的字段分开，以获得更高的性能。例如，把一个大的用户表分拆为用户基本信息表`user_info`和用户详细信息表`user_profiles`，大部分时候，只需要查询`user_info`表，并不需要查询`user_profiles`表，这样就提高了查询速度。

## 索引（INDEX)

索引是关系数据库中对某一列或多个列的值进行预排序的数据结构，用来获得查找记录时更快的速度。

索引的效率取决于索引列的值的`散列程度`，举例如果对学生列表的性别列进行索引就没有什么意义

索引的**优点**是提高了查询效率，**缺点**是在插入、更新和删除记录时，需要同时修改索引，因此，索引越多，插入、更新和删除记录的速度就越慢。

对于主键，关系数据库会自动对其创建主键索引。使用主键索引的效率是最高的，因为主键会保证绝对唯一。
### 1. 索引举例

假设在[students表](###\ 2.\ 外键举例)中经常根据`score`列进行查询，就可以对`score`列创建索引:  

    ALTER TABLE students
    ADD INDEX idx_score (score);
使用`ADD INDEX idx_score (score)`就创建了一个名称为`idx_score`，使用列`score`的索引。索引名称是任意的，索引如果有多列，可以在括号里依次写上，例如：

    ALTER TABLE students
    ADD INDEX idx_name_score (name, score);


### 2. 唯一索引
---
在设计关系数据表的时候，看上去唯一的列，例如身份证号、邮箱地址等，因为他们具有业务含义，因此不宜作为主键。

但是，这些列根据业务要求，又具有唯一性约束：即不能出现两条记录存储了同一个身份证号。这个时候，就可以给该列添加一个唯一索引。例如，我们假设`students`表的`name`不能重复：

    ALTER TABLE students
    ADD UNIQUE INDEX uni_name (name);

通过`UNIQUE`关键字我们就添加了一个唯一索引。 

-------------

也可以只对某一列添加一个唯一约束而不创建唯一索引：

    ALTER TABLE students
    ADD CONSTRAINT uni_name UNIQUE (name);
这种情况下，name列没有索引，但仍然具有唯一性保证。


# 查询数据
创建database: [.sql script](https://raw.githubusercontent.com/michaelliao/learn-sql/master/mysql/init-test-data.sql)
----
    -- 如果test数据库不存在，就创建test数据库：
    CREATE DATABASE IF NOT EXISTS test;

    -- 切换到test数据库
    USE test;

    -- 删除classes表和students表（如果存在）：
    DROP TABLE IF EXISTS classes;
    DROP TABLE IF EXISTS students;

    -- 创建classes表：
    CREATE TABLE classes (
        id BIGINT NOT NULL AUTO_INCREMENT,
        name VARCHAR(100) NOT NULL,
        PRIMARY KEY (id)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

    -- 创建students表：
    CREATE TABLE students (
        id BIGINT NOT NULL AUTO_INCREMENT,
        class_id BIGINT NOT NULL,
        name VARCHAR(100) NOT NULL,
        gender VARCHAR(1) NOT NULL,
        score INT NOT NULL,
        PRIMARY KEY (id)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

    -- 插入classes记录：
    INSERT INTO classes(id, name) VALUES (1, '一班');
    INSERT INTO classes(id, name) VALUES (2, '二班');
    INSERT INTO classes(id, name) VALUES (3, '三班');
    INSERT INTO classes(id, name) VALUES (4, '四班');

    -- 插入students记录：
    INSERT INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'M', 90);
    INSERT INTO students (id, class_id, name, gender, score) VALUES (2, 1, '小红', 'F', 95);
    INSERT INTO students (id, class_id, name, gender, score) VALUES (3, 1, '小军', 'M', 88);
    INSERT INTO students (id, class_id, name, gender, score) VALUES (4, 1, '小米', 'F', 73);
    INSERT INTO students (id, class_id, name, gender, score) VALUES (5, 2, '小白', 'F', 81);
    INSERT INTO students (id, class_id, name, gender, score) VALUES (6, 2, '小兵', 'M', 55);
    INSERT INTO students (id, class_id, name, gender, score) VALUES (7, 2, '小林', 'M', 85);
    INSERT INTO students (id, class_id, name, gender, score) VALUES (8, 3, '小新', 'F', 91);
    INSERT INTO students (id, class_id, name, gender, score) VALUES (9, 3, '小王', 'M', 89);
    INSERT INTO students (id, class_id, name, gender, score) VALUES (10, 3, '小丽', 'F', 85);

    -- OK:
    SELECT 'ok' as 'result:';
## 基本查询
- 使用SELECT查询的基本语句SELECT * FROM <表名>可以查询一个表的所有行和所有列的数据。

- SELECT查询的结果是一个二维表。
- e.g.  
  
      SELECT * FROM classes;

- OR
  
      SELECT 100+200;
  works also.

## 条件查询
SELECT语句可以通过`WHERE`条件来设定查询条件，查询结果是满足查询条件的记录。例如，要指定条件“分数在80分或以上的学生”，写成`WHERE`条件就是`SELECT * FROM students WHERE score >= 80`。

    SELECT * FROM <表名> WHERE <条件表达式>

We can also use `AND`, `OR` and `NOT`

如果不加括号，条件运算按照`NOT`、`AND`、`OR`的优先级进行，即`NOT`优先级最高，其次是`AND`，最后是`OR`。加上括号可以改变优先级。

一些特别的常用表达式：

条件|	表达式举例1|	表达式举例2|	说明
---|---|---|---
使用=判断相等|	score = 80|	name = 'abc'|	字符串需要用单引号括起来
使用>判断大于|	score > 80|	name > 'abc'|	字符串比较根据ASCII码，中文字符比较根据数据库设置
使用>=判断大于或相等|	score >= 80|	name >= 'abc'	
使用<判断小于|	score < 80|	name <= 'abc'	
使用<=判断小于或相等|	score <= 80|	name <= 'abc'	
使用<>判断不相等|	score <> 80|	name <> 'abc'	
使用LIKE判断相似|	name LIKE 'ab%'|	name LIKE '%bc%'|	%表示任意字符，例如'ab%'将匹配'ab'，'abc'，'abcd'

查询分数在60分(含)～90分(含)之间的学生可以使用的WHERE语句是：  
- [ ] WHERE score>=60 OR score<=90
- [X] WHERE score>=60 AND score<=90
- [ ] WHERE score IN (60,90)
- [X] WHERE score BETWEEN 60 AND 90
- [ ] WHERE 60<=score<=90

## 投影查询

只选取标的某几行或某几列：

    SELECT id, score, name FROM students;
输出

    +----+-------+------+
    | id | score | name |
    +----+-------+------+
    |  1 |    90 | 小明 |
    |  2 |    95 | 小红 |
    |  3 |    88 | 小军 |
    |  4 |    73 | 小米 |
    |  5 |    81 | 小白 |
    |  6 |    55 | 小兵 |
    |  7 |    85 | 小林 |
    |  8 |    91 | 小新 |
    |  9 |    89 | 小王 |
    | 10 |    85 | 小丽 |
    +----+-------+------+

使用SELECT 列1, 列2, 列3 FROM ...时，还可以给每一列起个别名，这样，结果集的列名就可以与原表的列名不同。
通过 `SELECT 列1 别名1, 列2 别名2, 列3 别名3 FROM ...`来加别名。
EX  

    SELECT id, score point, name FROM students;
输出（使用score的别名point作为输出）

    +----+-------+------+
    | id | point | name |
    +----+-------+------+
    |  1 |    90 | 小明 |
    |  2 |    95 | 小红 |
    |  3 |    88 | 小军 |
    |  4 |    73 | 小米 |
    |  5 |    81 | 小白 |
    |  6 |    55 | 小兵 |
    |  7 |    85 | 小林 |
    |  8 |    91 | 小新 |
    |  9 |    89 | 小王 |
    | 10 |    85 | 小丽 |
    +----+-------+------+

可以同时并列[条件查询](#条件查询)：

    SELECT id, score points, name FROM students WHERE gender = 'M';

## 排序
我们使用SELECT查询时，细心的读者可能注意到，查询结果集通常是按照`id`排序的，也就是根据主键排序。这也是大部分数据库的做法。如果我们要根据其他条件排序怎么办？可以加上`ORDER BY`子句。例如按照成绩从低到高进行排序：

    SELECT id, name, gender, score FROM students ORDER BY score;

默认为升序（`ASC`）排列，如果需要倒序，则在末尾加上`DESC`:  

    SELECT id, name, gender, score FROM students ORDER BY score DESC;

添加多个排序标准，先对排在前面的参数排序，并列时按后续的参数排序：

    SELECT id, name, gender, score FROM students ORDER BY score DESC, gender;

*如果有`WHERE`子句，那么`ORDER BY`子句要放到`WHERE`子句后面。例如，查询一班的学生成绩，并按照倒序排序：*

    SELECT id, name, gender, score
    FROM students
    WHERE class_id = 1
    ORDER BY score DESC;

## 分页查询
使用`SELECT`查询时，如果结果集数据量很大，比如几万行数据，放在一个页面显示的话数据量太大，不如分页显示，每次显示100条。

要实现分页功能，实际上就是从结果集中显示第1~100条记录作为第1页，显示第101~200条记录作为第2页，以此类推。

因此，分页实际上就是从结果集中“截取”出第M~N条记录。这个查询可以通过`LIMIT <M> OFFSET <N>`子句实现。

- 现在，我们把结果集分页，每页3条记录。要获取第1页的记录，可以使用LIMIT 3 OFFSET 0：

      SELECT id, name, gender, score
      FROM students
      ORDER BY score DESC
      LIMIT 3 OFFSET 0;   
  显示从0开始的一页也就是前三个元素；`LIMIT`限制输出的最大数目，`OFFSET`设置开始指针。

### 注意
`OFFSET`是可选的，如果只写`LIMIT 15`，那么相当于`LIMIT 15 OFFSET 0`。

在`MySQL`中，`LIMIT 15 OFFSET 30`还可以简写成`LIMIT 30, 15`。

使用`LIMIT <M> OFFSET <N>`分页时，随着N越来越大，查询效率也会越来越低。


## 聚合查询

#### COUNT
快速得到一定条件下，信息的条数，我们可以使用`SQL`内置的`COUNT()`函数查询： 

    SELECT COUNT(*) FROM students;

也可以加上条件和别名，这里`boys`是要输出的别名，`WHERE gender = 'M'`给出条件限制。

    SELECT COUNT(*) boys FROM students WHERE gender = 'M'

输出

    +------+
    | boys |
    +------+
    |    5 |
    +------+

#### 除了COUNT()函数外，SQL还提供了如下聚合函数：

函数|	说明
---|---
SUM|	计算某一列的合计值，该列必须为数值类型
AVG|	计算某一列的平均值，该列必须为数值类型
MAX|	计算某一列的最大值
MIN|	计算某一列的最小值

注意，`MAX()`和`MIN()`函数并不限于数值类型。如果是字符类型，MAX()和MIN()会返回排序最后和排序最前的字符。

#### 分组聚合
- 可以通过`GROUP BY`实现分组聚合

      SELECT COUNT(*) num FROM students GROUP BY class_id;
  输出

      +-----+
      | num |
      +-----+
      |   4 |
      |   3 |
      |   3 |
      +-----+

- 所以我们可以把class_id列也放入结果集中，让结果更好看：

      SELECT COUNT(*) num FROM students GROUP BY class_id;

  输出

      +----------+-----+
      | class_id | num |
      +----------+-----+
      |        1 |   4 |
      |        2 |   3 |
      |        3 |   3 |
      +----------+-----+
  这样班级对应的人数就一目了然了。

- **注意**：
  
      SELECT name, class_id, COUNT(*) num FROM students GROUP BY class_id;

  会报错！
  
  只有`class_id`都相同，`name`是不同的，`SQL`引擎不能把多个`name`的值放入一行记录中。因此，聚合查询的列中，只能放入分组的列。
  
#### 多列分组

也可以使用多个列进行分组。例如，我们想统计各班的男生和女生人数：

    SELECT class_id, gender, COUNT(*) num FROM students GROUP BY class_id, gender;

输出  

    +----------+--------+-----+
    | class_id | gender | num |
    +----------+--------+-----+
    |        1 | M      |   2 |
    |        1 | F      |   2 |
    |        2 | F      |   1 |
    |        2 | M      |   2 |
    |        3 | F      |   2 |
    |        3 | M      |   1 |
    +----------+--------+-----+

#### 练习
1. 请使用一条SELECT查询查出每个班级的平均分： 

        SELECT class_id, AVG(score) FROM students GROUP BY class_id;
2. 请使用一条SELECT查询查出男生和女生的平均分：
   
        SELECT gender, AVG(score) average FROM students GROUP BY gender;
3. 请使用一条SELECT查询查出每个班级男生和女生的平均分：

        SELECT class_id, gender, AVG(score) 
        FROM students 
        GROUP BY class_id, gender;


## 多表查询
SELECT查询不但可以从一张表查询数据，还可以从多张表同时查询数据。查询多张表的语法是：`SELECT * FROM <表1> <表2>`。

例如，同时从`students`表和`classes`表的“`乘积`”，即查询数据，可以这么写：

    SELECT * FROM students, classes;

也可以按需索取，定制别名：

    SELECT
        students.id sid,
        students.name,
        students.gender,
        students.score,
        classes.id cid,
        classes.name cname
    FROM students, classes;
注意，多表查询时，要使用`表名.列名`这样的方式来引用列和设置别名，这样就避免了结果集的列名重复问题。但是，用`表名.列名`这种方式列举两个表的所有列实在是很麻烦，所以SQL还允许给表设置一个别名，让我们在投影查询中引用起来稍微简洁一点：

    SELECT
        s.id sid,
        s.name,
        s.gender,
        s.score,
        c.id cid,
        c.name cname
    FROM students s, classes c;
    WHERE s.class_id = c.id;

也可以加上条件，例如：`WHERE s.class_id = c.id` 确保我们只取出乘积表中，班级对应正确的条目。

## 链接查询

要实现上面代码的结果，还可以使用链接查询：

    SELECT s.id, s.name, s.class_id, c.name class_name, s.gender, s.score
    FROM students s
    INNER JOIN classes c
    ON s.class_id = c.id;
需要使用到`INNER JOIN`的语句

**注意INNER JOIN查询的写法是：**

1. 先确定主表，仍然使用`FROM <表1>`的语法；
2. 再确定需要连接的表，使用`INNER JOIN <表2>`的语法；
3. 0然后0确定连接条件，使用`ON <条件...>`，这里的条件是`s.class_id = c.id`，表示`students`表的`class_id`列与`classes`表的`id`列相同的行需要连接；
1. 可选：加上WHERE子句、ORDER BY等子句。

#### 其他链接查询的方式

那什么是内连接（`INNER JOIN`）呢？先别着急，有内连接（`INNER JOIN`）就有外连接（`OUTER JOIN`）。我们把内连接查询改成外连接查询，看看效果：

    SELECT s.id, s.name, s.class_id, c.name class_name, s.gender, s.score
    FROM students s
    RIGHT OUTER JOIN classes c
    ON s.class_id = c.id;

执行上述`RIGHT OUTER JOIN`可以看到，和`INNER JOIN`相比，`RIGHT OUTER JOIN`多了一行，多出来的一行是“四班”，但是，学生相关的列如`name`、`gender`、`score`都为`NULL`。

> *这也容易理解，因为根据`ON`条件`s.class_id = c.id`，`classes`表的`id=4`的行正是“四班”，但是，`students`表中并不存在`class_id=4`的行。*

有`RIGHT OUTER JOIN`，就有`LEFT OUTER JOIN`，以及`FULL OUTER JOIN`。它们的区别是：
- `INNER JOIN`只返回同时存在于两张表的行数据，由于`students`表的`class_id`包含1，2，3，`classes`表的`id`包含1，2，3，4，所以，`INNER JOIN`根据条件`s.class_id = c.id`返回的结果集仅包含1，2，3。
  
- `RIGHT OUTER JOIN`返回右表都存在的行。如果某一行仅在右表存在，那么结果集就会以`NULL`填充剩下的字段。
- `LEFT OUTER JOIN`则返回左表都存在的行。如果我们给`students`表增加一行，并添加`class_id=5`，由于`classes`表并不存在`id=5`的行，所以，LEFT OUTER JOIN的结果会增加一行，对应的`class_name`是`NULL`

- `FULL OUTER JOIN`，它会把两张表的所有记录全部选择出来，并且，自动把对方不存在的列填充为`NULL`