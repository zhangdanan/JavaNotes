# Java多线程

## 一.线程和进程

### 1.1进程

进程是程序的一次执行过程，是系统运行程序的基本单位，因此进程是动态的。系统运行一个程序即是一个进程从创建，运行到消亡的过程。

在 Java 中，当我们启动 main 函数时其实就是启动了一个 JVM 的进程，而 main 函数所在的线程就是这个进程中的一个线程，也称主线程。

### 1.2线程

线程与进程相似，但线程是一个比进程更小的执行单位。一个进程在其执行的过程中可以产生多个线程。与进程不同的是同类的多个线程共享进程的**堆**和**方法区**资源，但每个线程有自己的**程序计数器**、**虚拟机栈**和**本地方法栈**，所以系统在产生一个线程，或是在各个线程之间作切换工作时，负担要比进程小得多，也正因为如此，线程也被称为轻量级进程。

### 1.3进程和线程的区别

线程是进程划分成的更小的运行单位，线程和进程最大的不提用在于基本上个进程都是独立的，而各线程则不一定，因为同一进程中的线程极有可能会先相互影响，线程执行开销小，但不利于资源的管理和 保护，而进程正相反。

### 1.4上下文切换

多线程编程中一般线程的个数都大于CPU核心的个事，而一个CPU核心在任意时刻只能被一个线程使用，为了让这些线程都能得到有效执行，CPU采取的策略是为每个线程分配时间片并轮转的形式，当一个线程的时间片用完的时候就会重新处于就绪状态让给其他线程使用，这个过程就属于一次上下文切换。

总结来说：当前任务在执行完CPU时间片切换到另一个任务之前会先保存自己的状态，以便下次再切换回这个任务时，可以再加载这个任务的状态。任务从保存到再加载的过程就是一次上下文切换。

上下文切换对系统来说意味着消耗大量的CPU时间，事实上，可能是操作系统中时间消耗最大的操作。

Linux相比与其他操作系统有很多的优点，其中有一项就是，其上下文切换和模式切换的时间消耗比较少。

## 二.Java是如何使用多线程的

- 继承Thread类，并重写run方法：
- 实现Runnable接口的run方法：

## 2.1 继承Thread类

```
public class test0 {
    public static class MyThread extends Thread {
        @Override
        public void run(){
            System.out.println("MyThread");
        }
    }
    public static void main(String[] args) {
        Thread myThread=new MyThread();
        myThread.start();
    }
}
```

### 2.2实现Runnable接口

```
public class test1 {
    public static class MyThread implements Runnable {
        @Override
        public void run() {
            System.out.println("MyThread");
        }
    }
    public static void main(String[] args) {
        new Thread(new MyThread()).start();
        new Thread(() ->{
            System.out.println("This is Thread");
        }).start();
    }
}
```

### 2.3 Thread类的几个常用方法

- currentThread（）：静态方法，返回对当前正在执行的线程对象的引用。
- start（）：开始执行线程的方法，java虚拟机会调用线程内的run（）方法。
- yield（）：当前线程愿意让出对当前处理器的占用，需要注意的 是，就算当前线程调用了yield（）方法，程序在调度的时候，也还有可能继续运行这个线程的。
- sleep（）：静态方法，让当前线程睡眠一段时间。
- join（）：时当前线程等待另一个线程执行完毕之后再继续执行，内部调用的时Object类的wait方法实现的。

### 2.4 Thread类与Runnable接口的比较

- 由于Java”单继承，多实现“的特性，Runnable接口使用起来比Thread更灵活
- Runnable接口出现更符合面向对象，将线程单独进行对象的封装
- Runnable接口出现，降低了线程对象和线程任务的耦合性
- 如果使用线程时不需要使用Thread类的诸多方法，显然使用Runnable接口更为轻量。

## 第三章 线程组和线程优先级

### 3.1线程组（ThreadGroup）

Java中用ThreadGroup来表示线程组，我们可以使用线程组进行批量控制

每个线程（Thread）比如存在于一个线程组中（ThreadGroup），Thread不能独立于ThreadGroup存在。

执行main（）方法线程 的名字是main，如果在new Thread没有显式指定，那么默认将发现场线程组设置为自己的线程组。

```
public class test2 {
    public static void main(String[] args) {
        Thread testThread = new Thread(() -> {
            System.out.println("testThread当前线程组名字：" +
                    Thread.currentThread().getThreadGroup().getName());
            System.out.println("testThread线程名字：" +
                    Thread.currentThread().getName());
        });
        testThread.start();
        System.out.println("执行main所在线程的线程组名字： " + Thread.currentThread().getThreadGroup().getName());
        System.out.println("执行main方法线程名字：" + Thread.currentThread().getName());
    }}
```

ThreadGroup管理着它下面的Thread，ThreadGroup是一个标准的向下引用的树状结构，这样设计的原因是防止上级线程被下级线程引用而无法有效地被GC回收。

### 3.2 线程的优先级

Java线程优先级可以指定，范围是1-10.但是不是所有的操作系统都支持10级优先级的划分，Java只是给操作系统一个优先级的参考值，线程最终在操作系统的优先级是多少还是由操作系统来决定

Java默认的线程优先级是5，线程的执行顺序由调度程序来决定，线程的优先级会在线程被调用之前设定。

通常情况下，高优先级的线程会比低优先级的线程有更高的几率得到执行，我们使用方法Thread类的setPriority（）实例方法来设定线程的优先级。

```
public class Test3 {
    public static void main(String[] args) {
        Thread a = new Thread();
        System.out.println("我是默认线程优先级："+a.getPriority());
        Thread b = new Thread();
        b.setPriority(10);
        System.out.println("我是设置过的线程优先级："+b.getPriority());
    }
}
```

不可以通过设定线程的优先级来指定线程执行的先后顺序

Java中的优先级并不是很可靠，Java程序中对线程所设置的优先级只是给操作系统一个建议，操作系统不一定会采纳，而真正的调用顺序，是由操作系统的线程调度算法决定的

Java提供一个线程调度器来监视和控制处于RUNNABLE状态的线程，线程的调度策略采用抢占式，优先级高的线程比优先级低的线程会有更大的几率优先执行，在优先级相同的情况下，按照”先到先得“的原则，每个Java程序都有一个默认的主线程，就是通过JVM启动的第一个线程main线程。

还有一种线程称为守护线程

# 3 说说并发与并行的区别

- **并发：** 同一时间段，多个任务都在执行 (单位时间内不一定同时执行)；
- **并行：** 单位时间内，多个任务同时执行。

# 4 使用多线程可能带来什么问题

并发编程的目的就是为了能提高程序的执行效率提高程序运行速度，但是并发编程并不总是能提高程序运行速度的，而且并发编程可能会遇到很多问题，比如：内存泄漏、死锁、线程不安全等等。

## 什么是线程死锁，如何避免死锁

### 什是线程死锁

线程死锁就是：多个线程同时被堵塞，它们中的一个或者全部都在等待某个资源被释放，由于线程被无限期地阻塞，由此程序不可能正常终止。

```
public class test2 {
    private static Object resource1 = new Object();//资源 1
    private static Object resource2 = new Object();//资源 2
    public static void main(String[] args) {
        new Thread(() -> {
            synchronized (resource1) {
                System.out.println(Thread.currentThread() + "get resource1");
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread() + "waiting get resource2");
                synchronized (resource2) {
                    System.out.println(Thread.currentThread() + "get resource2");
                }
            }
        }, "线程 1").start();
        new Thread(() -> {
            synchronized (resource2) {
                System.out.println(Thread.currentThread() + "get resource2");
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread() + "waiting get resource1");
                synchronized (resource1) {
                    System.out.println(Thread.currentThread() + "get resource1");
                }
            }
        }, "线程 2").start();
    }
}
```

产生死锁必须具备以下四个条件：

1. 互斥条件：该资源任意一个时刻只由一个线程占用。
2. 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
3. 不剥夺条件：线程已获得的资源在未使用完之前不能被其他线程强行剥夺，只有自己使用完毕后才释放资源。
4. 循环等待条件：若干进程之间形成一种头尾相接的循环等待资源关系。

### 如何避免线程死锁

我们只要破坏产生死锁的四个条件中的其中一个就可以了

1. 破坏互斥条件：这个条件我们没有办法破坏，因为我们用锁本来就是想让他们互斥的（临界资源需要互斥访问）
2. 破坏请求与保持条件：一次性申请所有的资源。
3. 破坏不剥夺条件：占用部分资源的线程进一步申请其他资源时，如果申请不到，可以主动释放它占有的资源。
4. 破坏循环等待条件：靠按序申请资源来预防，按某一顺序申请资源，释放资源则反序释放，破坏循环等待条件

