### 什么是JUnit

JUnit是一个测试集的简单框架，是xUnit的的一个子集，xUnit是一套基于测试驱动开发的测试框架。包括PythonUnit，CppUnit，JUnit

### 为什么使用JUnit

JUnit使用断言机制，可以把预期的结果和程序最终的结果进行一个比对，确保对结果的可预知性。

### 如何使用JUnit

在idea中编写一个方法，然后使用`Alt+Insert`快捷键生成JUnit测试方法。

**注意事项**

1. 测试方法必须使用@Test进行修饰
2. 测试方法必须使用public void进行修饰，不能带任何的参数
3. 测试单元的每个方法必须可以独立测试，测试方法间不能有任何的依赖
4. 测试用例不是用来证明你是对的，而是用来证明你没有错



### JUnit中的注解

- @Test：将一个普通的方法修饰成为一个测试方法
  - @Test(expected=XX.class）：可以抛出自定义的异常
  - @Test(timeout=毫秒)
- @BeforeClass：它会把所有的方法运行前被执行，static修饰
- @AfterClass：它会在所有的方法运行结束后被执行，static修饰
- @Before：会在每一个测试方法被运行前执行一次
- @After：会在每一个测试方法被运行后执行一次
- @Ignore：方法会被忽略掉
- @RunWith：可以更改测试运行器，org.junit.runner.Runner

例子如下：

```
import org.junit.*;
import static org.junit.Assert.*;
public class CalculateTest2 {
    @Before
    public void setUp() throws Exception {
        System.out.println("this is before");
    }
    @BeforeClass
    public static void set() throws Exception{
        System.out.println("this is before class");
    }
    @AfterClass
    public static void tear() throws Exception{
        System.out.println("this is after class");
    }
    @After
    public void tearDown() throws Exception {
        System.out.println("this is after");
    }
    @Test
    public void add() {
        System.out.println("this is add");
    }
    @Test
    public void divide() {
        System.out.println("this is divide");
    }
}
```

运行结果如下图所示：

![Image](https://github.com/aaaxma/JavaNote/blob/master/images/JUnit.png)