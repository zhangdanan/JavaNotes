# 什么是HTML

HTML 语言用于描述网页。

- HTML 是指超文本标记语言: **H**yper **T**ext **M**arkup **L**anguage
- HTML 不是一种编程语言，而是一种[**标记**语言](https://baike.baidu.com/item/标记语言/5964436?fr=aladdin)
- 标记语言是一套**标记标签** (markup tag)
- HTML 使用标记标签来**描述**网页
- HTML 文档包含了HTML **标签**及**文本**内容
- HTML 文档也叫做 **web 页面**

# HTML标签

HTML 标记标签通常被称为 HTML 标签 (HTML tag)

- HTML 标签是由*尖括号*包围的关键词，比如<html>
- HTML 标签通常是*成对出现*的，比如`<b>`和`</b>`
- 标签对中的第一个标签是*开始标签*，第二个标签是*结束标签*
- 开始和结束标签也被称为*开放标签*和*闭合标签*

# HTML 元素

------

"HTML 标签" 和 "[HTML 元素](https://www.w3cschool.cn/html/html-elements.html)" 通常都是描述相同的意思。

但是严格来讲，一个 HTML元素包含了开始标签与结束标签。

# <!DOCTYPE>声明

`<!DOCTYPE>`是标准通用标记语言的文档类型声明，有助于在浏览器中正确地显示网页。

　由于网络上文件的类型不一，因此需要正确声明 HTML 版本，以使得浏览器能够正确识别并显示您的网页内容。

`doctype`声明是不区分大小写的，

# 中文编码

<head>
<meta charset="UTF-8">
<title>页面标题</title>
</head>

# HTML基础

### HTML标题

HTML 标题（Heading）是通过[ -  ](https://www.w3cschool.cn/htmltags/tag-hn.html)标签来定义的.

这里有六个标题元素标签 —— `<h1>`、`<h2>` 、`<h3>`、`<h4>`、`<h5>`、`<h6>`，每个元素代表文档中不同级别的内容：

` <h1>` 表示主标题（the main heading），`<h2>` 表示二级子标题（subheadings），`<h3>`表示三级子标题（sub-subheadings），`<h4>`、`<h5>`、`<h6>`依次递减字体的大小。

```
<h1>一级标题</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>
<h4>四级标题</h4>
<h5>五级标题</h5>
<h6>六级标题</h6>
```

### HTML段落

HTML 段落是通过标签``来定义的，`P`是英文`paragraph`段落的缩写

```
<p>这是一个段落</p>
```

### HTML空格

无论你用了多少空格（包括空格字符，包括换行），当渲染这些代码的时候，HTML解释器会将连续出现的空格字符减少为一个单独的空格符。

为什么我们会使用那么多的空格呢? 

答案就是为了可读性——如果你的代码被很好地进行格式化，那么就很容易理解你的代码，反之就会很混乱。在我们的HTML代码中，我们让每一个嵌套的元素以两个空格缩进。

### HTML链接

HTML 链接是通过标签`<a>`来定义的。`a`标签，也叫`anchor（锚点）`元素，既可以用来链接到外部地址实现页面跳转功能，也可以链接到当前页面的某部分实现内部导航功能。

```
<a href="http://www.w3cschool.cn">这是一个链接</a>
```

##### target属性

使用 Target 属性，你可以定义被链接的文档在何处显示（在新的窗口打开，还是在原有的窗口中打开）。

```
<a href="//www.w3cschool.cn/" target="_blank">访问W3CSchool教程!</a>
```

**提示：**默认的被链接文档会在原有的窗口中打开的。如果将 target 属性设置为 "_blank" 则文档就会在新窗口打开。

##### id 属性

在HTML文档中插入ID:   

```
<a id="tips">Useful Tips Section</a>
```

在HTML文档中创建一个链接到"有用的提示部分(id="tips"）"：    

```
<a href="#tips">Visit the Useful Tips Section</a>
```

或者，从另一个页面创建一个链接到"有用的提示(id="tips"）部分"：  

```
<a href="//www.w3cschool.cn/html_links.html#tips"> Visit the Useful Tips Section</a>
```

### HTML图片

HTML 图像是通过标签`<img>`来定义的。使用`img`元素来为你的网站添加图片，使用`src` 属性指向一个图片的具体地址。

请注意：`img`元素是自关闭元素，不需要结束标记。

```
<img src="logonew2.png" width="206" height="36">
```

##### Alt属性

　`alt`属性用来为图像定义一串预备的可替换的文本

##### 设置图像的高度和宽度

```
<img src="pulpit.jpg" alt="Pulpit rock" width="304" height="228">
```

##### 设置图像边框

```
<img src="/statics/images/course/pulpit.jpg" alt="Pulpit rock" border = "3">
```

设置图像对齐

```
<img src="/statics/images/course/pulpit.jpg" alt="Pulpit rock" align="right">
```

### HTML强调

​	在HTML中我们可以使用`em（emphasis）`元素来标记这样的情况，浏览器默认风格为斜体：

```
<p>I am <em>glad</em> you weren't <em>late</em>.</p>
```

在HTML中我们还可以使用`(strong importance)`元素来标记这样的请况，浏览器默认风格为粗体：

```
<p>This liquid is <strong>highly toxic</strong>.</p>
<p>I am counting on you. <strong>Do not</strong> be late!</p>
```

### HTML水平线

<hr> 标签在 HTML 页面中创建水平线。

hr 元素可用于分隔内容，使用该元素产生的水平线可以在视觉上将文档分隔成各个部分。

### HTML注释

```
<!-- 这是一个注释 -->
```

### HTML折行

如果您希望在不产生一个新段落的情况下进行换行（新行），请使用 <br/>标签。

在 HTML 语言中， <br/>标签定义为一个换行符，它可以理解为简单的输入一个空行，而不是用来对内容进行分段：

### HTML文本格式化标签

|   标签    | 描述         |
| :-------: | ------------ |
| ***<b>*** | 定义粗体文字 |
|   <em>    | 定义着重文字 |
|    <i>    | 定义斜体文字 |
|  <small>  | 定义小号字   |
| <strong>  | 定义加重字   |
|   <sub>   | 定义下标字   |
|   <sup>   | 定义上标字   |
|   <del>   | 定义删除字   |
|   <ins>   | 定义插入字   |

### HTML“计算机输出”标签

|  标签  |        描述        |
| :----: | :----------------: |
| <code> |   定义计算机代码   |
| <kbd>  |     定义键盘码     |
| <samp> | 定义计算机代码样本 |
| <var>  |      定义变量      |
| <pre>  |   定义预格式文本   |

### HTML 引文, 引用, 及标签定义

|     标签     |        描述        |
| :----------: | :----------------: |
|    <abbr>    |      定义缩写      |
|  <address>   |      定义地址      |
|    <bdo>     |    定义文字方向    |
| <blockquote> |    定义长的引用    |
|     <q>      |   定义短的引用语   |
|    <cite>    |   定义引用、引证   |
|    <dfn>     | 定义一个定义项目。 |

### HTML head元素

|   标签   |                描述                |
| :------: | :--------------------------------: |
|  <head>  |          定义了文档的信息          |
| <title>  |          定义了文档的标题          |
|  <base>  |  定义了页面链接标签的默认链接地址  |
|  <link>  | 定义了一个文档和外部资源之间的关系 |
|  <meta>  |      定义了HTML文档中的元数据      |
| <script> |       定义了客户端的脚本文件       |
| <style>  |      定义了HTML文档的样式文件      |

### HTML表格

HTML 表格的基本结构：

`<table>...</table>`定义表格

`<th></th>`定义表格的标题栏（文字加粗）

`<tr></tr>`定义表格的行

`<td></td>`定义表格的列

##### HTML表格空间

有以下两个属性，用于调整HTML表格中单元格的空间：

- `cellspacing`属性-定义表格单元格之间的空间 
- `cellpadding`属性-表示单元格边框与单元格内容之间的距离

##### HTML合并单元格

- 如果要将两个或多个列合并为一个列，将使用`colspan`属性 
- 如果要合并两行或更多行，则将使用`rowspan`属性。

### HTML列表

##### 有序列表

```
<ol>
 <li>Coffee</li>
 <li>Milk</li>
 </ol> 
```

##### 无序列表

```
<ul>
 <li>Coffee</li>
 <li>Milk</li>
 </ul> 
```

