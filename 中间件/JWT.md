# JWT是啥

```
json  web  token// 一般用于用户认证（前后端分离/微信小程序/App）
```

本文的目标是让你学习JWT的工作原理和细节，以及它在Web应用中能如何帮助你实现用户认证和会话管理功能。那为什么需要深入理解JWT呢？因为这样有助于你：

1. 实现一个基于JWT的认证方案；
2. 各种故障排查：理解错误信息、堆栈信息；
3. 选择第三方库，并理解他们的文档；
4. 自己实现认证方案；
5. 选择和配置第三方认证服务；

即使选择了某个基于JWT的认证方案，同样还需要进行代码编写，编码工作主要是在客户端，但服务端也需要一些。

到本文的结尾，你将深刻理解JWT，包括它基于的加密技术，这种加密技术也广泛使用在其他安全案例中。你还将明白什么时候该用JWT和为什么要使用，同时理解JWT的数据格式，可以使用各种线上工具去分析解决签名上遇到的问题。

为什么是JWT？

相比在内存中存储随机token的用户会话管理方式来说，JWT最大的优势是，它使得将认证逻辑委托给第三方服务成为可能，这些服务包括：

1. 自己开发的、中心化的认证服务器；
2. 能生成JWT的LDAP服务；
3. 完全是外部的第三方认证服务提供商，比如Auth0；

外部认证服务可以完全独立于我们自己的应用服务，并且不需要通过网络共享任何密钥信息。应用服务器不需要安装任何密钥，减少了密钥丢失或者被盗窃的风险。

此外，应用服务可以完全无状态，因为不需要在多个请求之间将token存储在内存。认证服务可以在生成token并返回给客户端后，马上丢弃它！同样，密码摘要也没有必要保存在应用数据库中，因此减少了被盗的风险和其它安全相关的bug。

此刻也许你心里想：我有一个内部应用，对此，JWT是一个好的方案吗？是的，在本文的最后一节里，我们将讨论JWT在这种典型场景下的使用情况。

- **目录**

本文我们将讨论以下这些话题：

1. 什么是JWT？
2. JWT在线验证工具；
3. JWT的格式；
4. JWT的核心要素: Header, Payload, Signature；
5. Base64Url (vs Base64)；
6. 使用JWT进行会话管理: 主题和期限
7. HS256签名 – 它是如何工作的？
8. 数字签名；
9. 哈希函数和SHA-256；
10. RS256 JWT签名 – 谈谈公钥加密；
11. RS256 vs HS256 签名 – 哪种方式更好？
12. JWKS (JSON Web Key Set) 端点(Endpoints)；
13. 如何实现JWT签名的周期性键旋转(Periodic Key Rotation)；
14. JWT在企业应用中的使用；
15. 归纳和结论；

- **JWT是什么?**

JSON Web Token (or JWT)只是一个包含某种意义数据的JSON串。它最重要的特性就是，为了确认它是否有效，我们只需要看JWT本身的内容，而不需要借助于第三方服务或者在多个请求之间将其保存在内存中-这是因为它本身携带了信息验证码MAC(Message Authentication Code)。

一个JWT包含3个部分：头部Header，数据Payload，签名Signature。让我们逐个来了解一下，先从Payload开始吧。

- **JWT Payload看起来是怎样的呢?**

Payload只是一个普通的Javascript 对象。对于payload的内容，JWT是没有任何限制的，但必须注意的是，JWT是没有加密的。因此，任何放在token里面的信息，如果被截获了，对任何人别人是可读的。因此，我们不应该在Payload里面存放任何黑客可以利用的用户信息。

- **JWT Header – 为什么是必须的?**

Payload的内容在接收者端是通过签名(Signature)来校验的。不过存在多种类型的签名，因此，接收者需要知道使用的是哪种类型的签名。

这种关于token本身的元数据信息存放在另外的Javascript对象里面，并随着Payload一起发送给客户。这个独立的对象就是一个JSON对象，叫JWT Header，它也是普通的Javascript对象，在这里面我们可以看到签名类型信息，比如RS256。

- **JWT signatures – 如何被使用来完成认证的?**

JWT的最后一部分是签名，它也叫信息验证码MAC。签名只能由拥有Payload、Header和密钥的角色生成。

那签名是如何完成认证功能的呢，且看：

1. 用户向认证服务器提交用户名和密码，认证服务器也可以和应用服务器部署在一起，但往往是独立的居多；
2. 认证服务器校验用户名和密码组合，然后创建一个JWT token，token的Payload里面包含用户的身份信息，以及过期时间戳；
3. 认证服务器使用密钥对Header和Payload进行签名，然后发送给客户浏览器；
4. 浏览器获取到经过签名的JWT token，然后在之后的每个HTTP请求中附带着发送给应用服务器。经过签名的JWT就像一个临时的用户凭证，代替了用户名和密码组合，之后都是JWT token和应用服务器打交道了；
5. 应用服务器检查JWT签名，确认Payload确实是由密钥拥有者签过名的；
6. Payload身份信息代表了某个用户；
7. 只有认证服务器拥有私钥，并且认证服务器只把token发给提供了正确密码的用户；
8. 因此应用服务器可以认为这个token是由认证服务器颁发的也是安全的，因为该用户具有了正确的密码；
9. 应用服务器继续完成HTTP请求，并认为这些请求确实属于这个用户；

这样的话，黑客假扮合法用户的办法要么是盗到了用户名和密码组合，要么盗到了认证服务器上的签名私钥。

正如我们所见，签名的确是JWT的关键部分！

签名使得无状态的服务器只需要通过查看HTTP请求中的JWT token就能保证HTTP请求是来自某个用户，而不需要每次请求时都发送密码。

- **JWT的目标是让服务器无状态?**

实际上，JWT真正的好处是让认证服务器和校验JWT token的应用服务器可以完全分开，而让服务器无状态化只是它的一个副作用罢了。这意味着应用服务器只需要最简单的认证逻辑-校验JWT！我们可以将整个应用集群的登录/注册委托给一个单独的认证服务器。这也意味着应用服务器更简单更安全，因为更多的认证功能集中部署在认证服务器，可以被跨应用使用。

到此，我们从更高的层面了解了JWT是怎样完成无状态的第三方认证，接下来让我们了解它的实现细节。

- **JSON Web Token看起来是怎样的呢?**

让我们来看看JWT的实际例子，这是从[http://jwt.io](https://link.zhihu.com/?target=http%3A//jwt.io)的JWT校验工具得到的：

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```

你可能会想，JSON对象去哪了啊？不过，你会马上找回它。

我们可以看到，这个JWT包含3部分，是由“.”号分开的。第一部分是JWT的Header：

JWT Header:

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
```

第二部分是Payload:

JWT Payload:

```text
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9
```

第三方部分是签名Signature:

JWT Signature:

```text
TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```

如果你还想确认这些信息是否真的存在，可以拷贝JWT串到[http://jwt.io](https://link.zhihu.com/?target=http%3A//jwt.io)的在线校验工具校验一下即可。

但这些字符串代表什么意思呢？我们如何取回JWT的信息？

- **Base64，抑或是Base64Url?**

不管你信不信，现在的Payload，Header和Signature还是可读的。这只是因为我们不想在网络传输过程中出现一些垃圾文本，比如这样的字符串：qÃ®Ã¼Ã¶:Ã。

这是因为世界上不同的计算机以不同的编码方式处理字符串，比如UTF-8，ISO 8859-1，等等。因此，这种问题到处存在，只要我们在某个平台上用到一个字符串，它总是使用了某种编码方式，即使我们没有显示指定：

1. 操作系统的默认编码方式；
2. 服务器上的配置的编码参数；

我们希望在网络上传输字符串时没有这些问题，那就需要选择这些字符的一个子集，对于这个子集，几乎所有的编码方式都是一样的处理方式，这就是Base64编码方式产生的原因。

- **Base64 vs Base64Url**

但是我们在JWT看到的并不是Base64，实际上是Base64Url，它和Base64类似，但有一些字符不一样，因此我们可以将JWT作为URL的参数进行传递。

我们看一下Payload部分：

```text
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9
```

我们使用在线解码器来解析它，就得到了一个JSON对象，因此，我们可以得到这样的结论：JWT Header和Payload的内容是普通的javascript对象，转换成JSON并进行Base64Url编码，以“.”号隔开。

在学习签名Signature之前，我们先来看看在实际的用户认证案例中，我们是将哪些内容放入Payload中的。

- **基于JWT的用户会话管理: 主题和期限**

之前有提到，JWT的Payload理论上可以存放任何内容，不一定是用户身份信息，只不过使用JWT作为认证是最常用的方式。Payload还有一些特定的属性来支持：

1. 用户身份
2. 会话过期

这里是Payload的几个最常用的标准属性：

· iss 代表生成token的实体，一般就是认证服务器

· iat 创建JWT的时间戳(in seconds since Epoch)

· sub 包含用户的身份信息

· exp token的过期时间戳

我们把这叫做Bearer Token，意思是:

***认证服务器确认这个token的持有者是具有由sub属性表示的ID的用户，因此可以放行。***

现在我们理解了Payload在用户认证中是如何使用的，接下来我们来了解一下签名Signature。对于JWT，签名方式有很多种，这里我们主要了解HS256和RS256。

我们先来看看HS256.

- **HS256 JWT数字签名 – 它是如何工作的?**

和很多签名方法一样，HS256 数字签名基于一种特殊的函数：加密哈希函数。

这听起来有点唬人，不过是个值得学习的概念：这个知识已经被使用了20多年并还会持续很长时间。很多关于安全的实现都围绕着哈希，它在Web安全中随处可见。

我们将分为两步，首先要了解什么是哈希函数，然后再看通过这样的函数和密码，如何生成信息认证码(Message Authentication Code)，也就是数字签名。

- **什么是哈希函数(Hashing function)?**

哈希函数是一种特殊的函数：它在数字签名中有很多实际的使用案例。现在我们将谈论它四个有趣的属性，然后看看这些属性如何使得我们可以生成可校验的签名。这里我们将使用的哈希函数是：SHA-256。

- **哈希函数属性 1 – 不可逆性**

哈希函数有点类似绞肉机：你把牛排放入一端，然后从另一端得到汉堡包，你再也无法从汉堡包取回牛排了。因此，函数是完全不可逆的。这就意味着我们把Header和Payload作用于这个函数后，没有人可以从函数输出的信息中取回Header和Payload的原始值。

使用在线的哈希计算器，我们可以看到SHA-256的一个输出值如下：

```text
3f306b76e92c8a8fbae88a3ef1c0f9b0a81fe3a953fa9320d5d0281b059887c3
```

同时，哈希并不是加密，加密在定义中是可逆的，我们总是需要从加密后的信息中得到原始信息。

- **哈希函数属性 2 – 可重复生成**

另外一个需要知道的是，哈希函数是可重复生成信息的，也就是如果我们输入同样的Header和Payload信息，每次得到的结果是完全一样的。这就意味着，给定输入组合和哈希输出值，我们总是可以校验该输出值(比如签名signature)的正确性，因为我们可以重新计算(我们有输入值的情况下)。

- **哈希函数属性 3 – 没有冲突**

还有一个属性是，如果我们提供不同的输入值，总是得到不同的唯一的输出值。这就意味着我们将哈希函数作用于某个Payload和Header之后，总是得到相同的结果，其它输入值组合不会得到和这一样的结果，因此，哈希函数的不同输出值就代表了输入值的不同。

- **哈希函数属性 4 – 不可预测性**

哈希函数的最后一个属性就是不可预测性，给定一个输出值，无法通过各种手段猜测到输入值。假设我们尝试从上面的输出值中找到生成它的Payload，我们只能猜测输入值然后对比输出值看看是否匹配。

但对于哈希函数来说，这种方式是不可行的：

这是因为在哈希函数中，即使你改变了一个输入字符甚至一个比特值，输出中一般有50%的比特值都会被改变，输入值小小的变动，可能会得到完全不同的输出值。

这些听起来挺有趣的，不过你可能又在想了：哈希函数是怎样完成数字签名的呢？黑客是否可以拿着Header和Payload，而不管Signature呢？任何人都可以使用SHA-256哈希函数生成一个输出，然后附加到JWT的signature部分，对吧？

- **怎样使用哈希函数生成签名?**

这是正确的，任何人都可以使用哈希函数，然后输入Header和Payload来生成结果。但HS256签名不止这样，我们拿到Header、Payload外，还要加上一个密码，将这三个输入值一起哈希。输出结果是一个SHA-256 HMAC或者基于哈希的MAC。如果需要重复生成，则需要同时拥有Header、Payload和密码才可以。这也意味着，哈希函数的输出结果是一个数字签名，因为输出结果就表示了Payload是由拥有密码的角色生成并加签了的，没有其它方式可以生成这样的输出值了。

将哈希结果附加到消息上，是为了让接收者可以验证。哈希结果叫HMAC：Hash-Based Message Authentication Code，是数字签名的一种形式。这就是我们在JWT中所做的，JWT的第三部分是由Header、Payload通过SHA-256函数生成，并使用Base64Url进行编码。

- **如何校验JWT签名?**

当我们的服务接收到HS256签名的JWT时，我们需要使用同样的密码才能校验并确认token里面的Payload是否有效。为了验证签名，我们只需要将JWT Header和Payload以及密码通过哈希函数生成结果。如果是使用HS256函数，JWT的接收者需要拿到和发送者一样的密码值。如果我们得到的哈希结果和JWT第三部分的签名值是一致的，则说明有效，可以确认发送者确实和接收者拥有相同的密码值。

而数字签名和HMAC又是如何工作的呢？

- **手动确认SHA-256 JWT签名**

我们从之前的JWT中去掉签名和第二个“.”，只留下Header和Payload部分。看起来如下：

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9
```

现在如果你拷贝这个字符串到在线的HMAC SHA-256工具，并使用上密码，就可以取回JWT签名。或者，你会得到Base64编码后的内容，后面还有一个“=”字符，这算是已经接近Base64Url：

TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ=

那个“=”在URL栏中会显示为“%3D”，会显得混乱，这也解释了在我们把JWT拼接到URL发送时，需要Base64Url的原因。

- **为什么需要其它的签名类型呢?**

以上解释了JWT签名是如何应用于认证的，HS256只是一种具体的签名类型。其它的签名类型中，最常用的是：RS256。

有什么区别呢？我们介绍HS256只是为了更容易理解MAC码的概念， 你可能也会发现它在一些生产环境的应用中被使用。但是一般来说，使用RS256签名方式会更好，下一节我们将看到，RS256相对于HS256来说有诸多优势。

- **HS256签名方式的劣势**

如果输入的密码相对弱的话，HS256可能会被暴力破解，基于密钥的技术都有这个问题。更甚的是，HS256要求JWT的生产者和消费者都预先拥有相同的密码。

- **不切实际的密码分发**

这意味着我们在修改密码后，需要把它分发并安装到所有需要它的网络节点。这不仅不方便，而且容易出错，还涉及到服务器间的协调和暂停服务问题。如果服务器是由另外的团队维护，比如第三方组织，这种方式就更不可行了。

- **Token的创建和校验没有分离**

创建和校验JWT的能力没有区分开，使用HS256时，网络的任何人都可以创建和校验token，因为他们都有密码。这就意味着密码可能会从更多的地方丢失或者受攻击，因为密码到处分发，而并不是每个应用都具有一样的安全保护机制。

弥补这问题的一个方法是，创建一个共享的密码给每一种类型的应用。不过，我们马上要学习新的签名方式，这个签名方式解决了以上所有的问题，并且目前所有基于JWT的方案都默认使用的，那就是RS256。

- **RS256 JWT签名**

使用RS256我们同样需要生成一个MAC，其目的仍然是创建一个数字签名来证明一个JWT的有效性。只是在这种签名方式中就，我们将创建token和校验token的能力分开，只有认证服务器具备创建的能力，而应用服务器，具备校验的能力。

这样，我们需要创建两个密钥而不是一个：

1. 仍然需要一个私钥，不过这次它只能被认证服务器拥有，只用来签名JWT。
2. 私钥只能用来签名JWT，不能用来校验它。
3. 第二个密钥叫做公钥(public key)，是应用服务器使用来校验JWT。
4. 公钥可以用来校验JWT，但不能用来给JWT签名。
5. 公钥一般不需要严密保管，因为即便黑客拿到了，也无法使用它来伪造签名。

- **RSA加密技术介绍**

RS256使用一种特殊的密钥，叫RSA密钥。RSA是一种加解密算法，使用一个密钥进行加密，然后用另外一个密钥解密。值得注意的是，RSA不是哈希函数，从定义上来说，这种方式加密是可逆的，也就是我们可以从加密后的内容得到原始内容。

来看一下RSA公钥是怎样的:

—–BEGIN PUBLIC KEY—–

```text
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDdlatRjRjogo3WojgGHFHYLugdUWAY9iR3fy4arWNA1KoS8kVw33cJibXr8bvwUAUparCwlvdbH6dvEOfou0/gCFQsHUfQrSDv+MuSUMAe8jzKE4qW+jK+xQU9a03GUnKHkkle+Q0pX/g6jXZ7r1/xAK5Do2kQ+X5xK9cipRgEKwIDAQAB
```

—–END PUBLIC KEY—–

乍一看有点古怪，但它是使用命令行工具比如openssl 或者在线的RSA密钥生成工具来生成的。

这个公钥是公开发布的，因此黑客根本不需要猜测，他本来就可以拥有它。

但这里还有一个RSA私钥:

—–BEGIN RSA PRIVATE KEY—–

```text
MIICWwIBAAKBgQDdlatRjRjogo3WojgGHFHYLugdUWAY9iR3fy4arWNA1KoS8kVw33cJibXr8bvwUAUparCwlvdbH6dvEOfou0/gCFQsHUfQrSDv+MuSUMAe8jzKE4qW+jK+xQU9a03GUnKHkkle+Q0pX/g6jXZ7r1/xAK5Do2kQ+X5xK9cipRgEKwIDAQABAoGAD+onAtVye4ic7VR7V50DF9bOnwRwNXrARcDhq9LWNRrRGElESYYTQ6EbatXS3MCyjjX2eMhu/aF5YhXBwkppwxg+EOmXeh+MzL7Zh284OuPbkglAaGhV9bb6/5CpuGb1esyPbYW+Ty2PC0GSZfIXkXs76jXAu9TOBvD0ybc2YlkCQQDywg2R/7t3Q2OE2+yo382CLJdrlSLVROWKwb4tb2PjhY4XAwV8d1vy0RenxTB+K5Mu57uVSTHtrMK0GAtFr833AkEA6avx20OHo61Yela/4k5kQDtjEf1N0LfI+BcWZtxsS3jDM3i1Hp0KSu5rsCPb8acJo5RO26gGVrfAsDcIXKC+bQJAZZ2XIpsitLyPpuiMOvBbzPavd4gY6Z8KWrfYzJoI/Q9FuBo6rKwl4BFoToD7WIUS+hpkagwWiz+6zLoX1dbOZwJACmH5fSSjAkLRi54PKJ8TFUeOP15h9sQzydI8zJU+upvDEKZsZc/UhT/SySDOxQ4G/523Y0sz/OZtSWcol/UMgQJALesy++GdvoIDLfJX5GBQpuFgFenRiRDabxrE9MNUZ2aPFaFp+DyAe+b4nDwuJaW2LURbr8AEZga7oQj0uYxcYw==
```

—–END RSA PRIVATE KEY—–

好消息是，黑客没有任何办法猜测私钥。

而且，这两个密钥是相关的，一个密钥加密的内容只能由另外的密钥来解密。那我们又如何用它们生成签名呢？

- **为什么不用RSA加密Payload就完了?**

现在尝试着使用RSA来生成一个数字签名:

我们使用Header和Payload，然后使用私钥对其进行RSA加密，最后返回JWT。

接收者拿到JWT后，使用公钥解密，然后检查解密后的值。如果解密过程顺利并且其输出是一个JSON值，往往就意味着该JWT就是认证服务器创建并加密了的。

相比哈希函数，RSA加密过程比较慢。对于数据比较大的Payload来说，可能会是个问题。

那HS256签名方式在实际中又是如何使用RSA的呢?

- **使用RSA和SHA-256签名JWT (RSA-SHA256)**

在实际中，我们一般先将Header和Payload一起哈希，比如使用SHA-256。这个速度是很快的，这样我们就得到了一个代表输入数据的唯一表示，比实际输入数据要小得多。

然后我们使用RSA对哈希结果而不是完整的数据(Header+Payload)进行加密，就得到了RS256签名。我们将这个签名附加到JWT的第三部分，然后返回给客户端。

- **接收者是怎样检查RS256签名的?**

接收者将:

1. 取出Header和Payload，然后使用SHA-256进行哈希。
2. 使用公钥解密数字签名，得到签名的哈希值。
3. 接收者将解密签名得到的哈希值和刚使用Header和Payload参与计算的哈希值进行比较。如果两个哈希值相等，则证明JWT确实是由认证服务器创建的。

任何人都可以计算哈希值，但只有认证服务器可以使用RSA私钥对其进行加密。

接下来我们学习一下在RS256签名中遇到问题时的解决思路。

- **手工确认RS256 JWT签名**

我们看下[http://jwt.io](https://link.zhihu.com/?target=http%3A//jwt.io)上的例子，一个使用RS256加签的JWT。

```text
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.EkN-DOsnsuRjRO6BxXemmJDm3HbxrbRzXglbN2S4sOkopdU4IsDxTI8jO19W_A4K8ZPJijNLis4EZsHeY559a4DFOd50_OqgHGuERTqYZyuhtF39yxJPAjUESwxk2J5k_4zM3O-vtd1Ghyo4IbqKKSy6J9mTniYJPenn5-HIirE
```

从表面上看，这和HS256 JWT没有多大区别，但这是使用前面展示的同一个RSA私钥加签了的。

我们把签名部分去掉，只看Header和Payload:

```text
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9
```

现在我们需要做的就是使用SHA-256对其进行哈希，然后使用上面的RSA私钥进行加密。这样得到的结果就是JWT签名，我们可以使用Node的内嵌模块Crypto来确认。

首先，我们把RSA私钥保存到一个文本文件，比如叫private.key。然后在命令行运行node shell，执行一个小程序，得到下面的结果：

```text
 EkN+DOsnsuRjRO6BxXemmJDm3HbxrbRzXglbN2S4sOkopdU4IsDxTI8jO19W/A4K8ZPJijNLis4EZsHeY559a4DFOd50/OqgHGuERTqYZyuhtF39yxJPAjUESwxk2J5k/4zM3O+vtd1Ghyo4IbqKKSy6J9mTniYJPenn5+HIirE=
```

这个结果和JWT签名完全不同，不过等等，这里面还有斜杠和等号。如果不进一步处理，这是没法放到URL里面的。

这是因为我们生成的是Base64 版本的签名，而我们真正需要的是Base64Url 版本的。我们尝试转换一下:

bash$ node

const base64url = require(‘base64url’);

```text
base64url.fromBase64("EkN+DOsnsuRjRO6BxXemmJDm3HbxrbRzXglbN2S4sOkopdU4IsDxTI8jO19W/A4K8ZPJijNLis4EZsHeY559a4DFOd50/OqgHGuERTqYZyuhtF39yxJPAjUESwxk2J5k/4zM3O+vtd1Ghyo4IbqKKSy6J9mTniYJPenn5+HIirE=");
```

得到下面的结果:

```text
EkN-DOsnsuRjRO6BxXemmJDm3HbxrbRzXglbN2S4sOkopdU4IsDxTI8jO19W_A4K8ZPJijNLis4EZsHeY559a4DFOd50_OqgHGuERTqYZyuhtF39yxJPAjUESwxk2J5k_4zM3O-vtd1Ghyo4IbqKKSy6J9mTniYJPenn5-HIirE
```

这就是我们真正想要创建的RS256签名了！也证明了我们对RS256 JWT签名的理解是正确的，而且我们知道了在遇到问题时如何去分析解决。

总之，RS256 JWT签名就是使用RSA对Header和Payload的哈希值进行加密的结果。现在我们知道RS256签名是如何工作的了，但这些签名为什么好于HS256签名呢？

- **RS256签名 vs HS256 – 为什么使用RS256?**

使用RS256，黑客可以轻松实现创建签名的第一步，即根据盗来的JWT Header和Payload生成SHA-256哈希值，之后他还要暴力破解RSA才能继续生成签名。

但这还不是我们为什么选择RS256而不是HS256的客观原因。

我们知道，使用RS256时，私钥只有认证服务器持有，这就安全得多- 加签密钥丢失的风险降低了。然而选择RS256更重要的理由是-简化密钥分发。

- **如何进行密钥分发部署**

还记得之前我们说过，用来校验token的公钥可以随意分发，黑客无法使用它来做任何有意义的事情。然而黑客并不是想校验token，他们只是想伪造它们。这就使得我们将公钥放置到受我们自己控制的服务器上成为可能。

应用服务器连接到公钥放置的服务器获取公钥，然后定期检查公钥是否有变化。因此，在更新密钥时，应用服务器和认证服务器不需要同时暂停服务。

那公钥又如何分发呢？下面是一种可行的格式。

- **JSON Web Key Set Endpoints**

有多种发布公钥的格式，但这里有一种较为熟悉：JWKS，全称Json Web Key Set。

如果你好奇这些endpoints 看起来是怎样的，可以看一下这个线上例子live example，下面这个是我们从HTT GET请求得到的回复：

Kid是密钥身份, x5c是某种公钥的表示法。这种格式的优点是其标准化，我们只需要知道endpoint的URL，和一个可以解析JWKS的库，就可以使用公钥来校验JWT了，而不需要安装到自己的服务器。

JWT常常使用在公共网站上，以及社交产品的登录方案中。对于内部系统，它是怎么被使用的呢?

- **JWT在企业中的应用**

JWT同样适用于企业内部，替代经典的存在已知安全隐患的预身份验证设置(Pre-Authentication setup)方式。

预身份验证设置方式中，我们的应用服务器在私有网络的一个代理后面运行，然后从HTTP请求头中获取当前用户信息。代表用户身份的HTTP请求头通常由中心化的登录页面填充，同时中心化的节点也对用户session进行管理。

当session过期后，服务器将阻止对应用的访问，并要求用户重新登录认证。之后，它将所有请求转发到应用服务器并在HTTP请求头添加代表用户身份的信息。

***问题是这种设置方式，内网上的任何人都可以假扮成某个用户，只要设置同样的HTTP请求头。\***

对此也有一些解决方案，比如白名单列表，或者某种客户凭证。

- **更好的预身份验证设置方式**

预身份验证设置方式是一个好主意，毕竟这种方式可以使得应用开发者不需要实现认证逻辑，减少开发时间和潜在的安全问题。

如果能有预身份验证设置方式的便捷，又没有安全方面的妥协，岂不美哉？

如果我们考虑到JWT，则可以轻松做到。我们不像以往那样将用户名放到HTTP请求头，而是将HTTP请求头封装成一个JWT。我们将用户名放到Payload里面，再由认证服务器加签。

应用服务器不再从HTTP请求头获取用户名，而是首先校验JWT：

1. 如果签名是正确的，则用户认证通过，请求可以放行；
2. 否则，应用服务器简单的拒绝请求就好了；

这样的结果就是，即使在私有网络内，我们的认证功能也可以正常工作。我们再也不需要通过HTTP请求头来识别用户了，我们保证了HTTP请求头的有效性并且是由代理生成的，而不是某黑客试图以某个用户身份登录。

- **总结**

通过本文，我们对JWT是什么有了一个全面的了解，以及它是如何在认证中被使用的。JWT只是一个简单的JSON对象，并且易于验证、难于伪造。

此外，JWT并不是一定要用来做认证的，我们可以使用JWT在网络上发送各种数据。

另外一个和安全相关的使用JWT的情况是授权：我们可以在Payload里面放置用户的角色列表，比如只读用户、管理员等等，对用户在应用服务器上的行为进行限制。

好了，本文到此结束，祝你阅读愉快！

文章来源：[想全面理解JWT？一文足矣！](https://link.zhihu.com/?target=https%3A//www.nndev.cn/archives/1925)本文的目标是让你学习JWT的工作原理和细节，以及它在Web应用中能如何帮助你实现用户认证和会话管理功能。那为什么需要深入理解JWT呢？因为这样有助于你：

1. 实现一个基于JWT的认证方案；
2. 各种故障排查：理解错误信息、堆栈信息；
3. 选择第三方库，并理解他们的文档；
4. 自己实现认证方案；
5. 选择和配置第三方认证服务；

即使选择了某个基于JWT的认证方案，同样还需要进行代码编写，编码工作主要是在客户端，但服务端也需要一些。

到本文的结尾，你将深刻理解JWT，包括它基于的加密技术，这种加密技术也广泛使用在其他安全案例中。你还将明白什么时候该用JWT和为什么要使用，同时理解JWT的数据格式，可以使用各种线上工具去分析解决签名上遇到的问题。

为什么是JWT？

相比在内存中存储随机token的用户会话管理方式来说，JWT最大的优势是，它使得将认证逻辑委托给第三方服务成为可能，这些服务包括：

1. 自己开发的、中心化的认证服务器；
2. 能生成JWT的LDAP服务；
3. 完全是外部的第三方认证服务提供商，比如Auth0；

外部认证服务可以完全独立于我们自己的应用服务，并且不需要通过网络共享任何密钥信息。应用服务器不需要安装任何密钥，减少了密钥丢失或者被盗窃的风险。

此外，应用服务可以完全无状态，因为不需要在多个请求之间将token存储在内存。认证服务可以在生成token并返回给客户端后，马上丢弃它！同样，密码摘要也没有必要保存在应用数据库中，因此减少了被盗的风险和其它安全相关的bug。

此刻也许你心里想：我有一个内部应用，对此，JWT是一个好的方案吗？是的，在本文的最后一节里，我们将讨论JWT在这种典型场景下的使用情况。

- **目录**

本文我们将讨论以下这些话题：

1. 什么是JWT？
2. JWT在线验证工具；
3. JWT的格式；
4. JWT的核心要素: Header, Payload, Signature；
5. Base64Url (vs Base64)；
6. 使用JWT进行会话管理: 主题和期限
7. HS256签名 – 它是如何工作的？
8. 数字签名；
9. 哈希函数和SHA-256；
10. RS256 JWT签名 – 谈谈公钥加密；
11. RS256 vs HS256 签名 – 哪种方式更好？
12. JWKS (JSON Web Key Set) 端点(Endpoints)；
13. 如何实现JWT签名的周期性键旋转(Periodic Key Rotation)；
14. JWT在企业应用中的使用；
15. 归纳和结论；

- **JWT是什么?**

JSON Web Token (or JWT)只是一个包含某种意义数据的JSON串。它最重要的特性就是，为了确认它是否有效，我们只需要看JWT本身的内容，而不需要借助于第三方服务或者在多个请求之间将其保存在内存中-这是因为它本身携带了信息验证码MAC(Message Authentication Code)。

一个JWT包含3个部分：头部Header，数据Payload，签名Signature。让我们逐个来了解一下，先从Payload开始吧。

- **JWT Payload看起来是怎样的呢?**

Payload只是一个普通的Javascript 对象。对于payload的内容，JWT是没有任何限制的，但必须注意的是，JWT是没有加密的。因此，任何放在token里面的信息，如果被截获了，对任何人别人是可读的。因此，我们不应该在Payload里面存放任何黑客可以利用的用户信息。

- **JWT Header – 为什么是必须的?**

Payload的内容在接收者端是通过签名(Signature)来校验的。不过存在多种类型的签名，因此，接收者需要知道使用的是哪种类型的签名。

这种关于token本身的元数据信息存放在另外的Javascript对象里面，并随着Payload一起发送给客户。这个独立的对象就是一个JSON对象，叫JWT Header，它也是普通的Javascript对象，在这里面我们可以看到签名类型信息，比如RS256。

- **JWT signatures – 如何被使用来完成认证的?**

JWT的最后一部分是签名，它也叫信息验证码MAC。签名只能由拥有Payload、Header和密钥的角色生成。

那签名是如何完成认证功能的呢，且看：

1. 用户向认证服务器提交用户名和密码，认证服务器也可以和应用服务器部署在一起，但往往是独立的居多；
2. 认证服务器校验用户名和密码组合，然后创建一个JWT token，token的Payload里面包含用户的身份信息，以及过期时间戳；
3. 认证服务器使用密钥对Header和Payload进行签名，然后发送给客户浏览器；
4. 浏览器获取到经过签名的JWT token，然后在之后的每个HTTP请求中附带着发送给应用服务器。经过签名的JWT就像一个临时的用户凭证，代替了用户名和密码组合，之后都是JWT token和应用服务器打交道了；
5. 应用服务器检查JWT签名，确认Payload确实是由密钥拥有者签过名的；
6. Payload身份信息代表了某个用户；
7. 只有认证服务器拥有私钥，并且认证服务器只把token发给提供了正确密码的用户；
8. 因此应用服务器可以认为这个token是由认证服务器颁发的也是安全的，因为该用户具有了正确的密码；
9. 应用服务器继续完成HTTP请求，并认为这些请求确实属于这个用户；

这样的话，黑客假扮合法用户的办法要么是盗到了用户名和密码组合，要么盗到了认证服务器上的签名私钥。

正如我们所见，签名的确是JWT的关键部分！

签名使得无状态的服务器只需要通过查看HTTP请求中的JWT token就能保证HTTP请求是来自某个用户，而不需要每次请求时都发送密码。

- **JWT的目标是让服务器无状态?**

实际上，JWT真正的好处是让认证服务器和校验JWT token的应用服务器可以完全分开，而让服务器无状态化只是它的一个副作用罢了。这意味着应用服务器只需要最简单的认证逻辑-校验JWT！我们可以将整个应用集群的登录/注册委托给一个单独的认证服务器。这也意味着应用服务器更简单更安全，因为更多的认证功能集中部署在认证服务器，可以被跨应用使用。

到此，我们从更高的层面了解了JWT是怎样完成无状态的第三方认证，接下来让我们了解它的实现细节。

- **JSON Web Token看起来是怎样的呢?**

让我们来看看JWT的实际例子，这是从[http://jwt.io](https://link.zhihu.com/?target=http%3A//jwt.io)的JWT校验工具得到的：

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```

你可能会想，JSON对象去哪了啊？不过，你会马上找回它。

我们可以看到，这个JWT包含3部分，是由“.”号分开的。第一部分是JWT的Header：

JWT Header:

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
```

第二部分是Payload:

JWT Payload:

```text
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9
```

第三方部分是签名Signature:

JWT Signature:

```text
TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```

如果你还想确认这些信息是否真的存在，可以拷贝JWT串到[http://jwt.io](https://link.zhihu.com/?target=http%3A//jwt.io)的在线校验工具校验一下即可。

但这些字符串代表什么意思呢？我们如何取回JWT的信息？

- **Base64，抑或是Base64Url?**

不管你信不信，现在的Payload，Header和Signature还是可读的。这只是因为我们不想在网络传输过程中出现一些垃圾文本，比如这样的字符串：qÃ®Ã¼Ã¶:Ã。

这是因为世界上不同的计算机以不同的编码方式处理字符串，比如UTF-8，ISO 8859-1，等等。因此，这种问题到处存在，只要我们在某个平台上用到一个字符串，它总是使用了某种编码方式，即使我们没有显示指定：

1. 操作系统的默认编码方式；
2. 服务器上的配置的编码参数；

我们希望在网络上传输字符串时没有这些问题，那就需要选择这些字符的一个子集，对于这个子集，几乎所有的编码方式都是一样的处理方式，这就是Base64编码方式产生的原因。

- **Base64 vs Base64Url**

但是我们在JWT看到的并不是Base64，实际上是Base64Url，它和Base64类似，但有一些字符不一样，因此我们可以将JWT作为URL的参数进行传递。

我们看一下Payload部分：

```text
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9
```

我们使用在线解码器来解析它，就得到了一个JSON对象，因此，我们可以得到这样的结论：JWT Header和Payload的内容是普通的javascript对象，转换成JSON并进行Base64Url编码，以“.”号隔开。

在学习签名Signature之前，我们先来看看在实际的用户认证案例中，我们是将哪些内容放入Payload中的。

- **基于JWT的用户会话管理: 主题和期限**

之前有提到，JWT的Payload理论上可以存放任何内容，不一定是用户身份信息，只不过使用JWT作为认证是最常用的方式。Payload还有一些特定的属性来支持：

1. 用户身份
2. 会话过期

这里是Payload的几个最常用的标准属性：

· iss 代表生成token的实体，一般就是认证服务器

· iat 创建JWT的时间戳(in seconds since Epoch)

· sub 包含用户的身份信息

· exp token的过期时间戳

我们把这叫做Bearer Token，意思是:

***认证服务器确认这个token的持有者是具有由sub属性表示的ID的用户，因此可以放行。***

现在我们理解了Payload在用户认证中是如何使用的，接下来我们来了解一下签名Signature。对于JWT，签名方式有很多种，这里我们主要了解HS256和RS256。

我们先来看看HS256.

- **HS256 JWT数字签名 – 它是如何工作的?**

和很多签名方法一样，HS256 数字签名基于一种特殊的函数：加密哈希函数。

这听起来有点唬人，不过是个值得学习的概念：这个知识已经被使用了20多年并还会持续很长时间。很多关于安全的实现都围绕着哈希，它在Web安全中随处可见。

我们将分为两步，首先要了解什么是哈希函数，然后再看通过这样的函数和密码，如何生成信息认证码(Message Authentication Code)，也就是数字签名。

- **什么是哈希函数(Hashing function)?**

哈希函数是一种特殊的函数：它在数字签名中有很多实际的使用案例。现在我们将谈论它四个有趣的属性，然后看看这些属性如何使得我们可以生成可校验的签名。这里我们将使用的哈希函数是：SHA-256。

- **哈希函数属性 1 – 不可逆性**

哈希函数有点类似绞肉机：你把牛排放入一端，然后从另一端得到汉堡包，你再也无法从汉堡包取回牛排了。因此，函数是完全不可逆的。这就意味着我们把Header和Payload作用于这个函数后，没有人可以从函数输出的信息中取回Header和Payload的原始值。

使用在线的哈希计算器，我们可以看到SHA-256的一个输出值如下：

```text
3f306b76e92c8a8fbae88a3ef1c0f9b0a81fe3a953fa9320d5d0281b059887c3
```

同时，哈希并不是加密，加密在定义中是可逆的，我们总是需要从加密后的信息中得到原始信息。

- **哈希函数属性 2 – 可重复生成**

另外一个需要知道的是，哈希函数是可重复生成信息的，也就是如果我们输入同样的Header和Payload信息，每次得到的结果是完全一样的。这就意味着，给定输入组合和哈希输出值，我们总是可以校验该输出值(比如签名signature)的正确性，因为我们可以重新计算(我们有输入值的情况下)。

- **哈希函数属性 3 – 没有冲突**

还有一个属性是，如果我们提供不同的输入值，总是得到不同的唯一的输出值。这就意味着我们将哈希函数作用于某个Payload和Header之后，总是得到相同的结果，其它输入值组合不会得到和这一样的结果，因此，哈希函数的不同输出值就代表了输入值的不同。

- **哈希函数属性 4 – 不可预测性**

哈希函数的最后一个属性就是不可预测性，给定一个输出值，无法通过各种手段猜测到输入值。假设我们尝试从上面的输出值中找到生成它的Payload，我们只能猜测输入值然后对比输出值看看是否匹配。

但对于哈希函数来说，这种方式是不可行的：

这是因为在哈希函数中，即使你改变了一个输入字符甚至一个比特值，输出中一般有50%的比特值都会被改变，输入值小小的变动，可能会得到完全不同的输出值。

这些听起来挺有趣的，不过你可能又在想了：哈希函数是怎样完成数字签名的呢？黑客是否可以拿着Header和Payload，而不管Signature呢？任何人都可以使用SHA-256哈希函数生成一个输出，然后附加到JWT的signature部分，对吧？

- **怎样使用哈希函数生成签名?**

这是正确的，任何人都可以使用哈希函数，然后输入Header和Payload来生成结果。但HS256签名不止这样，我们拿到Header、Payload外，还要加上一个密码，将这三个输入值一起哈希。输出结果是一个SHA-256 HMAC或者基于哈希的MAC。如果需要重复生成，则需要同时拥有Header、Payload和密码才可以。这也意味着，哈希函数的输出结果是一个数字签名，因为输出结果就表示了Payload是由拥有密码的角色生成并加签了的，没有其它方式可以生成这样的输出值了。

将哈希结果附加到消息上，是为了让接收者可以验证。哈希结果叫HMAC：Hash-Based Message Authentication Code，是数字签名的一种形式。这就是我们在JWT中所做的，JWT的第三部分是由Header、Payload通过SHA-256函数生成，并使用Base64Url进行编码。

- **如何校验JWT签名?**

当我们的服务接收到HS256签名的JWT时，我们需要使用同样的密码才能校验并确认token里面的Payload是否有效。为了验证签名，我们只需要将JWT Header和Payload以及密码通过哈希函数生成结果。如果是使用HS256函数，JWT的接收者需要拿到和发送者一样的密码值。如果我们得到的哈希结果和JWT第三部分的签名值是一致的，则说明有效，可以确认发送者确实和接收者拥有相同的密码值。

而数字签名和HMAC又是如何工作的呢？

- **手动确认SHA-256 JWT签名**

我们从之前的JWT中去掉签名和第二个“.”，只留下Header和Payload部分。看起来如下：

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9
```

现在如果你拷贝这个字符串到在线的HMAC SHA-256工具，并使用上密码，就可以取回JWT签名。或者，你会得到Base64编码后的内容，后面还有一个“=”字符，这算是已经接近Base64Url：

TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ=

那个“=”在URL栏中会显示为“%3D”，会显得混乱，这也解释了在我们把JWT拼接到URL发送时，需要Base64Url的原因。

- **为什么需要其它的签名类型呢?**

以上解释了JWT签名是如何应用于认证的，HS256只是一种具体的签名类型。其它的签名类型中，最常用的是：RS256。

有什么区别呢？我们介绍HS256只是为了更容易理解MAC码的概念， 你可能也会发现它在一些生产环境的应用中被使用。但是一般来说，使用RS256签名方式会更好，下一节我们将看到，RS256相对于HS256来说有诸多优势。

- **HS256签名方式的劣势**

如果输入的密码相对弱的话，HS256可能会被暴力破解，基于密钥的技术都有这个问题。更甚的是，HS256要求JWT的生产者和消费者都预先拥有相同的密码。

- **不切实际的密码分发**

这意味着我们在修改密码后，需要把它分发并安装到所有需要它的网络节点。这不仅不方便，而且容易出错，还涉及到服务器间的协调和暂停服务问题。如果服务器是由另外的团队维护，比如第三方组织，这种方式就更不可行了。

- **Token的创建和校验没有分离**

创建和校验JWT的能力没有区分开，使用HS256时，网络的任何人都可以创建和校验token，因为他们都有密码。这就意味着密码可能会从更多的地方丢失或者受攻击，因为密码到处分发，而并不是每个应用都具有一样的安全保护机制。

弥补这问题的一个方法是，创建一个共享的密码给每一种类型的应用。不过，我们马上要学习新的签名方式，这个签名方式解决了以上所有的问题，并且目前所有基于JWT的方案都默认使用的，那就是RS256。

- **RS256 JWT签名**

使用RS256我们同样需要生成一个MAC，其目的仍然是创建一个数字签名来证明一个JWT的有效性。只是在这种签名方式中就，我们将创建token和校验token的能力分开，只有认证服务器具备创建的能力，而应用服务器，具备校验的能力。

这样，我们需要创建两个密钥而不是一个：

1. 仍然需要一个私钥，不过这次它只能被认证服务器拥有，只用来签名JWT。
2. 私钥只能用来签名JWT，不能用来校验它。
3. 第二个密钥叫做公钥(public key)，是应用服务器使用来校验JWT。
4. 公钥可以用来校验JWT，但不能用来给JWT签名。
5. 公钥一般不需要严密保管，因为即便黑客拿到了，也无法使用它来伪造签名。

- **RSA加密技术介绍**

RS256使用一种特殊的密钥，叫RSA密钥。RSA是一种加解密算法，使用一个密钥进行加密，然后用另外一个密钥解密。值得注意的是，RSA不是哈希函数，从定义上来说，这种方式加密是可逆的，也就是我们可以从加密后的内容得到原始内容。

来看一下RSA公钥是怎样的:

—–BEGIN PUBLIC KEY—–

```text
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDdlatRjRjogo3WojgGHFHYLugdUWAY9iR3fy4arWNA1KoS8kVw33cJibXr8bvwUAUparCwlvdbH6dvEOfou0/gCFQsHUfQrSDv+MuSUMAe8jzKE4qW+jK+xQU9a03GUnKHkkle+Q0pX/g6jXZ7r1/xAK5Do2kQ+X5xK9cipRgEKwIDAQAB
```

—–END PUBLIC KEY—–

乍一看有点古怪，但它是使用命令行工具比如openssl 或者在线的RSA密钥生成工具来生成的。

这个公钥是公开发布的，因此黑客根本不需要猜测，他本来就可以拥有它。

但这里还有一个RSA私钥:

—–BEGIN RSA PRIVATE KEY—–

```text
MIICWwIBAAKBgQDdlatRjRjogo3WojgGHFHYLugdUWAY9iR3fy4arWNA1KoS8kVw33cJibXr8bvwUAUparCwlvdbH6dvEOfou0/gCFQsHUfQrSDv+MuSUMAe8jzKE4qW+jK+xQU9a03GUnKHkkle+Q0pX/g6jXZ7r1/xAK5Do2kQ+X5xK9cipRgEKwIDAQABAoGAD+onAtVye4ic7VR7V50DF9bOnwRwNXrARcDhq9LWNRrRGElESYYTQ6EbatXS3MCyjjX2eMhu/aF5YhXBwkppwxg+EOmXeh+MzL7Zh284OuPbkglAaGhV9bb6/5CpuGb1esyPbYW+Ty2PC0GSZfIXkXs76jXAu9TOBvD0ybc2YlkCQQDywg2R/7t3Q2OE2+yo382CLJdrlSLVROWKwb4tb2PjhY4XAwV8d1vy0RenxTB+K5Mu57uVSTHtrMK0GAtFr833AkEA6avx20OHo61Yela/4k5kQDtjEf1N0LfI+BcWZtxsS3jDM3i1Hp0KSu5rsCPb8acJo5RO26gGVrfAsDcIXKC+bQJAZZ2XIpsitLyPpuiMOvBbzPavd4gY6Z8KWrfYzJoI/Q9FuBo6rKwl4BFoToD7WIUS+hpkagwWiz+6zLoX1dbOZwJACmH5fSSjAkLRi54PKJ8TFUeOP15h9sQzydI8zJU+upvDEKZsZc/UhT/SySDOxQ4G/523Y0sz/OZtSWcol/UMgQJALesy++GdvoIDLfJX5GBQpuFgFenRiRDabxrE9MNUZ2aPFaFp+DyAe+b4nDwuJaW2LURbr8AEZga7oQj0uYxcYw==
```

—–END RSA PRIVATE KEY—–

好消息是，黑客没有任何办法猜测私钥。

而且，这两个密钥是相关的，一个密钥加密的内容只能由另外的密钥来解密。那我们又如何用它们生成签名呢？

- **为什么不用RSA加密Payload就完了?**

现在尝试着使用RSA来生成一个数字签名:

我们使用Header和Payload，然后使用私钥对其进行RSA加密，最后返回JWT。

接收者拿到JWT后，使用公钥解密，然后检查解密后的值。如果解密过程顺利并且其输出是一个JSON值，往往就意味着该JWT就是认证服务器创建并加密了的。

相比哈希函数，RSA加密过程比较慢。对于数据比较大的Payload来说，可能会是个问题。

那HS256签名方式在实际中又是如何使用RSA的呢?

- **使用RSA和SHA-256签名JWT (RSA-SHA256)**

在实际中，我们一般先将Header和Payload一起哈希，比如使用SHA-256。这个速度是很快的，这样我们就得到了一个代表输入数据的唯一表示，比实际输入数据要小得多。

然后我们使用RSA对哈希结果而不是完整的数据(Header+Payload)进行加密，就得到了RS256签名。我们将这个签名附加到JWT的第三部分，然后返回给客户端。

- **接收者是怎样检查RS256签名的?**

接收者将:

1. 取出Header和Payload，然后使用SHA-256进行哈希。
2. 使用公钥解密数字签名，得到签名的哈希值。
3. 接收者将解密签名得到的哈希值和刚使用Header和Payload参与计算的哈希值进行比较。如果两个哈希值相等，则证明JWT确实是由认证服务器创建的。

任何人都可以计算哈希值，但只有认证服务器可以使用RSA私钥对其进行加密。

接下来我们学习一下在RS256签名中遇到问题时的解决思路。

- **手工确认RS256 JWT签名**

我们看下[http://jwt.io](https://link.zhihu.com/?target=http%3A//jwt.io)上的例子，一个使用RS256加签的JWT。

```text
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.EkN-DOsnsuRjRO6BxXemmJDm3HbxrbRzXglbN2S4sOkopdU4IsDxTI8jO19W_A4K8ZPJijNLis4EZsHeY559a4DFOd50_OqgHGuERTqYZyuhtF39yxJPAjUESwxk2J5k_4zM3O-vtd1Ghyo4IbqKKSy6J9mTniYJPenn5-HIirE
```

从表面上看，这和HS256 JWT没有多大区别，但这是使用前面展示的同一个RSA私钥加签了的。

我们把签名部分去掉，只看Header和Payload:

```text
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9
```

现在我们需要做的就是使用SHA-256对其进行哈希，然后使用上面的RSA私钥进行加密。这样得到的结果就是JWT签名，我们可以使用Node的内嵌模块Crypto来确认。

首先，我们把RSA私钥保存到一个文本文件，比如叫private.key。然后在命令行运行node shell，执行一个小程序，得到下面的结果：

```text
 EkN+DOsnsuRjRO6BxXemmJDm3HbxrbRzXglbN2S4sOkopdU4IsDxTI8jO19W/A4K8ZPJijNLis4EZsHeY559a4DFOd50/OqgHGuERTqYZyuhtF39yxJPAjUESwxk2J5k/4zM3O+vtd1Ghyo4IbqKKSy6J9mTniYJPenn5+HIirE=
```

这个结果和JWT签名完全不同，不过等等，这里面还有斜杠和等号。如果不进一步处理，这是没法放到URL里面的。

这是因为我们生成的是Base64 版本的签名，而我们真正需要的是Base64Url 版本的。我们尝试转换一下:

bash$ node

const base64url = require(‘base64url’);

```text
base64url.fromBase64("EkN+DOsnsuRjRO6BxXemmJDm3HbxrbRzXglbN2S4sOkopdU4IsDxTI8jO19W/A4K8ZPJijNLis4EZsHeY559a4DFOd50/OqgHGuERTqYZyuhtF39yxJPAjUESwxk2J5k/4zM3O+vtd1Ghyo4IbqKKSy6J9mTniYJPenn5+HIirE=");
```

得到下面的结果:

```text
EkN-DOsnsuRjRO6BxXemmJDm3HbxrbRzXglbN2S4sOkopdU4IsDxTI8jO19W_A4K8ZPJijNLis4EZsHeY559a4DFOd50_OqgHGuERTqYZyuhtF39yxJPAjUESwxk2J5k_4zM3O-vtd1Ghyo4IbqKKSy6J9mTniYJPenn5-HIirE
```

这就是我们真正想要创建的RS256签名了！也证明了我们对RS256 JWT签名的理解是正确的，而且我们知道了在遇到问题时如何去分析解决。

总之，RS256 JWT签名就是使用RSA对Header和Payload的哈希值进行加密的结果。现在我们知道RS256签名是如何工作的了，但这些签名为什么好于HS256签名呢？

- **RS256签名 vs HS256 – 为什么使用RS256?**

使用RS256，黑客可以轻松实现创建签名的第一步，即根据盗来的JWT Header和Payload生成SHA-256哈希值，之后他还要暴力破解RSA才能继续生成签名。

但这还不是我们为什么选择RS256而不是HS256的客观原因。

我们知道，使用RS256时，私钥只有认证服务器持有，这就安全得多- 加签密钥丢失的风险降低了。然而选择RS256更重要的理由是-简化密钥分发。

- **如何进行密钥分发部署**

还记得之前我们说过，用来校验token的公钥可以随意分发，黑客无法使用它来做任何有意义的事情。然而黑客并不是想校验token，他们只是想伪造它们。这就使得我们将公钥放置到受我们自己控制的服务器上成为可能。

应用服务器连接到公钥放置的服务器获取公钥，然后定期检查公钥是否有变化。因此，在更新密钥时，应用服务器和认证服务器不需要同时暂停服务。

那公钥又如何分发呢？下面是一种可行的格式。

- **JSON Web Key Set Endpoints**

有多种发布公钥的格式，但这里有一种较为熟悉：JWKS，全称Json Web Key Set。

如果你好奇这些endpoints 看起来是怎样的，可以看一下这个线上例子live example，下面这个是我们从HTT GET请求得到的回复：

Kid是密钥身份, x5c是某种公钥的表示法。这种格式的优点是其标准化，我们只需要知道endpoint的URL，和一个可以解析JWKS的库，就可以使用公钥来校验JWT了，而不需要安装到自己的服务器。

JWT常常使用在公共网站上，以及社交产品的登录方案中。对于内部系统，它是怎么被使用的呢?

- **JWT在企业中的应用**

JWT同样适用于企业内部，替代经典的存在已知安全隐患的预身份验证设置(Pre-Authentication setup)方式。

预身份验证设置方式中，我们的应用服务器在私有网络的一个代理后面运行，然后从HTTP请求头中获取当前用户信息。代表用户身份的HTTP请求头通常由中心化的登录页面填充，同时中心化的节点也对用户session进行管理。

当session过期后，服务器将阻止对应用的访问，并要求用户重新登录认证。之后，它将所有请求转发到应用服务器并在HTTP请求头添加代表用户身份的信息。

***问题是这种设置方式，内网上的任何人都可以假扮成某个用户，只要设置同样的HTTP请求头。\***

对此也有一些解决方案，比如白名单列表，或者某种客户凭证。

- **更好的预身份验证设置方式**

预身份验证设置方式是一个好主意，毕竟这种方式可以使得应用开发者不需要实现认证逻辑，减少开发时间和潜在的安全问题。

如果能有预身份验证设置方式的便捷，又没有安全方面的妥协，岂不美哉？

如果我们考虑到JWT，则可以轻松做到。我们不像以往那样将用户名放到HTTP请求头，而是将HTTP请求头封装成一个JWT。我们将用户名放到Payload里面，再由认证服务器加签。

应用服务器不再从HTTP请求头获取用户名，而是首先校验JWT：

1. 如果签名是正确的，则用户认证通过，请求可以放行；
2. 否则，应用服务器简单的拒绝请求就好了；

这样的结果就是，即使在私有网络内，我们的认证功能也可以正常工作。我们再也不需要通过HTTP请求头来识别用户了，我们保证了HTTP请求头的有效性并且是由代理生成的，而不是某黑客试图以某个用户身份登录。

- **总结**

通过本文，我们对JWT是什么有了一个全面的了解，以及它是如何在认证中被使用的。JWT只是一个简单的JSON对象，并且易于验证、难于伪造。

此外，JWT并不是一定要用来做认证的，我们可以使用JWT在网络上发送各种数据。

另外一个和安全相关的使用JWT的情况是授权：我们可以在Payload里面放置用户的角色列表，比如只读用户、管理员等等，对用户在应用服务器上的行为进行限制。

好了，本文到此结束，祝你阅读愉快！

文章来源：[想全面理解JWT？一文足矣！](https://link.zhihu.com/?target=https%3A//www.nndev.cn/archives/1925)