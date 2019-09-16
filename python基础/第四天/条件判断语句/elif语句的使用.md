# elif

## 一、 elif的功能

elif的使用格式如下:

```python
    if xxx1:
        事情1
    elif xxx2:
        事情2
    elif xxx3:
        事情3
```

+ 例如

```python 
score = float(input('请输入您的成绩：'))
# if 100 >= score >= 90:#     print('好棒棒')
## if 90 >= score >= 80:
#     print('好厉害')
## if 80 >= score >= 60:
#     print('一般般')
## if 60 >= score >= 0:
#     print('真垃圾')
# 100 >= score >= 90 其他语言可能不支持，需要score<=100 and #score >= 90
if 100 >= score >= 90:    
    print('好棒棒')
elif 90 >= score >= 80:    
    print('好厉害')
elif 80 >= score >= 60:    
    print('一般般')
elif 60 >= score >= 0:    
    print('真垃圾')
else:    print('输入数据错误')
```

应用:猜拳游戏

```python 
# python 里有一个内置模块，random专门用来生成随机数
# 一个模块就是一个py文件，如果想要使用一个模块，需要使用import语句先# 导入这个模块import random
#  获取玩家输入的数字
player = int(input('请输入剪刀 0，石头 1，布 2：'))computer = random.randint(0, 2)  
# 生成[0,2]的随机整数
print('player = %d,computer = %d' % (player, computer))
if player == 0 and computer == 2 or player == 1 and computer == 0 or player == 2 and computer == 1:   
    print('恭喜你获胜了\n你好厉害')
elif player == computer:    
    print('啊哦，竟然是平局')
else:    
    print('太遗憾了，你输了呀')
```