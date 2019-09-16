# 初识html

需要学习的内容：

1. html

2. css

3. js基础

4. jquery

5. vue

   **了解C/S和B/S模式：**

   C/S是终端和服务器的模式，例如手机上的app就是这种

   B/S是浏览器和服务器的交互方式，HTML就是这种方式，是当钱流行的网络模式，所有的软件都安装在服务器段，客户端的压力更小了

   DNS：网络服务的数据库

   **HTML： Hyptertext Markup Language	超文本标记语言**
   主要功能：控制网页的结构。比如什么是标题，什么地方是段落，什么是链接

   超文本的意思：除了文本之外，还可能有图片。音乐，视频，链接
   标记：可以理解成一种'标记''记号'‘标志’

   这里虽然说是语言，实际于程序没有半点关系

   ### 1.HTML的文件结构

   结构树:![](C:\Users\lwq\Desktop\web\img\tree.png)

结构：

```html
<!DOCTYPE html>  <!--不是HTML标签：只是告诉浏览器页面使用的是HTML版本-->
<!--HTML标签-->
<html lang="en">
<!--HTML的头部标签-->
<head>
<!--    meta  charset 设置字符集-->
    <meta charset="UTF-8">
<!--    标题的标签-->
    <title>Title</title>
</head>
<!--网页的正文内容，排版进行在body中-->
<body>

</body>
</html>
```



<head></head 称为文件头部标记，一般是一些控制信息，其中的信息在浏览器中是看不见的
<title></title>:表示网页的标题，其中的内容只能是纯文本
<meta /> 告诉浏览器，这个网页的汉字用什么编码解析 默认GB2312 对6763个汉字进行编码，GBK简体中文编码对9万个文字进行了编码，通常用utf-8多国语言编码

html4的meta写法：

<meta http-equiv='content-type'

content='text/html';charset=utf-8 />

html5中写法：

<meta charset='utf-8'  />

### 2.标签格式

两类：

一是双标记(常规标签)，二是单边标记(空标签)

<标签  属性 = "属性值">内容</标签>
<标签  属性 = "属性值" />

```
<font color='red' face="楷体" size="6">上海Python</font>
```

<font color='red' face="楷体" size="6">上海Python</font>





### 3.html 标签编写规范

HTML标记不区分大小写。如<Div>,<dIv>,<DIV>,<diV>

html标记可能有属性，也可能没有属性：`<br/>`换行、`<html>、``<head>`

标记和属性之间用空格隔开，个属性也用空格隔开

只能顺序嵌套，不能交叉嵌套，只能一层套一层

```
<font color='blue' face='楷体' size='7'><i>上海Python</i></font>
```

<font color='blue' face='楷体' size='7'><i>上海Python</i></font>





