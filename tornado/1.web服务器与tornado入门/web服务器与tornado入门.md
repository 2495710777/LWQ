## Web服务器与Tornado入门

### 一、HTTP服务器的真相

HTTP协议是建立在TCP协议之上的短连接协议

它利用TCP协议的可靠性，用来传输超文本(HTML),通信一次连接一次，通信完成后TCP连接关闭

所以如果想创建一个HTTP Server 需要通过Socket搭建一个服务端程序

#### 1、最简单的HTTP Server

```python
# 定义 "响应报文"
template ='''
HTTP/1.1 200 OK # 后面要空一行

<html>
   <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />

        <title>lwq</title>

        <style>
            h1, p {
                text-align: center;
                font-size: 2.5em;
            }
            .avatar {
                border-radius: 20px;
                box-shadow: 5px 5px 20px grey;
                width: 500px;
                margin: 0 auto;
                display: block;
            }
        </style>
    </head>
    <body>
        <h1>lwq</h1>
        <div><img class="avatar" src="https://inews.gtimg.com/newsapp_ls/0/10229330043_294195/0" /></div>
        <p>%s</p>
    </body>
</html>
'''
def get_url(request_str):
    first_line = request_str.split('\n')[0] # 取出第一行
    url = first_line.split(' ')[1] # 按空格切分，取出中间的URL
    return url


while True:
    print('服务器已运行，正在等待客户端连接。。。')

    # 等待接受客户端连接
    # 第一个返回值是客户端的 socket 对象
    # 第二个返回值是客户端的地址
    cli_sock, cli_addr = sock.accept()
    print('接收到来自客户端 %s:%s 的连接' % cli_addr)

    # 接收客户端传来的数据，1024是接收缓冲区的大小
    cli_request = cli_sock.recv(1024).decode('utf8')
    print('接收到客户端发来的 "请求报文": \n%s' % cli_request)

    # 获取用户的URL
    url = get_url(cli_request)

    # 根据URL的不同返回不同的返回值
    if url == '/foo':
        response = template % '姜胖胖是个大胖子'
    elif url == '/bar':
        response = template % '姜胖胖贼滑'
    else:
        response = template % 'hello world'

    cli_sock.sendall(response.encode('utf8'))  # 向客户端发送数据
def get_url(request_str):
    first_line = request_str.split('\n')[0] # 取出第一行
    url = first_line.split(' ')[1] # 按空格切分，取出中间的URL
    return url


while True:
    print('服务器已运行，正在等待客户端连接。。。')

    # 等待接受客户端连接
    # 第一个返回值是客户端的 socket 对象
    # 第二个返回值是客户端的地址
    cli_sock, cli_addr = sock.accept()
    print('接收到来自客户端 %s:%s 的连接' % cli_addr)

    # 接收客户端传来的数据，1024是接收缓冲区的大小
    cli_request = cli_sock.recv(1024).decode('utf8')
    print('接收到客户端发来的 "请求报文": \n%s' % cli_request)

    # 获取用户的URL
    url = get_url(cli_request)

    # 根据URL的不同返回不同的返回值
    if url == '/foo':
        response = template % '姜胖胖是个大胖子'
    elif url == '/bar':
        response = template % '姜胖胖贼滑'
    else:
        response = template % 'hello world'

    cli_sock.sendall(response.encode('utf8'))  # 向客户端发送数据
# 断开与客户端的连接
    cli_sock.close()
    print('连接断开,退出！')
```

### 二、Web框架概述

随着技术的发展，我们每天的要处理的信息量都在爆炸新的增加。传统的静态⻚⾯技术早已跟不上时代需求，因⽽催⽣了动态⻚⾯技术。

所谓的动态页面，即所有的页面用程序来生成，已实现细节上的不同，又可分为“前端动态页面”和“后端动作页面”

我们在Web前端阶段所学的Ajax、Vue等技术，就是前端动态页面，而今后我们所学的主要是后端动态页面技术，甚至是两者的结合

#### 1、Web服务器原理

第⼀⼩节的 SimpleServer 虽然代码仅仅 30 多⾏，但已经包含了⼀个⼩型 Web 系统的核⼼。⼀个完备的 Web 系统如下图所示:

​			![1568028883380](C:\Users\lwq\AppData\Roaming\Typora\typora-user-images\1568028883380.png)

#### 2、常见的Web框架

如果想完成更复杂的功能，还需要深⼊开发很多东⻄，⽐如模版系统、ORM系统、路由系统、会话机制……
好在这些基础且通⽤的东⻄已经被很多前辈开发完成，我们没有必要再造轮⼦。他们按照⾃⼰的⽤途和想法，将各种系统开发、组合，最终为我们提供了各种各样的 Web 框架。

同步：one by one

异步：你做你的，同时我做我的

| Web Framework | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| **Django**    | 全能型框架，大而全，插件丰富，文档丰富，社区活跃，适合快速开发，内部耦合度比较大 |
| **Flask**     | 微型框架，适合新手学习，极其灵活，便于二次开发和扩展，生态环境好，插件丰富 |
| **Tornado**   | 异步处理，事件驱动(epoll)，性能优异                          |
| Bottle        | 单文件框架，结构紧凑，是个初学者阅读源代码，了解Web原理      |
| web.py        | 代码优美，适合学习源码                                       |
| Falcon        | 性能优异适合写API接口                                        |
| Quixote       | 一个爷爷级别的框架，豆瓣网用的就是这个                       |
| Sanic         | 后起之秀，性能秒杀以上的所有前辈框架，但没有他们稳定         |

## 三、Tornado入门

Tornado 是有 FriendFeed 公司开发的 Web 框架，该公司已经于 2009 年被 Facebook 收购，原本的FriendFeed 已经成为了 Facebook 的⼀部分。

Tornado最大的特点便是他实现了一个**异步非阻塞**的HTTP Server，，性能非常优异

#### 1、安装

```sql
pip install tornado
```

#### 2、Hello World

```python
import tornado.ioloop
import tornado.web

class MainHeadler(tornado.web.RequestHeadler):
    def get(self):
        self.write("Hello world")

def make_app():
    return tornado.web.Application([
        (r'/',MainHeadler),    # '/'是根目录的意思
    ])
if __name__ == "__main__":
    app = make_app()
    app.listen(8888)
    tornado.ioloop.IOLoop.current().start()
```

#### 3、使用参数

```python
from tornado.options import parse_command_line,define,option
define("host", default='0.0.0.0', help="主机地址", type=str)
define("port", default=8888, help="主机端⼝", type=int)
parse_command_line()
print('你传⼊的 host: %s' % options.host)
print('你传⼊的 port: %s' % options.port)
```

#### 4、路由处理

```python
import tornado.ioloop
from tornado.web import RequestHandler, Application
class HomeHandler(tornado.web.RequestHandler):
 def get(self):
 self.write("欢迎进⼊主⻚")
class BookHandler(tornado.web.RequestHandler):
 def get(self):
 self.write("你想看的书应有尽有")
app = Application([
 ('/', HomeHandler),
 ('/book/', BookHandler),
])
app.listen(8000)
tornado.ioloop.IOLoop.current().start()
```

#### 5、处理 GET 和 POST 请求

```python
class StoryHandler(tornado.web.RequestHandler):
 stories = {1: '⼩红帽', 2: '⽪诺曹', 3: '阿拉丁神灯'}
 def get(self):
 story_id = self.get_argument('story_id')
 story = self.stories[story_id]
 self.write("你想看 %s 的故事" % story)
 def post(self):
 pass
```

HTTP 的请求⽅法:

| Method  | Description                                                  |
| ------- | ------------------------------------------------------------ |
| POST    | 向指定资源提交数据进⾏处理请求, 数据被包含在请求体中。一般是对服务器数据或创建或修改（更强调于创建） |
| GET     | 请求指定的⻚⾯信息，并返回实体主体。                         |
| PUT     | 从客户端向服务器传送的数据取代指定的⽂档的内容。只是修改服务器本身的内容 |
| DELETE  | 请求服务器删除指定的⻚⾯。                                   |
| HEAD    | 类似于 GET 请求，只不过返回的响应中没有具体的内容，⽤于获取报头 |
| PATCH   | 是对 PUT ⽅法的补充，⽤来对已知资源进⾏局部更新 。           |
| OPTIONS | 列举服务器⽀持的请求⽅法                                     |

#### 6、练习

1. 在 MySQL 中建⽴ user 表, 包含字段: id, name, age, sex, city 等, 并插⼊若⼲数据
2. 开发接⼝，并根据⽤户传⼊的 id 显示对应的⽤户信息
3. 开发接⼝，并根据⽤户传⼊的数值修改⽤户数据

