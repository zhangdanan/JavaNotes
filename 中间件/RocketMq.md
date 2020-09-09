# 相关概念

RabbitMQ是一个由erlang开发的AMQP（Advanced Message Queue Protocol)的开源实现。

核心概念：

- **1.1 Message**

消息：由消息头和消息体组成。消息体是不透明的，消息头是由一系列可选择属性组成，这些属性包括routing-key(路由方法键）、priority(相对于其他消息的优先级)、delivery-mode（指出该消息可能需要持久性存储）等。

- **1.2 Publisher**

消息的生产者，也是一个向交换器发布消息的客户端应用程序。

- **1.3 Exchange**

交换器，用来接收生产者发送的消息，并将这些消息路由给服务器中的队列。Exchange由4中类型：direct(默认)、fanout、topic和headers,不同类型的Exchange转发消息的策略有区别。（下文有三种交换器的详细说明）

- **1.4 Queue**

消息队列，用来保存消息直到发送给消费者。一个消息可投入一个或多个队列，消息一直在队列里面，等待消费者连接到这个队列将其取走。

- **1.5 Binding**

绑定，用于消息队列和交换器之间的关联。一个绑定就是基于路由键将交换器和消息队列连接起来的路由规则。Exchange和Queue之间可以是多对多的关系。

- **1.6 Connection**

网络连接，比如一个TCP连接。

- **1.7 Channel**

信道，多路复用连接中的一条独立的双向数据流通道。信道是建立在真实的TCP连接内的虚拟连接，AMQP命令都是通过信道发出去的，不管是发布消息、订阅队列还是接受消息，这些动作都是通过信道完成。因为对于操作系统来说建立和销毁TCP都是昂贵的开销，所以引入信道的概念，以复用一条TCP连接。

- **1.8 Consumer**

消息的消费者，表示一个从消息队列中取得消息的客户端应用程序。

- **1.9 Virtual Host**

虚拟主机，表示一批交换器、消息队列和相关对象。虚拟主机是共享相同的身份认证和加密环境的独立服务器域。每个vhost本质就是一个mini版的RabbitMQ服务器，拥有自己的队列、交换器、绑定和权限机制。vhost是AMQP概念的基础，必须在连接时指定，RabbitMQ默认的vhost是 / 。

- **1.10 Broker**

表示消息队列服务器实体。

![img](https://img-blog.csdnimg.cn/20190709153017232.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pob3VqaWFuX0xpdQ==,size_16,color_FFFFFF,t_70)

# windows安装rabbitmq3.8

### 一、ERL安装

##### 1.安装ERL

一直next就可以，不再描述

##### 2.配置环境变量

将D:\coding\erl-23.0\bin加入到Path中
##### 3.验证 
在cmd命令下输入:erl 
能够返回版本号则表示安装与配置环境变量成功 


### 二、RabbitMQ 安装

##### 1、将下载下来的 rabbitmq-server-windows-3.8.3.zip 解压到指定的安装目录即可。 
##### 2、配置环境变量 
添加 RABBITMQ_SERVER 并设置为RabbitMQ 解压到的目录，如我放置的目录为 ：D:\rabbitmq_server-3.8.3 
在 Path 系统变量末尾添加 %RABBITMQ_SERVER%\sbin

##### 3、验证 
打开cmd窗口，输入: `rabbitmq-service```

```
PS C:\WINDOWS\system32> rabbitmq-service

*********************
Service control usage
*********************

rabbitmq-service help   - Display this help
rabbitmq-service install - Install the RabbitMQ service
rabbitmq-service remove  - Remove the RabbitMQ service

The following actions can also be accomplished by using
Windows Services Management Console (services.msc):

rabbitmq-service start  - Start the RabbitMQ service
rabbitmq-service stop   - Stop the RabbitMQ service
rabbitmq-service disable - Disable the RabbitMQ service
rabbitmq-service enable  - Enable the RabbitMQ service
```

如有输出 以上 rabbitmq 命令的解释信息即表示安装成功。

##### 4、安装服务 
可以把RabbitMQ服务器作为服务运行，打开一个cmd窗口(管理员)，输入命令： `rabbitmq-service install`

```
PS C:\WINDOWS\system32> rabbitmq-service install
D:\Program Files\erl9.3\erts-9.3\bin\erlsrv: Service RabbitMQ added to system.
```


运行命令成功后我们可以查看一下服务是否已添加成功 

##### 5、启动RabbitMQ 

在cmd 窗口中输入命令:`rabbitmq-service start`

```
PS C:\WINDOWS\system32> rabbitmq-service start
RabbitMQ 服务正在启动 .
RabbitMQ 服务已经启动成功。
```

##### 6、安装web管理插件 
RabbitMQ 可以通用一个Web界面来进行管理。在cmd命令窗口中输入命令:`rabbitmq-plugins enable rabbitmq_management`

```
PS C:\WINDOWS\system32> rabbitmq-plugins enable rabbitmq_management
Enabling plugins on node rabbit@hwacer-hp:
rabbitmq_management
The following plugins have been configured:
 rabbitmq_management
 rabbitmq_management_agent
 rabbitmq_web_dispatch
Applying plugin configuration to rabbit@hwacer-hp...
The following plugins have been enabled:
 rabbitmq_management
 rabbitmq_management_agent
 rabbitmq_web_dispatch

set 3 plugins.
Offline change; changes will take effect at broker restart.
```

##### 7、最后：

安装好后需要重启RabbitMQ，使用 stop 停止 再使用start 启动即可。

```
PS C:\WINDOWS\system32> rabbitmq-service stop
RabbitMQ 服务正在停止.........
RabbitMQ 服务已成功停止。
```

```
PS C:\WINDOWS\system32> rabbitmq-service start
RabbitMQ 服务正在启动 .
RabbitMQ 服务已经启动成功。
```

重启之后我们访问 http://localhost:15672/ 登陆RabbitMQ 的web管理后台。默认用户密码为 guest/guest 
重启之后可能需要过一会访问才能打开 

# Windows下启动RocketMq

### **1.配置环境变量**

首先要有Java环境，这个不会的去网上搜教程

配置ROCKETMQ_HOME，NAMESRV_ADDR两个环境变量，ROCKETMQ_HOME的变量值是下载RocketMq文件的存放地址，如下图：

![img](https://pic1.zhimg.com/80/v2-e7855bf46297bf3afab69ee98a527d48_hd.jpg)

![img](https://pic2.zhimg.com/80/v2-5f9e6904c977a0b987bd52a6fc2070d5_hd.jpg)





### **2.启动NameServer**

直接双击bin目录下的mqnamesrv.cmd脚本来启动NameServer

![img](https://pic4.zhimg.com/80/v2-53d065397bac702fca21a738a8361cb7_hd.jpg)



看到 `The Name Server boot success` 字样，表示NameServer己启动成功

![img](https://pic4.zhimg.com/80/v2-85443e677c5d9cd49fbb23d106a6facb_hd.jpg)



### **3.启动Brokerr**

直接双击bin目录下的mqbroker.cmd脚本来启动Broker，如下图

![img](https://pic4.zhimg.com/80/v2-4fead76ea6deb13a8cd186fdd1c44723_hd.jpg)



### **4.验证RocketMq功能**

RocketMQ自带了恬送与接收消息的脚本`tools.cmd`，用来验证RocketMQ的功能是否正常 。

首先，打开一个cmd窗口，跳转到bin目录下

![img](https://pic4.zhimg.com/80/v2-6bd4086c7fe47525d4aedcf06f935a37_hd.jpg)



### **启动消费者**

依次输入以下命令

```text
set NAMESRV_ADDR=localhost:9876
tools.cmd org.apache.rocketmq.example.quickstart.Consumer
```

结果如下图：

![img](https://pic2.zhimg.com/80/v2-f715a14cf490e8f8163c8ad4bb6c9375_hd.jpg)



### **启动生产者**

重新打开一个cmd窗口，跳转到bin目录下，依次执行以下命令：

```text
set NAMESRV_ADDR=localhost:9876
tools.cmd org.apache.rocketmq.example.quickstart.Producer
```

启动成功后，生产者会发送1000个消息，然后自动推出，结果如下图：

![img](https://pic4.zhimg.com/80/v2-cbee59a260054d88aa7c439cd2f5667f_hd.jpg)



此时，在消费者界面按下Ctrl+C,就会接收到刚刚生产者发出的消息。如下图：

![img](https://pic4.zhimg.com/80/v2-49a5bfe882005212bea4ed75d9d85563_hd.jpg)



这样就验证了RocketMq的功能。