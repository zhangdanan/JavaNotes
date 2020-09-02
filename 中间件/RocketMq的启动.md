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

![img](https://pic4.zhimg.com/80/v2-4fead76ea6deb13a8cd186fdd1c44723_hd.jpg)





### **3.启动Brokerr**

直接双击bin目录下的mqbroker.cmd脚本来启动Broker，如下图

![img](https://pic4.zhimg.com/80/v2-85443e677c5d9cd49fbb23d106a6facb_hd.jpg)





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