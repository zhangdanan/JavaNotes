#### 1. 安装make

```
yum -y install gcc automake autoconf libtool make
```

#### 2. 安装gcc

```
yum -y install gcc gcc-c++
```

#### 3. 安装OpenSSL（具体版本根据实际情况更新）

```
#下载openssl
cd /usr/local/src
wget https://www.openssl.org/source/openssl-1.1.1b.tar.gz
#解压
tar -zxvf openssl-1.1.1b.tar.gz
#安装
cd openssl-1.1.1b
./config && make && make install
```

#### 4. 安装PCRE库（具体版本根据实际情况更新）,是nginx支持rewrite

```
#下载
cd /usr/local/src
wget https://netix.dl.sourceforge.net/project/pcre/pcre/8.40/pcre-8.40.tar.gz
#解压
tar -zxvf pcre-8.40.tar.gz
#安装
cd pcre-8.40
./configure && make && make install
```

#### 5. 安装zlib库（具体版本根据实际情况更新）

```
#下载
cd /usr/local/src
wget http://zlib.net/zlib-1.2.11.tar.gz
#解压
tar -zxvf zlib-1.2.11.tar.gz
#安装
cd zlib-1.2.11
./configure && make && make install
```

#### 6. 安装nginx（具体版本根据实际情况更新）

```
#下载
cd /usr/local/src
wget http://nginx.org/download/nginx-1.18.0.tar.gz
#解压
tar -zxvf nginx-1.18.0.tar.gz
#安装
cd nginx-1.18.0
./configure && make && make install
```

#### 7. 查看安装位置和版本

```
whereis nginx
#记录安装位置（以/usr/local/nginx为例）
cd /usr/local/nginx/sbin
./nginx -v
```

#### 8. 启动

```
/usr/local/nginx/sbin/nginx
#查看启动状态
ps -ef|grep nginx
```

#### 9. 添加端口开放，默认80端口

```
#查看防火墙状态（not running为未开启，running为开启中）
firewall-cmd --state
#方式一，直接关闭防火墙
systemctl stop firewalld.service
#方式二，开启80端口并重启防火墙
firewall-cmd --zone=public --add-port=80/tcp --permanent
systemctl restart firewalld.service
```

#### 10. 浏览器访问

[http://192.168.0.100](http://192.168.0.100/)
[![img](https://img2020.cnblogs.com/blog/1119097/202006/1119097-20200602150222122-230893108.png)](https://img2020.cnblogs.com/blog/1119097/202006/1119097-20200602150222122-230893108.png)

#### 11. 启动、重启、停止、重新加载/检查/指定配置文件

```
#启动
/usr/local/nginx/sbin/nginx     		   
#停止
/usr/local/nginx/sbin/nginx -s stop
/usr/local/nginx/sbin/nginx -s quit

#强制停止
ps -ef | grep nginx
killall -9 nginx

#重启
/usr/local/nginx/sbin/nginx -s reopen
 
#重新载入配置文件
/usr/local/nginx/sbin/nginx -s reload

#检查配置文件
/usr/local/nginx/sbin/nginx -t

#启动时检查并指定配置文件
/usr/local/nginx/sbin/nginx -t -c /usr/local/nginx/conf/nginx.conf
```

#### 12. 映射静态文件目录[#](https://www.cnblogs.com/cao-lei/p/13031451.html#1031803578)

```
#创建data文件夹
cd /usr/local/nginx/
mkdir data
#创建test.txt
cd data/
touch test.txt
#编辑文件
vi test.txt
#添加映射
cd /usr/local/nginx/conf
vi nginx.conf
#在http下添加配置
#listen 监听的端口
#server_name 服务名称，域名。无域名则配置本机IP
server {
        listen       8089;
        server_name  192.168.0.100;
        location / {
            root /usr/local/nginx/data/;
        }  
    }
#重新载入配置文件
/usr/local/nginx/sbin/nginx -s reload
#开放端口
firewall-cmd --zone=public --add-port=8089/tcp --permanent
systemctl restart firewalld.service
```

浏览器访问：http://192.168.0.100:8089/test.txt

#### 13. Nginx upstream(三种常见)[#](https://www.cnblogs.com/cao-lei/p/13031451.html#2809315953)

  如果后端服务器down掉，则自动剔除。

- 默认轮询

```
Copyupstream backend {
    server 192.168.0.101; 
    server 192.168.0.102; 
} 
```

- weight，访问比例与权重成正比

```
Copyupstream backend {
    server 192.168.0.101 weight=1;
    server 192.168.0.102 weight=2; 
} 
```

- ip_hash，解决session共享问题

```
Copyupstream backend {
    ip_hash;
    server 192.168.0.101; 
    server 192.168.0.102; 
} 
```

**负载均衡：**

```
Copy#以轮询为例，在http下配置
upstream backend {
    server 192.168.0.101; 
    server 192.168.0.102; 
} 
server {
    listen  80;
    server_name  192.168.0.100;
        
    location / {
        proxy_pass  http://backend;
    }
}
```

浏览器访问：[http://192.168.0.100](http://192.168.0.100/)

文章来源：https://www.cnblogs.com/cao-lei/p/13031451.html


