# 2019-4-28-springMVC概述（一）

## 什么是Spring MVC

Spring MVC属于SpringFrameWork的后续产品，已经融合在Spring Web Flow里面。SpringMVC是一种web层mvc框架，用于替代servlet（处理|响应请求，获取表单参数，表单校验等。SpringMVC是一个MVC的开源框架，SpringMVC=struts2+spring，springMVC就相当于是Struts2加上Spring的整合。

## Spring MVC处理流程

1. `DispatcherServlet`把请求分发给`HandlerMapping`
2. `HandlerMapping`匹配到处理该url请求的`Controller、Interceptor`（根据xml配置、注解进行查找）返回给`DispatcherServlet`
3. `DispatcherServlet`调用`Interceptor、Controller`进行请求处理
4. `Controller`处理结果为`ModelAndView`返回给`DispatcherServlet`
5. `DispatcherServlet`调用`ViewResolver`渲染`ModelAndView`为最终的View，最终转为response返回给用户

Spring MVC的原理与组成图如下：

![springmvc01](https://github.com/aaaxma/JavaNote/blob/master/images/springmvc01.jpg)



##### SpringMvc的控制器是单例模式，所以在多线程访问的时候有线程安全问题，不要用同步，会影响性能，解决方案是在控制器里面不能用字段。



##### spring设定重定向和转发

在返回值前面加“forward” 可以实现结果转发

在返回值前面加“redirect” 可以返回值重定向



# 2019-5-8-springMVC九大组件（二

### Spring MVC中的Servlet

Spring MVC的Servlet一共有三个层次：

- HttpServletBean:继承与Java的HttpServlet，作用是将Servlet中配置的参数设置到相应的属性。
- FrameworkServlet:初始化了WebApplicationContext
- DispatcherServlet:初始化自身9个组件

DispatcherServlet的继承关系如下图：

![springmvc01](https://github.com/aaaxma/JavaNote/blob/master/images/springmvc02.jpg)

### DispatcherServlet的9个组件

1. **HandlerMapping**

   是用来查找Handler的。在SpringMVC中会有很多请求，每个请求都需要一个Handler处理，具体接收到一个请求之后使用哪个Handler进行处理呢？这就是HandlerMapping需要做的事。

2. **HandlerAdapterz**

   名字上看，它就是一个适配器。因为SpringMVC中的Handler可以是任意的形式，只要能处理请求就ok，但是Servlet需要的处理方法的结构却是固定的，都是以request和response为参数的方法。如何让固定的Servlet处理方法调用灵活的Handler来进行处理呢？这就是HandlerAdapter要做的事情。

   小结：Handler是用来干活的工具；HandlerMapping用于根据需要干的活找到相应的工具；HandlerAdapter是使用工具干活的人。

3. **HandlerExceptionResolver**

   对异常情况进行处理的组件，此组件的作用是根据异常设置ModelAndView，之后再交给render方法进行渲染。

4. **ViewResolver**

   ViewResolver用来将String类型的视图名和Locale解析为View类型的视图。View是用来渲染页面的，也就是将程序返回的参数填入模板里，生成html（也可能是其它类型）文件。这里就有两个关键问题：使用哪个模板？用什么技术（规则）填入参数？这其实是ViewResolver主要要做的工作，ViewResolver需要找到渲染所用的模板和所用的技术（也就是视图的类型）进行渲染，具体的渲染过程则交由不同的视图自己完成。

5. **RequestToViewNameTranslator**

   ViewName是根据ViewName查找View，但有的Handler处理完后并没有设置View也没有设置ViewName，这时就需要从request获取ViewName了，如何从request中获取ViewName就是RequestToViewNameTranslator要做的事情了。RequestToViewNameTranslator在Spring MVC容器里只可以配置一个，所以所有request到ViewName的转换规则都要在一个Translator里面全部实现。

6. **LocaleResolver**

   解析视图需要两个参数，一个是视图名，另一个是Locale，视图名是处理器返回的，Locale是从哪里来的呢？这就是LocaleResolver要做的事情，LocaleResolver用于从request解析出Locale,Locale就是zh-cn之类，表示一个区域，有了这个就可以对不同区域的用户显示不同的结果。SpringMVC主要有两个地方用到了Locale：一是ViewResolver视图解析的时候；二是用到国际化资源或者主题的时候。

7. **ThemeResolver**

   用于解析主题，SpringMVC中一个主题对应一个properties文件，里面存放着跟当前主题相关的所有资源，如图片，css样式等，SpringMVC的主题也支持国际化，同一个主题不同区域也可以显示不同的风格，SpringMVC中跟主题相关的类有ThemeResolver、ThemeSource和Theme，主题是同过一系列资源来具体体现的，要得到一个主题的资源，首先要得到资源的名称，这是ThemeResolver的工作，然后通过主题名称找到对于的主题（可以理解为一个配置）文件，这是Theme Source的工作，最后从主题中获取资源就可以了

8. **MultipartResolver**

   用来处理上传请求，处理方法就是将普通的request包装成MultipartHttpServletRequest，后者可以直接调用getFile方法获取File，如果上传多个文件，还可以调用getFileMap得到FileName->File结构的Map，此组件中一共有以下三个方法：

   ```
   boolean isMultipart(HttpServletRequest request);
   //是不是上传请求，是不是Multipart
   MultipartHttpServletRequest 
   resolveMultipart(HttpServletRequest request);
   //对请求的数据进行解析，然后将文件数据解析成MultipartFile并封装在MultipartHttpServletRequest对象中，最后传递给Controller
   void cleanupMultipart(MultipartHttpServletRequest request);
   //处理完后清理上传过程中产生的临时资源
   ```

9. **FlashMapManager**

   用来管理FlashMap的，FlashMap主要用来在redirect中传递参数