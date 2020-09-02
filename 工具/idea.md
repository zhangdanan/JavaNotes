# 2019-4-19-idea快捷键

### 1、一次性添加多行注释的快捷键

首先选中要注释区域，然后

ctrl+/ 这个是多行代码分行注释，每行一个注释符号

ctrl+shift+/ 这个是多行代码注释在一个块里，只在开头和结尾有注释符号

### 2、取消多行注释快捷键

怎样添加快捷键的，用相同方法取消，

如 ctrl+/ 添加注释，则ctrl+/取消注释

ctrl+shift+/添加注释，则ctrl+shift+/取消注释

<https://blog.csdn.net/qq_34581118/article/details/78409782>

<https://blog.csdn.net/JavaCoder_juejue/article/details/82730819>	

### 3.取消大小写敏感

具体步骤：File | Settings | Editor | General | Code Completion Case | Sensitive Completion = None



这样在编写代码的时候，代码的自动提示将更加全面和丰富



### 4.快捷键

**A. 按【鼠标中键】快速打开智能提示，取代alt+enter 。**

File->Settings-> Keymap-> 搜索 Show Intention Actions -> 添加快捷键为鼠标中键。

**B. 按【F2】快速修改文件名，告别双手操作。**

File->Settings-> Keymap-> 搜索 Rename -> 将快捷键设置为F2 。

**C. 按【F3】直接打开文件所在目录，浏览一步到位。**

File->Settings-> Keymap-> 搜索 Show In Explorer -> 将快捷键设置为F3 。

**D. 按【Ctrl+鼠标右键】直接打开实现类，方便开发查询。**

File->Settings-> Keymap-> 搜索 implementation-> Add Mouse Shortcut 将快捷键设置为Ctrl+ 鼠标右键。





### 5.视图查看

Ctrl+F12 查看file，method结构图、类继承机构图

Ctrl+shift+Alt+U 查看maven依赖，类图

Ctrl＋Alt+H 查看方法调用层次；



### 6.定位

1.项目之间的跳转
Ctrl+Alt+[　　跳转到下一个项目
Ctrl+Alt+]　　跳转到上一个项目


2.文件之间的跳转
Ctrl+E　　 定位到最近浏览过的文件 
Ctrl+Shift+E　　最近更改的文件
Shift+Click　　可以关闭文件


3.位置的跳转
Ctrl+Shift+Backspace　　 跳转上一次修改的地方
Ctrl+Alt+B　　跳转到方法实现处
Ctrl+Shift+左箭头　　上一个浏览的地方
Ctrl+Shift+右箭头　　下一个浏览的地方


4.其他的跳转
Ctrl+H　　显示类结构图（类的继承层次）
Ctrl+Q　　显示注释文档
Alt+1　　快速打开或隐藏工程面板
Alt+left/right　　切换代码视图
F2 或 Shift+F2　　高亮错误或警告快速定位
Tab　　代码标签输入完成后，按 Tab，生成代码
Ctrl+Shift+F7　　高亮显示所有该文本，按 Esc 高亮消失


5.搜索
Ctrl＋N　　快速搜索类
Ctrl＋Shift＋N　　快速搜索文件
Ctrl＋Alt+Shift＋N　　快速搜索函数
三个里面都有Include non-porjecct items选项,勾选则表示非当前文件中的jar里面所有的类也会被查找；

![img](https://pic4.zhimg.com/80/v2-40ef41c44d56d496e5b245f79ecc40e7_hd.jpg)


Ctrl+Shift+F　　快速搜索字符串

![img](https://pic2.zhimg.com/80/v2-d45daf84b5eed513ed78eb48153b6fe1_hd.jpg)


Alt+F1　　查找代码所在位置
Alt+F3　　逐个往下查找相同文本，并高亮显示


6.光标移动和选中
Ctrl＋Alt+Shift＋J 选中所有相应的目标
Alt+Up/Down　　在方法间快速移动定位
Ctrl+Shift+Up/Down　　向上/下移动语句
*Ctrl+Up/Down　　光标中转到第一行或最后一行下*
*Ctrl+B/Ctrl+Click　　快速打开光标处的类或方法（跳转到定义处）*



### 7.Alt+Enter

1. 代码提示
2. 自动创建函数
3. list replace
4. 实现接口
5. 单词拼写
6. 导包

### 8.重构

shift+F6   重命名

ctrl+F6     重构函数

### 9.idea代码规范插件

在IEDA中，file->settings->plugins,然后搜索alibaba，就会出现如下界面，我们只需要下载，安装，然后重启我们的IDEA就可以使用；

