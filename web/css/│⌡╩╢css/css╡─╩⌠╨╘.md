### 尺寸属性

width:元素的宽度

heigh：元素的高度

### 字体属性

font-size:文字大小

font-weight:加粗效果（blod）

font-style：斜体效果（italic）

font-family:字体

### 文本属性

color：文本颜色

line-height:行高，可以是百分比，也可以是固定值

text-align：文本的水平对齐方式，取值：left,center,right

letter-spacing:字间距

text-decoration:文本修饰线 underline下划线，none，overline上划线

linethrough 删除线

text-indent：首行缩进

### px,em,rem

px像素，相对长度单位，显示屏分辨率

em是相对长度单位，根据父类的变化而变化

rem相对于根即HTML标签相变化

HTML根的默认大小是16px

需要在css中的body选择器中声明font-size=80%才能使用

```
body{font-size:100%;}
div{font-size:1.5em;}
span{font-size:2rem;}
```

```
<body>
	<p>你好</p>
	<div>你好<br/>
	<span>你好</span>
	</div>
</body>
```

