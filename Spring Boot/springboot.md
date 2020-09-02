# 2019-8-20-springboot概述（一）

### 什么是springboot

```
Build Anything with Spring Boot：Spring Boot is the starting point for building all Spring-based applications. Spring Boot is designed to get you up and running as quickly as possible, with minimal upfront configuration of Spring.
```

上面是springboot官网上的一句话，意思就是springboot是所有基于spring开发应用的起点，springboot的设计是为了让你尽可能快 的跑起来spring应用程序并且尽可能减少你的引用配置。

- 使用“习惯优于配置”（项目中存在大量的配置，此外还内置一个习惯性的配置，让你无须）的理念让你的项目快速运行起来。
- 不是什么新的框架，而是默认配置了很多框架的使用方式，就像Maven整合了所有的jar包一样，springboot整合了所有框架。

### 使用spring boot的好处

无需像ssm那样出现很多复杂的配置。划重点就是简单、快速、方便地搭建项目；对主流开发框架的无配置集成；极大提高了开发、部署效率。

### 应用入口类

`@SpringBootApplication`是springboot的核心注解，是一个组合注解，该注解包括了`@Configuration`、`@EnableAutoConfiguration`、`@ComponentScan`。如果不用`@SpringBootApplication`注解，可以使用这三个注解

- `@EnableAutoConfiguration`是让Springboot根据类路径中的jar包依赖为当前项目进行自动配置，例如就是如果添加了spring-boot-starter-web依赖，会自动添加Tomcat和SpringMvc的依赖，Springboot会对Tomcat和SpringMvc进行自动配置。

### springboot的配置文件

springboot使用一个全局的配置文件application.properties或application.yml，放置在src/main/resources目录下

### Spring Boot的原理和特性

Spring Boot基本上是Spring框架的扩展，它消除了设置Spring应用程序所需的XML配置，为更快，更高效的开发生态系统铺平了道路。

Spring Boot中的一些特点：

1. 创建独立的spring应用。
2. 嵌入Tomcat, Jetty Undertow 而且不需要部署他们。
3. 提供的“starters” poms来简化Maven配置
4. 尽可能自动配置spring应用。
5. 提供生产指标,健壮检查和外部化配置
6. 绝对没有代码生成和XML配置要求。

spring boot的组成和结构图如下：

![springboot01](https://github.com/aaaxma/JavaNote/blob/master/images/springboot01.jpg)

从图中可以看出SpringBoot是包含了Spring的核心（IOC）和（AOP）；以及封装了一些扩展，如Stater：

![springboot02](https://github.com/aaaxma/JavaNote/blob/master/images/springboot02.jpg)





# 2019-8-20-springboot（二）热部署

总共有两种方式

- 使用Spring Loaded
- 使用Spring-boot-devtools

### 使用Spring-boot-devtools

1. 修改pom.xml文件，在pom.xml中添加一个依赖

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional> <!-- 这个需要为 true 热部署才有效 -->
</dependency>
```

2. 在idea中设置以下两项

   ```
   1. “File” -> “Settings” -> “Build,Execution,Deplyment” -> “Compiler”，选中打勾 “Build project automatically” 。
   2.  组合键：“Shift+Ctrl+Alt+/” ，选择 “Registry” ，选中打勾 “compiler.automake.allow.when.app.running” 。
   ```

### 使用Spring Loaded

1. 在plugins中添加依赖

   ```
   <build>
           <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
                   <dependencies>
                       <!-- spring热部署 -->
                       <dependency>
                           <groupId>org.springframework</groupId>
                           <artifactId>springloaded</artifactId>
                           <version>1.2.6.RELEASE</version>
                       </dependency>
                   </dependencies>
               </plugin>
           </plugins>
       </build>
   ```

   

### Devtools相关

1. 页面热部署

   devtools可以实现页面热部署，即页面修改后会立即生效，在**application.properties**文件中配置`spring.thymeleaf.cache=false`来实现这个功能

2. 监听文件夹的变化

   不想重新编译java类，就可以直接使用devtools监听文件夹的变化，想监听某一个文件夹下面的时候，直接在**application.properties**中添加：`spring.devtools.restart.additional-paths=com\\zkn\\learnspringboot(事例)`

3. devtools原理

   当我们修改一个java类的时候，我们只需要重新编译一下，springboot就会重启了，devtools会监听classpath下的文件变动，当java类重新编译的时候，devtools会监听到这个变化，然后就会重新启动springboot。重启是很快的一个过程，因为在springboot中有两个类加载器，一个是加载工程外部资源的，例如jar包，还有一个类加载器是用来加载本工程 的class的，