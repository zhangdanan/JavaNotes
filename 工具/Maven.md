# 2019-4-22-Maven相关知识

### Maven作用

- 统一集中管理好所有的依赖包，不需要程序员去寻找。
- 对应第三方组件用到的共同jar，maven自动解决重复和冲突问题。
- Maven作为一个开放的架构，提供了公共接口，方便同第三方插件集成，程序员可以将自己需要的插件，动态的集成到Maven，从而扩展新的管理功能。
- Maven可以统一每个项目的构件过程，实现不同项目的兼容性管理。

### Maven简介

​     Maven是Apache开源组织奉献的一个开源项目，Maven的本质是一个项目管理工具，将项目开发和管理过程抽象成一个项目对象模型（POM）。

### Maven环境配置

Maven是一个基于java的工具，所以先要进行JDK的安装。Maven的环境配置步骤如下：

- 先检查Java的安装，Windows端打开命令行输入`java -version`,结果如下：

  ![Image5](https://github.com/aaaxma/JavaNote/blob/master/images/maven01.jpg)

- 从官网下载Maven

- 右键 "计算机"，选择 "属性"，之后点击 "高级系统设置"，点击"环境变量"，来设置环境变量，有以下系统变量需要配置：

  新建环境变量MAVEN_HOME，变量值为maven的安装路径，如下图：

  ![Image5](https://github.com/aaaxma/JavaNote/blob/master/images/maven02.png)

  编辑系统变量Path，添加变量值：%MAVEN_HOME%\bin，或者可以直接为安装路径：D:\coding\maven\apache-maven-3.5.3\bin

  ![Image5](https://github.com/aaaxma/JavaNote/blob/master/images/maven03.png)

- 打开命令行，输入mvn -v，如果出现maven的一些信息，就说明安装成功。如下图：

  ![Image5](https://github.com/aaaxma/JavaNote/blob/master/images/maven04.png)

### Maven仓库

在Maven的术语中，仓库是一个位置，Maven仓库是项目中依赖的第三方库，这个库所在的位置叫做仓库，在Maven中，任何一个依赖，插件或者项目构建的输出，都可以称为构件,Maven仓库能 帮助我们管理构件（主要是JAR)，它就是放置所有JAR文件（WAR，ZIP，POM等）的地方。Maven仓库主要有三种类型:

- **本地仓库**

Maven的本地仓库，在安装Maven的时候并不会创建，在你执行第一次maven命令的时候才会被创建。每个用户在自己的用户目录下都有一个路径为.m2/responsitory/的仓库目录。你可以通过修改Maven安装路径中的conf目录中的Maven的setting.xml来定义另一个路径。

```
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 
   http://maven.apache.org/xsd/settings-1.0.0.xsd">
      <localRepository>C:/MyLocalRepository</localRepository>
</settings>
```

- **中央仓库**

Maven中央仓库是由Maven社区提供的仓库，其中包含了大量常用的库，里面包含了绝大多数留下的开源Java构件，以及源码、作者信息、SCM、信息、许可信息等。一般来说，简单的java项目依赖的构件都可以在这里下载到。中央仓库不需要配置，但需要通过网络才能访问。

- **远程仓库**

如果Mave在中央仓库中找不到依赖的文件，它会停止构建过程并输出错误信息到控制台，Maven提供了远程仓库的概念，它是开发人员自己定制仓库，包含了所需要的代码库或者其他工程中用到的jar文件。

### Maven命令

​       mvn clean +Enter 清空以前编译安装过的历史结果

​       mvn  compile+Enter 编译源代码

​       mvn test+Enter 运行测试案例进行测试

​       mvn  install+Enter将当前代码打包成jar包

​       mvn  site 自动生成站点信息

​       mvn javadoc:javadoc+Enter自动生成API Doc文档

### Maven私服的搭建



### 配置阿里的仓库

由于墙的缘故，maven下载一些依赖会非常慢，可以把仓库配置为国内阿里的仓库，步骤如下:

1. ​	打开maven下的conf/setting.xml。

2. ​    搜索 <mirrors>；找到 <mirrors>。在 <mirrors> 节点下添加。

   ```
   <mirror>
         <id>alimaven</id>
         <name>aliyun maven</name>
         <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
         <mirrorOf>central</mirrorOf>        
   </mirror>
   ```

3. 在你的pom.xml文件里添加：

   ```
   <repositories>  
           <repository>  
               <id>alimaven</id>  
               <name>aliyun maven</name>  
               <url>http://maven.aliyun.com/nexus/content/groups/public/</url>  
               <releases>  
                   <enabled>true</enabled>  
               </releases>  
               <snapshots>  
                   <enabled>false</enabled>  
               </snapshots>  
           </repository>  
   </repositories>
   ```

   



# 2019-4-23-Maven需要掌握的知识

要解决的问题：

- 生成可执行jar，理解scope生成最精确的jar
- 解决类冲突，包依赖 NoClassDefFoundError问题定位以及解决
- 全面理解Maven的Lifecycle\Phase\Goal；
- 用Maven生成Archetype
- Nexus环境搭建，上传，配置
- gradle和Maven的对比

c