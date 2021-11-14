前提是安装好maven。

1、    打开maven存放文件夹找到 conf ->settings.xml 
 ![img](file:///C:/Users/m1885/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)
 找到节点 
 把下面内容写入节点内 配置为阿里云的镜像

```
<mirror>
   <id>nexus-aliyun</id>
   <mirrorOf>central</mirrorOf>
   <name>Nexus aliyun</name>
   <url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```

2、idea中配置maven

File->Settings 配置如下 
 ![img](file:///C:/Users/m1885/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)

