# 2019-8-8-mysql报错

### 错误

在安装mysql 5.7的时候，在命令行输入`net start mysql`出现服务名无效的错误：

![Image2](https://github.com/aaaxma/JavaNote/blob/master/images/mysql_error_1.png)

### 解决方法

命令行切到mysql的bin目录下`D:\coding\mysql 5.7\mysql-5.7.27-winx64\bin>`

输入`mysqld --install`,出现`Service successfully installed`的字样，再在命令行中输入`net start mysql`就行了

