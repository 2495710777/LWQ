# 字符串的format方法

## 1. 概念:

- `str.format()` 方法通过字符串中的大括号`{}`来识别替换字段 `replacement field`，从而完成字符串的格式化。
- `替换字段` 由字段名 `field name` 和转换字段 `conversion field` 以及格式说明符 `format specifier` 组成，即一般形式为 {字段名!转换字段:格式说明符}。
- 字段名分为简单字段名 `simple field name` 和复合字段名 `compound field name`。而转换字段和格式说明符都是可选的。

## 2. 字段名

form的完整格式是{字段名!转换字符:格式说明符}。其中字段名师必须的，而且可以分为简单字段名和复合字段名。

```python
print('你好，我叫%s,今年%d岁' % ('zhangsan', 18))
```

#### 使用{}作为占位符

```python
s1 = '你好，我的名字是{}，今年{}岁'.format('zhangsan',18)
print(s1)
```

#### 使用{数字}作为占位符

```python
s2 = '你好，我的名字是{0}，今年{1}岁'.format('zhangsan',18)
print(s2)
# format 后面的参数可以多于前面占位符的个数
s3 = '你好，我的名字是{0}，今年{1}岁,我同学也{1}'.format('zhangsan',18,'hello')
print(s3)
```

#### 使用关键字参数

```python
# 使用关键字参数
s4 = '你好，我的名字是{name}，今年{age岁'.format(name='zhangsan', age=18, gender='male')
print(s4)
```

#### 使用数字（位置参数）和关键字参数

```python
# 使用关键字参数
s4 = '你好，我的名字是{name}，今年{age岁'.format(name='zhangsan', age=18, gender='male')
print(s4)
# 使用数字和关键字混合使用
# 关键字参数一定要写到位置参数后面
s5 = '你好，我的名字是{0}，今年{age}岁'.format('zhangsan',age=18)
print(s5)
```

#### 使用空和关键字参数混合使用

数字和空不能混合使用

```python
s6 = '你好，我的名字是{}，今年{age}岁'.format('zhangsan', age=18)
print(s6)
# s7 = '你好，我的名字是{0}，今年{}岁'.format('zhangsan', 18)
# print(s7)
```

