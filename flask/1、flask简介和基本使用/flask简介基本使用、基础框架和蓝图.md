### 学习目标：

- 框架简介
  - 官方文档
  - 依赖库
  - 流行原因
- BS/CS
- MVC/MTV介绍
- Flask基本使用
  - 虚拟环境的创建
- Flask基本使用
  - 虚拟环境的创建
  - flask项目的创建
  - 启动服务器参数修改
  - 命令行参数
- Flask的视图函数返回值
  - 字符串
  - 页面
- Flask的基础架构
- 蓝图

- 路由参数
- postman安装
- 反向解析

### 一、框架简介

1、基于python的web(微)框架

```
重量与轻量：框架的核心代码的多少
重量级框架 Django
	为了方便业务程序的开发，提供了丰富的工具及组件
	自己本身什么都有，需要什么功能自己写
轻量级框架 flask
	只提供web核心功能，自由灵活，高度定制，flask也被称为“microframework”，因为它使用简单的核心，用extension增加其他功能
所有的功能都是借鉴别人的，，扩展别人的功能
```

2、官方文档

```
https://flask.palletsprojects.com/en/1.1.x/     英文
http://docs.jinkan.org/docs/flask/index.html    中文
```

3、flask依赖库

```
flask 一般依赖三个库
	jinja2 模板引擎
	werkzeug WSGI工具集
	Itsdangerous 基于Django的签名模块
	安装的时候会出现6个依赖的库
```

4、flask流行的主要原因

```
1、有非常齐全的官方文档
2、有非常好的扩展机制和第三方扩展环境，工作中常见的软件都会有对应的扩展，动手实现扩展
3、社区活跃度非常高，因为要不断的更新引用的库。flask的热度已经超过Django好几百了
4、微型框架的形式给了开发者更大的选择空间
```

### 二、BS/CS

概念：

```
BS:B browser 浏览器  S server 服务器    主流
CS:C client  客户端  S server 服务器
B/S结构是WEB兴起后的一种网络结构模式，web 浏览器是客户端最主要的应用软件，这种模式统一了客户端，将系统功能实现的核心部分集中到服务器上，简化了系统的开发、维护和使用
```

CS/BS区别：

![BS-CS区别](D:\开班软件\tornado\Day05\文档\Tornado课件\Tornado课件\BS-CS区别.png)

### 3、MVC和MTV

MVC

```
MVC:一种软件架构思想
	简介：MVC开始是存在于桌面程序中的，M是指业务模型model，V是指用户界面 view，C则是控制器 controller,使用MVC的目的是将M和V实现代码分离，从而使同一个程序可以使用不同的表现形式。比如一批统计数据可以分别用柱状图、饼图来表示、C存在目的则是确保M和V的同步，一旦M改变，V应该实现同步更新
实现了模型层的复用
	核心思想：解耦合
	面向对象语言：高内聚，低耦合
	Model
		模型
		封装数据的交互操作
			CRUD
	View
		视图
		是用来将数据呈现给用户的
	Controller
		控制器
		接受用户输入输出
		用来协调Model和View的关系，并对数据进行操作，筛选
	流程
		控制器接受用户请求
		调用模型，获取数据
		控制器将数据展示到视图中
```

![img](https://gss3.bdstatic.com/-Po3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike80%2C5%2C5%2C80%2C26/sign=7948cf4dbf096b63951456026d5aec21/b03533fa828ba61edbddc04d4034970a304e59a4.jpg)

MTV也叫作MVT

```
MTV
	也叫做MVT
	本质上就是MVC，变种
	Model
		同MVC中Model
	Template
		模板
		只是一个html，充当的是MVC中View的角色，用来做数据展示
	Views
		视图函数
		相当于MVC中Controller
```

### 4、Flask基本使用

虚拟机、虚拟容器、只有python有（虚拟环境）

1、虚拟环境的创建

```
1.创建flask的虚拟环境
	以前：mkvirtualenv Flaskpython1905 -p /usr/bin/python3
	现在：virtualenv Flaskpython1905 -p /usr/bin/python3
2.查看虚拟环境
	pip freeze
	pip list
3.虚拟环境迁移
	pip freeze > requirements.txt
		迁出
	pip install -r requirements.txt
		迁入
```

2、Flask项目的创建

```
1、安装
	国外源：pip install flask
	国内源：pip install flask
				-i https://pypi.douban.com/simple
2、创建项目
	mkdir python1905 mkdir Flaskday01  mkdir FirstFlask  vim HelloFlask.py
	代码结构
		from flask import Flask
		app = Flask(__name__)
		
		@app.route("/")
		def index():
			return "Hello"
		app.run()
3、启动服务器 python 文件名字.py
	默认端口号 5000 只允许本机连接
```

3、启动服务器参数修改

```
run 方法中添加参数
	在启动的时候可以添加参数 在run()中
	debug
		是否开启调试模式，值为True时修改过python代码自动重启
		如果修改的html/js/css 都不会自动重启
	host
		主机，默认ip是127.0.0.1 指定为0.0.0.0 代表局域网所有ip
		只能是字符串
	port
		指定服务器端口号，可以为字符串也可以为整型
		pymysql里的端口号只能是整数
	threaded
		是否开启多线程
```

扩展：PIN码

```
全称Personal Identification Number.就是SIM卡的个人识别密码。手机的PIN码是保护SIM卡的一种安全措施，防止别人盗用SIM卡，如果启用了开机PIN码，那么每次开机后就要输入4到8位数PIN码。
在输入三次PIN码错误时，手机便会自动锁卡，并提示输入PUK码解锁，需要使用服务密码拨打运营商客服热线，客服会告知初始的PUK码，输入PUK码之后就会解锁PIN码
```

4、命令行参数定义端口号与ip

```
1、需要安装
	pip install flask-script
	作用
		启动命令行参数
2、初始化
	首先把 文件名.py 该为manager.py
	manager = Manager(app=app)
	修改 运行的文件  文件.run()==>manager.run()
3、运行
	python manager.py runserver -p xxx -h xxxx -d -r
	参数
	-p 端口号 port
	-h 主机ip host
	-d 调试模式 debug
	-r 重启(重新加载) reload(restart)
```

### 5、视图函数的返回值

```
1、index返回字符串
	@app.route("/index/")
	def index():
		return 'index'
2、模板first.html
	@app.route("/first/")
	def hello():
		return render_template("first.html")
静态文件css
	注意
	<link rel="stylesheet" href="/static/css/hello.css">
```

### 6、Flask基础结构

```
App
	templates
		模板
		默认也需要和项目保持一致
	static
		静态资源
		默认需要和我们的项目保持一致，在一个路径中，指的是Flask对象创建的路径
	__init__ 创建Flask对象
	views
	models
manager.py C,主函数与APP一个层级
	坑点
		执行过程中manager.py和其他的文件的路径问题
	第二个坑点： 封装__init__文件
```

### 7、蓝图

```
蓝图
	1、宏伟蓝图(宏伟规划)
	2、蓝图也是一种规划，主要是用来规划urls(路由)
	3、蓝图基本使用
		1、pip install flask-blueprint
		2、初始化蓝图   blue = BluePrint('first',__name__)
		3、调用蓝图进行路由注册
巨坑：
app.register_blueprint(blueprint=blue)
```

`views.py`

```python
from flask import Blueprint
# 使用蓝图的位置 必须在views里
# 导入蓝图的包是flask中的，否则会形成循环导包的错误
blue = Blueprint('first',__name__)
@blue.route('/index/')
def index():
    return 'index'
```

`__init__.py`

```python
from flask import Flask
# 不能在这进行路由注册，会造成循环导包的错误
def create_app():
    app = Flask(__name__)
    return app
```

`manager.py`

```python
from flask_script import Manager

from App import create_app
from App.views import blue

app = create_app()
manager = Manager(app=app)
app.register_blueprint(blueprint=blue)

if __name__ == '__main__':
    manager.run()
```

### 8、Flask请求流程

```python
Flask请求流程
	请求到路由    app.route()
    视图函数
    视图函数和models交互
	模型返回数据到视图函数
	视图函数渲染模板
	模板返回给用户
```

![img](https://upload-images.jianshu.io/upload_images/1801379-02bfe06281d809cf.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

### 9、Flask路由参数

```
带参数的请求
	从客户端或者浏览器发过来的请求带参数
		@blue.route('/getstudent/<id>')
		def getstudents(id):
			return '学生%s' + id
	路由参数
		基础语法
			<converter:var_name>
				书写的converter可以省略，默认类型就是string
请求路由参数一下六种：
1、string (默认)
接收的时候是str,匹配到 / 的时候是匹配结束
@blue.route('/testString/<string:id>')
def testString(id):
    print(type(id))
    return 'hello'+id
2、path
接收的时候也是str， / 只会当作字符串中的一个字符处理
@blue.route('/testPath/<path:name>')
def testPath(name):
    print(type(name))
    return name
3、int
只能接收整数数字，return需要字符串
@blue.route('/testInt/<int:id>')
def testInt(id):
    print(type(id))
    return str(id)
4、float
视图函数名不能相同
@blue.route('/testFloat/<float:id>')
def testFloat(id):
    print(type(id))
    return str(id)
5、uuid
@blue.route('/testuuid/')
def testuuid():
    num = uuid.uuid4()
    print(num)
    return str(num)

@blue.route('/testuuid1/<uuid:id>')
def testuuid1(id):
    print(type(id))
    return str(id)
6、any
任意一个
已提供选项的任意一个 而不能写参数外的内容  注意的是/
@blue.route('/testany/<any(a,b,c):p>/')
def testany(p):
    return p
```

### 10、postman

```请求方式
请求方式
	postman
		模拟请求工具
			路由参数中添加methods=['get','post']
安装
https://blog.csdn.net/Shyllin/article/details/80257755
1. 默认支持GET，HEAD，OPTIONS
2. 如果想支持某一请求方式，需要自己手动指定
3. 在route方法中，使用methods=["GET","POST","PUT","DELETE"]
```

### 11、反向解析

```
反向解析
	1、概念
		获取请求资源路径
	2、语法格式
	    url_for(蓝图的名字.方法名字)
	3、使用
@blue.route('/dskfugsdgb/',methods=['get','post','put'])
def hehe():
    return 'hehe'

@blue.route('/testReverse/')
def testReversr():
    p = url_for('blue.hehe')
    return p
```

