# break和continue

break和continue都用在循环语句里，用来控制循环。

## break的使用

结束整个循环。

```python
i = 1
while i <= 10:
    if i == 7:
        break
    print(i)
    i += 1
```

输出结果是:

```python
1
2
3
4
5
6
```

## continue的使用

结束本次循环，开始下一轮循环。

```python
i = 1
while i <= 10:
    if i == 7:
        continue
    print(i)
    i += 1
```

输出结果是:

```python
1
2
3
4
5
6
8
9
10
```

## 练习

不断的询问用户，"我爱你，你爱我吗?"，只有用户回答"爱"时，结束循环。

```python 
while True:
    feel = input('我爱你，你爱我么？：')    
    if feel == '爱':        
        break
#  不断地提示用户输入用户名和密码，只有用户名是张三，密码是123才停止while True:    
	user_name = input('请输入用户名：')    
    password = input('请输入密码：')    
    if user_name == '张三' and password == '123':        			break
```

## 注意点

1. 在Python中，break和continue只能用于循环语句中。
2. break和continue在嵌套循环中使用时，只当层循环有效。
3. continue语句和break支队离他最近的循环有效
4. 后面都不能跟任何的语句