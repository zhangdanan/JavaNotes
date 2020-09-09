第一步：下载安装包

下载Linux环境下的jdk1.8，请去（[官网](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)）中下载jdk的安装文件；

由于我的Linux是64位的，因此我下载[jdk-8u131-linux-x64.tar.gz](http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.tar.gz)。

如下图所示：

![img](https://images2017.cnblogs.com/blog/506829/201709/506829-20170927215516903-1578780579.png)

如果Linux本身连接到互联网，我们可以直接通过wget命令直接把JDK安装包下载下来，如图所示：

![img](https://images2017.cnblogs.com/blog/506829/201709/506829-20170927215531778-796970077.png)

要是没有外网的环境，还是安装上面的方法下载安装包，然后上传到服务器当中

第二步、解压安装包

将我们下载好的JDK安装包上传到服务器，进行解压

![img](https://images2017.cnblogs.com/blog/506829/201709/506829-20170927215551387-1988954460.png)

解压命令进行解压

```
1 $ cd  /home/cmfchina
2 $ tar  -zxvf  jdk-8u131-linux-x64.tar.gz
```

![img](https://images2015.cnblogs.com/blog/506829/201707/506829-20170712154949462-1567604342.png)

解压完成之后，可以在当前目录下看到一个名字为【jdk1.8.0_131】的目录，里面存放的是相关文件

![img](https://images2017.cnblogs.com/blog/506829/201709/506829-20170927215606637-1339440704.png)

我们要将解压后的【jdk1.8.0_131】里面的所有数据移动到我们需要安装的文件夹当中，我们打算将jdk安装在usr/java当中，我们在usr目录下新建一个java文件夹

```
mkdir /usr/java
```

![img](https://images2015.cnblogs.com/blog/506829/201707/506829-20170712155622509-501402302.png)

将【jdk1.8.0_131】里的数据拷贝至java目录下

```
mv /home/cmfchina/jdk1.8.0_131 /usr/java
```

![img](https://images2015.cnblogs.com/blog/506829/201707/506829-20170712160243556-345559176.png)

![img](https://images2017.cnblogs.com/blog/506829/201709/506829-20170927215620215-1679478260.png)

第三步、修改环境变量

至此，我们最后需要修改环境变量，通过命令

```
vim /etc/profile
```

![img](https://images2015.cnblogs.com/blog/506829/201707/506829-20170712161307134-1500571117.png)

用vim编辑器来编辑profile文件，在文件末尾添加一下内容（按“i”进入编辑）：

```
1 export JAVA_HOME=/usr/java/jdk1.8.0_131
2 export JRE_HOME=${JAVA_HOME}/jre
3 export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib:$CLASSPATH
4 export JAVA_PATH=${JAVA_HOME}/bin:${JRE_HOME}/bin
5 export PATH=$PATH:${JAVA_PATH}
```

如图所示：

![img](https://images2017.cnblogs.com/blog/506829/201709/506829-20170927215632028-1294986463.png)

然后，保存并退出(按：wq!)

保存完之后，我们还需要让这个环境变量配置信息里面生效，要不然只能重启电脑生效了。

通过命令source /etc/profile让profile文件立即生效，如图所示

![img](https://images2015.cnblogs.com/blog/506829/201707/506829-20170712162556978-2141450378.png)

第四步、测试是否安装成功

①、使用javac命令，不会出现command not found错误

②、使用java -version，出现版本为java version "1.8.0_131"

③、echo $PATH，看看自己刚刚设置的的环境变量配置是否都正确

如图所示：

![img](https://images2017.cnblogs.com/blog/506829/201709/506829-20170927215645919-791601294.png)

至此，安装结束