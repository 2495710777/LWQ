### 列表属性

list-style:指定样式的符号。取值：none（无符号）

.ul{list-style:none}

### 边框属性

border-left right bottom top

格式：粗细（px） 线型 颜色

线型：none   solid(实线)  dotted(点状线)  dashed(虚线)  double(双线)

div{border:5px solid red;}

### 填充属性

#### 内边距 边框线到内容的距离

padding-left right top bottom

padding:10px  四边都是10px

padding:10px 20px 上下10px  左右20px

padding:10px 20px 30px  上10px 左右20px 下30px

padding:10px  20px  30px  40px 上右下左顺时针

#### 外边距  边框线往外的距离margin 同padding

### 背景属性

background-color：背景颜色

background-image:url(image/bg.png)  背景图片

background-repeat:背景图片的平铺方式  默认都平铺

no-repeat:不平铺  repeat-x:水平方向平铺 repeat-y:垂直方向平铺

background-position：背景图片定位  left center  right top bottom

background-position：center center；位居容器的正中

background-position：0% 50%；

background-position：5px 5px；距离容器上左都是5px

**想使用图片定位，图片不能平铺**

### 浮动和清除

float：浮动 取值：left或right

浮动的元素不再占空间了，层级高于普通元素

浮动的元素一定是块元素。行内元素浮动后也变成了块元素

clear:清除浮动 取值：left right both clear:both

有浮动，必须要有清除浮动

### 继承性和优先级

多个外层元素的样式，最终都要叠加到内层元素上。

内层元素的样式，可以从多个外层元素上去继承

css继承主要是文本和字体方面的样式。如：font-size、font-weight、font-style、font-family、line-height、text-indent、text-align、color、text-decoration、letter-spacing、word-spacing

**优先级**

指向越精确，优先级越高

行内样式>id选择器>类选择器>标签选择器>通配符