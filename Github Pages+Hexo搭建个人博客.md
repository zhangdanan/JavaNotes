### 1.预备工作

1. 首先要提前安装Git和node.js，如果电脑里没有安装的提前安装，这就不详细说明了。
2. 要有github账号，没有GitHub账号的去注册一个。
3. 有git和GitHub账号的，记得提前把ssh密钥添加到GitHub上去，具体的去百度。

### 2.搭建GitHub page

#### 创建仓库

创建一个新的仓库，名字为GitHub名称+github.io，如下图，

![image-20211114142220006](C:\Users\m1885\Desktop\1.png)

#### 开启GitHub Pages

进入设置

![image-20211114142318784](C:\Users\m1885\Desktop\2.png)

找到Pages里的GitHub Pages选项打开它，一般是默认打开的。

![image-20211114142512213](C:\Users\m1885\Desktop\3.png)

设置成功后就可以通过<u>username.github.io</u>来访问你的博客。

### 3.hexo

#### 安装hexo

使用hexo的前置条件是要有git和node.js。提前安装

新建一个文件夹右键选择Git Bash

```
npm install hexo-cli -g    //安装hexo
hexo init                  //初始化网站
npm install 
hexo g                     //生成文件，等同于 hexo generate
hexo s                     //启动本地服务器，等同与 hexo server,这一步之后就可以通过http://localhost:4000查看了
```

对于如何创建一篇文章，你可以手动在source\\\_posts目录下创建xxxx.md，也可以在命令行创建，命令如下

```
hexo new "文章名"          //新建文章
hexo new page "页面名"     //新建页面
```

创建完文章或者上传文章后，先执行hexo g命令生成，如果执行hexo s启动服务器，最后打开http://localhost:4000网址查看，如果想结束查看或者重新编辑文章并上传，按ctrl+c结束hexo s后持续的界面。

#### 添加主题

**安装主题（3-hexo主题）**

cd到文件夹的themes下，

```
hexo clean
git clone git@github.com:yelog/hexo-theme-3-hexo.git
```

**启动主题**

找到目录下的_config.yml文件，打开找到theme设置为theme: 3-hexo

**更新主题**

```
cd themes/hexo-theme-3-hexo
git pull
hexo g
hexo s
```

重新打开http://localhost:4000网址就能看到新的主题。

### 4 使用hexo deploy部署到github上

#### 本地设置

找到目录下的_config.yml文件，添加上下面这些

```
deploy:
    type: git
    repo: git@github.com:xxxxx/xxxxx.github.io.git  #这里的网址填你自己的
    branch: main  
```

因为现在github的更新，以前的分支一般是master，现在的是main，这个一定要注意，不然会失败的。

保存完之后安装一个扩展

```
npm install hexo-deployer-git --save   
```

#### Github设置

添加本地公共密钥到github上。

#### 部署到github

```
hexo d
```

重新打开username.github.io就可以看到你的博客了