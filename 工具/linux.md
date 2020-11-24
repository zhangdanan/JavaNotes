# 查看linux系统是多少位数的

```
uname -m
```

# 查看是否启动某服务

```
ps -ef |grep helloblog
```

# Linux下查看和停止所有java进程

查看所有Java进程命令

```
ps -ef |grep java
```

停止所有java进程命令

```
pkill -9 java
```

停止特定Java进程命令

```
kill -9 java进程序号
```

# linux查看服务基本命令

查看IP：

```
ip addr show
```

查看端口与服务：

```
netstat -anp
```

查看某个端口进程

```
netstat -anp | grep 8080
```

关闭某个进程

```
kill -9 进程ID
```

查看CPU 

```
top 
```

查看tomcat运行

```
ps -aux | grep tomcat
```

查看springBoot运行状态

```
jobs -l
```

启动springBoot jar包

-- 后台运行

```
nohup java -jar 你的jar命名.jar > logs.log &
```

切换root 

```
sudo -i 之后输入密码即可
```

```
// 以用户为主的格式来显示所有的进程
　　ps aux
// 搜寻所有含有tomcat进程的详细信息并打印在屏幕上.（“| ”是管道符，管道符左边命令的输出就会作为管道符右边命令的输入）
　ps aux | grep tomcat
// 以用户为主的格式来显示所有的进程并通过less分页显示，按q退出，按h进入帮助
　　ps aux | less
　　// 显示进程信息
　　ps -A
　　// 显示root进程用户信息
　　ps -u root
　　// 显示所有命令，连带命令行
　　ps -ef
```



# window上传文件到linux

Centos中使用lrzsz

### 1.安装

```
yum install lrzsz
```

### 2.文件上传

安装完成后执行，输入命令后会弹出文件选择框，选择需要上传的文件进行上传

```
rz
```

### 3.文件下载

命令输入后，会弹出选择框，设置需要下载到windows的指定目录

```
sz 文件名
```

**注意事项**：必须要使用xshell等连接工具使用

# linux下的文件的压缩和解压

### .zip

#### 压缩

``` 
命令格式：
zip [选项] 压缩包名 源文件或源目录

选项：
-r：压缩目录

实例：
zip test.zip abc

压缩多个文件：
zip test.zip abc abcd
```

#### 解压

```
命令格式：
unzip [选项] 压缩包名

选项：
-d：指定压缩位置

实例：
unzip -d /tmp/ test.zip
```

### .gz

```
命令格式：
gzip [选项] 源文件

选项：
-c：将压缩数据输出到标准输出中，可以用于保留原文件
-d：解压缩
-r：压缩目录

gzip -r 123
注意事项：上面命令会将123这个目录下的每个文件分别进行压缩，而不是将整个1223目录进行压缩，也就是说 gzip命令不会打包压缩。

解压缩：
gunzip install.log.gz
=
gzip -d install.log.gz

```

### .bz2

压缩算法更先进，压缩比更高，压缩时间长，**注意bzip2不能压缩目录，会报错**

```
命令格式：
bzip2 [选项] 源文件

选项：
-d：解压缩
-k：压缩时，保留源文件
-v：显示压缩的详细信息

实例：
压缩成.bz2格式
bzip2 abc
保留源文件压缩
bzip2 -k test
```

### .tar

只是打包不会压缩文件

``` 
打包

命令格式：
tar [选项] [-f 压缩包名] 源文件或目录

选项：
-c：打包
-f：指定压缩包的文件名，压缩包的扩展名是用来给管理员识别格式的，所以一定要正确指定扩展名
-v：显示打包文件过程

实例：
tar -cvf test.tar abc

打包多个文件：
tar -cvf test.tar abc bcd

```

```
解包

命令格式：
tar [选项] 压缩包

选项：
-x：解打包
-f：指定压缩包的文件名
-v：显示解打包文件过程
-t：测试，就是不解打包，只是查看包中有哪些文件
-C(大)：指定解打包的目录
```

### .tar.gz或.tar.bz2：实现同时进行打包或压缩

```
命令格式：
tar [选项] 压缩包 源文件或目录

选项：
-z：压缩和解压缩.tar.gz格式
-j：压缩和解压缩.tar.bz2格式

实例：
将/tmp/目录直接打包压缩为.tar.gz格式
tar -zcvf tem.tar.gz /tmp/
解压缩与解打包.tar.gz格式
tar -zxvf tmp.tar.gz
```

# linux中文件复制

文件复制命令cp

```
命令格式：
cp [选项] 源文件 目标文件

选项：
-r：递归复制，用于目录的复制操作
-p：与文件的属性一起复制，而非使用默认属性
-i：若目标文件已存在，在覆盖时先询问是否真的操作
-f：强制复制
-a：复制所有的目录

实例：
将file复制到/test目录下
cp file /test

将/test1目录下的file1复制到/test2目录，并将文件名改为file2
cp /test1/file1 /test2/file2
```

# linux文件移动

```
命令格式：
mv [选项] 源文件 目的地

选项：
-f：强制直接移动而不询问
-i：若目标文件已经存在，就会询问是否覆盖
-u：若目标文件已经存在，且源文件比较新，才会更新

实例：
将/test目录下的file1文件移动到/test2，并将文件名改为file2
mv /test/file1 /test2/file2
```

# linux文件删除

```
命令格式：
rm [] 文件或者目录

选项：
-f：强制删除
-i：交互模式，在删除前询问用户是否操作
-r：递归删除，常用在目录的删除

实例：
rm -rf /test/file1
```

# Linux运行jar包

查看jar命令

```
ps -ef|grep xxx.jar
ps aux|grep xxx.jar

pid号为123，杀掉命令为
kill -9 123
```

这里&表示后台运行，ssh窗口不被锁定，但是Linux系统关闭窗口时，程序还是会退出

```
java -jar xxx.jar &
```

nohup表示不挂断运行命令行，当linux系统账号退出或关闭终端时，程序仍然运行，用nohup命令执行作业时，该作业的所有输出被重定向到nohup.out的文件中，除非指定了输出文件

```
nohup java-jar xxx.jar &
```

将所有启动的日志信息记录到temp.txt文件中

```
nohup java-jar xxx.jar>/usr/local/test.txt&
```

# Linux运行Vue项目

### 1.部署Nginx

不再重复

### 2.Vue打包

```
npm run build
```

### 3.讲打包后的dist文件夹上传至服务器

> 本地项目为/usr/local/webapp

### 4.修改niginx的conf文件

```
#修改如下
server {
  listen 80;
  server_name localhost;

  # 注意设定 root路径是有dist的
  location / {
    root /usr/local/webapp/dist;
    index /index.html;
  }

  #跨域 ip和port自行替换
  location /adminApi {
    proxy_pass http://ip:port;
  }

}
```

### 5.使配置生效

```
sbin/nginx -s reload
sbin/nginx -s stop
sbin/nginx
```

### 6.访问ip地址

# Linux查看端口状态

**netstat命令各个参数说明如下：**

　　**-t : 指明显示TCP端口**

　　**-u : 指明显示UDP端口**

　　**-l : 仅显示监听套接字(所谓套接字就是使应用程序能够读写与收发通讯协议(protocol)与资料的程序)**

　　**-p : 显示进程标识符和程序名称，每一个套接字/端口都属于一个程序。**

　　**-n : 不进行DNS轮询，显示IP(可以加速操作)**

**即可显示当前服务器上所有端口及进程服务，于grep结合可查看某个具体端口及服务情况··**

```
netstat -ntlp  //查看当前所有tcp端口

netstat -ntulp |grep 80  //查看所有80端口使用情况

netstat -an | grep 3306  //查看所有3306端口使用情况

查看一台服务器上面哪些服务及端口
netstat -lanp

查看一个服务有几个端口。比如要查看mysqld

ps -ef |grep mysqld

查看某一端口的连接数量,比如3306端口

netstat -pnt |grep :3306 |wc

查看某一端口的连接客户端IP 比如3306端口

netstat -anp |grep 3306

netstat -an 查看网络端口 

lsof -i :port，使用lsof -i :port就能看见所指定端口运行的程序，同时还有当前连接。 

nmap 端口扫描
netstat -nupl  (UDP类型的端口)
netstat -ntpl  (TCP类型的端口)
netstat -anp 显示系统端口使用情况
```