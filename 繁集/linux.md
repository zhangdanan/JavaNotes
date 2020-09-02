# Linux中查找文件

### 1.使用find命令在Linux中搜索文件和文件夹

find 命令被广泛使用，并且是在 Linux 中搜索文件和文件夹的著名命令。它搜索当前目录中的给定文件，并根据搜索条件递归遍历其子目录。
它允许用户根据大小、名称、所有者、组、类型、权限、日期和其他条件执行所有类型的文件搜索。

```
find / -iname "sshd_config"
```

运行以下命令以查找系统中的给定文件夹。要在 Linux 中搜索文件夹，我们需要使用 -type参数。

```
find / -type d -iname "ssh"
```

使用通配符搜索系统上的所有文件。我们将搜索系统中所有以 .config 为扩展名的文件。

```
find / -name "*.config"
```

使用以下命令格式在系统中查找空文件和文件夹。

```
find / -empty
```

按照文件名查找

```
#在根目录下查找文件httpd.conf，表示在整个硬盘查找
find / -name httpd.conf
#在/etc目录下文件httpd.conf
find /etc -name httpd.conf　　
#使用通配符*(0或者任意多个)。表示在/etc目录下查找文件名中含有字符串‘srm’的文件
find /etc -name '*srm*'
#表示当前目录下查找文件名开头是字符串‘srm’的文件
find . -name 'srm*' 　
```

按照文件特征查找 　　　　　　

```
find / -amin -10 　　# 查找在系统中最后10分钟访问的文件(access time)
find / -atime -2　　 # 查找在系统中最后48小时访问的文件
find / -empty 　　# 查找在系统中为空的文件或者文件夹
find / -group cat 　　# 查找在系统中属于 group为cat的文件
find / -mmin -5 　　# 查找在系统中最后5分钟里修改过的文件(modify time)
find / -mtime -1 　　#查找在系统中最后24小时里修改过的文件
find / -user fred 　　#查找在系统中属于fred这个用户的文件
find / -size +10000c　　#查找出大于10000000字节的文件(c:字节，w:双字，k:KB，M:MB，G:GB)
find / -size -1000k 　　#查找出小于1000KB的文件
```

使用混合查找方式查找文件

参数有： ！，-and(-a)，-or(-o)。

```
find /tmp -size +10000c -and -mtime +2 　　#在/tmp目录下查找大于10000字节并在最后2分钟内修改的文件
find / -user fred -or -user george 　　#在/目录下查找用户是fred或者george的文件文件
find /tmp ! -user panda　　#在/tmp目录中查找所有不属于panda用户的文件
```


原文链接：https://blog.csdn.net/xxmonstor/java/article/details/80507769

### 2.使用locate命令在Linux中搜索文件和文件夹

locate 命令比 find 命令运行得更快，因为它使用 updatedb 数据库，而 find 命令在真实系统中搜索。

locate搜索类似于一种模糊搜索。

这个数据库默认一天一更新，一般新建的文件，如果不手动更新该数据库，在该天内是无法使用locate命令来查看文件位置的，数据库通过 cron 任务定期更新，但我们可以通过运行以下命令手动更新它。

locate搜索类似于一种模糊搜索。

```
sudo updatedb
```

在系统中搜索 ssh 文件夹。

```
locate --basename '\ssh'
```

在系统中搜索 sshd_config 文件。

```
locate --basename '\sshd_config'
```

### 3.使用whereis及which命令

这两个命令用来搜索命令的路径（也遵循/etc/updatedb.conf配置文件的筛选规则）

**whereis 命令名**：搜索命令所在路径及帮助文档所在位置

选项：
-b：只查找可执行文件
-m：只查找帮助文件

**which 命令名**：查找命令是否存在，以及命令的存放位置在哪儿

# Linux常用命令

### mv命令

移动文件到指定文件夹下

```
mv mysql-5.7.24-linux-glibc2.12-x86_64 /usr/local/
```

改名字为mysql

```
mv mysql-5.7.24-linux-glibc2.12-x86_64 mysql
```

### vim命令

我们要知道一些必要的指令，比如：

- ls：显示当前目录的文件&文件夹；

- cd：到某个文件夹去；

- rm：删除文件，如果要删除文件夹的话用rm -r；要知道这种删除不会进回收站，**记得不要随便用rm -rf命令，除非你知道你在干什么！**

- vim：用一个叫做vim的程序进行文件的创建&修改，里面指令挺多的，你可以在网上搜索一下，我们刚开始一定要记得：

- 用 i 进入编辑模式（刚进去就是普通输入指令的模式，按下i之后才能修改这个文件）；
  - 进入编辑模式之后，你可以直接输入，可以用方向键控制光标位置

  - 用 esc按键 退出编辑模式（也就是从按下i的状态进入了普通输入指令的模式）；

  - 用 :wq 退出并保存（在普通输入指令的模式下，记得有前面的一个英文冒号！）；

  - 用 :q! 退出并且不保存；

  - 其他的指令和快捷键能记得就记一下，记不得的话……你用上面的指令也能凑合～

- 直接执行某一个程序的指令

- - 比如你当前目录下有一个脚本文件a.sh要执行，那你可以用 bash a.sh，也可以用 ./a.sh；
  - 如果你有一个python代码a.py要执行，你可以用 python3 a.py；
  - 如果你有一个编译出来的文件 a.out 要执行，直接用 ./a.out；
  - （上面的 文件名 代表 文件的相对/绝对路径）

- 包管理的命令：比如Ubuntu16.04是用apt作为包管理器的，可以用sudo apt install xxx来安装自己需要的软件

### rm文件删除命令

-r 就是向下递归，不管有多少级目录，一并删除

-f 就是直接强行删除，不作任何提示的意思

-i 就是进行交互式地删除

-v 就是详细显示进行地步骤

```
rm -rf /usr/local/mysql
```

就是删除/usr/local/mysql目录以下所有文件，文件夹。

```
rm a.txt
```

就是删除a.txt的这个文件

### 查看系统信息

查看当前系统版本：

```
cat /etc/redhat-release
```