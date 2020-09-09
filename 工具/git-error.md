# 2019-4-23-git-error（一）

### 问题描述

出现以下错误：

```
$ git add .
warning: LF will be replaced by CRLF in .idea/workspace.xml.
The file will have its original line endings in your working directory
```

### 问题解决

windows中的换行符为 CRLF， 而在linux下的换行符为LF，所以在执行add . 时出现提示，解决办法：

```
$ rm -rf .git  // 删除.git
$ git config --global core.autocrlf false  //禁用自动转换  
```

然后重新运行命令：

```
$ git init  
$ git add .
```



# 2019-4-5-git-error（二）

### 问题描述

从github上把仓库克隆下来之后，修改了某些文档，但是也在github上修改了某些东西，当我`git push origin master`的时候就出现了以下错误。这个错误的原因是因为我在本地修改了文档，但是我在github上也修改了文档，所以就出现这个错误。

![Image3](https://github.com/aaaxma/JavaNote/blob/master/images/Image4.png)

### 问题解决

遇到这种情况可以使用`git pull --rebase origin master`来同步一下本地仓库和远程仓库的文件，然后再进行`git push origin master`

如果还不行的话你就重新`clone`一下仓库，然后尽量别修改github上的文件。