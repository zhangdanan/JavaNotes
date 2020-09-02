# 1

今天运行npm run dev 报错：missing script:dev

![img](https://upload-images.jianshu.io/upload_images/5836176-72394e44ce32ff02.png?imageMogr2/auto-orient/strip|imageView2/2/w/1106/format/webp)

检查一下该项目文件夹中的package.json文件

![img](https://upload-images.jianshu.io/upload_images/5836176-1f07e4b60c66fa4e.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

在script里，并没有dev，而是serve，应该用npm run serve命令运行vue项目即可

# 2

安装过VUE脚手架，创建项目

vue init webpack vueDemoOne

报错Sorry, name can no longer contain capital letters

翻译了一下，意思就是项目名不能包含大写字母，本来想用驼峰命名但是不行呀，那就改成小写试下吧。

vue init webpack vuedemoone，果然可以成功创建
