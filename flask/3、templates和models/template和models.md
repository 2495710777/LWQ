- ### 5、Template

- 简介

```
1、MVC中的view,MTV中的Template
2、主要用来做数据展示的
3、模板处理过程分为2个部分
	1、加载
	2、渲染
4、jinja2模板引擎
	1、本质上是html
	2、支持特定的模板语法
	3、flask作者开发的，一个现代化设计和友好的python模板语言  模仿的django的模板引擎
	4、优点：
		速度快，被广泛使用
		HTML设计和后端python分离
		减少Python复杂度
		非常灵活，快速和安全
		提供了控制，继承等高级功能
```

- 模板语法

  1、基本语法

  ```
  模板语言动态生成的HTML
  	{{ var }}  变量的接收
  	从views传递过来的数据
  	前面定义出来的数据
  模板对参数传递的优化: 1、页面接受该参数 视图函数不传递使用默认的
  				   2、页面不接受，视图函数传递，无视掉
  ```

  2、结构标签

  ```
  1、block
  	首次出现挖坑操作
  	第二次出现填坑操作
  	第N次出现，填坑操作，会覆盖前面填的坑
  	不想被覆盖，需要在后面的填坑操作中添加{{ super() }}
  2、extends
  	继承于哪个父模板  {% extends 'base_a.html' %}
  	把自己放入到父模板中
  3、include
  	包含，将一个指定的模板包含进来
  	把其他的页面拿过来，如果不包含在一个block中，会默认添加到页面最上方
  ```

  3、宏定义(macro)

  ```
  1、无参数   
  就是在模板html页面中定义函数 {% macro say() %}
  							包含内容
  						 {% endmacro%}
  在后面调用 {{ say() }}
  2、有参数
  {% macro getuser(name,age) %}
  	{{ name }} 今年 {{ age }}岁了
  {% endmacro%}
  {{ getuser('张三',18) }}
  3、在另外一个页面的宏定义调用需要导入，也可以使用include
  testMacro1.html:
  	{% macro getName(name) %}
      	那是 {{ name }}
  	{% endmacro%}
  在testMacro.html:
  	{% from 'testMacro1.html' import getName %}
  	{{ getName('张三') }}
  	或者直接 {% include 'testMacro.html' }}
  			{{ getName('李瘸子') }}
  ```

  4、循环控制

  ```
  views:
  @blue.route('/testFor/')
  def testFor():
      score_list = [59, 67, 85, 40, 100]
      return render_template('testFor.html', score_list=score_list)
  
  testFor.html:
  {% for score in score_list %}
  	{{ loop.first }}  第一个
  	{{ loop.last }}  最后一个
  	{{ loop.index }} 从一开始的索引下标
  	{{ loop.index0 }} 从0开始的索引下标
  	{{ loop.revindex }} 由1结束的索引下标
  	{{ loop.revindex0 }} 由0结束的索引下标
  {% endfor %}
  {% if ... %}
  	...
  {% elif ...%}
  	...
  {% else %}
  	...
  {% endif %}
  ```

  5、过滤器  |

  ```
  语法格式： {{ 变量名|xxx|yyy|zzz }}
  没有数量限制
  		lower 全部小写
  		upper 全部大写
  		trim  前后没有空格
  		reverse 反转字符串
  		striptags 渲染之前将值中的标签去掉
  		safe     标签生效
  		eg:
  		{% for i in code3 %}
     		 <li>{{ loop.index0 }}:{{ loop.index1 }}:{{ 		i|lower|reverse}}</li>
      	{% endfor %}
  ```

  ![1568901336913](C:\Users\lwq\AppData\Roaming\Typora\typora-user-images\1568901336913.png)

### 6、models

- 简介

```
1、数据交互的封装
2、Flask默认并没有提供任何数据库操作的API
	Flask中可以自由的选择数据，用原生语句实现功能
		原生SQL缺点：
		(1)代码利用率低，条件越复杂代码语句越长，有很多相似语句
		(2)一些SQL是在业务逻辑中拼出来的，修改需要了解业务逻辑
		(3)直接写SQL容易忽略SQL问题
	也可以选择ORM(Object Relation Map)
		SQLAlchemy
		MongoEngine
		将对象的操作转换为原生SQL
		优点
			(1)易用性，可以有效减少重复SQL
			(2)性能损耗少
			(3)设计灵活，可以轻松实现复杂查询
			(4)移植性好
3、Flask中并没有提供默认ORM
	ORM对象关系映射
	通过操作对象，实现对数据的操作
```

- sqlalchemy

```
flask-sqlalchemy
	使用步骤：
	1、pip install flask-sqlalchemy
	2、创建SQLALCHEMY对象,有两种方法
		(1)db=SQLAlchemy(app=app)
		(2)db=SQLAlchemy() 这句话一般会放在models中，因为需要db来调		db.init_app(app=app)这句话写在__init__的create_app中
	3、config中配置 
  app.config['SQLALCHEMY_DATABASE_URI']=
  dialect+pymsql://username:password@host:port/database
  数据库	驱动		用户名		密码		主机	端口	数据库
 例如：app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://lwq:123123@localhost:3306/day031905'		4、执行
 		views视图函数中db.create.all()
	注意在models中创建模板时有坑：
		(1)primary-key   添加主键
		(2)SQLALCHEMY_TRACK_MODIFICATIONS
	app.config['SQLALCHEMY_TRACK_MODIFICATIONS']=False  
	用来防止数据库未来可能发生的错误
app.config['']中的参数必须是全大写
```

使用：

```python
1、定义模型
	在models中
	继承SQLAlchemy对象中的model
	例如：
		class Animal(db.Model):
            # 必须有主键
			id=db.Column(db.Integer,primary_key=True,
						autoincrement=True)
			# String类型必须有长度
			name=db.Column(db.String(32))
            color = db.Column(db.String(32))
2、创建
	在views视图中
    	db.create_all()
3、删除
	在views视图中
		db.drop_all()
4、修改表名
	在models中，Animal中
		__tablename__="animal"
5、数据操作
	views视图中
	添加
    	db.session.add(对象)
        db.session.commit()
    查询
    	animal_list = Animal(模板的类名).query.all()


        
@blue.route('/addanimal/')
def addanimal():
    a = Animal()
    a.name = 'hen'
    a.color = 'yellow'
    db.session.add(a)
    db.session.commit()
    return '添加成功'

@blue.route('/findall/')
def findall():
    animal_list = Animal.query.all()
    for animal in animal_list:
        print(animal.name)
    return '查询成功'
```

