## Servlet 简介

### Servlet是什么

Servlet是运行在Web服务器或者应用服务器上的程序，它是作为来自Web浏览器或其他HTTP客户端的请求和HTTP服务器上的数据库或应用程序之间的中间层

### Servlet任务

- 读取客户端（浏览器）发送的显式的数据，也就是html表单
- 读取客户端（浏览器）发送的隐式的HTTP请求数据，包括cookies等
- 处理数据并生成结果，这个过程可能需要访问数据库
- 发送显式的数据（文档）到客户端（浏览器），包括html、xml、二进制文件、excel
- 发送隐式的HTTP响应到客户端（浏览器），包括告诉浏览器或其他客户端被返回的文档类型（html）,设置cookies和缓存参数，以及其他类似的任务。

## Servlet生命周期

### 生命周期过程

调用**init()**方法进行初始化------>调用**service()**方法处理客户端的请求------>调用**destroy()**方法结束------->由JVM的垃圾回收器进行垃圾回收

### init()方法

init()方法被设计只能调用一次，就是在第一次创建的时被调用，在后续每次用户请求时不在调用。init()方法简单的创建或加载一些数据，这些数据将被用于Servlet的整个生命周期。

init()方法的定义如下

```
public void init() throw ServletException{
       //初始化代码...
}
```

### Service()方法

service()方法时执行实际任务的主要方法，Servlet容器调用service()来处理来自客户端（浏览器）的请求，并把格式化的响应写回给客户端。

每次服务器接收到一个Servlet请求时，服务器会产生一个新的线程并调用服务，service()方法检查HTTP请求类型（GET、POST、PUT、DELETE）等，并在适当的时候调用doGet、doPost、doPut、doDelete等方法

```
public void service(ServletRequest request,ServletResponse response) throws ServletException,IOException{

}
```

### doPost()方法

POST请求来自一个特别指定了method为POST的HTML表单，它有doPost()方法处理

```
public void doPost(HttpServletRequest request,HttpServletResponse response) throws ServletException,IOException{
     //Servlet代码
}
```

### doGet()方法

GET请求来自于一个url的正常请求，或者来自一个未指定method的html表单，它由都doGet()方法处理

```
public void doGet(HttpServletRequest request,HttpServletResponse response) throws ServletException,IOException{
     //Servlet代码
}
```

### destroy()方法

destroy()方法只会被调用一次，在Servlet生命周期结束时被调用，destroy()方法可以让你的Servlet关闭数据库连接，停止后台线程，把Cookie列表或点击计数器写入到磁盘，并执行其他类似的清理活动，在调用destroy()方法之后，servlet对象被标记为垃圾回收。

```
public void destroy(){
    //终止代码
}
```

## Servlet处理表单数据

### 常用方法

- getParameter()：获取表单参数的值
- getParameterValues()：如果参数出现一次以上，则调用该方法，并返回多个值，例如复选框。
- getParameterNames()：如果你想要得到当前请求中的所有参数的完整列表，这调用该方法。

## Servlet 编写过滤器

