## 一、服务器上的配置mysql数据库

进入mysql：

```shell
mysql -uroot -p
```

输入密码。

选择mysql数据库：

```mysql
use mysql;
```

增加允许远程访问的用户或者允许现有用户的远程访问。
给root授予在任意主机（%）访问任意数据库的所有权限。

```mysql
update user set host='%' where user='root' and host='localhost';
```

退出mysql：

```mysql
exit
```

重启数据库：

```shell
service mysql restart
```

# 使用Navicat连接服务器数据库

首先安全组开放3306端口

新建数据库连接，点General，填写相关信息

在host里面填上localhost

下面是数据库用户和密码

![image-20200606163251400](C:\Users\sloth\AppData\Roaming\Typora\typora-user-images\image-20200606163251400.png)

然后

点击SSH，在下面填写相关信息

host填写服务器公网ip

User name是服务器用户名，一般服务器都是linux是root，window是Administrator

密码是服务器连接密码。

