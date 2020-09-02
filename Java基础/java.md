[Java学习一](#2019-4-5-Java学习一（用命令行运行程序）)

[Java学习四](#2019-4-5-Java学习四（基本数据类型）)





# 2019-4-5-Java学习一（用命令行运行程序）

1. 首先创建一个TXT文件，在里面写上

```java
class HelloWorld{
     public static void main(String[] args){
       System.out.println(arg[0]);
       System.out.println(arg[1]);
}
}
```

2. 然后改名为HelloWorld.java进入命令行，到达HelloWorld.java文件的JavaBasicDemo目录下，输入javac HelloWorld.java，然后会有一个HelloWorld.class文件生成

![Image](https://github.com/aaaxma/JavaNote/blob/master/images/Image1.1.png)

3. 上文中的**args[0]和**args[1]是用来接收键盘的值的，命令行输入java HelloWorld 值一 值二，执行结果如下

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/Image1.2.png)

​	

# 2019-4-5-Java学习二（一个java程序是如何实现的）

一个Java文件的执行步骤如下图所示

![Image2](https://github.com/aaaxma/JavaNote/blob/master/images/Image2.1.png)

Java语言为啥是跨平台的，其实就是字节码文件的原因，在各个平台虚拟机都统一的使用相同的程序存储格式。实际上JVM和Java语言不是想象中的那样紧紧绑在一起，简单来说就是JVM只是识别字节码文件的，只要你熟悉字节码文件，你完全可以自己编写一个符合要求的字节码文件来交给JVM去运行，JVM完全可以跑的通，而且你还可以把其他语言编写的源码编译成字节码文件，交给JVM去运行，只要是合法的字节码文件，JVM完全可以跑的通，所以还实现了跨语言。

在命令行中可以用javap -v 类名来查看相关类的字节码文件

![Image4](https://github.com/aaaxma/JavaNote/blob/master/images/Image2.2.png)

可以只用命令javap -v Student > Student.txt来进行输出重定向

![Image5](https://github.com/aaaxma/JavaNote/blob/master/images/Image2.3.png)

你的文件里会多出来个txt文件

![Image6](https://github.com/aaaxma/JavaNote/blob/master/images/Image2.4.png)





# 2019-4-5-Java学习三（JVM的基本结构和内存分区）

### 1.java虚拟机的基本结构

![Image3](https://github.com/aaaxma/JavaNote/blob/master/images/Image3.png)

 JVM中把内存分为直接内存、方法区、Java栈、Java堆、本地方法栈、PC寄存器等。

​       **直接内存**：就是原始的内存区

​       **方法区**：用于存放类、接口的元数据信息，加载进来的字节码数据都存储在方法区

​       **Java栈**：执行引擎运行字节码时的运行时内存区，采用栈帧的形式保存每个方法的调用运行数据

​       **本地方法栈**：执行引擎调用本地方法时的运行时内存区

​       **Java堆**：运行时数据区，各种对象一般都存储在堆上

​       **PC寄存器**：功能如同CPU中的PC寄存器，指示要执行的字节码指令。

  JVM的功能模块主要包括类加载器、执行引擎和垃圾回收系统。



对于各个模块的详细操作，现在水平有限就不一一说明了，下面链接中有详细说明。

<https://www.cnblogs.com/dqrcsc/p/4671879.html>



# 2019-4-5-Java学习四（基本数据类型）

### 1.数据类型的分类

数据类型分为基础数据类型和引用数据类型，引用数据类型包括数组和类。

### 2.基础数据类型

**byte：**  

byte 数据类型是8位、有符号的，以二进制补码表示的整数；

最小值是 **-128（-2^7）**；

最大值是 **127（2^7-1）**；

默认值是 **0**；

byte 类型用在大型数组中节约空间，主要代替整数，因为 byte 变量占用的空间只有 int 类型的四分之一；

例子：byte a = 100，byte b = -50。

**short：**

short 数据类型是 16 位、有符号的以二进制补码表示的整数

最小值是 **-32768（-2^15）**；

最大值是 **32767（2^15 - 1）**；

Short 数据类型也可以像 byte 那样节省空间。一个short变量是int型变量所占空间的二分之一；

默认值是 **0**；

例子：short s = 1000，short r = -20000。

**int：**

int 数据类型是32位、有符号的以二进制补码表示的整数；

最小值是 **-2,147,483,648（-2^31）**；

最大值是 **2,147,483,647（2^31 - 1）**；

一般地整型变量默认为 int 类型；

默认值是 **0** ；

例子：int a = 100000, int b = -200000。

**long：**

long 数据类型是 64 位、有符号的以二进制补码表示的整数；

最小值是 **-9,223,372,036,854,775,808（-2^63）**；

最大值是 **9,223,372,036,854,775,807（2^63 -1）**；

这种类型主要使用在需要比较大整数的系统上；

默认值是 **0L**；

例子： long a = 100000L，Long b = -200000L。

"L"理论上不分大小写，但是若写成"l"容易与数字"1"混淆，不容易分辩。所以最好大写。

**float：**

float 数据类型是单精度、32位、符合IEEE 754标准的浮点数；

float 在储存大型浮点数组的时候可节省内存空间；

默认值是 **0.0f**；

浮点数不能用来表示精确的值，如货币；

例子：float f1 = 234.5f。

**double：**

double 数据类型是双精度、64 位、符合IEEE 754标准的浮点数；

浮点数的默认类型为double类型；

double类型同样不能表示精确的值，如货币；

默认值是 **0.0d**；

例子：double d1 = 123.4。

**boolean：**

boolean数据类型表示一位的信息；

只有两个取值：true 和 false；

这种类型只作为一种标志来记录 true/false 情况；

默认值是 **false**；

例子：boolean one = true。

**char：**

char类型是一个单一的 16 位 Unicode 字符；

最小值是 **\u0000**（即为0）；

最大值是 **\uffff**（即为65,535）；

char 数据类型可以储存任何字符；

例子：char letter = 'A';





# 2019-4-5-Java学习五（基本语法）

### 1.标识符

标识符由任意顺序的字母、下划线、美元符号和数字组成，并且第一个字不能是数字，标识符不能使java中的保留关键字。

### 2.声明变量

变量就是申请内存来存储值，也就是说，在创建变量的时候，需要在内存中申请空间，内存管理系统根据变量的类型为变量分配空间，分配的空间只能用来存储该类型数据。

系统内存大约可以分为三个区域，即系统（os）区，程序（program）区和数据（data）区,当程序运行时，程序代码会加载到内存中的程序区，程序区会为变量分配内存空间，数据暂时存储在数据区中，

### 3.变量范围

分为成员变量和局部变量，

##### 成员变量

成员变量又分为静态变量和实例变量，静态变量的有效范围可以跨类，甚至可以在整个应用程序里面使用，，对于静态变量来说，除了能在定义他的类内存取，还能直接以“类名.静态变量”的方式在其他类内使用

##### 局部变量

在类的方法体中定义的变量，只能在当前代码块中使用。

### 4.自增和自减运算符

自增和自减运算符是单目运算符，可以放在操作元前，也可以放在操作元后，操作元必须是一个班整型或浮点型变量，

```
++a(--a)   //表示在使用变量a之前，先使a的值加(减)1
a++(a--)   //表示在使用变量之后，使a的值加(减)1
```

### 5.数据类型转换

#### 隐式类型转换

从低级类型到高级类型的转换，系统会自动进行，称为隐式转换，按照精度从低到高排列的顺序是byte<short<char<int<long<float<double

#### 显示类型转换（强制类型转换）

把高精度的变量的值赋给低精度的变量时，语法如下：

```
（类型名）要转换的值
```

**注意**：执行显示转换时可能会导致精度损失

### 6.流程控制

#### 条件语句

**if条件语句**

简单的if条件语句，布尔表达式返回的结果是true，则执行其后的语句，返回的结果是false，则不执行其后的语句

```java
if(布尔表达式){
语句序列
}
```

if·····else语句：if后面的括号中 的表达式一定要是boolean型的，如果表达式的值为true，则执行紧跟其后的语句，如果表达式的值是false，则执行else中的语句

```java
if(表达语句){
     若干语句
}
else{
    若干语句
}
```

if····else if语句：满足哪个条件就进行哪个处理

```
if(表达式1){
    语句序列1
}else if(表达式2){
    语句序列2
}
····
else if(表达式n){
    语句序列n
}
```

**switch多分支语句**

switch语句中表达式的值必须是整型、字符型或字符串类型的，常量也必须是整型、字符型或字符串型的。

switch语句首先计算表达式的值，如果表达式的值和某个case后面的常量值相同，则执行该case语句后的若干个语句指导break语句为止，此时如果该case语句中没有break语句，将继续执行后面的case中的若干个语句，直到遇到break为止，若没有一个常量的值于表达式的值相同，则执行default后面的语句，default语句为可选语句，如果他不存在，且switch语句表达式的值不与任何case常量相同，swith则不做任何处理。

```java
switch(表达式){
    case 常量值 1:
       语句块1
       break；
    ·····
    case 常量值 n：
       语句块n
       break；
    default：
       语句n+1；
       break；
}

```

#### 循环语句

**while语句**

先判断条件表达式，表达式为真是，执行{}内的语句，当条件表达式为假时，这退出循环。

```java
while(条件表达式){
    执行语句
}
```

**do····while循环语句**

先执行一次循环，然后再开始判断条件表达式是否成立

```
do{
    执行语句
}
while(条件表达式)
```

**for循环语句**

```
for(表达式1;表达式2;表达式3){
    语句序列
}
```

**foreach循环语句**

在遍历数组的方面很方便

```java
for(元素变量x;遍历对象obj){
    引用了x的java语句
}
```

**break语句**

使用break可以跳出当前循环语句

**continue语句**

continue不是立即跳出循环，而是跳出本次循环结束的语句，回到循环的条件测试，重新开始执行循环







# 2019-4-5-Java学习六（字符串）

### 01.String的一些方法

IndexOf（String s）

该方法用于返回参数字符串s在指定字符串中首次出现的索引位置，当调用这个方法的时候，会从当前字符串的开始位置搜索s的位置，如果没有检索到字符串s，该方法的返回值是-1

###### lastIndexOf（String s）

该方法用于返回参数字符串s在指定字符串最后一次出现的索引位置，当调用这个方法的时候，会从当前字符串的开始位置检索s，并将最后一次出现s的位置返回，如果没有检索到该字符串s，该方法的返回值为-1

###### charAt（）

将指定索引出的字符返回

```
str.charAt(int index)
```

###### substring(int beginIndex)

该方法返回的是从指定的索引位置开始截取直到该字符串结尾的子串

###### substring(int beginIndex,int endindex)

该方法返回的是字符串某一索引位置开始截取至某一索引位置结束的子串‘

###### trim（）

该方法返回字符串的副本，忽略前导空格和尾部空格

###### replace(char oldChar,char newChar)

该方法可实现将指定的字符或者字符串替换成新的字符或字符串

###### startsWith()

该方法用于判断当前字符串对象的前缀是否为参数指定的字符串，返回值为boolean类型

###### endsWith()

该方法用于判断当前字符串是否以给定的子字符串结束，返回值为boolean类型

###### equals（）

如果两个字符串具有相同的字符和长度，则使用equals()方法来进行比较，返回值为true

###### equalsIgnoreCase()

使用equals方法对字符串进行比较时是区分大小写的，而使用equalsIgnoreCase()是在忽略大小写的情况下比较两个字符串是否相等。

###### compareTo（）

此方法是为按字典顺序比较两个字符串，该比较基于字符串中各个字符的Unnicode值

###### toLowerCase()

该方法是把字符串中的所有字符从大写字母改写为小写字母

###### toUpperCase()

该方法是把字符串中的所有字符从小写字母改为大写字母

###### split（String sign）

该方法可根据给定的分隔符对字符串进行拆分

###### split（String sign,int limit）

该方法根据给定的分隔符对字符串进行拆分，并限定拆分的次数

###### format (String format,Object···args)

该方法使用指定的格式化字符串和参数返回一个格式化字符串，格式化后的新字符使用本地默认的语言环境

###### format（Local l,String format.Object···args）

格式化过程中要应用的语言环境，如果l为null，则不进行本地化                  











# 2019-4-8-Java学习七（数组）

### int[] array 和int array[]的区别

对于int[10] array来讲，是先为array分配一个内存地址空间，然后在里面进行内存地址的分配

对于int array[]来讲，是为每一个数组变量分配一个内存地址，

也就是说，对于int[10] array来说，就是先分配一个整的内存地址，然后再里面进行分配，对于int array[10]来说，就是一个变量分配一个内存地址，也就是one to one

### 数组定义

对于一维数组的定义

```
int[] array=new int[];
```

对于数组的赋值

```
int[] array=new int[]{1,3,6,7};
int[] array1={2,4,6,8}
```

对于二维数组的定义

```
int[][] array=new int[][];
```

对于数组的赋值

```
int[][] array=new int[][]{{1,4,6},{3,6,8}};
```

### 数组的基本操作

1. 遍历

   ```
   int[][] array1=new int[][]{{1,3,4},{2,8,6},{3,6,4}};
           for (int i = 0; i <array1.length ; i++) {
               for (int j = 0; j <array1[i].length ; j++) {
                   System.out.print(array1[i][j]);
               }
               System.out.println();
   ```

   用foreach语句进行遍历

   ```
      int[][] array2=new int[][]{{1,3,6,5},{4,6,7,9},{3,5,3,2},{4,2,6,8}};
           int i=0;
           for (int x[]:array2          //先遍历外层数组，就相当于遍历一位数组
                ) {
               i++;
               int j=0;
               for (int e:x               //遍历内层数组，遍历每一个数组元素
                    ) {
                   j++;
                   if (i==array2.length&&j==x.length){
                       System.out.print(e);
                   }else {
                       System.out.print(e+"、");
                   }
               }
   
           }
   ```

2. 填充替换数组元素

   `fill(int[] a,int value)`方法，该方法可将指定的int值分配给int型数组的每个元素

   ```
    int[] array3=new int[6];
           Arrays.fill(array3,8);
           System.out.println();
           for (int j = 0; j <array3.length ; j++) {
               System.out.print(array3[j]);
           }
   ```

   `fill(int[] a,int fromIndex,int toIndex,int value)`方法，该方法将指定的int值分配给int型数组 指定范围中的每个元素。

   ```
    int[] array4=new int [6];
           Arrays.fill(array4,1,2,3);
           System.out.println();
           for (int j = 0; j < array4.length; j++) {
               System.out.print(array4[j]);
           }
   ```

3. 对数组进行排序

   `sort(object)`方法可对任意类型的数组进行升序排序

   ```
    int[] array5=new int[]{4,4,3,2,5};
           Arrays.sort(array5);
           System.out.println();
           for (int j = 0; j <array5.length ; j++) {
               System.out.print(array5[j]);
           }
   ```

4. 复制数组

   `copyOf(arr,int newlength)`方法，满足不同类型数组的复制

   ```
    int[] array6=new int[]{4,2,9};
           int[]  array7=Arrays.copyOf(array6,6);
           System.out.println();
           for (int j = 0; j <array7.length ; j++) {
               System.out.print(array7[j]);
           }
   ```

   `copyOfRange(arr,int formIndex,int toIndex)`方法，可以将指定范围内的数组复制出来

   ```
    int[] array8=new int[]{2,4,5,7,1};
           int[] array9=Arrays.copyOfRange(array8,2,4);
           System.out.println();
           for (int j = 0; j <array9.length ; j++) {
               System.out.print(array9[j]);
           }
   ```

5. 数组查询

   `binarySearch(Object[],Object key)`方法，此方法采用二分搜索法来搜索指定数组，来获得指定对象，该方法返回的是要搜索元素的索引值。

   ```
    int[] array0=new int[]{1,6,93};
           Arrays.sort(array0);
           int index=Arrays.binarySearch(array0,6);
           System.out.println("6的索引是"+index);
   
   ```

   `binarySearch(Object[],int fromIndex,int toIndex,Object key)`此方法在指定的范围内检索某一元素。

   ```
    int[] zhang=new int[]{8,4,5,3,5};
           Arrays.sort(zhang);
           int index1=Arrays.binarySearch(zhang,2,4,5);
           System.out.println("索引为"+index1);
   ```

   

### 数组排序算法

##### 冒泡算法

```
public class Bubblesort {
    public static void main(String[] args) {
        int[] array=new int[]{42,43,64,15,93,53};
        Arrays.sort(array);
        for (int i = 1; i <array.length ; i++) {
            for (int j = 0; j <array.length-i ; j++) {
                if (array[j]>array[j+1]){
                    int temp=array[j];
                    array[j]=array[j+1];
                    array[j+1]=temp;
            }
        }
        }
        for (int m:array){
            System.out.print(">"+m);
        }
    }
}
```

##### 直接排序算法

```

```



# 2019-4-8-Java学习八（类和对象）

### 万物皆对象

类是封装对象的属性和行为的载体，也就是具有相同属性和行为的一类实体被称为类。

### 封装

封装是面向对象编程的核心思想，就是将对象的属性和行为封装起来，其载体就是类，封装的思想是对客户隐藏其实现细节，客户只需要用就行了。例如，用户使用计算机，通过敲打键盘就可以实现某些功能，而无需知道计算机内部是如何操作的。

采用封装的思想就是保证类内部数据结构的完整性，应用该类的用户不能轻易的直接操作此数据结构，只能执行类允许公开的数据，这就避免了外部操作对内部数据的影响，提高了程序的可维护性。

### 继承

继承就是利用特定对象中的共有属性，分为子类和父类，子类继承与父类

### 多态

将父类对象应用于子类的特征就是多态，多态的实现不是依赖于具体类，而是依赖与抽象类和接口，在抽象类中，不能实例化对象，而且只能给出一个方法的标准，不能给出实现的具体流程。

### 权限修饰符

private的范围是在本类中，

public的范围是在应用程序中都可以使用

protected的范围是在同包的其他类或子类中使用

### 类的构造方法

构造方法是一个与类同名的方法，对象的创建就是通过构造方法完成的，每当类实例化一个对象时，类都会自动调用构造方法，构造方法没有返回值。

### this关键字

在java语言中规定使用this关键字来代表本类对象的引用，this关键字被隐式地用于引用对象的成员变量和方法。

```
Public Class Student { 
 String name; //定义一个成员变量name
 private void SetName(String name) { //定义一个参数(局部变量)name
  this.name=name; //将局部变量的值传递给成员变量
 }
}
```

在上面的例子中，this.name是成员变量，后面的name就是形参的值，，其实实质上setter()方法实现的功能就是将形参的值赋予成员变量。在静态方法中不能使用this关键字。

对于更多的this关键字的应用   https://www.cnblogs.com/lzq198754/p/5767024.html

### ==和equals()方法的区别

对于基本类型（byte，short，int，long，float，double，boolean，char）

“==“比较的是两个对象的值是否相同，equals()方法比较的是两个对象的地址是否相同。

对于引用类型（除基础类型的值）

equals()方法是String类中的方法，用于比较两个对象引用所指的内容是否相等。“==”运算符比较的是两个对象引用的地址是否相同

https://www.cnblogs.com/Latiny/p/8099581.html

### 对象的销毁

每个对象都有生命周期的，当对象的生命周期结束时，分配给该对象的内存地址将会被回收，，Java有一套完整的垃圾回收机制，用户不必担心废弃的对象占用内存，垃圾回收器将回收无用的但占用内存的资源，在JVM中，有两种情况的会被视为垃圾，一种是对象引用超过其应用范围，一种是将对象赋值为null。

java中只能回收那些有new操作符创建的对象，对于那些不是通过new操作符创建的对象，一般采用Object类提供的finalize()方法，用户可以在自己类中定义这个方法，如果用户在类中定义了finalize()方法，在垃圾回收的时候会首先调用该方法，在下一次垃圾回收动作发生时，才能真正回收被对象占用的内存。

> 垃圾回收或finalize()方法不保证一定会发生，如JVM内存损耗待尽时，是不会执行垃圾回收的。

由于垃圾回收不受认为控制，具体执行时间也不确定，所以finalize()方法也就无法执行，为此，java提供了System.gc()方法强制启动垃圾回收器。



# 2019-4-9-Java学习九（接口继承和多态）

### 类的继承

基本思想就是基于某个父类的扩展，制定一个新的子类，子类可以继承原有的属性和方法，也可以增加父类不具备的属性和方法，也可以直接重写父类中的某些方法，

重写就是在子类中将父类的成员方法的名称保留，重写成员方法的实现内容，更改成员方法的存储权限，或是修改成员方法的返回值类型。

重构是一种特殊的重写方法，子类与父类的成员方法返回值、方法名称、参数类型和个数完全相同，唯一不同的是方法实现内容。

### Object类

java中的类都来源于java.lang.Object类，也就是说所有的类都是Object的子类。

Object类中的getClass()、notify()、notifyAll()、wait()等方法不能被重写

Object类中的clone()、finalize()、equals()、toString()方法可以被重写

##### getClass()方法

getClass()方法是Object定义的方法，他会返回对象执行时的Class实例，然后使用此实例调用getName()方法可以取得类的名称。

```
getClass().getName();
```

##### toString()方法

toString()方法的功能就是将一个对象返回为字符串形式，然后会返回一个String实例。

### 对象类型的转换

##### 向上转型

把子类对象赋值给父类类型的变量，这种技术称为向上转型。

##### 向下转型

将较抽象的类转化为较具体的类

###  使用instanceof操作符判断对象类型

如果程序在执行向下转型操作时，如果父类对象不是子类对象的实例，就会发生ClassCastException异常，所以在执行向下转型操作时，应该先判断父类对象是否为子类对象的实例，这个判断由instanceof操作符来完成，语法格式如下

```
myobject instanceof ExampleClass
//myobject为某类的对象引用，ExampleClass为某个类
```

使用instanceof操作符的表达式返回值为布尔值，如果myobject对象是ExampleClass的实例对象，则返回true，如果myobject对象不是ExampleClass的实例对象，则返回false

```
class Quadrangle{
    public static void draw(Quadrangle q) {
    }
}

class Square extends Quadrangle{
    //SomeSentence
}

class Anything{
    //somesentence
}

public class Parallelogram {
    public static void main(String[] args) {
        Quadrangle q=new Quadrangle();
        if(q instanceof Parallelogram){    //向下转型操作
            Parallelogram parallelogram=(Parallelogram) q;
        }
        if (q instanceof Square){
            Square s=(Square) q;          //进行向下转型操作
        }
    }
}

```

### 方法重载

方法重载就是在同一类中允许同时存在一个以上的同名方法，只要这些方法的参数个数或类型不同即可。

> 参数类型不同，构成重构
>
> 参数顺序不同，构成重构
>
> 参数个数不同，构成重构

编辑器是利用方法名、方法各参数类型和参数的个数以及参数的顺序来确定类中的方法是否唯一

### 抽象类和接口

abstract关键字是定义抽象类的关键，使用abstract关键字创作的类称为抽象类，使用abstract关键字创作的方法称为抽象方法，只要类中有一个抽象方法，就可以称这个类是抽象类。继承抽象类后必须要实现抽象类中所有的抽象方法。

接口就是一个纯粹的抽象类，接口中的所有方法都没有方法体，接口使用关interface关键字进行定义，一个类实现一个接口可以使用implements关键字。

在接口中，定义的方法必须被定义为public或abstract形式，其他修饰权限不被java编译器认可。

在Java中不允许多重继承，但使用接口就可以实现多重继承，因为一个类可以实现多个接口，语法如下

```
class 类名 implements 接口1，接口2，接口3
```





# 2019-4-9-Java学习十（final的用法）

### final的用法

##### final变量

final关键字定义的变量必须在声明时对其进行赋值操作。

final除了可以修饰基本数据类型 的常量还可以修饰对象引用，由于数组可以被当做一个对象来引用，所以final也可以修饰数组。

一旦一个对象引用被修饰为final时，只能恒定指向一个对象，无法将其改变以指向另一个对象。

被定义为final的对象引用只能指向唯一一个对象，但是对象的值是可以改变的，为了使一个常量真正做到不可改变，可以将常量声明为`static final`

##### final方法

定义为final的方法不可以被重写。将方法定义为final类型可以防止之类修改该类的定义与实现方式，同时定义为final的方法的执行效率要高于非final方法。

##### final类

定义为final的类不能被继承，如果一个类被定义为final形式，则类中的所有方法都被隐式设置为final形式，到那时final类中的成员变量可以被定义为final或非final形式





# 2019-4-10-Java学习十一（异常处理）

### 概念

异常就是Java运行时出现的错误，异常是一个在程序执行期间发生的事件，它中断了正在执行的程序的正常指令流。

### 异常处理

###### 捕捉异常

Java中异常捕捉的结构是由try、catch和final三个部分构成，try语句块中存放的是可能发生异常的java语句，catch程序块在try语句块之后，用来激发被捕获的异常；finally语句块是异常处理结构的最后执行部分，无论try语句块中的代码如何退出，都将执行finally语句块

```
try{
    //程序代码块
}
catch (Exceptiontype1 e){
    //对Exceptiontype1的处理
}
catch (Exceptiontype2 e){
     //对Exceptiontype2的处理 
}
....
finally{
    //程序块
}
```

完整的异常处理语句一定要包含finally语句，但是有四种特殊情况，finally语句块不会被执行：

- 在finally语句块中发生了异常
- 在前面的代码中使用了System.exit()退出程序
- 程序所在的线程死亡
- 关闭CPU

### Java常见异常

![Image4](https://github.com/aaaxma/JavaNote/blob/master/images/Exception.png)

在 Java 中，所有的异常都有一个共同的祖先java.lang包中的 **Throwable类**。Throwable： 有两个重要的子类：**Exception（异常）** 和 **Error（错误）** ，二者都是 Java 异常处理的重要子类，各自都包含大量子类。

**Error（错误）:是程序无法处理的错误**，表示运行应用程序中较严重问题。大多数错误与代码编写者执行的操作无关，而表示代码运行时 JVM（Java 虚拟机）出现的问题。例如，Java虚拟机运行错误（Virtual MachineError），当 JVM 不再有继续执行操作所需的内存资源时，将出现 OutOfMemoryError。这些异常发生时，Java虚拟机（JVM）一般会选择线程终止。

这些错误表示故障发生于虚拟机自身、或者发生在虚拟机试图执行应用时，如Java虚拟机运行错误（Virtual MachineError）、类定义错误（NoClassDefFoundError）等。这些错误是不可查的，因为它们在应用程序的控制和处理能力之 外，而且绝大多数是程序运行时不允许出现的状况。对于设计合理的应用程序来说，即使确实发生了错误，本质上也不应该试图去处理它所引起的异常状况。在 Java中，错误通过Error的子类描述。

**Exception（异常）:是程序本身可以处理的异常**。Exception类可根据错误发生的原因分为RuntimeException和非RuntimeException之外的异常，RuntimeException 异常由Java虚拟机抛出。**NullPointerException**（要访问的变量没有引用任何对象时，抛出该异常）、**ArithmeticException**（算术运算异常，一个整数除以0时，抛出该异常）和 **ArrayIndexOutOfBoundsException** （下标越界异常）。详细的如下图

![Image4](https://github.com/aaaxma/JavaNote/blob/master/images/RuntimeException.png)

**注意：异常和错误的区别：异常能被程序本身可以处理，错误是无法处理。**

### Throwable类常用方法

- **public string getMessage()**:返回异常发生时的详细信息

- **public string toString()**:返回异常发生时的简要描述

- **public string getLocalizedMessage()**:返回异常对象的本地化信息。使用Throwable的子类覆盖这个方法，可以声称本地化信息。如果子类没有覆盖该方法，则该方法返回的信息与getMessage（）返回的结果相同

- **public void printStackTrace()**:在控制台上打印Throwable对象封装的异常信息

  

### 自定义异常

在程序中使用自定义异常类，通常有几个步骤。

1. 创建自定义异常类。
2. 在方法中通过throw关键字抛出异常对象。
3. 如果在当前抛出异常的方法中处理异常，可以使用try-catch语句块捕获并处理，否则在方法的声明处通过throws关键字指明要抛出给方法调用者的异常，继续进行下一步操作。
4. 在出现异常方法的调用者中捕获并处理异常。
5. 此为自己定义的异常类

```
public class MyException extends Exception{
   
   public MyException(String ErrorMessage){
    super(ErrorMessage);
}

}
```

6. 此为自己定义的普通类

```

//自定义异常
public class Tran {
    static int avg(int number1,int number2)throws MyException{
        if(number1<0||number2<0){
            throw new MyException("不可以使用负数");
        }
        if (number1>100||number2>100){
            throw new MyException("数值太大了");
        }
        return (number1+number2)/2;
    }

    public static void main(String[] args) {
        try{
            int result=avg(102,150);
            System.out.println(result);
        }catch (MyException e){
            System.out.println(e);
        }
    }

}

```



### 在方法中抛出异常

##### 使用throws关键字抛出异常

throws关键字通常被应用在声明方法的时候，用来指出方法中可能抛出的异常，多个异常之间用逗号隔开。

```
//在方法使用throws中抛出异常
public class Shoot {
    static void pop() throws NegativeArraySizeException{
        int[] arr=new int[-3];
    }

    public static void main(String[] args) {
        try {
            pop();
        }catch (NegativeArraySizeException e){
            System.out.println("pop抛出的异常");
        }
    }

}

```



##### 使用throw关键字抛出异常

throw关键字通常用于方法体中，并且抛出一个异常对象，程序在执行到throw语句时**立即终止**，后面的语句都不执行，通过throw抛出异常后，如果想在上一级代码中来捕获并处理异常，则需要在抛出异常的方法中使用throws关键字在方法的声明中指明要抛出的异常，如果要捕获throw抛出的异常，则必须用try-catch语句块

- 自己定义的异常类MyException，继承与Exception。

```

//此为自己定义的异常类MyException,继承与Exception
public class MyException extends Exception{
    String message;
   public MyException(String ErrorMessage){
    message=ErrorMessage;
}
public String getMessage(){
       return message;
}
}
```

- 测试类

```
//使用throw关键字抛出异常
public class Captor {
    static int quotient(int x,int y)throws MyException{
        if (y<0){
            throw new MyException("除数不能为负");
        }
        return x/y;
    }

    public static void main(String[] args) {
        try{
            int result=quotient(3,-1);
        }catch (MyException e){
            System.out.println(e.getMessage());
        }catch (ArithmeticException e){
            System.out.println("除数不能为0");
        }catch (Exception e){
            System.out.println("程序出现了其他方面的异常");
        }
    }

}

```



# 2019-4-10-Java学习十二（集合类）

### 概述

集合类又被称为容器，数组也算是个容器，集合类和数组的区别就是：数组的长度是固定的，集合的长度是可变的，数组是用来存放基本类型的数据，集合用来存放对象的引用。

常见的集合有List集合、Set集合和Map集合。如下图：

![Image](https://github.com/aaaxma/JavaNote/blob/master/images/Object.png)



### Collection接口

##### 常用的一些方法

- add(E e)方法：将指定的对象添加到该集合中
- remove(Object o)方法：将指定的对象从该集合中移除
- isEmpty()方法：返回boolean值，用于判断当前集合是否为空
- iterator()方法：返回在此Collection的元素上进行迭代的迭代器，用于遍历集合中的对象
- size()方法：返回int型值，获取该集合中元素的个数



### List集合

List集合包括List接口以及List接口的所有实现类。

##### List接口

List接口继承了Collection接口，包含Collection中的所有方法，另外，List接口还定义了两个重要的方法

- get(int index)：获得指定索引位置的元素
- set(int index,Object obj)：将集合中指定索引位置的对象修改为指定的对象

##### List接口的实现类

List接口的常用实现类有ArrayList和LinkedList

**ArrayList**：此类实现了可变的数组，允许保存所有元素，包括null，并可以根据索引位置对集合进行快速的随机访问，缺点是向指定的索引位置插入对象或删除对象的速度较慢

**LinkedList**：此类采用链表结构保存对象，这种结构的优点是便于向集合中插入和删除 对象，需要向集合中插入、删除对象的时候，使用LinkedList类实现的List集合的效率更高，但对于随机访问集合中的对象，使用LinkedList类实现List集合的效率较低

```
//使用ArrayList、LinkedList类实例化List集合
List<E> list=new ArrayList<>();
List<E> list=new LinkedList<>();
```



### Set集合

Set集合中的对象不是按照特定的顺序排列的，只是简单的把对象加入到集合中，但Set集合中不能包含重复对象，Set集合包括Set接口和Set接口的实现类

##### Set接口

Set接口继承与Collection接口，包含Collection接口的所有方法

##### Set接口的实现类

Set接口常用的实现类有HashSet类和TreeSet类

**HashSet**：此类实现Set接口，由哈希表(实际上是一个HashMap实例)支持，它不保证Set的迭代顺序，特别是不保证该顺序恒定不变，此类允许使用null元素

**TreeSet0**：此类不仅实现了Set接口，还实现类java.util.SortedSet接口，因此，TreeSet类实现的Set集合在遍历集合时按照自然顺序递增排序，也可以按照指定比较器递增排序，就是可以通过比较器对用TreeSet类实现的Set集合中的对象进行排序。TreeSet新增的方法如下

- first()：返回此Set中当前第一个(最低)元素
- last()：返回此Set中当前最后一个(最高)元素
- comparator()：返回对此Set中的元素进行排序的比较器，如果此Set使用自然排序，则返回null
- headSet(E toElement)：返回一个新的Set集合，新集合是toElement(不包含)之前的所有对象
- subSet(E fromElement，E fromElement)：返回一个新的Set集合，是fromElement(包含)对象与fromElement(不包含)对象之间的所有对象
- tailSet(E fromElement)：返回一个新的Set集合，新集合包含对象fromElement(包含)之后的所有对象



### Map集合

Map集合提供的是key到value的映射，Map中不能包含相同的key，每个key只能映射一个value,key还决定了存储对象在映射中的存储位置，但不是由key对象本身决定的，而是通过一种“散列技术”进行处理，产生一个散列码的整数值，散列码通常用作一个偏移量，该偏移量对于分配给映射的内存区域的起始位置，从而确定存储对象在映射中的存储位置，Map集合包括Map接口和Map接口的所有实现类

##### Map接口

Map接口提供了将key映射到值的对象，一个映射不能包含重复的key，每个key最多只能映射到一个值，Map接口的常用方法

- put(K key,V value)：向集合中添加指定的key与value的映射关系
- containsKey(Object key)：如果此映射包含指定key的映射关系，则返回true
- containsValue(Object value)：如果此映射将一个或多个映射到指定值，则返回true
- get(Object ket)：如果存在指定的key对象，则返回该对象对应的值，否则返回null
- keySet()：返回该集合中的所有key对象形成的Set集合
- values()：返回该集合中所有值对象形成的Collection集合

##### Map接口的实现类

Map接口常用的实现类有HashMap和TreeMap,建议使用HashMap类实现Map集合，因为由HashMap类实现的Map集合添加和删除映射关系效率更高。

**HashMap**：此类基于哈希表的Map接口的实现，此实现提供可选的映射操作，并允许使用null值和null键，但必须保证键的唯一性，HashMap通过哈希表对其内部的映射关系进行快速查找，此类不保证映射的顺序，特别是不保证该顺序恒久不变

**TreeMap**：此类不仅实现了Map接口，还实现了java.util.SortedMap接口，因此，集合中的映射关系具有一定 的顺序，但在添加、删除和定位映射关系时，TreeMap类比HashMap类性能稍差，由于TreeMap类实现的Map集合中的映射关系是根据键对象按照一定的顺序排列的，因此不允许键对象是null



# 2019-4-11-java学习十三（IO）

### 流概述

流是一组有序的数据序列，根据操作的类型，可分为输入流和输出流，I/O流提供了一条通道程序，可以使用这条通道把源中的字节序列送到目的地，虽然I/O流通常与磁盘文件存取有关，但是程序的源和目的地也可以是键盘，鼠标，内存或显示器窗口。

Java由数据流处理输入/输出模式，程序从指向源的输入流中读取源中的数据，输出流的指向是数据要到达的目的地，程序通过向输出流中写入数据把信息传递到目的地。

### 输入/输出流

关于各种方式的输入/输出，这些类都放在java.io包中，其中，所有输入流类都是抽象类InputStream（字节输入流）或抽象流Reader（字符流输入流)的子类，所有输出流类都是抽象类OutputStream（字节输出流）或抽象类Writer（字符输出流）的子类

#### 输入流

###### InputStream类

InputStream类是所有字节输入流的父类，该类中所有的方法遇到错误是都会引发IOException异常，

- read()方法：从输入流中读取数据下一个字节，返回0~255范围内的int字节值，如果因为已经到达流末尾而没有可用的字节，则返回值为-1
- read(byte[] b)：从输入流中读入一定长度的字节，并以整数的形式返回字节数。
- mark(int readlimit)方法：在输入路的当前位置放置一个标志，readlimit参数告知此输入流在标记位置失效之前允许读取的字节数。
- reset()方法：将输入指针返回到当前所作的标记处
- skip(long n)方法：跳过输入流上的n个字节并返回实际跳过的字节数
- markSupported()方法：如果当前流支持mark()/set()操作就返回true。
- close()方法：关闭此输入流并释放与该流关联的所有系统资源。

**注意**：并不是所有的InputStream类的子类都支持Input Stream中的方法，Input Stream类中某些方法只对某些子类有用。

下图为InputStream类的层次结构

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/InputStream类的层次结构.png)

###### Reader类

Reader类是字符输入流的抽象类，所有字符输入流的实现都是它的子类，Reader类中的方法与Input Stream类中方法类似，Reader类结构图如下

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/Reader类的层次结构.png)

#### 输出流

###### OutputStream

OutputStream类是字节输出流的抽象类，此抽象类是所有输出字节流的父类，OutputStream类的层次结构如下图：

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/OutputStream.png)

OutputStream类的方法均返回void，在遇到错误是会引发IOException异常，以下是此类中各个方法的介绍：

- write（int b)方法：将指定的字节写入此输出流。
- write（byte[] b)方法：将b个字节从指定的byte数组写入此输出流。
- write（byte[] b,int off,int len)方法：将指定byte数组中从偏移量off开始的len个字节写入此输出流。
- flush（)方法：彻底完成输出并清空缓存区。
- close（)方法：关闭输出流

###### Writer

Writer类是字符输出流的抽象类，所有字符输出类的实现都是它的子类。Writer的层次结构如下图：

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/Writer.png)

### File类

File类是java.io包中唯一代表磁盘文件本身的对象，可以通过File类中的一些方法，实现创建、删除、重命名文件等操作。File类中的对象主要用来获取文件本身的一些信息，如文件所在的目录、文件的长度、文件的读写权限。

#### 文件的创建与删除

1. File(String pathname)：此构造方法通过将给定路径名字符串转换成抽象路径名来创建一个新File实例，语法结构如下：

   ```
   new File(String pathname);
   //实例
   File file=new File("d:/1.txt");
   ```

2. File(String parent,String child):根据定义的父路径和子路径字符串创建一个新的File对象，语法如下：

   ```
   new File(String parent,String child);
   ```

3. File(File f,String parent)：该构造方法根据parent抽象路径名和child路径字符串创建一个新的File实例，语法如下：

   ```
   new File(File f,String child);
   ```



#### 获取文件信息

File类提供了很多获取文件信息的方法，如下。

1. getName()方法：返回值是String，获取文件的名称。
2. canRead()方法：返回值是boolean，用来判断文件是否是可读的。
3. canWrite()方法：返回值是boolean，用来判断文件是否可被写入。
4. exits()方法：返回值是boolean，用来判断文件是否存在。
5. length()方法：返回值是long，用来获取文件的长度。
6. getAbsolutePath()方法：返回值是String，用来获取文件的绝对路径。
7. getParent()方法：返回值是String，用来获取文件的父路径。
8. isFile()方法：返回值是boolean，用来判断文件是否存在。
9. isDirectory方法：返回值是boolean，用来判断文件是否为一个目录。
10. isHidden()方法：返回值是boolean，用来判断文件是否为隐藏文件。
11. lastModified()方法：返回值是long，用来获取文件最后修改时间。

以下为例子

```
import java.io.File;
import java.sql.SQLOutput;

public class FileTest {
    public static void main(String[] args) {
        //File file=new File("D:/1.txt");
        //File file=new File(")
        File file=new File("D:/school/","letter.txt");
        if (file.exists()){
            file.delete();
            System.out.println("文件已删除");
        }else {
            try{
                file.createNewFile();
                System.out.println("文件已创建");
                String name=file.getName();
                long length=file.length();
                boolean hidden=file.isHidden();
                System.out.println("文件名字"+name);
                System.out.println("文件长度"+length);
                System.out.println("该文件是否为隐藏文件"+hidden);
            }catch (Exception e){
                e.printStackTrace();
            }
        }

    }
}

```

### 文件输入/输出流

#### FileInputStream与FileOutputStream类

FileInputStream与FileOutputStream类都用来操作磁盘对象，FileInputStream类继承自InputStream类，FileOutputStream类继承自OutputStream类。

FileInputStream类常用的构造方法：

```
FileInputStream(String name);
FileInputStream(File file);
```

FileOutputStream类常用的构造方法：创建一个FileOutputStream对象时，可以指定不存在的文件名，但此文件不能是一个已被其他程序打开的文件。

```
FileOutputStream(String name);
FileOutputStream(File file);
```

以下是例子

```
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;

public class FileTest2 {
    public static void main(String[] args) {
        File file=new File("D:/word.txt");
        try{
            FileOutputStream out=new FileOutputStream(file);
            byte[] buy="我u一直是的哈手机号大数据库打卡机是 ".getBytes();
            out.write(buy);
            out.close();
        }catch (Exception e){
            e.printStackTrace();
        }
        try{
            FileInputStream in=new FileInputStream(file);
            byte[] bytes=new byte[1024];
            int len=in.read(bytes);
            System.out.println("文件的信息是"+new String(bytes,0,len));
            in.close();
        }catch (Exception e){
            e.printStackTrace();
        }
    }
}

```

#### FileReader和FileWriter类

FileInput Stream和FileOutputStream这两个类只提供了对字节或字节数组的读取方法，如果是读取汉字的话，使用字节流，如果读取不好的话会出现乱码现象，此时采用字符流Reader或Writer类就可避免这种现象。

### 带缓存的输入/输出流

缓存是I/O的一种性能优化，缓存流为I/O流增加了内存缓存区，有了缓存区，使得在流上执行skip()，mark()，reset()方法都成为可能。

#### BufferedInputStream和BufferedOutputStream类

###### BufferedInputStream

BufferedInputStream类可以对所有InputStream类进行带缓存区的包装已达到性能的优化，BufferedInputStream类有两个构造方法：第一种构造方法创建了一个带有32个字节的缓存流，第二种构造方法按指定的大小来创建缓存区，一个最优 的缓存区的大小，取决于它所在的操作系统、可用的内存空间和机器配置。

```
BufferedInputStream（InputStream in）；
BufferedInputStream（InputStream in，int size）；
```

下图为BufferedInputStream的读取文件过程

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/BufferedInputStream.png)

###### BufferedOutputStream

使用BufferedOutputStream输出信息和使用OutputStream输出信息完全一样，但是BufferedOutputStream类有一个flush()方法用来将缓存区的数据强制输出完，BufferedOutputStream类有两个构造方法：

```
BufferedOutputStream(OutputStream in);
BufferedOutputStream(OutputStream in,int size);
```

**注意** ：flush()方法就是用于即使在缓存区没有满的情况下，也将缓存区的内容强制写入到外设，flush()方法只对使用缓存区的OutputStream类的子类有效，当调用close()方法时，系统在关闭流之前，也会将缓存区中的信息刷新到磁盘文件中

#### BufferedReader和BufferedWriter类

###### BufferedReader

常用方法：

- read()方法：读取单个字符。
- readLine()方法：读取一个文本行，并将其返回为字符串，若无数据可读，则返回null。

###### BufferedWriter

常用方法：

- write(String s,int off,int len)方法：写入字符串的某一部分。
- flush()方法：刷新该流的缓存。
- newLine()方法：写入一个行分隔符。

**注意**：在使用BufferedWriter类的Write()方法时,数据并没有立刻被写入输出流，而是首先进入缓存区中，如果向立刻将缓存区中的数据写入输出流，一定要调用flush()方法。下面是例子。

```
import java.io.*;

public class BufferedTest {
    public static void main(String[] args) {


    String content[]={"好久不见","最近好吗","再联系"};
    File file=new File("D:/wordd.txt");
    try{
        FileWriter fileWriter=new FileWriter(file);
        BufferedWriter bufferedWriter=new BufferedWriter(fileWriter);
        for (int i=0;i<content.length;i++){
            bufferedWriter.write(content[i]);
            bufferedWriter.newLine();
        }
        bufferedWriter.close();
        fileWriter.close();
    }catch(Exception exception){
        exception.printStackTrace();
    }
    try{
        FileReader fileReader=new FileReader(file);
        BufferedReader bufferedReader=new BufferedReader(fileReader);
        String s=null;
        int k=0;
        while ((s=bufferedReader.readLine())!=null){
            k++;
            System.out.println("第"+k+"行"+s);
        }
        bufferedReader.close();
        fileReader.close();
    }catch (Exception e){
        e.printStackTrace();
    }
}
}

```



# 2019-4-17-java学习十四（反射）

### Class类的使用

类也是对象，都是java.lang.Class的实例对象，这个对象我们称为该类的类类型。

# 2019-4-15-java学习十五（枚举类型和泛型）

# 2019-4-18-java学习十六（多线程）

### 线程简介

Java语言提供了并发机制，可以在程序中执行多个线程，每一个线程完成一个功能，并与其他线程并发执行，这种机制称为多线程。

多线程在Windows操作系统中的运行模式，Window操作系统就是多任务操作系统，它以进程为单位，一个进程是一个包含有自身地址的程序，每个独立执行的程序称为进程，也就是正在执行的程序，**系统可以分配给每个进程一段有限的使用CPU的实践（也可以称为CPU时间片），CPU在这段时间内执行某个进程，然后下一个时间片又跳至另一个进程中去执行，由于CPU转换够快，所以使得每个进程好像同时执行了一样。**

一个线程则是进程中的执行流程，一个进程中可以同时包括多个线程，每个线程可以得到一小段程序的执行时间，这样一个进程就可以具有多个并发执行的线程，在单线程中，程序代码按调用顺序依次往下执行，如果需要一个进程同时完成多段代码的操作，就需要产生多线程。

### 实现进程的两种方式

#### 继承Tread类

Tread类是java.lang包中的一个类，从这个类中实例化的对象代表线程，程序员启动一个新线程需要建立Tread实例，Thread类中常用的两个构造方法如下：

```
public Thread():创建一个新的线程对象。
public Thread()(String threadName):创建一个名称为threadName的线程对象。
```

继承Thread类创建一个新的线程的语法如下：

```
public class ThreadTest extends Thread{
}
```

完成线程真正功能的代码放在类的run()方法中，当一个类继承Tread类后，就可以在该类中覆盖run()方法，将实现线程功能的代码写入run()方法中，然后同时调用Thread类中的start()方法执行线程，也就是调用run()方法。

Thread对象需要一个任务来执行，任务是指线程在启动是执行的工作，该工作的功能代码被写在run()方法中，run()方法必须使用下列语法结构：

```
public void run(){
    
}
```

当执行一个线程程序的时候，就自动产生一个线程，主方法正是在这个线程上运行的，当不再启动其他线程时，该线程就为单线程程序。主方法线程是由java虚拟机负责，而自己的线程就需要自己来启动，代码如下：

```
public static void main(String[] args){
    new ThreadTest.start();
}
```

下面是一个例子：

```
public class ThreadTest extends Thread {
    private int count=10;
    public void run(){
        while (true){
            System.out.println(count+"");
            if (--count==0){
                return;
            }
        }
    }

    public static void main(String[] args) {
        new ThreadTest().start();
    }
}

```

#### 实现Runnable接口

到目前为止，线程都是通过扩展Thread类来创建的，但是如果你的程序需要继承其他的类，也就是非Thread类，而且还需要使用当前类实现多线程，就可以通过Runnable接口来实现，实现Runnable接口的语法如下：

```
public class ThreadTest extends Object implements Runnable
```

**注意**：实际上Thread类实现了Runnable接口，其中的run()方法正是对Runnable接口中的run()方法的具体实现。

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/Thread.png)

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/Runnable.png)

实现Runnable接口的程序会先创建一个Thread对象，并将Runnabled对象和Thread对象相关联，Thread类中有两个构造方法：

```
public Thread(Runnable target)
public Thread(Runnable target,String name)
```

这两个构造方法的参数都存在Runnable实例，使用以上的构造方法就可以把Runnable

实例和Thread实例相关联。

使用Runnable接口启动新的线程的步骤如下：

1. 建立Runnable对象
2. 使用参数为Runnable对象的构造方法创建Thread实例
3. 调用start()方法启动线程

例子如下：

```
public class RunnableTest implements Runnable {
    private int count = 15;

    public void run() {
        while (true) {
            System.out.println(count + "");
            if (--count == 0) {
                return;
            }
        }
    }

    public static void main(String[] args) {
        RunnableTest runnableTest = new RunnableTest();
        Thread t1 = new Thread(runnableTest);
        t1.start();
    }
}
```

### 两种方式的优劣

- 一般都是用实现Runnable接口的方式来进行多线程程序的编写，因为java只能单继承，如果你要继承其他的类，而且还要实现子线程的话，就不能使用继承与Thread类，只能使用实现Runnable接口的方式
- 如果一个类继承了Thread类，则不适合资源共享，如果实现了Runnable接口的方式，非常适合进行资源共享
- 如果继承与Thread类，线程代码是放在Thread子类run()方法中，如果是实现Runnable接口的话，线程代码是放在接口的子类的run()方法中。

### 线程的生命周期

线程具有生命周期，其中包含7种状态，分别是：

- 出生状态：线程被创建时处于的状态，实例调用start()方法之前都处于出生状态。
- 就绪状态：当用户调用start()方法后，线程处于就绪状态。
- 运行状态：当线程得到系统资源后就进入运行状态。
- 等待状态：当处于运行状态下的线程调用Thread类中的wait()方法时，该线程便进入等待状态，进入等待状态的线程必须调用Thread类中的notify()方法才能被唤醒，而notifyAll()方法是将所以处于等待状态下的线程唤醒。
- 休眠状态：当线程调用Thread类中的sleep()方法时，则会进入休眠状态。
- 阻塞状态：如果一个线程在运行状态下发出输入/输出请求，该线程将进入阻塞状态，在其等待输入/输出结束时线程进入就绪状态，对于阻塞的线程来说，即使系统资源空闲，线程依然不能回到运行状态。
- 死亡状态：当线程的run()方法执行完毕时，线程进入死亡状态。

下面是线程的生命周期状态图：

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/Thread01.png)

使线程处于就绪状态有以下几种方法：

1. 调用sleep()方法
2. 调用wait()方法
3. 等待输入/输出完成

当线程处于就绪状态后，使线程再次进入运行状态有以下几种方法：

1. 线程调用notify()方法
2. 线程调用notifyAll()方法
3. 线程调用interrupt()方法
4. 线程的休眠时间结束
5. 输入/输出结束

### 操作线程的方法

#### 线程的休眠

一种控制线程行为的方法是调用sleep()方法，sleep()方法需要一个参数用于指定该线程休眠的时间，该时间以毫秒为单位，语法如下：

```
try{
    Thread.sleep（2000）；
}catch（InterruptedException e）{
    e.printStackTrace();
}

```

使用了sleep()方法的线程在一段时间内会醒来，但是并不能保证它醒来后进入运行状态，只能保证它进入就绪状态。

#### 线程的加入

当某个线程使用join()方法加入到另外一个线程时，另一个线程会等待该线程执行完毕后在继续执行。例子如下：

```
public class JoinTest implements Runnable {
    private int count = 15;

    public void run() {
        while (true) {
            try {
                System.out.println(count + "");
                if (--count == 0) {
                    return;
                }
            }catch (Exception e){
                e.printStackTrace();
            }
        }

    }
    public static void main(String[] args) {
       try {
           JoinTest joinTest = new JoinTest();
           Thread t1 = new Thread(joinTest);
           t1.start();
           t1.join();
           System.out.println("执行了子线程在执行主线程");
       }catch (InterruptedException e){
           e.printStackTrace();
       }
    }
}

```

运行结果如下图：

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/JoinTest.png)

#### 线程的中断

以前是使用stop()方法来停止线程，现在的JDK已经废除了stop()方法，现在提倡在run()方法中使用无限循环的形式，然后使用一个布尔型标记控制循环的停止。例子如下：

```
public class Interrupted implements Runnable{
    private boolean isContinue=false;
    public void run(){
        while(true){
            //····
            if(isContinue)
            break;
        }
    }
    public void setContinue(){
        this.isContinue=true;
    }
}

```

如果线程使用了sleep()方法或wait()方法进入就绪状态，可以使用Thread类中interrupt()方法使线程离开run()方法。同时结束进程，但是程序会抛出InterruptException异常，用户可以在处理该异常的时候完成线程的中断业务处理，如终止while循环。例子如下：

```
public class InterruptedTest extends Thread {
    public InterruptedTest(String name){
              super(name);
    }
   public void run(){
       try {
           int i=0;
           while (!isInterrupted()) {
               Thread.sleep(100); // 休眠100ms
               i++;
               System.out.println(Thread.currentThread().getName()+" ("+this.getState()+") loop " + i);
           }
       } catch (InterruptedException e) {
           System.out.println(Thread.currentThread().getName() +" ("+this.getState()+") catch InterruptedException.");
       }
   }
    public static void main(String[] args) {
        try {
            Thread t1 = new InterruptedTest("t1");  // 新建“线程t1”
            System.out.println(t1.getName() +" ("+t1.getState()+") is new.");

            t1.start();                      // 启动“线程t1”
            System.out.println(t1.getName() +" ("+t1.getState()+") is started.");

            // 主线程休眠300ms，然后主线程给t1发“中断”指令。
            Thread.sleep(300);
            t1.interrupt();
            System.out.println(t1.getName() +" ("+t1.getState()+") is interrupted.");

            // 主线程休眠300ms，然后查看t1的状态。
            Thread.sleep(300);
            System.out.println(t1.getName() +" ("+t1.getState()+") is interrupted now.");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
   }



```

运行结果如下;

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/Interrupt.png)

#### 线程礼让

Thread类中提供了一种礼让方法，使用yield()方法，它只是给当前正处于运行状态的线程一个提醒，告知它可以将资源礼让给其他线程，但这仅是一种暗示，没有任何一种机制保证当前线程会将资源礼让。

yield()方法使具有同样优先级的线程有进入可执行状态的机会，当当前线程放弃执行权时会再度回到就绪状态。

对于支持多任务的操作系统来说，不需要调用yield()方法，因为操作系统会为线程自动分配CPU时间片来执行。

### 线程的优先级

如果有很多进程处于就绪状态，系统会根据优先级决定首先使用哪个线程进入运行状态，但这并不意味着低优先级的线程得不到运行，而只是它运行的几率比较小，如垃圾回收线程的优先级就较低。

Thread类中包含的成员变量代表了线程的某些优先级，如Thread.MIN_PRIORITY(常数1)、Thread.MAX_PRIORITY(常数10）、Thread.NORM_PRIORITY(常数5)，其中每个线程的优先级都在Thread.MIN_PRIORITY(常数1)~Thread.MAX_PRIORITY(常数10）之间，在默认情况下，其优先级都是Thread.NORM_PRIORITY(常数5)，每个新产生的线程都继承了父线程的优先级。

线程的优先级可以使用setPriority()方法调整，如果使用该方法设置的优先级不在1~10之间，将产生IllegalArgumentException异常。

对于处于优先级状态下的运行顺序,举个例子。有四个线程，优先级5的A和B，优先级4的C,优先级3的D，首先是优先级5的线程A首先得到CPU时间片，当该时间结束时，轮换到与线程A相同优先级的线程B，当线程B的运行时间结束后，会继续轮换到线程A，直到线程A和B都执行完毕，才会轮到线程C，当线程C完毕之后，才能轮到线程D。

### 线程同步

线程同步机制的产生是由于在多线程编程中资源访问冲突，线程同步是为了防止资源访问的冲突。

#### 线程安全

以下是资源冲突出现问题的例子：

```
public class ThreadSafeTest implements Runnable{
    int num=10;
    public void run(){
        while (true){
            if(num>0){
                try{
                    Thread.sleep(100);
                }catch (Exception e){
                    e.printStackTrace();
                }
                System.out.println("tickets"+num--);
            }
        }
    }
    public static void main(String[] args) {
        ThreadSafeTest threadSafeTest=new ThreadSafeTest();
        Thread a=new Thread(threadSafeTest);
        Thread b=new Thread(threadSafeTest);
        Thread c=new Thread(threadSafeTest);
        Thread d=new Thread(threadSafeTest);
        a.start();
        b.start();
        c.start();
        d.start();
    }
}


```

运行结果如下：

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/ThreadSafeTest.png)

造成这个结果的原因是：这四个线程都执行run()方法，在num变量为1时，线程1、线程2、线程3、线程4都对num这个变量有存储功能，当线程1执行run()方法时，还没有来得及做递减操作，就指定它调用sleep()方法进入就绪模式，这时线程2、线程3、线程4都进入run()方法，发现num变量依然大于0，但此时线程1休眠时间已到，将num变量值递减，同时线程2、线程3、线程4也对num变量进行递减操作，从而产生了负值。

#### 线程同步机制

###### 同步块

在Java中提供了同步机制，可以有效地防止资源冲突，同步机制使用synchronized关键字。其语法如下：

```
synchronized(Object){
}

```

以下是上面线程安全的解决方案：

```
public class ThreadSafeTest implements Runnable{
    int num=10;
    public void run(){
        while (true){
            synchronized (""){
            if(num>0){
                try{
                    Thread.sleep(100);
                }catch (Exception e){
                    e.printStackTrace();
                }
                System.out.println("tickets"+num--);
            }
        }}
    }
    public static void main(String[] args) {
        ThreadSafeTest threadSafeTest=new ThreadSafeTest();
        Thread a=new Thread(threadSafeTest);
        Thread b=new Thread(threadSafeTest);
        Thread c=new Thread(threadSafeTest);
        Thread d=new Thread(threadSafeTest);
        a.start();
        b.start();
        c.start();
        d.start();
    }
}


```

运行结果如下：

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/synchronized.png)

打印结果没有出现负数是因为将资源放在了同步块中，这个同步块也被称为临界区。这样讲共享资源放置在synchronized定义的区域中，这样其他线程也获取这个锁时，必须等待被释放时才能进入该区域，Object为任意一个对象，每个对象都存在一个标志位，并具有两个值，分别是0和1，一个线程运行到同步块时首先检查该对象的标志位，如果为0状态，表明此同步块中存在其他线程运行，这个该线程就处于就绪状态，直到处于同步块中的线程执行完同步块中的代码为止，这时该对象的标志位被设置为1，该线程才能执行同步块中的代码，并将Object对象的标志位设置为0，防止其他线程执行同步块中的代码。

###### 同步方法

同步方法就是在方法前面修饰synchronized关键字的方法，其语法如下：

```
synchronized void f(){
}

```

当某个对象调用了同步方法时，该对象上的其他同步方法必须等待该同步方法执行完毕后才能被执行，必须将每个能访问共享资源的方法修饰为synchronized，否则就会出错，以下为例子：

```
public class ThreadSafeTest implements Runnable{
    int num=10;
    public synchronized void doit(){
        if(num>0){
            try{
                Thread.sleep(100);
            }catch (Exception e){
                e.printStackTrace();
            }
            System.out.println("tickets"+num--);
        }
    }
    public void run(){
        while (true){
            doit();
        }
    }
    public static void main(String[] args) {
        ThreadSafeTest threadSafeTest=new ThreadSafeTest();
        Thread a=new Thread(threadSafeTest);
        Thread b=new Thread(threadSafeTest);
        Thread c=new Thread(threadSafeTest);
        Thread d=new Thread(threadSafeTest);
        a.start();
        b.start();
        c.start();
        d.start();
    }
}


```

运行结果如下：

![Image1](https://github.com/aaaxma/JavaNote/blob/master/images/synchronized.png)

# 2019-4-20-java学习十七（网络编程）