# Vue介绍

### vue.js是什么

Vue是一套用于构建用户界面的渐进式框架，与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与[现代化的工具链](https://cn.vuejs.org/v2/guide/single-file-components.html)以及各种[支持类库](https://github.com/vuejs/awesome-vue#libraries--plugins)结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

### Vue.js的优点
1.体积小

压缩后33K

2.更高的运行效率

基于虚拟DOM，一种可以预先通过javascript进行各种计算，把最终的DOM操作计算出来并优化的技术，由于这个dom操作属于预处理操作，并没有真实的操作dom，所以叫虚拟DOM

3.双向数据绑定

让开发者不用再去操作dom对象，把更多的精力用在业务逻辑上。

4.生态丰富

市场上有很多成熟，稳定的基于vue.js的ui框架，组件。

### vue安装

可以通过如下方式引入Vue

```
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

或者：

```
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

Vue Devtools：允许在一个更友好的界面中审查和调试Vue应用

# 创建Vue项目

### 1.使用命令行创建vue项目

选择个文件夹cmd进去

npm install vue-cli -g(下载全局vue-cli)

下载完成后，输入命令vue init webpack  hellovue（hellovue是项目名）

如何他会问你一些问题

①、Project name (myproject)；项目名称（myproject）。（确定按enter，否按N） 

②、 Project description (A Vue.js project)；项目描述（一vue.js项目）。（随意输入一段简短介绍，用英文，不写直接回车也行） 

③、Author (sunsanfeng)；作者（sunsanfeng）。（确定按enter，否按N） 

④、Vue build (Use arrow keys)> Runtime + Compiler: recommended for most usersRuntime-only: about 6KB lighter min+gzip, but templates (or any Vue-specificHTML) are ONLY allowed in .vue files - render 　　　　　　　　functions are required elsewhere；Vue公司的建立（使用箭头键）>运行时+编译器：大多数用户推荐运行时间：约6kb轻民+ gzip，但模板（或任何Vue具体HTML）只允许在。VUE文件渲染功能是必需的其他地方。（按enter） 

⑤、Install vue-router? (Y/n)；安装的路由？（/ N）。（可安可不安，建议安装，因为项目肯定能用上） 

⑥、Use ESLint to lint your code? (Y/n)；使用ESlint语法？（Y/ N）。（使用ESLint语法，就要做好心理准备，除非你非常懂ESLint语法，要不就会处处报错，之前不明白的时候选择过一次，总之很烦，若想要挑战一下，下面这个网址会给你帮助的：https://cloud.tencent.com/developer/chapter/12618        建议N） 

⑦、Setup unit tests with Karma + Mocha? (Y/n)；设置单元测试？（Y / N）。（选N） 

⑧、Setup e2e tests with Nightwatch? (Y/n)；Nightwatch建立端到端的测试？（Y / N）。（选N） ui

 ⑨、should we run 'npm install' for you after the ogject has been created? ;(选择Yes，use NPM)
等待一会，项目就建好了，输入命令cd hellovue进去项目文件中

输入命令：npm install初始化安装依赖

npm run dev执行项目

浏览器打开http://localhost:8080，会看到欢迎页面

### 2.使用vue ui创建项目

命令行输入：npm install -g @vue/cli

然后命令行输入：vue ui













# vue-cli

### 为什么使用vue-cli

vue-cli是vue的脚手架工具

平台无关性，功能更齐全

占内存少，更高效

帮助我们写好vue基础代码的工具

cli：Command-Line-Interface

### 常用的dos命令

cd:打开文件夹

md：创建文件夹

dir：查看文件夹内容

cd..：返回上一级文件夹

### npm和cnpm的区别

npm：是nodejs的包管理器，用于node插件管理（包括安装，卸载，管理依赖等）

cnpm：npm安装插件是从国外服务器下载，受网络影响大，可能出现异常，所以有这个淘宝团队使用国内镜像来代替国外服务器

##### -g参数

全局安装，可以在命令行下直接使用

可以通过`npm root -g`查看全局安装的文件夹位置

##### -S参数

--save安装包信息将加入到dependencies（生产阶段的依赖）

##### -D参数

--save--dev安装包信息将加入到devDependencies（开发阶段的依赖）所以开发阶段一般使用他

##### i参数

i是install的缩写，

### vue-cli2安装

`npm install -g vue-cli`

`cnpm install -g vue-cli`

安装脚手架的时候使用

`npm install -gd express --registry=http://registry.npm.taobao.org`

设置npm的下载位置

`npm config  set registry http://registry.npm.taobao.org`

### cnpm下载安装

