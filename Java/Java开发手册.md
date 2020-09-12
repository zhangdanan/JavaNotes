# Java中vo，po，bo等的区别

### VO 

value object值对象

ViewObject表现层对象

主要对应界面显示的数据对象。对于一个WEB页面，用一个VO对象对应整个界面的值。

### PO

persistant object持久对象

可以理解为数据库中的表的一条记录。

好处是可以把一条记录作为一个对象处理，可以方便的转为其它对象。

### POJO 

Plain Old Java Object 简单java对象

可以理解为VO和PO的父类。

一个POJO持久化以后就是PO

直接用它传递、传递过程中就是DTO

直接用来对应表示层就是VO

### BO

business object业务对象

主要作用是把业务逻辑封装为一个对象。这个对象可以包括一个或多个其它的对象。

用来处理业务逻辑

### DAO

data access object数据访问对象

主要用来封装对数据库的访问。通过它可以把POJO持久化为PO，用PO组装出来VO、DTO

### DTO 

Data Transfer Object数据传输对象

是一种设计模式之间传输数据的软件应用系统。数据传输目标往往是数据访问对象从数据库中检索数据。数据传输对象与数据交互对象或数据访问对象之间的差异是一个以不具有任何行为除了存储和检索的数据（访问和存取器）



作者：小飞鱼1986
链接：https://www.jianshu.com/p/58413c5c4395
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

# @EqualsAndHashCode 注解

这个注解会生成equals(Object other) 和 hashCode()方法。 
它默认使用非静态，非瞬态的属性 
可通过参数exclude排除一些属性 
可通过参数of指定仅使用哪些属性 
它默认仅使用该类中定义的属性且不调用父类的方法 
可通过callSuper=true解决上一点问题。让其生成的方法中调用父类的方法。
另：@Data相当于@Getter @Setter @RequiredArgsConstructor @ToString @EqualsAndHashCode这5个注解的合集。

通过官方文档，可以得知，当使用@Data注解时，则有了@EqualsAndHashCode注解，那么就会在此类中存在equals(Object other) 和 hashCode()方法，且不会使用父类的属性，这就导致了可能的问题。 


比如：

        有多个类有相同的部分属性，把它们定义到父类中，恰好id（数据库主键）也在父类中，那么就会存在部分对象在比较时，它们并不相等，却因为lombok自动生成的equals(Object other) 和 hashCode()方法判定为相等，从而导致出错。

解决方案： 

在使用@Data时同时加上@EqualsAndHashCode(callSuper=true)注解。（开发一般都会同时加上这两个注解）
————————————————
版权声明：本文为CSDN博主「selfimpr626」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_41888813/java/article/details/81530272

# CollectionUtils.isEmpty（）

　**例1: 判断集合是否为空:**
　　CollectionUtils.isEmpty(null): true
　　CollectionUtils.isEmpty(new ArrayList()): true　　
　　CollectionUtils.isEmpty({a,b}): false

　　**例2: 判断集合是否不为空:**
　　CollectionUtils.isNotEmpty(null): false
　　CollectionUtils.isNotEmpty(new ArrayList()): false
　　CollectionUtils.isNotEmpty({a,b}): true

#  StringUtils中 isNotEmpty 和isNotBlank的区别

```
isNotEmpty ：
判断某字符串是否非空
StringUtils.isNotEmpty(null) = false
StringUtils.isNotEmpty("") = false
StringUtils.isNotEmpty(" ") = true
StringUtils.isNotEmpty("bob") = true

isNotBlank：
判断某字符串是否不为空且长度不为0且不由空白符(whitespace)构成，
下面是示例：
StringUtils.isNotBlank(null) = false
StringUtils.isNotBlank("") = false
StringUtils.isNotBlank(" ") = false
StringUtils.isNotBlank("\t \n \f \r") = false
```

# Axios

**1.jQuery ajax**



```jsx
$.ajax({
   type: 'POST',
   url: url,
   data: data,
   dataType: dataType,
   success: function () {},
   error: function () {}
});
```

传统 Ajax 指的是 XMLHttpRequest（XHR）， 最早出现的发送后端请求技术，隶属于原始js中，核心使用XMLHttpRequest对象，多个请求之间如果有先后关系的话，就会出现**回调地狱**。
 JQuery ajax 是对原生XHR的封装，除此以外还增添了对**JSONP**的支持。经过多年的更新维护，真的已经是非常的方便了，优点无需多言；如果是硬要举出几个缺点，那可能只有：
 1.本身是针对MVC的编程,不符合现在前端**MVVM**的浪潮
 2.基于原生的XHR开发，XHR本身的架构不清晰。
 3.JQuery整个项目太大，单纯使用ajax却要引入整个JQuery非常的不合理（采取个性化打包的方案又不能享受CDN服务）
 4.不符合关注分离（Separation of Concerns）的原则
 5.配置和调用方式非常混乱，而且基于事件的异步模型不友好。
 **PS:MVVM(Model-View-ViewModel), 源自于经典的 Model–View–Controller（MVC）模式。MVVM 的出现促进了 GUI 前端开发与后端业务逻辑的分离，极大地提高了前端开发效率。MVVM 的核心是 ViewModel 层，它就像是一个中转站（value converter），负责转换 Model 中的数据对象来让数据变得更容易管理和使用，该层向上与视图层进行双向数据绑定，向下与 Model 层通过接口请求进行数据交互，起呈上启下作用。View 层展现的不是 Model 层的数据，而是 ViewModel 的数据，由 ViewModel 负责与 Model 层交互，这就完全解耦了 View 层和 Model 层，这个解耦是至关重要的，它是前后端分离方案实施的最重要一环。**
 如下图所示：

![img](https:////upload-images.jianshu.io/upload_images/6943526-cb96269b27bf3d2d.png?imageMogr2/auto-orient/strip|imageView2/2/w/966/format/webp)

image.png



**2.axios**



```jsx
axios({
    method: 'post',
    url: '/user/12345',
    data: {
        firstName: 'Fred',
        lastName: 'Flintstone'
    }
})
.then(function (response) {
    console.log(response);
})
.catch(function (error) {
    console.log(error);
});
```

Vue2.0之后，尤雨溪推荐大家用axios替换JQuery ajax，想必让axios进入了很多人的目光中。
 axios 是一个基于Promise 用于浏览器和 nodejs 的 HTTP 客户端，本质上也是对原生XHR的封装，只不过它是Promise的实现版本，符合最新的ES规范，它本身具有以下特征：
 1.从浏览器中创建 XMLHttpRequest
 2.支持 Promise API
 3.客户端支持防止CSRF
 4.提供了一些并发请求的接口（重要，方便了很多的操作）
 5.从 node.js 创建 http 请求
 6.拦截请求和响应
 7.转换请求和响应数据
 8.取消请求
 9.自动转换JSON数据
 **PS:防止CSRF:就是让你的每个请求都带一个从cookie中拿到的key, 根据浏览器同源策略，假冒的网站是拿不到你cookie中得key的，这样，后台就可以轻松辨别出这个请求是否是用户在假冒网站上的误导输入，从而采取正确的策略。**



作者：赵客缦胡缨v吴钩霜雪明
链接：https://www.jianshu.com/p/8bc48f8fde75
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

# UserAgentUtils   获取浏览器信息

`<dependency>`
    `<groupId>eu.bitwalker</groupId>`
    `<artifactId>UserAgentUtils</artifactId>`
    `<version>1.21</version>`
`</dependency>`

`import eu.bitwalker.useragentutils.Browser;`
`import eu.bitwalker.useragentutils.UserAgent;`
`import eu.bitwalker.useragentutils.Version;`

`Browser browser = UserAgent.parseUserAgentString(request.getHeader("User-Agent")).getBrowser();`
`Version version = browser.getVersion(request.getHeader("User-Agent"));`
`logger.info("获取浏览器信息:{},获取浏览器信息:{}",browser.getName(), version.getVersion());`
————————————————
版权声明：本文为CSDN博主「创客公元」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_37264997/java/article/details/88993729

借鉴https://blog.csdn.net/qq_23832313/article/details/82775316

# Optional

### 简介

Optional类是Java8为了解决null值判断问题，借鉴google guava类库的Optional类而引入的一个同名Optional类，使用Optional类可以避免显式的null值判断（null的防御性检查），避免null导致的NPE（NullPointerException）。

### orElse()

orElse()方法功能比较简单，即如果包装对象值非空，返回包装对象值，否则返回入参other的值（默认值）。

# 关于权限验证和登录

登录：当用户填写完账号和密码后向服务端验证是否正确，验证通过之后，服务端会返回一个**token**，拿到token之后（我会将这个token存贮到cookie中，保证刷新页面后能记住用户登录状态），前端会根据token再去拉取一个 **user_info** 的接口来获取用户的详细信息（如用户权限，用户名等等信息）。

权限验证：通过token获取用户对应的 **role**，动态根据用户的 role 算出其对应有权限的路由，通过 **router.addRoutes** 动态挂载这些路由。


作者：花裤衩
链接：https://juejin.im/post/591aa14f570c35006961acac
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

# 注解

### @RequestBody

@RequestBody主要用来接收前端传递给后端的json字符串中的数据的(请求体中的数据的);

### @PathVariable

通过 @PathVariable 可以将 URL 中占位符参数绑定到控制器处理方法的入参中：URL 中的 {xxx} 占位符可以通过@PathVariable(“xxx“) 绑定到操作方法的入参中。