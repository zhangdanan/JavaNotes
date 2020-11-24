### 1.查询SQL尽量不要使用select *    而是select具体字段

```
正确
select id,name from user

错误
select * from user
```

原因：

- 只取需要的字段，节省资源、减少网络开销
- select*进行查询时，很可能就不会使用到覆盖索引了，就会造成回表查询。

### 2.如果知道查询结果只有一条或者只要最大/最小一条记录，建议用limit 1

```
正确
select id,name from user where name='zhang' limit 1

错误
select id,name from user where name='zhang' limit 1
```

原因：

- 加上limit 1后，只要找到了对应的一条记录，就不会继续向下扫描了，效率将会大大提高。
- 如果name是唯一索引的话，是不必要加上limit 1了，limit的存在主要就是为了防止全表扫描。

### 3.应尽量避免在where子句中使用or来连接条件

```
正确
select * from user where id=1  union all select * from user where name="zhang"

select * from user where id=1;
select * from user where name="zhang";


错误
select * from user where id=1 or name="zhang"

```

原因：

- 使用or可能会使索引失效，从而全表扫描。

### 4.优化limit分页

### 5.优化like语句

### 6.使用where条件限定要查询的数据，避免返回多余的行

### 7.尽量避免在索引列上使用mysql的内置函数

### 8.应尽量避免在where子句中对字段进行表达式操作，这将导致系统放弃使用索引而进行全表扫描

### 9.