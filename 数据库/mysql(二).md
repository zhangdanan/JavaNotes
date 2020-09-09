# 基本数据类型

主要分为数值型，浮点型，日期/时间吗，字符串（字符）型和二进制型。

unsigned：无符号的，只能是正数。signed：有符号数，可能是正数也可能是负数，浮点数默认是有符号数。

### 1.数值型

![img](https://pic2.zhimg.com/80/v2-69f428d2c084b9ff48108ad5fda13e55_hd.jpg)

### 2.浮点型

![img](https://pic1.zhimg.com/80/v2-1a4941e2acc0f8dd4b0f5324085d23e0_hd.png)

### 3.日期/时间

  **timestamp**：时间戳类型，就是指一个时间的数据值，本质是一个数字，一个重要作用就是能够自动获得时间戳的数据值。   

![img](https://pic2.zhimg.com/80/v2-31ef3b71be0a60d79358b5afb10dbef9_hd.jpg)

### 4.字符型

**varchar** ：变长字符串 使用时必须设定长度，最大值理论值65535个

**char** ：定长字符串，使用时需要设定长度，不设定默认为1，最大理论值255个，适用于存储的数据都是可预见的明确的固定长度的字符，如手机号，身份证号码

![img](https://pic2.zhimg.com/80/v2-f741e55e0e0ae6c04c7db0b4514b9b89_hd.jpg)

### 5.二进制类型

**blob类型**：小图片用**blob**类型，最大长度64K，

**mediumblob类型**：大图片使用**mediumblob**，最大是16M

**longblob类型**：最大长度是4G

![img](https://pic3.zhimg.com/80/v2-47856a610d759ad97ac3a7e7ec44bbee_hd.jpg)

### 6.特殊类型

  **enum** （枚举类型）单选项字符串数据类型：只能插入指定的数据格式，否则会报错。

```
mysql-> create table user3(id int primary key auto_increment,
     -> name varchar(10),
     -> sex enum('boy','girl')
     -> );

mysql> insert into user3(name,sex)
    -> values
    -> ("zhang","boy"),
    -> ("wang","girl");

mysql> select * from user3;
+----+-------+------+
| id | name  | sex  |
+----+-------+------+
|  1 | zhang | boy  |
|  2 | wang  | girl |
+----+-------+------+
```

**set** （集合类型）多选字符串的数据类型：适用于存储表单界面的多选项值   

```\
mysql> create table user4(
    -> id int primary key auto_increment,
    -> name varchar(10),
    -> hobby set('zhang','wang','li','yang')
    -> );
    
mysql> insert into user4(hobby)
    -> values
    -> ("zhang,wang");
    
mysql> select hobby as 爱好 from user4;
    
+------------+
| 爱好       |
+------------+
| zhang,wang |
+------------+
```



# 数据库储存引擎

#### 查看引擎命令

```mysql
show engines; //查看系统所支持的引擎类型:

show variables like '%storage_engine'; //查看mysql引擎

show create table tablename; //可以查看某个表所使用的引擎
```

#### InnoDB引擎

InnoDB 是事务型数据库的首选引擎，**支持事务安全表 (ACID ) ，支持行锁定和外键。**

InnoDB 作为**默认存储引擎**，特性有:

- InnoDB 给 MySQL 提供了**具有提交、回滚和崩溃恢复能力的事务安全 (ACID 兼容)存储引擎**。InnoDB 锁定在**行级**并且也在 SELECT 语句中提供一个类似 Oracle 的**非锁定读**。这些功能增加了多用户部署和性能。在 SQL 查询中，可以自由地将 **InnoDB 类型的表与其他MySQL 的表的类型混合起来**，甚至在同一个查询中也可以混合。
- InnoDB 是**为处理巨大数据量的最大性能设计**。它的 CPU 效率可能是任何其他基于磁盘的关系数据库引擎所不能匹敌的。
- InnoDB 存储引擎完全与 MySQL 服务器整合，I**nnoDB 存储引擎为在主内存中缓存数据和索引而维持它自己的缓冲池**。InnoDB **将它的表和索引存在一个逻辑表空间中，表空间可以包含数个文件〈或原始磁盘分区) 。**这与 MyISAM 表不同，比如在 `MyISAM` 表中每个表被存在分离的文件中。InnoDB 表可以是任何尺寸,，即使在文件尺寸被限制为 2GB 的操作系统上。
- InnoDB **支持外键完整性约束 (FOREIGN KEY)** 。存储表中的数据时, 每张表的存储都按主键顺序存放, 如果没有显示在表定义时指定主键，InnoDB 会为每一行生成一个 6B 的ROWID，并以此作为主键。
- InnoDB 被用在众多需要高性能的大型数据库站点上。
- InnoDB 不创建目录，使用 InnoDB 时，MySQL 将在 MySQL 数据目录下创建一个名为`ibdata1` 的 10MB 大小的自动扩展数据文件，以及两个名为` ib_logfile0` 和` ib_logfilel `的 `5MB`大小的日志文件。

#### MyISAM引擎

MyISAM 基于 ISAM 的存储引擎，并对其进行扩展。它是在 **Web、数据存储**和其他应用
环境下最常使用的存储引擎之一。MyISAM 拥有较高的插入、查询速度，**但不支持事务**。在
MyISAM 主要特性有:

- **大文件** (达 63 位文件长度) 在支持大文件的文件系统和操作系统上被支持。
- 当把删除、更新及插入操作混合使用的时候，动态尺寸的行产生更少碎片。这要通过合并相邻被删除的块，以及若下一个块被删除，就扩展到下一块来自动完成。
- 每个 MyISAM 表最大索引数是 64，这可以通过重新编译来改变。每个索引最大的列数是 16 个。
- 最大的键长度是 1000B，这也可以通过编译来改变。对于键长度超过 250B 的情况，一个超过 1024B 的键将被用上。
- **BLOB 和TEXT 列可以被索引**。
- **NULL 值被允许在索引的列中。这个值占每个键的 0~1 个字节**。
- 所有数字键值以高字节优先被存储以允许一个更高的索引压缩。
- 每表一个`AUTO_INCREMENT` 列的内部处理。MyISAM 为 `INSERT` 和 `UPDATE` 操作自动更新这一列。这使得 `AUTO_INCREMENT `列更快〈至少 10%) 。在序列顶的值被删除之后就不能再利用。
- 可以把**数据文件和索引文件**放在不同目录。
- 每个字符列可以有不同的字符集。
- 有VARCHAR 的表可以固定或动态记录长度。
- VARCHAR 和CHAR 列可以多达 64KB。

> 使用 MyISAM 引擎创建数据库，将生产 3 个文件。文件的名字以**表的名字**开始，扩展名指出文件类型， `frm`文件存储表定义，数据文件的扩展名为`.MYD (MYData)`，索引文件的扩展名是`.MYI MYIndex)` 。

#### MEMORY引擎

MEMORY 存储引擎**将表中的数据存储到内存中，为查询和引用其他表数据提供快速访问**。MEMORY 主要特性有:

- MEMORY 表的每个表可以有多达 32 个索引，每个索引 16 列，以及 500B 的最大键长度。     
- MEMORY 存储引擎执行 **HASH 和 BTREE** 索引。
- 可以在一个MEMORY 表中有非唯一键。
- MEMORY 表使用一个固定的记录长度格式。
- MEMORY 不支持BLOB 或TEXT 列。
- MEMORY 支持 `AUTO_INCREMENT` 列和**对可包含NULL 值的列的索引**。
- MEMORY 表在所有客户端之间共享 (就像其他任何非 TEMPORARY 表) 。
- **MEMORY 表内容被存在内存中，内存是 MEMORY 表和服务器在查询处理时的空闲中创建的内部表共享**。
- 当不再需要 MEMORY 表的内容时，**要释放被 MEMORY 表使用的内存**，应该执行`DELETE FROM` 或TRUNCATE TABLE，或者删除整个表 〈使用DROP TABLE) 。

#### 存储引擎的选择

不同存储引擎都有各自的特点，以适应不同的需求。下面是各种引擎的不同的功能: 

- 如果要提供提交、回滚和崩溃恢复能力的**事务安全** (ACID 兼容) 能力，并要求实现**并发控制**，InnoDB 是个很好的选择；
- 如果数据表主要用来**插入和查询记录**，则 MyISAM 引擎能提供较**高的处理效率**；
- 如果只是**临时存放数据**，数据量不大，并且**不需要较高的数据安全性**，可以选择将**数据保存在内存中**的 Memory 引擎，MySQL 中使用该引擎作为临时表，存放查询的中间结果；
- 如果只有 **INSERT 和 SELECT 操作**，可以选择 Archive 引擎，Archive 存储引擎支持高并发的插入操作，但是本身**并不是事务安全**的。Archive 存储引擎非常适合**存储归档数据**，如记录日志信息可以使用 Archive 引擎。

使用哪一种引擎要根据需要灵活选择, 一个数据库中多个表可以使用不同引擎以满足各种性能和实际需求。使用合适的存储引擎，将会提高整个数据库的性能。

# 常用的mysql命令

`mysql -u root -p`  进入root账户中

`show databases`显示所有的数据库

`use databasename`使用某个数据库

`show tables`看本数据库中有多少张表



`describe tablename`查看表结构  ==```desc tablename```

`show create table tablename`查看建表语句

`select * from tablename`查看表数据

# mysql之like模糊查询

**%：表示任意个字符，可以是0个或多个，可匹配任意类型和长度的字符。**

**_：表示单个字符，常用来限制表达式的字符长度。**

1.**like '%国%'** 查询所有含国字的记录  

```
select * from student where name like '%国%';
```

2.**like '%国%' and like '%飞%'**查询既有国字又有飞字的记录,国字和飞字不分先后

```
select * from student where name like '%国%'and name like '%飞%';
```

3.**like '%国%飞%'**查询既有国字又有飞字的记录，国字必须在前，飞字必须在后。

```
select * from student where name like '%国%飞%';
```

4.**like '张__'**查询姓张的记录，张后面有两横杠，所以必须是三个字的

```
select * from student where name like '张__';
```

5..**like '%张__%'**查询姓张的记录，可以是两个字的也可以是三个字的

```
select * from student where name like '%张__%';
```

# 数据操作

### 更新数据

```
update tablename set field1=new-values1，field2=new-values2
[where cause]
```

### 插入数据

```
insert into tablename(column1,column2) 
values
("values1","values2");//指定列插入一条数据

insert into tablename
values
("values1","values2");//全部列插入一条数据

insert into tablename(column1,column2) 
values
("values1","values2"),
("values1","values2"),
......;//插入多条数据
```

### 删除数据

```
delete from tablename;//删除某个表的全部数据

delete from tablename where cause;//删除指定条件的数据
```

### 更新数据

```
update tablename set field1=new-values1，field2=new-values2
[where cause]
```

### 查询数据





# limit的使用

```
select * from tablename limit m,n;//m表示从第几天开始记录数据，n代表记录多少条数据

select * from tablename limit 0,5;//表示从第一条开始记录数据，取出第一到第五的数据

select * from tablename limit 5,5;//表示取出第六条到第十条的数据，取出五条数据


select * from tablename limit m,n;//表示跳过m条数据，然后记录n条数据
select * from tablename limit m offset n;//表示跳过n条记录，然后记录m条数据
```

# MySQL中查询sql语句的运行时间

查看执行时间步骤：

1.show profiles；

![img](https://pic3.zhimg.com/80/v2-ee3a18b44f4e3112bda21dc773ab1e89_hd.png)

2.show variables;查看 profiling是否是on状态；

![img](https://pic3.zhimg.com/80/v2-6697898dfae233109e8d534efa6cba6f_hd.png)

3.如果是off，执行命令 set profiling=1；

![img](https://pic3.zhimg.com/80/v2-d26f91041c15a3a6ec9239f126049d6d_hd.png)

4.执行sql语句

![img](https://pic2.zhimg.com/80/v2-3650f039fb99145b00ae6f27860e5b97_hd.png)

5.show profiles；然后就可以看到sql语句的执行时间了

![img](https://pic3.zhimg.com/80/v2-950606152bfea79eee46eafd280a138f_hd.png)

# binary关键字

binary：mysql的where子句的字符串比较是不区分大小学的，可以使用binary关键字来设定where子句的字符串比较是区分大小写的

```
//区分大小写，zhang和ZHANG是不一样的
select * from student where binary name="zhang";

//不区分大小写，zhang和ZHANG是一样的
select * from student where name="zhang"; 
```



# Mysql一些语句

### 1.把时间更新成为当前系统时间

```update tablename SET Date=Now() where 条件；```

# Mysql优化

