# 2019-8-7-git常用命令

### 1.秘钥配置

配置用户名

```
git config --global user.name "XXXXXXXXX"
```

配置邮箱

```
git config --global user.email "XXXXXXXX@163.com"
```

然后在你的C:\Users\Administrator目录下会生成.gitconfig配置文件

然后使用命令

```
ssh-keygen -t rsa -C "XXXXXXXX@163.com"
```

生成的路径是`C:\Users\Administrator\.ssh`

在这个文件夹下面有两个文件一个是私钥`id_rsa`这个是自己留着的，一个是公钥`id_rsa.pub`,公钥可以添加在github、gitlab等代码管理平台。

### 2.更新远程仓库的代码

对于如何更新git服务器上的代码

首先把仓库克隆下来**git clone** [ssh://git@192.168.85.209:10022/hxy1993/develope-code.git](ssh://git@192.168.85.209:10022/hxy1993/develope-code.git)

然后进入你克隆的仓库里面进行操作

**git add .**添加所有的文件夹到缓存区

**git commit -m “注释”**提交到分支master下

**git push -u origin master** 

把你的代码push到远程仓库上面如果没有关联远程仓库，请使用命令**git remote add origin**  [ssh://git@192.168.85.209:10022/hxy1993/develope-code.git](ssh://git@192.168.85.209:10022/hxy1993/develope-code.git)

### 3.创建分支

`git checkout -b dev`**创建dev分支**

`git branch`**显示现在所在分支**

`git checkout master`**切换到master分支**

`git push origin dev`**提交该分支到远程仓库**

`git brach -d dev`**删除分支**

`git branch --set-upstream-to=origin/dev`**设置git push.pull默认的提交获取分支**

`git branch --unset-upstream master`**取消对master的跟踪**

### 4.别的命令

`git status`**显示工作区状态**

`git init`**初始化仓库**

`git log`**日志功能**

`git push origin master`**将本地master分支的最新修改推送到远程仓库**

`git merge dev`**合并并指定分支到当前分支**

`git stash`**把当前的工作现场储藏起来，以备以后继续合作**

`git stash list`**查看隐藏的工作区**

`git checkout -b branch-name origin/branch-name`**在本地创建和远程分支对应的分支**

`git branch --set-upstream branch-name origin/branch-name`**建立本地分支和远程分支的关联**

`git pull`**抓取远程的提交，或抓取分支l**

`git rebase rebase`**可以把本地未push的分支提交历史整理成直线**

**注意**

当git无法自动合并冲突时，应先解决冲突再提交，再合并**git status**查看冲突的文件**git log --graph**可以看到分支合并图



# 2019-4-23-git需要掌握的知识

要掌握的问题：

- 什么是Git以及Git的工作原理
- Git的常用命令Best Practise（避坑教学）
- Git冲突是怎么引起的，如何解决
- Git flow规范团队git使用教程