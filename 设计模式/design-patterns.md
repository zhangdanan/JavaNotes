# 设计模式的六大原则

- 开闭原则：一个软件实体如类、模块和函数应该对修改封闭，对扩展开放 。
- 单一职责原则：一个类只做一件事，一个类应该只有一个引起它修改的原因。
- 里氏替换原则：子类应该可以完全替换父类，也就是说在使用继承时，只扩展新功能，而不要破坏父类原有的功能。
- 依赖倒置原则：细节应该依赖与抽象，抽象不应依赖于细节，把抽象层放在程序设计的高层，并保持稳定，程序的细节变化由底层的实现层来完成。
- 迪米特法则：又名最少知道原则，一个类不应该知道自己操作的类的细节，换言之，只和朋友谈话，不和朋友的朋友谈话
- 接口隔离原则：客户端不应依赖它不需要的接口，如果一个接口在实现时，部分方法由于冗余被客户端空实现，则应该将接口拆分，让实现类只需要依赖自己需要的接口方法

# 工厂方模式

工厂模式是用于封装对象的设计模式

## 简单工厂模式

## 工厂方法模式

## 抽象工厂模式

# 抽象工厂模式

# 

# 单例模式

## 单例模式

单例模式是Java中最简单的设计模式之一，这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式，

在应用这个模式的时候，单例对象的类必须保证只有一个实例存在，单例模式有两种实现方式：饿汉式和懒汉式

## 单例模式的特点

1. 单例类只能有一个实例
2. 单例类必须给自己创建自己的唯一实例
3. 单例类必须给所有其他对象提供这一实例

## 单例模式的优点

- 它能够避免对象重复创建，节约空间并提升效率
- 避免由于操作不同实例导致的逻辑错误

## 饿汉式

- 饿汉式：变量在声明时边初始化

```
public class Singleton{
    private static Singleton instance=new Singleton();
    private Singleton(){
    }
    pubilc static Singleton getInstance(){
        return instance;
    }
}
```

将构造方法定义为private，这就保证了其他类无法实例化此类，必须通过getInstance方法才能获取到唯一的instance实例，非常直观，但是饿汉式有一个弊端，那就是即使这个单例不需要使用，他也会在类加载之后立即创建起来，占用一块内存，并增加类初始化时间。

一个很好的比喻就是：就好比一个电工在修理灯泡时，先把所有工具拿出来，不管是不是所有的工具都用得上，就像一个饥不择食的饿汉，所以称为饿汉式。

## 懒汉式

- 懒汉式：先声明一个空变量，需要时才初始化

```
public class Singleton{
        private static Singleton instance=null;
        
        private Singleton(){}
        
        public static Singleton getInstance(){
           if(instance == null){
               instance =new Singleton();
           }
           return instance;
        }
        


}
```

一个很好的比喻：电工在修理灯泡时，开始比较偷懒，什么工具都不拿，当发现需要使用螺丝刀时，才把螺丝刀拿出来，当需要钳子时，再把钳子拿出来，就像一个不到万不得已不会行动的懒汉，所以称之为懒汉式。



懒汉式解决了饿汉式的弊端，好处是按需加载，避免了内存浪费，减少了类初始化时间。

缺点就是它不是线程安全的，如果有多个线程同一时间调用getInstance方法，instance变量可能会被实例化多次，所以为了保证线程安全，我们需要给判空过程加个锁

```
public class Singleton{
    private static Singletyon instance= null;
    
    private Singleton(){}
    
    public static Singleton getInstance(){
        synchronized(Singletyon.class){
        if(instance == null){
            instance =new Singleton();
           }
        }
        return instance;
    }
}
```

这样就能保证多个线程调用getInstance时，一次最多只有一个线程能够执行判空并new出实例的操作，所以instance只会实例化一次，但是存在的问题时，当多个线程调用getInstance时，每次都需要执行synchronized同步化方法，这样会严重影响程序的执行效率。所以最好在同步化之前，再加上一层检查。

### 双检锁式懒汉式单例模式

```
public class Singleton{
    private static Singletyon instance= null;
    
    private Singleton(){}
    
    public static Singleton getInstance(){
      if(instance == null){
        synchronized(Singletyon.class){
        if(instance == null){
            instance =new Singleton();
           }
        }
        return instance;
    }
   }
}
```

这样的写法仍然有一个问题，JVM底层为了优化程序运行效率，可能会对我们的代码进行指令重排序，在一些特殊情况下会导致单例模式线程不安全，为了防止这个问题，更进一步的优化是给instance变量加上volatile关键字

### 静态内部类式懒汉式单例模式

```
public class Singleton{
     private static class SingletonHolder{
         public static Singleton instance =new Singleton();
    }
    
    private Singleton(){}
    
    public static Singleton getInstance(){
        return SingletyonHolder.instance;
    }

}
```

分析下原理

**1.静态内部类方式是怎么实现懒加载的**

Java 类的加载过程包括：加载、验证、准备、解析、初始化。初始化阶段即执行类的 clinit 方法（clinit = class + initialize），包括为类的静态变量赋初始值和执行静态代码块中的内容。但不会立即加载内部类，内部类会在使用时才加载。所以当此 Singleton 类加载时，SingletonHolder 并不会被立即加载，所以不会像饿汉式那样占用内存。

另外，Java 虚拟机规定，当访问一个类的静态字段时，如果该类尚未初始化，则立即初始化此类。当调用Singleton 的 getInstance 方法时，由于其使用了 SingletonHolder 的静态变量 instance，所以这时才会去初始化 SingletonHolder，在 SingletonHolder 中 new 出 Singleton 对象。这就实现了懒加载。

**2.静态内部类方式是怎么保证线程安全的**

Java 虚拟机的设计是非常稳定的，早已经考虑到了多线程并发执行的情况。虚拟机在加载类的 clinit 方法时，会保证 clinit 在多线程中被正确的加锁、同步。即使有多个线程同时去初始化一个类，一次也只有一个线程可以执行 clinit 方法，其他线程都需要阻塞等待，从而保证了线程安全。



## 总结

懒加载方式在平时非常常见，比如打开我们常用的美团、饿了么、支付宝 app，应用首页会立刻刷新出来，但其他标签页在我们点击到时才会刷新。这样就减少了流量消耗，并缩短了程序启动时间。再比如游戏中的某些模块，当我们点击到时才会去下载资源，而不是事先将所有资源都先下载下来，这也属于懒加载方式，避免了内存浪费。

但懒汉式的缺点就是将程序加载时间从启动时延后到了运行时，虽然启动时间缩短了，但我们浏览页面时就会看到数据的 loading 过程。如果用饿汉式将页面提前加载好，我们浏览时就会特别的顺畅，也不失为一个好的用户体验。比如我们常用的 QQ、微信 app，作为即时通讯的工具软件，它们会在启动时立即刷新所有的数据，保证用户看到最新最全的内容。著名的软件大师 Martin 在《代码整洁之道》一书中也说到：不提倡使用懒加载方式，因为程序应该将构建与使用分离，达到解耦。饿汉式在声明时直接初始化变量的方式也更直观易懂。所以在使用饿汉式还是懒汉式时，需要权衡利弊。

一般的建议是：对于构建不复杂，加载完成后会立即使用的单例对象，推荐使用饿汉式。对于构建过程耗时较长，并不是所有使用此类都会用到的单例对象，推荐使用懒汉式。

# 建造型模型

建造型模式用于创建过程稳定，但配置多变的对象。一个形象的比喻就是：我们要制作一杯奶茶，它的制作过程是稳定的，除了必须要知道奶茶的种类和规格外，是否加珍珠和是否加冰是可选的，

# 原型模式

原型模式：用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。

