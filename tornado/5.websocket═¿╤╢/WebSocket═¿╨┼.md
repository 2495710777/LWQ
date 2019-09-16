



## 使用websocket进行聊天

如果使用Tornado 仅仅做普通的短连接web站点开发就有点大材小用了，tornado很早就加入了对WebSocket的支持，可以用来进行长连接通信

## 一、WebSocket介绍

### 什么是WebSocket

WebSocket是一种网络通信协议。在2009年诞生，在2011年被IETF定为标准RFC6455通信标准。WebSocket API 也被定为W3C定为标准

WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行**全双工 (full-duplex) 通讯**的协议。没有了 Request 和 Response 的概念，两者地位完全平等，连接一旦建立，就建立了**持久性连接**，浏览器和服务器双方可以随时向对方发送数据。

HTML5 是 HTML 最新版本，包含一些新的标签和全新的 API。HTTP 是一种协议，目前最新版本是 **HTTP/2** ，所以 WebSocket 和 HTTP 有一些交集，两者相异的地方还是很多。两者交集的地方在 HTTP **握手阶段**，握手成功后，数据就直接从 TCP 通道传输。

### Web上的即时通信

在没有WebSocket之前，服务器很难主动向客户端推送数据

web为了实现即时通信，经历了最初的polling(短轮询)，到之后的Long polling(长轮询)，等若干种方式。

1、短轮询 Polling

![polling](C:\Users\lwq\Desktop\tornado\5.websocket通讯\polling.png)

这种方式下，不适合获取实时信息，客户端和服务器之间会一直进行连接，每隔一段时间就询问一下，这种方式连接数会很多，一个接收，一个发送，而且每次发送请求都会有HTTP的header，会很耗流量，也会消耗CPU的利用率。在web端，短轮询用ajax jsonp polling 轮巡实现![polling_via_ajax](C:\Users\lwq\Desktop\tornado\5.websocket通讯\polling_via_ajax.png)

- 优点：短连接，服务器处理简单，支持跨域、浏览器兼容性好
- 缺点：有一定的延迟、服务器压力较大，浪费带宽流量、大部分是无效请求

2、长轮询Long Polling

![long_polling](D:\开班软件\tornado\Day05\文档\Tornado课件\Tornado课件\img\long_polling.png)

长轮询是对轮询的改进版，客户端发送HTTP给服务器之后，有没有新消息，如果没有新消息，就这一直等待，直到有消息或者等待超时了，才会返回给客户端。消息返回后，客户端再次建立连接，如此反复，这种做法在某种程度上减小了网络带宽和CPU的利用率等问题。

但也有弊端，实时性不高。如果是高实时的系统，肯定不会采用这种方法因为一个 GET 请求来回需要 2个 RTT，很可能在这段时间内，数据变化很大，客户端拿到的数据已经延后很多了。

- 优点：减少轮询次数，低延迟，浏览器兼容性好
- 缺点：服务器需要保持大量连接。

3、WebSocket

![websocket](C:\Users\lwq\Desktop\tornado\5.websocket通讯\websocket.png)

为了解决其他机制的各种问题，人们设计出WebSocket协议

WebSocket是HTML5开始提供的一种独立在单个TCP连接上进行全双工通讯的有状态的协议(它不同于无状态的HTTP)，并且还能支持二进制帧、扩展协议、部分自定义的子协议、压缩等特性

### 与普通的HTTP协议的异同

1、WebSocket协议的URL是`ws://`或者`wss://`开头的，而不是`HTTP://`或者`HTTPS://`

2、WebSocket使用与普通HTTP协议相同的80端口和443端口进行连接

3、WebSocket的Header中有个特殊字段，代表它是由HTTP协议升级为WebSocket协议

```python
Connection:Upgrade
Upgrade:websocket
```

### 通过 JS 建议一个简单的 WebSocket 连接

```python
import tornado.ioloop
import tornado.websocket
import tornado.web
from tornado.options import parse_command_line, define, options
define("host", default="localhost", help="主机地址", type=str)
define("port", default=8000, help="主机端口", type=int)
# define("xyz",default='ascda',help="测试参数",type=str)


class MsgHandler(tornado.websocket.WebSocketHandler):
    conn_pool = set()

    def open(self):
        print("与客户端建立了连接")
        self.conn_pool.add(self)

    def on_message(self, message):
        print("收到了客户端发来的消息：%s" % message)
        self.write_message("我收到了你的消息：%s" % message)
        self.broadcast(message)

    def on_close(self):
        print("客户端与我断开了连接")
        self.conn_pool.remove(self)

    # 广播的方法
    def broadcast(self, message):
        # 广播消息
        for conn in self.conn_pool:
            if conn is not self:
                conn.write_message(message)


def make_app():
    return tornado.web.Application([
            (r"/msg", MsgHandler),

    ])


if __name__ == '__main__':
    parse_command_line()
    # print(options.host)
    # print(options.port)
    # print(options.xyz)
    app = make_app()
    print("Server running on %s:%s" % (options.host, options.port))
    app.listen(options.port, options.host)  # 第一个参数是端口号，第二个是地址

    # 把协程驱动起来
    loop = tornado.ioloop.IOLoop.current()
    loop.start()
```

在网页控制台输入：

```js
var ws = new WebSocket("ws://localhost:8000/msg");
ws.onopen = function(){
    ws.send("连接已经完成!")
};
ws.onmessage = function(event){
    console.log('客户端收到了服务器返回的信息',event.data)
};
ws.onclose = function(){
    ....
} 
ws.onerror = function(error){
    ...
}
```







### Tornado中使用WebSocket

```python
class WebsocketHandler(tornado.websocket.webSocketHandler):
    def open(self):
        '''该方法处理建立连接时执行的操作'''
        pass
    def on_close(self):
        '''该方法处理断开连接时执行的操作'''
        pass
    def on_message(self):
        '''该方法处理收到消息时进行的操作'''
        pass
    def on_write(self):
        '''该方法可以给其他人发送消息'''
        pass
```

## 二、任务目标

1. 通过 Tornado 开发一个聊天室程序
2. 通过 WebSocket 进行长连接通信
3. 使用 Redis 保留 100 条离线消息

./main.py --logging=debug

logging.debug()

logging.info()

logging.warning()

logging.error()

logging.fatal()   致命错误，一旦报错，运行全部停下

日志级别从低到高，设置为debug的话，会有大量的日志

static_url是一个封装的函数会自动把它转化成static/

