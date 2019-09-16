# if嵌套

通过学习if的基本用法，已经知道了

- 当需要满足条件去做事情的这种情况需要使用if
- 当满足条件时做事情A，不满足条件做事情B的这种情况使用if-else

## 一、if嵌套的格式

```python
    if 条件1:

        满足条件1 做的事情1
        满足条件1 做的事情2

        if 条件2:
            满足条件2 做的事情1
            满足条件2 做的事情2
```

## 二、if嵌套的应用

```python 
print('欢迎来到上海火车站')
is_ticket = input('是否已经买票：')
if is_ticket == '是':    
    print('有票')    
    is_access = input('是否通过安检：')    
    if is_access == '是':        
        print('通过安检\n可以上车')    
    else:        
        print('米有通过安检')        
        is_danger = input('是否带有违禁物品:')        
        if is_danger == '是':            
            print('派出所七日游')        
        else:            
            print('处理违禁物品\n可以上车了')
else:    print('你米有票，不欢迎你')
```