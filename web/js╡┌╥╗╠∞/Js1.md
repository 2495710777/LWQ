### JavaScript是一种小型的、轻量级的、面向对象的、跨平台的客户端脚本语言

JavaScript是集成在浏览器中的，只要安装了浏览器，Javascript就能够解析

他是面向对象的一种语言，可以把网页中的任何元素都堪称一个**对象**

**特点**

跨平台：可以运行在多种平台上：window、Linux、unix、mac os等

客户端脚本程序：JS只能运行在客户端即浏览器

服务端的脚本程序有：PHP、ASP、NET、ASP、Python、Ruby等

**Javascript可以用来网页的动态效果**

### 格式

```
<script type="text/javascript">
	JS代码
</script>
```

### js的输出方法

在输出加上console.log(eval(a))  //会把a的引号拿掉，即还原字符串，尽量不使用

#### 1.在网页中输出(html的body)

**document.write(str)**在网页中输出一个字符串

document可以看成一个对象，document对象有很多的属性和方法

write()是document对象的一个方法(带小括号)

#### 2.window.alert(str) 

他可以弹出一个警告对话框，警告对话框的信息是str

window是浏览器窗口对象，代表一个浏览器窗口

#### 3.console.log(str)

在浏览器检查的console控制台中输出，用来测试代码和调试

在python中有两种输出：

1.print()

2.导入pprint模块   pprint.pprint(123)

区别是pprint会把输出的大括号和，分行格式化输出

### js的注释

html:<!--内容-->

css注释：/*内容**/

js单行注释：//  多行注释和css一样

### JS的变量

变量是临时存储数据的容器，在内存中存在和运行

#### 1.变量的声明

和python不同的是，js变量在使用之前需要先声明，即通知内存开个空间

使用**var 变量名**

命名规则跟python一样

匈牙利命名法就是驼峰命名法

下划线连接的命名法叫蛇形命名法

#### 2.给变量赋值

“=”左边只能是一个变量名称，左边不能进行计算

“=”右边是一个值，也可以是一个计算表达式，右侧运算完后，一定有一个具体的值

也可以使用三元运算符定义：var name = a > b ? 10 : 20

python 中：10 if a > b else 20



