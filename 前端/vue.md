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

# Vue基础

### el挂载点

vue会管理el选项命中的元素及其内部的后代元素，可以使用其他的选择器，但是建议选择ID选择器，

可以使用其他的双标签，但是不能使用html和body。

```
<div id="app" class="app">
    {{ message }}
</div>


<script>
    var app = new Vue({
        el: '#app',
        // el: '.app',
        // el: 'div',
        data: {
            message: 'Hello Vue!'
        }
    })
</script>
```

### data:数据对象

Vue中用到的数据定义在data中，data中可以写复杂的数据，比如对象，数组。渲染复杂类型数据时，遵守js的语法就行，

```
<div id="app">
  {{message}} {{school.name}}{{school.aihao}}
    {{array[0]}}
    {{array[1]}}
    {{array[2]}}
    {{array[3]}}
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            message: "我是张大楠",
            school:{
                name:"张大楠",
                aihao:"看漂亮妹妹"
            },
            array:[1,2,3,4]
        }
    })
</script>
```

### v-text指令

- v-text指令的作用是：设置标签的内容
- 默认写法会替换全部内容，使用差值表达式{{}}可以替换指定内容。
- 内部支持写表达式

```
<div id="app">
    <h2 v-text="message+'好帅'"></h2>
    <h2 v-text="info"></h2>
    {{message}}
    {{info}}
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
           message:"张大楠",
           info:"想看美女"
        }
    })
</script>
```

### v-html指令

- 设置标签的innerHTML
- 内容中有html结构会被解析为标签
- v-text指令无论内容是什么，只会解析为文本

```
<div id="app">
    <h2>{{message}}</h2>
    <h2>{{info}}</h2>
    <h2 v-html="info"></h2>
</div>
<script>
    var app=new Vue({
        el:"#app",
        data:{
            message:"张大楠",
            info:"<a href='https://www.bilibili.com/'>B站</a>"
        },
    })
</script>
```

### v-on指令

- 为元素绑定事件

```
<div id="app">
    <button v-on:click="greet">v-on绑定</button>
    <button v-on:click="doit">v-on简写</button>
    <input type="button" value="test" v-on:click="greet">
    <input type="button" value="test" v-on:click="doit">
</div>
<script>
    var app = new Vue({
        el: '#app',
        methods: {
            greet: function () {
                alert("做it")
            },
            doit: function () {
                alert("这是啥")
            },
        }
    })
</script>
```



### v-if指令

- v-if指令的作用是根据表达式的真假切换元素的显示状态

- 根据表达式的真假，切换元素的显示和隐式（操控dom元素）
- 表达式的值为true时，元素存在于dom树中，为false时，从dom树中移除

```
<div id="app">
    <input type="button" value="显示" v-on:click="add">
    <h2 v-if="isShow" >黑马程序员</h2>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    var app = new Vue({
        el: '#app',
        data:{
            isShow:false
        },
        methods: {
            add: function () {
                this.isShow=!this.isShow
            },
        }
    })
</script>
```

### v-show指令

- v-show指令的作用是根据真假切换元素的显示状态
- 原理是修改元素的display，实现显示隐藏
- 指令后面的内容，最终都会解析为布尔值

```
<div id="app">
    <input type="button" value="测试" v-on:click="changeIsShow">
    <img v-show="isShow" src="https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1141259048,554497535&fm=26&gp=0.jpg" alt="">
</div>	
<script>
        var app=new Vue({
            el:"#app",
            data:{
                isShow:false,
                age:17
            },
            methods: {
                changeIsShow: function () {
                    this.isShow=!this.isShow;
                },
            }
        })
</script>
```

### v-bind指令

- 设置元素的属性（比如src，title，class）
- v-bind的作用是：为元素绑定属性
- 完整写法为v-bind:属性名,简单写法是:属性名
- 需要动态的增删class建议使用对象的形式

```
<div id="app">
    <img v-bind:src="imgsrc" alt="">
    <img v-bind:src="imgsrc" v-bind:title="istitle" v-bind:class="isActive?'active':''" @click="isActive" alt="">
    <img v-bind:src="imgsrc" v-bind:title="istitle" v-bind:class="{active:isActive}" @click="isActive" alt="">
</div>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    var app=new Vue({
        el:"#app",
        data:{
            imgsrc:"https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1141259048,554497535&fm=26&gp=0.jpg",
            istitle:"zhangdanan",
            isActive:false,
        },
        methods:{
            isActive:function () {
                this.isActive=!this.isActive;
            }
        }
    })
</script>
```

### v-for指令

- v-for指令的作用是根据数据生成列表结构
- 数组经常跟v-for结合使用
- 语法为（item，index）in 数据

```
<div id="app">
    <ul>
        <li v-for="(item,index) in array">{{item}}</li>
    </ul>
    <ul>
        <li v-for="(obj,index) in object">{{obj.name}}</li>
    </ul>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    var app=new Vue({
        el:"#app",
        data:{
            array:["zhang","wang","li","zhou","xiang"],
            object:[
                {name:"zhangdanan"},
                {name:"haoshuai"}
            ]
        }
    })
</script>
```

### v-model

- v-model指令的作用是便捷的设置和获取表单元素的值
- 绑定的数据会和表单元素值相关联

```
<div id="app">
    <input type="button" value="修改message" @click="setM">
    <input type="text" v-model="message" @keyup.enter="getM">
    {{message}}
</div>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    var app=new Vue({
        el:"#app",
        data:{
            message:"张大楠最帅"
        },
        methods:{
            getM:function () {
                alert(this.message);
            },
            setM:function () {

                this.message="张小楠";
            }
        }
    })
</script>
```

### axios使用