# 2019-4-27-junit-error

###  junit 单元测试报错：java.lang.NoClassDefFoundError: org/hamcrest/SelfDescribing

##### 错误如下图：

![Image](https://github.com/aaaxma/JavaNote/blob/master/images/junit.png)

##### 解决方法如下：

 今天在写代码的时候想把老系统里面加上单元测试，所以用最近做的springmvc上的一个项目中的junit扒一个下来：junit-4.12.jar 但是很奇怪在原来系统中好好能运行的，放到现在的项目中就老是报错：java.lang.NoClassDefFoundError: org/hamcrest/SelfDescribing。

疯掉了后来查发现有人说换一个低版本的就行了，引入junit4.10.jar。果然行了，但是我们要知其然更要只其所以然 

> 查官网：JUnit now uses the latest version of Hamcrest. Thus, you can use all the available matchers and benefit from an improved assertThat which will now print the mismatch description from the matcher when an assertion fails.
>
> unit.jar: Includes the Hamcrest classes. The simple all-in-one solution to get started quickly.**Starting with version 4.11, Hamcrest is no longer included in this jar**.
> junit-dep.jar: Only includes the JUnit classes but not Hamcrest. Lets you use a different Hamcrest version.

注意加粗的部分意思是4.11以上版本不在包含hamcrest。
所以现在有两个办法解决：

1. junit版本降到4.10
2. 导入hamcrest-core-1.3.jar

