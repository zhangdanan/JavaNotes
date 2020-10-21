### 1.秘钥配置

首先，要有ssh秘钥，在git命令行里面输入**ssh keygen**，如何一直next下去，找到你的用户所在位置有一个.ssh文件夹里，有两个文件id_rsa私钥，id_rsa.pub公钥，把公钥添加到github或者是私有git服务器上

**创建一个SSH key**

```
ssh-keygen -t rsa -C "your_email@example.com"
```

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

`git pul`**抓取远程的提交，或抓取分支**

`git rebase rebase`**可以把本地未push的分支提交历史整理成直线**

**注意**

当git无法自动合并冲突时，应先解决冲突再提交，再合并**git status**查看冲突的文件**git log --graph**可以看到分支合并图

### 5.使用git回滚版本

```
//查看每次操作对于的commitid的账号
git reflog    

//本地端口回滚指定的版本，这种回滚是不可逆的，会导致之前的提交记录都没有了
git reset --hard commitId

//强制推送到远程分支
git push -f

//查看所有提交的版本号
git log --oneline

//git revert命令是撤销某次操作，而在此次操作之前和之后的提交记录都会保留
git revert commitid
```

### git从github上面拉取更新代码

```
git remote   //可以查看关联的远程仓库
git remote -v   //可以查看关联的远程仓库的具体url
```



# 2019-4-23-git需要掌握的知识

要掌握的问题：

- 什么是Git以及Git的工作原理
- Git的常用命令Best Practise（避坑教学）
- Git冲突是怎么引起的，如何解决
- Git flow规范团队git使用教程