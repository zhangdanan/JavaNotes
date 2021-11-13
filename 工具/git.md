### 学习目标

要掌握的问题：

- 什么是Git以及Git的工作原理
- Git的常用命令Best Practise（避坑教学）
- Git冲突是怎么引起的，如何解决
- Git flow规范团队git使用教程

### 1.秘钥配置

想要本地推送到远程仓库或者是克隆仓库，需要ssh密钥

**查看ssh**

```
查看电脑是否存在id_rsa.pub
cd ~/.ssh
如果不存在则会提示No such file or directory 否则会自动进入目录，用ls就可以看到
ls
id_rsa  id_rsa.pub
```

**创建一个SSH key**

```
ssh-keygen -t rsa -C "your_email@example.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/user/.ssh/id_rsa)://可以指定⽬
录也可以不指定⽬录。直接回⻋
Enter passphrase (empty for no passphrase):
Enter same passphrase again://可以不输⼊密码，直接回⻋，以后每次push就不⽤输⼊密码
Your identification has been saved in /c/Users/user/.ssh/id_rsa.
Your public key has been saved in /c/Users/user/.ssh/id_rsa.pub.
The key fingerprint is:
这⾥是⽣成的key fingerprint
The key's randomart image is:
这⾥是⽣成的key's randomart image
此时创建ssh成功
```

### 2.git常用命令

**创建版本库**

```
git init
git add .   /git add <file name>
git commit -m "****" //说明修改内容
```

**仓库克隆**

```
git clone xxxxx.git    //默认是main分支
git clone -b <branch_name>  xxxxxx.git   //克隆特定分支
```

**远程推送**

```
git remote add origin xxxxx.git
git push -u origin <branch_name>
```

删除远程分支

```
git push origin -d <branch_name>
```

删除本地分支

```
git branch -D <branch_name>
```

查看本地分支和远程分支

```
git branch      //查看本地分支
git branch -a   //查看远程仓库和本地所有分支
```

创建分支

```
git checkout -b <branch_name>    //创建并切换到当前分支
等同于
git branch <branch_name>
git checkout <branch_name>
```

切换当前分支

```
git checkout <branch_name>
```

其他命令

```
git branch --set-upstream-to=origin/dev     //设置git push.pull默认的提交获取分支

git branch --unset-upstream master      //取消对master的跟踪

git status        //显示工作区状态

git init         //初始化仓库

git log          //日志功能

git merge dev      //合并并指定分支到当前分支

git stash         //把当前的工作现场储藏起来，以备以后继续合作

git stash list     //查看隐藏的工作区

git checkout -b branch-name origin/branch-name    //在本地创建和远程分支对应的分

git branch --set-upstream branch-name origin/branch-name   //建立本地分支和远程分支的关联

git rebase rebase   //可以把本地未push的分支提交历史整理成直线

git remote   //可以查看关联的远程仓库

git remote -v   //可以查看关联的远程仓库的具体url
```

**注意**

当git无法自动合并冲突时，应先解决冲突再提交，再合并**git status**查看冲突的文件**git log --graph**可以看到分支合并图

### 3.使用git回滚版本

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
