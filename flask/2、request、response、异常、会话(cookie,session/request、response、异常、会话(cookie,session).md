### 学习目标

- request
- response
- 异常
- 会话
  - cookie
  - session
- 模板
- 模型

### 学习课程

```
# 状态码
# 200 成功  数据传输没有丢失，浏览器完全接受
# 301 重定向
# 302 永久重定向
# 403 防跨战攻击 forbidden
# 404 路径错误
# 405 请求方式错误
# 500 服务器 业务逻辑错误

# 反向解析
# 应用场景
#       1、redirect('/index/') ,重定向到index请求
#           尽量不要使用硬编码 redirect(url_for('blue.index'))
#       2、页面中 不要使用硬编码 form action='/login/'
#           form action = url_for('blue.login')
```



#### 1、request

```
request是一个内置对象
内置对象：不需要创建就可以直接使用的对象
属性：
1	method **
		获取的是请求方式/http方法
2	base_url
		去掉get参数的url
		127.0.0.1:5000/testRequest/
3	host_url
		只有主机和端口号的url
		127.0.0.1:5000
4	url	**
		完整的请求地址,主机的路径不带请求资源路径
		127.0.0.1:5000/
5	remote_addr **
		完整的url路径（请求资源路径，请求参数）
		127.0.0.1:5000/testRequest/?name=zs
6	files **   form标签中有一个参数 enctype=maltipart/form-data  请求方式必须是post  使用files接收
		文件上传
7	headers        
		请求服务器带的数据，要符合服务器的要求
		请求头
8	path			**
		请求资源路径 /testRequest/
9	cookies        **
		获取请求的cookies
一般情况下  get请求方式都是在浏览器的地址栏上显示
     eg：http：//www.baiduc.com/s?name=zs&age=18
 获取get请求方式的参数的方式：
	request.args.get('name')
10	args  **
		1. args
         - get请求参数的包装，args是一个ImmutableMultiDict对象，类字典结构对象
         - 数据存储也是key-value
         - 外层是大列表，列表中的元素是元组，元组中左边是key，右边是value
@blue.route('/testArgs/')
def testArgs():
    name = request.args.get('name')
    print(name)
    name1 = request.args.getlist('name')
    print(name1)
    return 'testArgs'
11  post    **
一般情况下 post请求方式都是通过表单形式使用的
@blue.route('/testForm/',methods=['post'])
def testForm():
    name = request.form.get('name')
    print(name)
    name1 = request.form.getlist('name')
    print(name1)
    return 'testArgs'

12  session
	与request类似，也是一个内置对象，可以直接打印
print(session)  -->  <NullSession {}>
```

### 2、Response

```
创建方式
1	返回字符串
		如果只有字符串，就是返回内容，数据
		还有第二个返回，放的是状态码
@blue.route('/response/')
def get_response():
    return '德玛西亚', 404

2  render_template
渲染模板
将模板变成字符串
@blue.route('/rendertemplate/')
def render_temp():
    resp = render_template('welcomecookie.html')
    print(resp)
    print(type(resp))
    return resp,500
    
3  make_response
	Response对象
	返回内容
	状态码
	@blue.route('/makeresponse/')
	def make_resp():
        resp = makeg_response('<h2>我爱你</h2>',502)
        print(resp)
        print(type(resp))
        return resp
        
4  redirect
    重定向
	@blue.route('/redirect/')
    def make_redir():
    return redirect('/makeresponse/')
    
反向解析 url_for
	@blue.route('/redirect/')
	def make_redir():
    return redirect(url_for('blue.make_resp'))
    
5 response()也可以返回make_response的内容

返回字符串对象的有：默认、render_template
返回response对象的是：make_response、redirect、response
response是一个类，方法更加的齐全，比make_response更加的高级，可以互换使用
```

### 3、异常

```
abort
	直接抛出 显示错误状态码  终止程序运行
	abort(404)
	eg:
		@blue.route('/makeabort/')
         def make_abort():
              abort(404)
              return '天还行'
```

```
捕获
	@blue.errorhandler()
		- 异常捕获
		- 可以根据状态或 Exception进行捕获
		- 函数中要包含一个参数，参数用来接收异常信息
	eg:
	@blue.errorhandler(502)
    def handler502(exception):
        return '不能让你看到状态码'
```

```python
# 异常abort
@blue.route('/testAbort/')
def testAbort():
    abort(404)
    return 'testAbort'

@blue.errorhandler(404)
def testAbort1(Exception):
    return '系统正在升级，请稍候再试...'
```

### 4、会话技术

```
1、请求通过Request开始，到Response结束
2、连接都是短连接
3、延长交互的生命周期
4、将关键数据记录下来
5、Cookie是保存在浏览器端/客户端的状态管理技术
6、Session是服务器端的状态管理技术
```

##### cookie

```
Cookie
	1,一种客户端会话技术，数据以key-value的形式存储在客户端
	2、服务器不做任何存储
	3、特性
		支持过期时间
			max_age 毫秒为单位
			expries 具体日期时间
		根据域名进行cookie存储
		不能跨网站(域名)
		不能跨浏览器
		自动携带本网站的所有cookie
	4、cookie是服务器过Response操作客户端的数据
	
```

浏览器对服务器发起请求，服务器创建一个session_key,返回给浏览器作为session_id存放在cookie中

session_id 现在设计每三十分钟清除一次

cookie:一种客户端会话技术，由服务器产生，以key-value存放在客户端

```
cookie登录使用
   
   设置
   response = redirect(url_for('blue.welcomecookie'))
   cookie response(对象).set_cookie('username',name)
	
   获取cookie username=request.cookies.get('username','游客')
   游客是默认值
   
   删除
   response = redirect(url_for('blue.welcomecookie'))
   cookie response.delete_cookie('username')
```

##### session

```
Session
	1、服务端会话技术
	2、所有数据存储在服务器中
	3、默认存在服务器的内存中
		Django默认做了数据持久化(存在了数据库中)
	4、存储结构也是key-value形式，键值对
【注】单纯的使用session是会报错的，需要使用在__init__方法中配置app.config['SECRET_KEY']=‘110’
```

```
session登录使用
	设置	session['username']=username
	获取	session.get('username')
	删除
		resp.delete_cookie('session')
		session.pop('username')
```

##### cookie和session总结

```
1、cookie：客户端浏览器的缓存；session:服务端服务器的缓存
2、cookie不是很安全，别人可以分析存放在本地的cookie并进行cookie欺骗，考虑到安全应使用session
3、session会在一定时间内保存在服务器上。当访问增多是，会比较占用服务器的性能，考虑到减轻服务器性能方面，应当使用cookie
可以考虑将登陆信息等重要信息存放为session，其他信息如果需要保留，可以放在cookie中
```

##### session持久化问题

- 持久化简介

  ```
  1、Django中对session做了持久化，存储在数据库中
  2、flask中没有对默认session进行任何处理
  	flask-session可以实现session的数据持久化
  	可以持久化到各种设置，更推荐使用redis
  	缓存在磁盘上的事就，管理磁盘文件使用lru，最近最少使用原则
  ```

  **持久化实现方案**

  ```
  1、 pip install flask-session
  		在国内源安装pip install flask-sessin -i https://pipy.douban.com/simple
  2、初始化Session对象
  	(1)持久化位置
  		配置__init__中app.config['SESSION_TYPE'] = 'redis'
  	(2)初始化
  		创建session的对象有2种方式，分别是以下两种
  		1、Session(app=app)
  		2、session=Session()	session.init_app(app=app)
  	(3)安装redis
  		pip install redis
  	(4)需要配置SECRET_KEY='110'后面的数字是任意的
  	注意：flask把session的key存储在客户端的cookie中，通过这个key可以从flask的内存中获取					 
  	用户的session信息，出于安全性考虑，使用secret_key进行加密处理。所以需要先设置secret_key的值。
  	(5)其他配置-视情况而定
  		app.config['SESSION_KEY_PREFIX']='flask'
  		redis中会出现以flask开头的key值
  	说明：
  		查看redis内容：
  			默认不启动，使用需要先启动
  			redis-server 启动redis服务器
  			redis-cli	启动redis客户端
  			keys *	查看redis中所有key
  			get [key] 查看对应的key值(二进制)
  			del [key] 删除
  			session生存时间31天
  			可以使用 ttl session
  			Django的session生存时间是15天
  ```

