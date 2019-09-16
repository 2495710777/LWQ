# set的使用

集合（set）是一个**无序的不重复元素**序列，可以使用大括号 **{ }** 或者 **set()** 函数创建集合。

**注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。**

创建格式：

```python
parame = {value01,value02,...}
或者
set(value)
```

## 添加元素

**语法格式如下：**

```python
s.add(x)
```

将元素 x 添加到集合 s 中，如果元素已存在，则不进行任何操作。

```python
companys = {'百度', '淘宝', '华为'}
# add 只能添加一个元素
companys.add('腾讯')
print(companys)
# 把元组当作一个整体添加进去
companys.add(('搜狗', '字节跳动'))
print(companys)
# update 添加多个数据
companys.update(('小米', '京东'))
```

还有一个方法，也可以添加元素，且参数可以是列表，元组，字典等，语法格式如下：

```python
s.update( x )
```

x 可以有多个，用逗号分开。



## 移除元素

语法格式如下：

```python
s.remove( x )
```

将元素 x 从集合 s 中移除，如果元素不存在，则会发生错误。

```python
thisset = set(("Google", "Runoob", "Taobao"))
thisset.remove("Taobao")
print(thisset)
{'Google', 'Runoob'} thisset.remove("Facebook")   # 不存在会发生错误
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# KeyError: 'Facebook'
```

此外还有一个方法也是移除集合中的元素，且如果元素不存在，不会发生错误。格式如下所示：

```python
s.discard( x )
thisset = set(("Google", "Runoob", "Taobao"))
thisset.discard("Facebook")  # 不存在不会发生错误
print(thisset)
# {'Taobao', 'Google', 'Runoob'}
```

我们也可以设置随机删除集合中的一个元素，语法格式如下：

```python
s.pop()
thisset = set(("Google", "Runoob", "Taobao", "Facebook"))
x = thisset.pop()# 且会返回被删除的值
print(x)
print(thisset)
```

## set常见方法列表

| 方法                          | 描述                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| add()                         | 为集合添加元素                                               |
| clear()                       | 移除集合中的所有元素                                         |
| copy()                        | 拷贝一个集合                                                 |
| difference()                  | 返回多个集合的差集                                           |
| difference_update()           | 移除集合中的元素，该元素在指定的集合也存在。                 |
| discard()                     | 删除集合中指定的元素                                         |
| intersection()                | 返回集合的交集                                               |
| intersection_update()         | 删除集合中的元素，该元素在指定的集合中不存在。               |
| isdisjoint()                  | 判断两个集合是否包含相同的元素，如果没有返回 True，否则返回 False。 |
| issubset()                    | 判断指定集合是否为该方法参数集合的子集。                     |
| issuperset()                  | 判断该方法的参数集合是否为指定集合的子集                     |
| pop()                         | 随机移除元素                                                 |
| remove()                      | 移除指定元素                                                 |
| symmetric_difference()        | 返回两个集合中不重复的元素集合。                             |
| symmetric_difference_update() | 移除当前集合中在另外一个指定集合相同的元素，并将另外一个指定集合中不同的元素插入到当前集合中。 |
| union                         | 返回两个集合的并集                                           |
| update()                      | 给集合添加元素                                               |