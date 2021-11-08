# Java基础知识
### Java三大特性
封装：把数据和操控数据的方法封装起来，对数据的访问只能通过接口
继承：继承是从已有类得到继承信息创建新类的过程
>1.子类拥有父类对象所有的属性和方法（包括私有属性和私有方法），但是父类中的私有属性和方法子类是无法访问，只是拥有，
>2.子类可以拥有自己的属性和方法
>3.子列可以用自己的方式实现父类的方法

多态
多态：多态就是同一个行为具有多个不同的表现形式或形态的能力，就是同一个接口，使用不同的实例而执行不同操作
### 重写和重载的区别
重载：重载就是同一个类中多个同名方法根据不同的传参来执行不同的逻辑处理
重写：重写就是子类对父类方法的重新改造，外部样子不能改变，内部逻辑可以改变
### Java中是否可以重写一个private或者static方法
Java中static方法不能被覆盖，因为方法覆盖是基于运行时动态绑定的，而static方法是编译时静态绑定的，static方法跟类的任何实例都不相关，
Java中也不可以覆盖private的方法，因为private修饰的变量和方法只能在当前类中使用，如果是其他的类继承当前类是不能访问到private变量和方法的
>静态的方法可以被继承，但是不能被重写，如果父类和子类中存在同样名称和参数的静态方法，那么该子类的方法会把原来继承过来的父类的方法隐藏，而不是重写

### Java中创建对象的几种方式

1. 使用new
2. 使用class类的newInstance方法，该方法调用无参的构造器创建对象（反射），Class.forName.newInstance()
3. 使用clone方法
4. 反序列化，比如调用ObjectInputStream类的readObject（）方法
### 抽象类和接口有什么不同
#### 不同点

1. 抽象类可以定义构造函数，接口不能定义构造函数
2. 抽象类可以有抽象方法和具体方法，接口中只能由抽象方法
3. 抽象类的成员权限可以是public ，默认，protected(抽象类中抽象方法就是为了重写，所以不能被private修饰)，而接口的成员只可以是public（方法默认：public abstrat，成员变量默认：public static final）
4. 抽象类中可以包含静态方法，而接口中不可以包含静态方法（接口JDK1.8之后可以包含静态方法，之前不能包含是因为，接口不可以实现方法，只可以定义方法，所以不能使用静态方法（因为静态方法必须实现）现在可以包含了，只能直接用接口调用静态方法，1.8仍然不可以包含静态代码块）
#### 相同点

1. 都不能被序列化
2. 可以将抽象类和接口作为引用类型
3. 一个类如果继承了某个抽象类或者实现了某个接口，就必须对其中所有的抽象方法全部进行实现，否则该类仍然需要被声明为抽象类
### Constructor是否可被override
继承的时候就知道父类的私有属性和构造方法不能被继承，所以Constructor也不能被override，但是可以overload
### Java基础类型

1. byte  8位     -2'7-2'7-1
2. short  16位   -2'15-2;15-1
3. int  32位       -2'31-2'31-1
4. long  64位     -2'63-2'63-1
5. float  32位
6. double  64位
7. boolean   只有true和false两个取值
8. char  16位，储存Unicode码，用单引号赋值

### int和Integer的区别

Integer是为int类型提供的封装类，int型变量的默认值是0，Integer变量的默认值是null

### 装箱和拆箱

自动装箱就是Java编译器在基本数据类型和对应得包装类之间做的一个转化，比如把int转化为Integer，反之就是自动拆箱

### String，StringBuilder，StringBuffer得区别

1. String：用于字符串操作，属于不可变类
2. StringBuffer：用于字符串操作，StringBuffer属于可变类，对方法加了同步锁，现场安全（StringBuffer中并不是所有方法都是用了Synchronized修饰来实现同步）
3. StringBuilder：与StringBuffer类似，都是字符串缓冲区，但线程不安全

执行效率：StringBuilder>StringBuffer>String

### String与基本数据类型转换

parseXXX（String）或者valueOf（String）方法

例如praseInt方法直接转换为基本数据类型int，valueOf方法是转换为包装类型

### String的常用方法

1. indexOf()：返回指定字符的索引。 
2. charAt()：返回指定索引处的字符。 
3. replace()：字符串替换。 
4. trim()：去除字符串两端空白。
5.  split()：分割字符串，返回一个分割后的字符串数组。
6.  getBytes()：返回字符串的 byte 类型数组。
7.  length()：返回字符串长度。 
8. toLowerCase()：将字符串转成小写字母。
9.  toUpperCase()：将字符串转成大写字符。 
10. substring()：截取字符串。
11.  equals()：字符串比较。

### final，finally，finalize的区别

final：用于声明属性，方法和类，分别表示属性不可变，方法不可覆盖，被其修饰的类不可继承

finally：异常处理语句结构的一部分，表示总是执行

finalize：Object的一个方法，在垃圾回收时会调用被回收对象的finalize

### static

#### 静态变量

静态变量：又称为类变量，也就是说这个变量属于类的，类所有的实例都共享静态变量，可以直接通过类名来访问他，静态变量在内存中只存在一份

实例变量：每创建一个实例就会产生一个实例变量，他与该实例同生共死

#### 静态方法

静态方法在类加载的时候就存在了，它不依赖于任何实例。所以静态方法必须有实 现，也就是说它不能是抽象方法。只能访问所属类的静态字段和静态方法，方法中不能有 this 和 super 关键字。

#### 静态语句块

静态语句块在类初始化时运行一次。

### super

访问父类的构造函数：可以使用super()函数访问父类的构造函数，从而委托父类完成一些初始化的工作

访问父类的成员：如果子类重写了父类的某个方法，可以通过使用super关键字来应用父类的方法实现

### ==和equals的区别

==：如果比较的对象是基本数据类型，是比较数值是否相等，如果是比较引用数据类型，则比较的是对象的地址值是否相等

equals方法：用来比较两个对象的内容是否相等，equals方法不能用于比较基本数据类型的变量，如果没有对equals方法进行重写，则比较的是引用类型的变量所指向的对象的地址，但是有很多类重写了equals方法，比如String,Integer等把它变成了值比较，所以一般情况下equals比较的是值是否相等

### 两个对象的hashCode()相同，则equals()也一定为true吗

两个对象的hashCode()相同，equals()不一定为true，因为在散列表中，hashCode()相等即两个键值对的哈希值相等，然后哈希值相等，并不一定能得出键值对相等（散列冲突）

### error和exception的区别

error和exception的父类都是Throwable类

Error类：一般是指虚拟机相关的问题，如系统崩溃，虚拟机错误，内存空间不足，这类错误直接回导致应用程序中断，仅靠程序本身无法恢复和预防

Exception：分为运行时异常和受检查的异常

-    运行时异常：【如空指针异常、指定的类找不到、数组越界、方法传递参数错误、数 据类型转换错误】可以编译通过，但是一运行就停止了，程序不会自己处理； 
- 受检查异常：要么用 try … catch… 捕获，要么用 throws 声明抛出，交给父类处理。

### throw和throws的区别

throw： 

throw 在方法体内部，表示抛出异常，由方法体内部的语句处理；

 throw 是具体向外抛出异常的动作，所以它抛出的是一个异常实例； 

throws： 

throws 在方法声明后面，表示如果抛出异常，由该方法的调用者来进行异常的处理； 表示出现异常的可能性，并不一定会发生这种异常。



### 常见的异常类

- NullPointerException：当应用程序试图访问空对象时，则抛出该异常。
-  SQLException：提供关于数据库访问错误或其他错误信息的异常。
-  IndexOutOfBoundsException：指示某排序索引（例如对数组、字符串或向量的排序） 超出范围时抛出。 
- FileNotFoundException：当试图打开指定路径名表示的文件失败时，抛出此异常。 
- OException：当发生某种 I/O 异常时，抛出此异常。此类是失败或中断的 I/O 操作生成 的异常的通用类。 
- ClassCastException：当试图将对象强制转换为不是实例的子类时，抛出该异常。
-  IllegalArgumentException：抛出的异常表明向方法传递了一个不合法或不正确的参 数。

### 对象克隆的实现

两种方式： 

1. 实现 Cloneable 接口并重写 Object 类中的 clone() 方法；
2. 实现 Serializable 接口，通过对象的序列化和反序列化实现克隆，可以实现真正的深克 隆。

 注意：深克隆和浅克隆的区别：

1. 浅克隆：拷贝对象和原始对象的引用类型引用同一个对象。浅克隆只是复制了对象的引 用地址，两个对象指向同一个内存地址，所以修改其中任意的值，另一个值都会随之变 化，这就是浅克隆（例：assign()）。 
2. 深克隆：拷贝对象和原始对象的引用类型引用不同对象。深拷贝是将对象及值复制过 来，两个对象修改其中任意的值另一个值不会改变，这就是深拷贝（例：JSON.parse() 和 JSON.stringify()，但是此方法无法复制函数类型）。 

> 深克隆的实现就是在引用类型所在的类实现 Cloneable 接口，并使用 public 访问修 饰符重写 clone 方法； Java 中定义的 clone 没有深浅之分，都是统一的调用 Object 的 clone 方法。为什 么会有深克隆的概念？是由于我们在实现的过程中刻意的嵌套了 clone 方法的调用。 也就是说深克隆就是在需要克隆的对象类型的类中重新实现克隆方法 clone()。

### Java序列化

对象序列化是一个用于将对象状态转换为字节流的过程，可以将其保存到磁盘文件中 或通过网络发送到任何其他程序。从字节流创建对象的相反的过程称为反序列化。而创建 的字节流是与平台无关的，在一个平台上序列化的对象可以在不同的平台上反序列化。序 列化是为了解决在对象流进行读写操作时所引发的问题。 

序列化的实现：将需要被序列化的类实现 Serializable 接口，该接口没有需要实现的 方法，只是用于标注该对象是可被序列化的，然后使用一个输出流（如： FileOutputStream）来构造一个 ObjectOutputStream 对象，接着使用 ObjectOutputStream 对象的 writeObject(Object obj) 方法可以将参数为 obj 的对象写 出，要恢复的话则使用输入流。 

什么情况下需要序列化

a）当你想把的内存中的对象状态保存到一个文件中或者数据库中时候； 

b）当你想用套接字在网络上传送对象的时候； 

c）当你想通过 RMI 传输对象的时候。

### 1、动态代理是什么？有哪些应用？ 

动态代理：当想要给实现了某个接口的类中的方法，加一些额外的处理。比如说加日志，加事务 等。可以给这个类创建一个代理，故名思议就是创建一个新的类，这个类不仅包含原来类 方法的功能，而且还在原来的基础上添加了额外处理的新功能。这个代理类并不是定义好 的，是动态生成的。具有解耦意义，灵活，扩展性强。

动态代理的应用： Spring 的 AOP 、加事务、加权限、加日志。

 ### 2、怎么实现动态代理？ 

首先必须定义一个接口，还要有一个 InvocationHandler（将实现接口的类的对象传 递给它）处理类。再有一个工具类 Proxy（习惯性将其称为代理类，因为调用它的 newInstance() 可以产生代理对象，其实它只是一个产生代理对象的工具类）。利用到 InvocationHandler，拼接代理类源码，将其编译生成代理类的二进制码，利用加载器加 载，并将其实例化产生代理对象，最后返回。 每一个动态代理类都必须要实现 InvocationHandler 这个接口，并且每个代理类的实 例都关联到了一个 handler，当我们通过代理对象调用一个方法的时候，这个方法的调用 就会被转发为由 InvocationHandler 这个接口的 invoke 方法来进行调用。我们来看看 InvocationHandler 这个接口的唯一一个方法 invoke 方法： 

```
Object invoke(Object proxy, Method method, Object[] args) throws Throwable 
```

> proxy: 指代我们所代理的那个真实对象 
>
> method: 指代的是我们所要调用真实对象的某个方法的 Method 对象 
>
> args: 指代的是调用真实对象某个方法时接受的参数 

Proxy 类的作用是动态创建一个代理对象的类。它提供了许多的方法，但是我们用的 最多的就是 newProxyInstance 这个方法：

 

```
public static Object newProxyInstance(ClassLoader loader, Class[] interfaces, InvocationHandler handler) throws IllegalArgumentException 
```

> loader： 一个 ClassLoader 对象，定义了由哪个 ClassLoader 对象来对生成的代理 对象进行加载； 
>
> interfaces：一个 Interface 对象的数组，表示的是我将要给我需要代理的对象提供 一组什么接口，如果我提供了一组接口给它，那么这个代理对象就宣称实现了该接口 (多态)，这样我就能调用这组接口中的方法了 
>
> handler：一个 InvocationHandler 对象，表示的是当我这个动态代理对象在调用方 法的时候，会关联到哪一个 InvocationHandler 对象上。 

通过 Proxy.newProxyInstance 创建的代理对象是在 Jvm 运行时动态生成的一个对 象，它并不是我们的 InvocationHandler 类型，也不是我们定义的那组接口的类型，而是 在运行是动态生成的一个对象

# Java集合

### Collection

#### Set

1. SetTreeSet： 基于红黑树实现，支持有序性操作，例如：根据一个范围查找元素的操 作。但是查找效率不如 HashSet，HashSet 查找的时间复杂度为 O(1)，TreeSet 则为 O(logN)。
2. HashSet： 基于哈希表实现，支持快速查找，但不支持有序性操作。并且失去了元素 的插入顺序信息，也就是说使用 Iterator 遍历 HashSet 得到的结果是不确定的。
3. LinkedHashSet： 具有 HashSet 的查找效率，且内部使用双向链表维护元素的插入 顺序。

#### List

1. ArrayList： 基于动态数组实现，支持随机访问。
2. Vector： 和 ArrayList 类似，但它是线程安全的。
3. LinkedList： 基于双向链表实现，只能顺序访问，但是可以快速地在链表中间插入和 删除元素。不仅如此，LinkedList 还可以用作栈、队列和双向队列。

### Map

1. TreeMap： 基于红黑树实现。
2. HashMap： 基于哈希表实现。
3. HashTable： 和 HashMap 类似，但它是线程安全的，这意味着同一时刻多个线程可 以同时写入 HashTable 并且不会导致数据不一致。它是遗留类，不应该去使用它。现在可 以使用 ConcurrentHashMap 来支持线程安全，并且 ConcurrentHashMap 的效率会更 高，因为 ConcurrentHashMap 引入了分段锁。
4. LinkedHashMap： 使用双向链表来维护元素的顺序，顺序为插入顺序或者最近最少 使用（LRU）顺序。

### ArrayList和LinkedList的区别

ArrayList： 底层是基于数组实现的，查找快，增删较慢；

 LinkedList： 底层是基于链表实现的。确切的说是循环双向链表（JDK1.6 之前是双向循 环链表、1.7 之后取消了循环），查找慢、增删快。LinkedList 链表由一系列表项连接而 成，一个表项包含 3 个部分：元素内容、前驱表和后驱表。链表内部有一个 header 表 项，既是链表的开始也是链表的结尾。header 的后继表项是链表中的第一个元素， header 的前驱表项是链表中的最后一个元素。

### 是不是Array List的增删就是比LinkedList要慢

**ArrayList的增删未必就是比LinkedList慢**

1. 如果增删都是在末尾来操作【每次调用的都是 remove() 和 add()】，此时 ArrayList 就不需要移动和复制数组来进行操作了。如果数据量有百万级的时，速度是会比 LinkedList 要快的。(我测试过) 
2. 如果删除操作的位置是在中间。由于 LinkedList 的消耗主要是在遍历上，ArrayList 的 消耗主要是在移动和复制上（底层调用的是 arrayCopy() 方法，是 native 方法）。 LinkedList 的遍历速度是要慢于 ArrayList 的复制移动速度的如果数据量有百万级的时， 还是 ArrayList 要快。(我测试过) 

> 补充：https://blog.csdn.net/weixin_39148512/article/details/79234817 **ArrayList 集合实现 RandomAccess 接口有何作用？为何 LinkedList 集合却没实 现这接口？**
>
>  1、RandomAccess 接口只是一个标志接口，只要 List 集合实现这个接口，就能支持 快速随机访问。通过查看 Collections 类中的 binarySearch() 方法，可以看出，判断 List 是否实现 RandomAccess 接口来实行indexedBinarySerach(list,key) 或 iteratorBinarySerach(list,key)方法。再通过查看这两个方法的源码发现：实现 RandomAccess 接口的 List 集合采用一般的 for 循环遍历，而未实现这接口则采用 迭代器，即 ArrayList 一般采用 for 循环遍历，而 LinkedList 一般采用迭代器遍 历。 
>
> 2、ArrayList 用 for 循环遍历比 iterator 迭代器遍历快，LinkedList 用 iterator 迭代器遍历比 for 循环遍历快。所以说，当我们在做项目时，应该考虑到 List 集合的 不同子类采用不同的遍历方式，能够提高性能！

### ArrayList的扩容机制

1. 当使用 add 方法的时候首先调用 ensureCapacityInternal 方法，传入 size+1 进去， 检查是否需要扩充 elementData 数组的大小； 
2. newCapacity = 扩充数组为原来的 1.5 倍(不能自定义)，如果还不够，就使用它指定要 扩充的大小 minCapacity ，然后判断 minCapacity 是否大于 MAX_ARRAY_SIZE(Integer.MAX_VALUE - 8) ，如果大于，就取 Integer.MAX_VALUE 
3. 扩容的主要方法：grow 
4. ArrayList 中 copy 数组的核心就是 System.arraycopy 方法，将 original 数组的所有 数据复制到 copy 数组中，这是一个本地方法。