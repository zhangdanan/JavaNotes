# linux的wget命令

## 简介

wget是linux中的一个下载文件的工具，支持断点下载功能，同时支持FTP和HTTP下载，支持代理服务器，设置起来方便简单lls

## 命令

#### 使用wget下载单个文件

```
wget http：//xxxxxxxx
```

#### 使用wget -O进行重命名

```
wget -O xxxx.zip http://xxxxxxxxx
```

#### 使用wget -limit -rate进行限速下载

```
wget -limit -rate=1024k http://xxxxxxxx
```

#### 使用wget -c断点重连

下载某个文件突然中断时，使用wget -c重新下载

```
wget -c http://xxxxxxxxxxx
```

#### 使用wget -i下载多个文件

首先，先把众多链接保存在一个文件里面

```
cat > filelist.txt
url1
url2
url3
```

接着使用这个文件和参数-i下载

```
wget -i fillist.txt
```



> https://www.cnblogs.com/cindy-cindy/p/6847502.html