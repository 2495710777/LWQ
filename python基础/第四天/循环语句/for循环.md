## for循环的格式

```python
for 临时变量 in 列表或者字符串等可迭代对象:
    循环满足条件时执行的代码
```

## for循环的使用

- 遍历字符串:

```python
for s in "hello":
    print(s)
```

输出结果:

```
h
e
l
l
o
```

- 打印数字

```python
for i in range(5):
    print(i)
```

输出结果:

```
0
1
2
3
4
```

```python
# for ele in iter 循环用来遍历一个可迭代的对象
# iter 必须是一个可迭代对象（字符串，列表，元组，字典）
# ele 可迭代对象里的所有元素
a = 'hello'
for x in a:
    print(x)
# in 后面必须跟一个可迭代对象
for i in range(10):  # range(n)  是一个[0,1,2,3...n)可迭代对象
    print(i + 1)
# range(n,m)  生成[n,m)的数据

# 遍历 把里面的数据都访问一遍
x = ['hi', 'hello', 23, True]
for n in x:
    print(n)
# 用for计算1-100的和
result = 0
for m in range(1, 101):
    result = result + m
print(result)

```