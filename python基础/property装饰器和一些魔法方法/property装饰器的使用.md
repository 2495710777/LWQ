@property可以让一个函数像是属性一样被调用

让私有属性或方法像普通属性一样访问

```python
class Person(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age
        self.__money = 2000

    def get_money(self):
        return self.__money

    @property
    def money(self):
        print('查询余额了！！！！')
        return self.__money

    @money.setter
    def money(self, qian):
        print('存取款了！！！！')
        self.__money += qian

    @money.deleter
    def money(self):
        print('呵呵')
        del self.__money


p = Person('张三', 18)
print(p.name)
print(p.age)

print(p.get_money())

# @property 可以让一个函数像是属性一样被调用
print(p.money)
p.money = 2000
print(p.money)

del p.money

print(p.money)
```

#### property类属性的使用

```python
class Foo(object):
    def get_bar(self):
        print("getter...")
        return 'laowang'

    def set_bar(self, value):
        """必须两个参数"""
        print("setter...")
        return 'set value' + value

    def del_bar(self):
        print("deleter...")
        return 'laowang'

    BAR = property(fget=get_bar, fset=set_bar, fdel=del_bar, doc="description...")


obj = Foo()
# obj.get_bar()
# obj.set_bar()
# obj.del_bar()

obj.BAR  # 自动调用第一个参数中定义的方法：get_bar
x = obj.BAR = "alex"  # 自动调用第二个参数中定义的方法：set_bar方法，并将“alex”当作参数传入
print(x)# alex
desc = Foo.BAR.__doc__  # 自动获取第四个参数中设置的值：description...
print(desc)
del obj.BAR  # 自动调用第三个参数中定义的方法：del_bar方法

```

