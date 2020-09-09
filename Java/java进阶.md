# 2019-4-15-Java进阶学习（对象的序列化和反序列化）

#### 什么是序列化和反序列化

- **序列化**：指把堆内存中的java对象数据，通过某种方式把对象存储在磁盘文件中或者传递给其他网络节点，通俗来讲就是将数据结构或对象转换成字节序列（二进制串）的过程。
- **反序列化**：把磁盘文件中的对象数据或者网络节点上的对象数据，恢复成java对象模型的过程，也就是将在序列化过程中所生成的字节序列（二进制串）转换成数据结构或者对象的过程。

#### 为什么要做序列化和反序列化

- 在分布式系统中，此时需要把对象在网络上传输，就得把对象数据转换成二进制形式，需要共享的数据的JavaBean对象，都得做序列化。
- 有些服务器发生钝化现象，如果服务器发现某些对象好久没活动了，那么服务器就把这些内存中的对象持久化在本地磁盘文件中（Java对象转换成二进制文件）；如果服务器发现某些对象需要活动时，先去内存中寻找，找不到再去磁盘文件中反序列化我们的对象数据，恢复成java对象，这样能节省服务器内存。

#### 怎么去做序列化和反序列化

1. 需要做序列化的对象的类，必须实现序列化接口：java.lang.Serializable接口（这是一个标志接口，没有任何抽象方法），java中大多数类都实现了该接口，比如：String，Integer
2. 底层会判断，如果当前对象是Serializable的实例，才允许做序列化，Java对象instanceof  Serializable来判断。
3. 在Java中使用对象流进行序列化和反序列化的操作
   - **ObjectOutputStream**：通过writeobject()方法做序列化操作。
   - **ObjectInputStream**：通过readobject()方法做反序列化操作。

具体操作步骤如下：

1. 先建立一个Person类,继承与Serializable接口。

   ```
   package bean;
   
   import java.io.Serializable;
   
   public class Person implements Serializable {
       private String name;
       private int age;
   
       public String getName() {
           return name;
       }
   
       public void setName(String name) {
           this.name = name;
       }
   
       public int getAge() {
           return age;
       }
   
       public void setAge(int age) {
           this.age = age;
       }
   
       @Override
       public String toString() {
           return "Person{" +
                   "name='" + name + '\'' +
                   ", age=" + age +
                   '}';
       }
   
       public Person(String name, int age) {
           super();
           this.name = name;
           this.age = age;
       }
   }
   
   ```

   2. 进行编写SerializableTest类，进行序列化和反序列化的操作。

   ```
   package io;
   
   import bean.Person;
   
   import java.io.*;
   
   public class SerializableTest {
       public static void main(String[] args) throws IOException, ClassNotFoundException {
           //进行序列化
           ObjectOutputStream ooo=new ObjectOutputStream((new FileOutputStream("D:/data.txt")));
           Person person=new Person("zzzz",1);
           ooo.writeObject(person);
           ooo.close();
   
           //进行反序列化
           ObjectInputStream oos=new ObjectInputStream(new FileInputStream("D:/data.txt"));
           Person person1=(Person)oos.readObject();
           System.out.println("name="+person1.getName()+"  "+"age="+person1.getAge());
           oos.close();
       }
   
   }
   
   ```

   