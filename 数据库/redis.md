# 2019-8-21-redis概述（一）

### Redis

REmote DIctionary Server(Redis) 是一个由Salvatore Sanfilippo写的key-value存储系统。

Redis是一个开源的使用ANSI C语言编写、遵守BSD协议、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。

它通常被称为数据结构服务器，因为值（value）可以是 字符串(String), 哈希(Hash), 列表(list), 集合(sets) 和 有序集合(sorted sets)等类型。

### Redis简介

Redis 是完全开源免费的，遵守BSD协议，是一个高性能的key-value数据库。

Redis 与其他 key - value 缓存产品有以下三个特点：

- Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
- Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
- Redis支持数据的备份，即master-slave模式的数据备份。

### Redis优势

- 性能极高 – Redis能读的速度是110000次/s,写的速度是81000次/s 。
- 丰富的数据类型 – Redis支持二进制案例的 Strings, Lists, Hashes, Sets 及 Ordered Sets 数据类型操作。
- 原子 – Redis的所有操作都是原子性的，意思就是要么成功执行要么失败完全不执行。单个操作是原子性的。多个操作也支持事务，即原子性，通过MULTI和EXEC指令包起来。
- 丰富的特性 – Redis还支持 publish/subscribe, 通知, key 过期等等特性。

### Redis与其他key-value存储有什么不同

- Redis有着更为复杂的数据结构并且提供对他们的原子性操作，这是一个不同于其他数据库的进化路径。Redis的数据类型都是基于基本数据结构的同时对程序员透明，无需进行额外的抽象。
- Redis运行在内存中但是可以持久化到磁盘，所以在对不同数据集进行高速读写时需要权衡内存，因为数据量不能大于硬件内存。在内存数据库方面的另一个优点是，相比在磁盘上相同的复杂的数据结构，在内存中操作起来非常简单，这样Redis可以做很多内部复杂性很强的事情。同时，在磁盘格式方面他们是紧凑的以追加的方式产生的，因为他们并不需要进行随机访问。



# 2019-8-21-redis的安装（二）

### 一、下载 Redis

下载地址： [https://github.com/MicrosoftA...](https://github.com/MicrosoftArchive/redis/releases)

Redis 官方没有 Windows 版，但是微软的开发人员移植了一个。页面中会有两种下载格式：.msi 安装包和 .zip 压缩包。本文仅介绍前者，因为用起来比较方便。

### 二、安装 Redis

如果你下载的是 .msi 结尾的安装包，那么双击一路 Next 就安装完成了。

![clipboard.png](https://segmentfault.com/img/bVWW7K?w=495&h=387)

### 三、运行 Redis

安装完之后你就会发现有一个名为 Redis 的服务已经在运行了。

![clipboard.png](https://segmentfault.com/img/bVWW8W?w=666&h=238)

你可以在服务控制界面中启动和停止它。

### 四、客户端

Redis 提供一个命令行客户端，就在安装目录下。但是为了方便使用，我们还是要先把它加入到 PATH 里面。方法是：

1. 按 Win+R 打开运行对话框，键入 cmd 命令打开命令行窗口。
2. 键入下面的命令： `setx PATH "%PATH%;C:\Program Files\Redis"`，其中分号后面的路径就是刚才 Redis 的安装目录。
3. 如果得到提示 `成功: 指定的值已得到保存。`，那么表示 PATH 设置成功，关闭命令行窗口。
4. 重新打开另一个命令行窗口（因为环境变量的修改只会在新的命令行窗口生效），键入命令 `redis-cli` 即可运行 Redis 客户端了：

![clipboard.png](https://segmentfault.com/img/bVWXcu?w=528&h=262)

### 五、修改配置

Redis 服务器的缺省端口是 6379，而且只能本机访问。如果你想换一个端口，或者开放局域网访问，那么就需要修改配置文件。配置文件就在 Redis 安装目录下：

1. 打开 Redis 安装目录下的 `redis.windows-service.conf` 文件。
2. 如果你想开放局域网访问，那么找到 `bind 127.0.0.1`，改为 `bind 0.0.0.0`。
3. 如果你想修改端口，例如改为 10000，那么找到 `port 6379`，改为 `port 10000`。
4. 修改完毕后，保存文件。
5. 重新启动服务：

![clipboard.png](https://segmentfault.com/img/bVWXd3?w=666&h=293)

如果你改了端口号，那么运行客户端的时候就要指定新的端口号，方法是使用 `-p` 参数（假设新端口号为 10000）：

```
redis-cli -p 10000
```





# 2019-8-22-redis的数据类型（三）

### Redis数据类型

Redis支持五种数据类型：String 、hash、list、set、zset（sorted set：有序集合 ）

### String字符串

String类型是Redis最基本的数据类型，一个键最大可以存储512MB

```
127.0.0.1:6379> set name zhang
OK
127.0.0.1:6379> get name
"zhang"
127.0.0.1:6379>
```

### Hash哈希

Redis hash是一个键值对集合

Redis hash是一个string类型的field和value的映射表，hash特别适合用于存储对象

```
127.0.0.1:6379> hmset zhang:1 usernamae wang password zhang
OK
127.0.0.1:6379> hgetall zhang:1
1) "usernamae"
2) "wang"
3) "password"
4) "zhang"
127.0.0.1:6379> hmset zhang:2 username zhang password wang
OK
127.0.0.1:6379> hgetall zhang:2
1) "username"
2) "zhang"
3) "password"
4) "wang"
127.0.0.1:6379>
```

### List(列表)

Redis列表是简单的字符串列表，按照插入顺序排序，你可以添加一个元素到列表的头部或者尾部，列表最多可存储 232 - 1 元素 (4294967295, 每个列表可存储40多亿)。

```
127.0.0.1:6379> lpush spring zhang
(integer) 1
127.0.0.1:6379> lpush spring wang
(integer) 2
127.0.0.1:6379> lpush spring yang
(integer) 3
127.0.0.1:6379> lrange spring 0 5
1) "yang"
2) "wang"
3) "zhang"
127.0.0.1:6379>
```

### Set（集合）

Redis的set是string类型的无序集合，集合是通过哈希表实现的，所以添加、删除、查找的复杂度都是O（1）

语法如下：

```
sadd key member
```

实例如下：

```
127.0.0.1:6379> sadd li java
(integer) 1
127.0.0.1:6379> sadd li python
(integer) 1
127.0.0.1:6379> sadd li go
(integer) 1
127.0.0.1:6379> sadd li php
(integer) 1
127.0.0.1:6379> smembers li
1) "php"
2) "go"
3) "python"
4) "java"
127.0.0.1:6379>
```

### Zset(sorted set:有序集合)

Redis zset和set一样也是string类型元素的集合，且不允许重复的成员，不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。zset的成员是唯一的,但分数(score)却可以重复。

语法如下：

```
zadd key score member
```

实例如下：

```
127.0.0.1:6379> zadd zhu 0 zhang
(integer) 1
127.0.0.1:6379> zadd zhu 1 wang
(integer) 1
127.0.0.1:6379> zadd zhu 2 adasjdh
(integer) 1
127.0.0.1:6379> zadd zhu 5 dsaj
(integer) 1
127.0.0.1:6379> zadd zhu 9 zdsa
(integer) 1
127.0.0.1:6379> zadd zhu 3 dasda
(integer) 1
127.0.0.1:6379> zrangebyscore zhu 0 10
1) "zhang"
2) "wang"
3) "adasjdh"
4) "dasda"
5) "dsaj"
6) "zdsa"
127.0.0.1:6379>c
```







# 2019-8-22-redis的相关命令

### 1.keys键操作

```
exists key　　　　　　　　　测试指定key是否存在
del key1 key2….keyN　　　　　　　　删除指定key
type key　　　　　　　　　返回指定key的value类型
keys pattern　　　　　　　返回指定模式的所有key
rename oldkey newkey　　　　　　　改名字
dbsize　　　　　　　　　　返回当前数据路的key数量
expire key seconds　　　　　 为key指定过期时间
ttl key　　　　　　　　　　返回key的过期剩余秒数
select db-index　　　　　　　　　　　选择数据库
move key db-index　     把key从当前数据库移动到指定数据库
flushdb　　　　　　　　　  删除当前数据库所有key
flushall　　　　　　 　删除所有数据库中的所有key
```

### 2.string类型操作

```
set key value　　　　　　　　　　　　设置key对应值为string类型的value
setex key seconds value　　　　　　设置key对应值为string类型的value,增加到期时间
mset key1 value1…keyN valueN　　　一次设置多个key的值
mget key1 …keyN　　　　　　　　　　一次获取多个key的值
incr key　　　　　　　　　　　　　　对key的值++操作，并返回新值
decr key　　　　　　　　　　　　　　同上，但是做的是–操作
incrby key integer　　　　　　　　　　同incr，加指定值
decrby key integer　　　　　　　　　同desr，减指定值
incrbyfloat key increment　　　　　　对key的值增加一个浮点数
append key value　　　　　　　　　给指定key的字符串追加value
substr key start end　　　　　　　　返回截取过的key的字符串值　
getrange key start end　　　　　　　获取存储在key上的值的一个子字符串
setrange key offset value　　　　　　将从start偏移量开始的子串设置指定的值
```

### 3.list链表操作（有序，可重复）

```
lpush key string　　　　　　　　　　　在key对应list的头部添加字符串元素　　　　　　　　　　　　　
rpop key　　　　　　　　　　　　　　　　在list的尾部删除元素，并返回删除元素
rpush key string
lpop key
lpush key string
llen key　　　　　　　　　　　　　　　　　返回对应list的长度
lrange key start end　　　　　　　　　　　返回指定区间内的元素，从下表0开始
ltrim key start end　　　　　　　　　　　　截取list, 保留指定区间内元素
lindex key 下标　　　　　　　　　　　　　获取列表下标对应的指定元素
blpop key[key…] time out　　　　　　　　删除，并获得该列的第一元素， 或阻塞，直到有一个可用
brpop key[key…] time out　　　　　　　　删除， 并获得该列的最后一个元素， 或阻塞，直到有一个可用
rpoplpush source destination　　　　　　　删除列表中的最后一个元素，将其追加到另一个列表
brpoplpush source destination timeout　　弹出一个列表的值，将他推到另一个列表，并返回他，直到有一个可用 

可以模拟 队列（先进后出） 和 栈（先进先出）
```

### 4.hash散列操作

```
hdel key field[field…]　　　　　　　　删除一个或多个hash的field
hexists key field　　　　　　　　　　判断field是否存在hash中
hget key field　　　　　　　　　　　获取hash中field的值
hgetall key　　　　　　　　　　　　从hash中读取全部的域和值
hincrby key field increment　　　　将hash中指定域的值增加给定的值
hincrbyfloat key field increment　　将hash中指定域的值增加给定的浮点数
hkeys key　　　　　　　　　　　　　获取hash 中所有field
hlen key　　　　　　　　　　　　　获取hash中所有字段的数量
hmget key field[field…]　　　　　　获取hash里面指定字段的值
hmset key field[field…]　　　　　　设置hash字段值
hset key field value　　　　　　　　设置hash里面一个字段的值
hsetnx key field value　　　　　　　设置hash的一个字段，只有这个字段不存在是有效
hstrlen key field　　　　　　　　　　获取hash里面指定field的长度
hvals key　　　　　　　　　　　　　获取hash的所有值
hscan key cursor　　　　　　　　　迭代hash里面的元素
```

### 5.set集合操作（无序，唯一）

```
sadd key member　　　　　　　　　添加一个string元素到key对应的set集合中
srem key member　　　　　　　　　从key对应set中移除给定元素
smove p1 p2 member　　　　　　　从p1对应set中移除给定元素并添加到p2对应set中
scard key　　　　　　　　　　　　　返回set的元素个数
sismember key member　　　　　　判断member是否在set中
sinter key p1 p2…pN　　　　　　　　返回所有给定key的交集
sunion key p1 p2…pN　　　　　　　返回所有给定key的并集
sdiff key p1 p2…pN　　　　　　　　返回所有给定key 的差集
smembers key　　　　　　　　　　返回key对应set的所有元素，结果是无序的
sinterstore destination key [key….]　获取两个集合的交集，并存储在一个关键的结果集
sunionstore destination key [key…]　合并set集合，并将结果存入新的set里面
sdifferstore destination key[key…]　　获取队列的差集，并存储在一个新的结果集
srandmember key [count]　　　　　从集合中随机获取一个key
spop key[count]　　　　　　　　　　删除并取得一个集合里面的元素
smove source destination member　移动集合里的一个key到另一个集合
```

### 6.sorted set有序集合操作（有序，唯一）

```
 zadd key score member　　　　　　添加元素到集合，元素在集集合中存在则更新应对的score 
 zrem key member　　　　　　　　　删除指定元素 
 zcount key min max　　　　　　　　返回分数范围内的成员变量 
 zincrby key incr member　　　　　　按照incr幅度增加对应member的score值，返回score值 
zrank key member　　　　　　　　　返回指定元素在集合中的排名（下标），集合中元素是按score从小到大排序的 
zrevrank key member　　　　　　　集合中元素是按score从大到小排序的 
zrange key start end　　　　　　　　从集合中选择指定区间的元素，返回的是有序集合 
 zrevrange key start end　　　　　　同上，返回结果是按score逆序的 
zcard key　　　　　　　　　　　　　返回集合中元素的个数 
zscore key member　　　　　　　　返回给定元素对应的score 
zremrangebyrank key min max　　　删除集合中排名在给定区间的元素 
zinterstore distination numkeys　　　相交多个结果集，导致排序的设置存储在一个新的结果集 
zunionstore destination numberkeys　添加多个排序集合导致排序的设置存储在一个新的结果集，可以实现取得最大值（max），取得最小值（min）

```

### 7.redis的基本事务

```
乐观锁： watch只会在数据被其他客户端抢先修改了的情况下通知执行这个命令的客户端，而不会阻止其他客户端对数据进行修改 

 discard　　　　　　　　　　　　　　丢弃所有multi之后发的命令 
 exec　　　　　　　　　　　　　　　执行所有multi之后发放人命令 
 multi　　　　　　　　　　　　　　　标记一个事务块开始 
 unwatch　　　　　　　　　　　　　取消事务命令 
 watch key[key…]　　　　　　　　　　锁定key，直到执行了multi/exec命令
```

### 8.redis持久化的两种方式

##### 8.1.快照持久化

```
1 ./redis-cli bgsave 异步快照持久化命令　　 save操作是在主线程中保存快照的（不推荐）
2 当执行shutdown命令后，会执行一个save命令，执行完毕之后关闭服务器
3 当从服务器向主服务器发送一个sync命令来执行一次复制操作，那么主服务器会执行bgsave命令
4 配置文件快照配置信息 
save 900 1 （900秒内有1次修改备份）
save 300 10 （900秒内有10次修改备份）
save 60 10000 （60 秒内有10000 次修改备份）

原文链接：https://blog.csdn.net/dongganen/article/details/78882024
```

##### 8.2.AOF持久化

```
1.开启AOF持久化(设置之前所有数据被清空)
2.开启AOF持久化—>修改配置文件 appendonly yes
3.AOF备份存储文件—> appendfilename appendonly.aof
    a.appendfsync always                                    
    b.每次收到写命令就立即强制写入磁盘，最慢的，但是保证完全的持久化，不推荐使    用，还有可能影响固态硬盘的寿命
    c.appendfsync everysec                                 
    d.每秒钟强制写入磁盘一次，在性能和持久化方面做了很好的折中，推荐
    e.appendfsync no                                          
4.AOF备份文件优化处理 ./redis-cli bgrewriteaof
```



### 9.redis主从复制

```
1.从服务器（可读）配置文件修改：slaveof (主服务器ip地址和端口号)ip port
2.从服务器默认禁止写入操作：slave-read-only yes
3.当3个或3个以上的从数据库连接到主数据库时，主数据库才可以写入：min-slaves-to-write 3
4.允许从数据库失去连接的最长时间：min-slave2-max-lag 10
5.slaveof on one 服务器终止复制操作
6.slaveof host port 服务器开始复制一个新的主服务器
7.从服务器在进行同步时，会清空自己的所有数据
8.redis不支持主主复制
9.主从链：随着读请求操作的重要性明显高于写请求的操作性，增加从服务器，减轻主服务器的负担，从服务器可以有自己的从服务器
```

### 10.处理系统故障

```
遇到系统故障时,redis提供了数据恢复工具：redis-check-aof 和 redis-check-dump
```



# Jedis的使用

<https://www.jianshu.com/p/a1038eed6d44>

