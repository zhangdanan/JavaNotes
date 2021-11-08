# Spring学习一（spring概述）

### 如何去学习

学习方法----掌握用法----深入理解----不断实践----反复总结----再次深入理解与实践

### 什么是Spring

- Spring是一个开源框架

- Spring是为了简化企业级应用开发而生，使用spring可以使简单的JavaBean实现以前只有EJB才能实现的功能

- Spring使JavaSE/EE的一站式框架

- 方便解耦，简化开发

  ——Spring就是一个大工厂，可以将所有对象创建和依赖关系维护，交给Spring管理

- AOP编程的支持

  ——Spring提供面向切面编程，可以方便的实现对程序进行权限拦截、运行监控等功能

- 声明式事务的支持

  ——只需要通过配置就可以完成对事物的管理，而无需手动编程

### 为什么使用Spring

- 是一种轻量级的容器

- 提供了对多种技术的支持（JMS，MQ支持，Unit Test等）

- AOP（事务管理，日志等）

- 提供了众多方便应用的辅助类（JDBC Template）

- 对主流应用框架提供了良好的支持

- 方便程序的测试

  ——Spring对Junit4支持，可以通过注解方便的测试Spring程序

- 降低JavaEE API的使用难度

  ——Spring对JavaEE 开发中非常难用的一些API（JDBC、JavaMail、远程调用等）都提供了封装，使这些API使用难度大大降低

### Spring的适用范围

- 构建企业应用（SSM或SSH）
- 单独使用Bean容器，对于Bean管理
- 单独使用AOP进行切面处理
- 其他的Spring功能如对消息的支持等
- 在互联网中的应用

### Spring体系结构

spring体系结构图如下：

![Image](https://github.com/aaaxma/JavaNote/blob/master/images/Spring01.png)

1. **核心容器**

   核心容器由**spring-core，spring-beans，spring-context，spring-context-support和spring-expression**（SpEL，Spring表达式语言，Spring Expression Language）等模块组成，它们的细节如下：

   - **spring-core**模块提供了框架的基本组成部分，包括 IoC 和依赖注入功能。
   - **spring-beans** 模块提供 BeanFactory，工厂模式的微妙实现，它移除了编码式单例的需要，并且可以把配置和依赖从实际编码逻辑中解耦。
   - **context**模块建立在由**core**和 **beans** 模块的基础上建立起来的，它以一种类似于JNDI注册的方式访问对象。Context模块继承自Bean模块，并且添加了国际化（比如，使用资源束）、事件传播、资源加载和透明地创建上下文（比如，通过Servelet容器）等功能。Context模块也支持Java EE的功能，比如EJB、JMX和远程调用等。**ApplicationContext**接口是Context模块的焦点。**spring-context-support**提供了对第三方库集成到Spring上下文的支持，比如缓存（EhCache, Guava, JCache）、邮件（JavaMail）、调度（CommonJ, Quartz）、模板引擎（FreeMarker, JasperReports, Velocity）等。
   - **spring-expression**模块提供了强大的表达式语言，用于在运行时查询和操作对象图。它是JSP2.1规范中定义的统一表达式语言的扩展，支持set和get属性值、属性赋值、方法调用、访问数组集合及索引的内容、逻辑算术运算、命名变量、通过名字从Spring IoC容器检索对象，还支持列表的投影、选择以及聚合等。

2. **数据访问/集成**

   数据访问/集成层包括 JDBC，ORM，OXM，JMS 和事务处理模块，它们的细节如下：

   （注：JDBC=Java Data Base Connectivity，ORM=Object Relational Mapping，OXM=Object XML Mapping，JMS=Java Message Service）

   - **JDBC** 模块提供了JDBC抽象层，它消除了冗长的JDBC编码和对数据库供应商特定错误代码的解析。
   - **ORM** 模块提供了对流行的对象关系映射API的集成，包括JPA、JDO和Hibernate等。通过此模块可以让这些ORM框架和spring的其它功能整合，比如前面提及的事务管理。
   - **OXM** 模块提供了对OXM实现的支持，比如JAXB、Castor、XML Beans、JiBX、XStream等。
   - **JMS** 模块包含生产（produce）和消费（consume）消息的功能。从Spring 4.1开始，集成了spring-messaging模块。。
   - **事务**模块为实现特殊接口类及所有的 POJO 支持编程式和声明式事务管理。（注：编程式事务需要自己写beginTransaction()、commit()、rollback()等事务管理方法，声明式事务是通过注解或配置由spring自动处理，编程式事务粒度更细）。

3. **Web**

   Web 层由 Web，Web-MVC，Web-Socket 和 Web-Portlet 组成，它们的细节如下：

   - **Web** 模块提供面向web的基本功能和面向web的应用上下文，比如多部分（multipart）文件上传功能、使用Servlet监听器初始化IoC容器等。它还包括HTTP客户端以及Spring远程调用中与web相关的部分。。
   - **Web-MVC** 模块为web应用提供了模型视图控制（MVC）和REST Web服务的实现。Spring的MVC框架可以使领域模型代码和web表单完全地分离，且可以与Spring框架的其它所有功能进行集成。
   - **Web-Socket** 模块为 WebSocket-based 提供了支持，而且在 web 应用程序中提供了客户端和服务器端之间通信的两种方式。
   - **Web-Portlet** 模块提供了用于Portlet环境的MVC实现，并反映了spring-webmvc模块的功能。

4. **其他**

   还有其他一些重要的模块，像 AOP，Aspects，Instrumentation，Web 和测试模块，它们的细节如下：

   - **AOP** 模块提供了面向方面的编程实现，允许你定义方法拦截器和切入点对代码进行干净地解耦，从而使实现功能的代码彻底的解耦出来。使用源码级的元数据，可以用类似于.Net属性的方式合并行为信息到代码中。
   - **Aspects** 模块提供了与 **AspectJ** 的集成，这是一个功能强大且成熟的面向切面编程（AOP）框架。
   - **Instrumentation** 模块在一定的应用服务器中提供了类 instrumentation 的支持和类加载器的实现。
   - **Messaging** 模块为 STOMP 提供了支持作为在应用程序中 WebSocket 子协议的使用。它也支持一个注解编程模型，它是为了选路和处理来自 WebSocket 客户端的 STOMP 信息。
   - **测试**模块支持对具有 JUnit 或 TestNG 框架的 Spring 组件的测试。





# Spring学习二（springIOC容器）

### 接口及面向接口编程

##### 接口是什么

- 用于沟通的中介物的抽象化
- 实体把自己提供给外界的一种抽象化说明，用以由内部操作分离出外部沟通方法，使其能修改内部而不影响外界其他实体与其交互的方式

##### 面向接口编程

- 结构设计中，分清层次及调用关系，每层只向外（上层）提供一组功能接口，各层间仅依赖接口而非实现类
- 接口实现的变动不影响各层间的调用，这点在公共服务中尤为重要
- 面向接口编程中的接口是用于隐藏具体实现和实现多态性的组件

### 什么是IOC

**IOC**：控制反转，控制权的转移，应用程序本身不负责依赖对象的创建和维护，而是由外部容器负责创建和维护

**DI**：（依赖注入）是其一种实现方式，由IOC容器在运行期间，动态的将某种依赖关系注入到对象之中

**目的**：创建对象并且组装对象之间的关系

**哪些方面的控制被反转了：获得依赖对象的过程被反转了**

控制什么：控制对象的创建及销毁（生命周期）

反转什么：将对象的控制权交给Ioc容器

### Bean容器的初始化

##### 基础包

- org.springframework.beans
- org.springframework.context
- BeanFactory提供配置结构和基本功能，加载并初始化Bean
- ApplicationContext保存了Bean对象并在Spring中被广泛使用

##### 方式 ApplicationContext

1. 文件

   ```
   FileSystemXmlApplicationContext context=new FileSystemXmlApplicationContext("F:/workspace/appcontext.xml");
   ```

2. Classpath

   ```
   ClassPathXmlApplicationContext context=new ClassPathXmlApplicationContext("classpath:spring-context.xml");
   ```

3. Web应用

   ```
   <listener>
       <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
   </listener> 
   
   <servlet>
      <servlet-name>context</servlet-name>
      <servlet-class>org.springframework.web.context.ContextLoaderListener</servlet-class>
      <load-on-startup>1</load-on-startup>
   </servlet>
   ```

### Spring的常用注入方式

在启动spring容器加载bean配置的时候，完成对变量的赋值行为，常见的注入方式有两种，如下：

1. 设值注入

   ```
   <!xml version="1.0" encoding="UTF-8">
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="
          http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
          http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">
          <bean id="oneInterface" class="com.imooc.ioc.interfaces.OneInterfaceImpl"></bean>
   </beans>
   ```

2. 构造注入

   ```
   <!xml version="1.0" encoding="UTF-8">
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="
          http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
          http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">
          <bean id="oneInterface" class="com.imooc.ioc.interfaces.OneInterfaceImpl"></bean>
   </beans>
   ```

   



# Spring学习三（spring Bean管理）

### 什么是Spring Beans

Spring beans是那些形成Spring应用的主干的Java对象

### Bean的生命周期

bean整个生命周期有定义---初始化---使用-----销毁

##### 初始化

- 实现org.springframework.beans.factory.InitializingBean接口，覆盖afterPropertiesSet方法，如下：

  ```
  public class ExampleInitializingBean implements InitializingBean{
      @Override
      public void afterPropertiesSet() throws Exception{
      //do something
  }
  }
  ```

- 配置init-method

  ```
  <bean id="exampleInitBean" class="examples.ExampleBean" init-method="init">
  ```

  ```
  public class ExampleBean{
     public void init(){
     //do someting
  }
  }
  ```

##### 销毁

- 实现org.springframeword.beans.factory.DisposableBean接口，覆盖destroy方法。

  ```
  public class ExampleDisposableBean implements DisposableBean{
      @Override
      public void destory() throws Exception{
      //do something
      }
  }
  ```

- 配置destory-method

  ```
  <bean id="exampleInitBean" class="examples.ExampleBean" destory-method="cleanup">
  ```

  ```
  public class ExampleBean{
     public void cleanup(){
     //do someting
  }
  }
  ```

##### 配置全局默认初始化，销毁方法

```
<!xml version="1.0" encoding="UTF-8">
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd"
       default-init-method="init" default-destroy-method="destroy">
```

### 实例化Bean

1. 通过构造方法实例化bean
2. 通过静态方法实例化bean
3. 通过实例化方法实例化bean
4. bean的别名

### Bean的配置

```
<!xml version="1.0" encoding="UTF-8">
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">
       <bean id="oneInterface" class="com.imooc.ioc.interfaces.OneInterfaceImpl"></bean>
</beans>
```

### Bean配置项

- **Id**：唯一标识
- **Class**：具体要实例化的类
- **Scope**：范围（Singleton单例，prototype）
- **Constructor arguments**：构造器的参数
- **Properties**：属性
- **Autowiring mode**：自动装配
- **Lazy-initialization mode**：懒加载
- **Initialization/destruction method**：初始化和销毁的方法

### Bean的作用域

- Singleton：单例，指一个bean容器中只存在一份
- Prototype：每次请求创建新的实例，destroy方式不生效
- Request：每次HTTP请求创建一个实例且仅在当前request内有效（仅在web项目中能用)
- Session：同上，每次HTTP请求创建，当前session内有效（仅在wenb项目中能用）
- Global session：基于portlet的web中有效，如果是在web中，同session（仅在web项目能用）

# Spring学习四（springAOP）

### 面向切面编程

编程范式分为五种：

- 面向过程编程
- 面向对象编程
- 函数式编程
- 事件驱动编程
- 面向切面编程

### AOP是什么

- 是一种思想，是一种编程范式，不是编程语言
- 解决特定问题，不能解决所有问题
- 是OOP的补充，不是替代、

### 为什么会有AOP

- Don't Repeat Yourself

- Separation of Concerns

  --水平分离：展示层->服务层->持久层

  --垂直分离：模块划分（订单，库存等）

  --切面分离：分离功能性需求和非功能性需求

### 使用AOP的好处

- 集中处理某一关注点/横切逻辑
- 可以方便地添加/删除关注点
- 侵入性少，增强代码可读性及可维护性

### AOP的应用场景

- 权限控制
- 缓存控制
- 事物控制
- 审计日志
- 性能监控
- 分布式追踪
- 异常处理

### AOP的使用

### AOP原理

### AOP开源运用

# 2019-4-24-spring学习五（spring基于AspectJ的AOP开发）

# 2019-4-24-spring学习六（JDBC Template）

# 2019-4-24-spring学习七（spring事务管理）

<https://zhuanlan.zhihu.com/p/37108469>

# Spring的一些注解

- @Required：适用于bean属性的setter方法，它表明受影响的bean属性在配置是必须放在xml配置文件中，否则      容器会抛出一个BeanInitializationException异常
- @Autowired  ：
  -  setter方法中的@Autowired当spring遇到一个在setter方法中使用的@Autowired注解，它会在方法红视图执行byType自动连接
  - 属性中的@Autowired他可以在属性中使用@Autowired注释来除去setter方法，当时使用为自动连接属性传递的时候，spring会将这些传递过来的值或者引用自动分配给那些属性
  - 构造函数中的@Autowired在构造函数中使用@Autowired，一个构造函数@Autowired说明当创建bean时，即使在xml文件中没有使用元素配置bean，构造函数也会自动连接
- @Qualifier：当你创建多个具有相同类型的bean时，并且想要用一个属性只为他们其中的一个进行装配，这种情况下，你可以使用@Qualifier注释和@Autowired注释通过指定哪一个真正的bean将会被装配来消除混乱，
- @Configuration：带有这个注释的类表示这个类可以使用spring ioc容器作为bean定义的来源
- @Bean： @Bean注解告诉spring，一个带有@Bean的注解方法将返回一个对象，该对象应该被注册为在spring应用程序上下文中的bean
- @Import：该注解允许从另一个配置类中加载@Bean定义