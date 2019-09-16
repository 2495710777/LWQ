### 一.基本选择器

#### （1）通配符*

+ 将代表HTML所有的标签

+ 兼容性不好，IE6不支持的

  

  #### (2) 标签选择器

  标签选择器与HTML一一对应

`<style type="text/css">
div{color:blue;font-size:12px;background-color:yellow;}
</style>`

`<div class="div">
你好
</div>`

#### （3）类选择器

给一类的HTML标签添加样式，只要class属性一样，就是一类

公共属性：每个标签都可以有的属性：id，name, class, style, title

类选择器以 . 开头

同一类样式可以给不同的HTML，一个HTML可以包含多个类样式

#### （4）id选择器

给网页中指定id属性的HTML样式

在一个网页中，不能有多个相同id值的元素

class用来给元素添加css的，而id用来添加JS的

id选择器命名：必须以#开头命名

### 二.组合选择器

#### (1)多元素选择器

同时给多个元素加同一种样式，多个元素之间用英文下的逗号分割

ul,ol,li,dl,dt,dd{margin:0px;padding:0px;}

#### （2）后代选择器

给某个元素的所有后代元素，添加样式，两个选择器之间用空格隔开

```html
#div h2{color:blue;border:1px solid blue;background-color:yellow;}
```

```
`<div id='div'>
	<h2>新闻标题1</h2>
	<div>
		<h2>新闻标题2</h2>
	</div>
</div>`
```

#### (3)子元素选择器

```
#div>h2{color:blue;border:1px solid blue;background-color:yellow;}
```

### 三.伪类选择器

一般用来选择`**<a>**`元素的

超级链接有四种状态：正常状态，放上状态，访问过状态，激活状态

- ：link 正常链接效果
- ：visited 访问过的效果
- ：hover 鼠标放上的效果

+ ：active 激活状态（鼠标点击的一瞬间出现）

**注意** 顺序不能弄错，否则没效果

**text-decoration属性**

none 没有装饰

underline 文本下划线

overline 文本上的一条线，删除线

line-through 穿过文本下的一条线

blink 定义闪烁的文本

```
a.a1:link{color:black;text-decoration:none;}
	a.a1:visited{color:gray;text-decoration:underline;}
	a.a1:hover{color:blue;}
	a.a2:link{color:red;text-decoration:none;}
	a.a2:visited{color:black;text-decoration:underline;}
	a.a2:hover{color:green;}
```



