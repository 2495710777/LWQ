kernal和shell组成操作系统



```py
root
x 原本是密码，现在没用
0 UID
0 GID（0代表权限最大）
root  对用户的描述
/root 用户的家目录
/bin/bash 登录进来后使用的shell（nologin表示账号不能登录）
```

**shadow格式**

lwq:$6$lwq:$6$MQChKuVq$/JNV5IdFxKpZNGiVdHVY74nGnc6Sz.GI/HSSMlcE2lhzgJ3i91a6UtLwSpG5zZIkZV564Lc/uQsy5sWn//TRB0:18134:0:99999:7:::MQChKuVq$/JNV5IdFxKpZNGiVdHVY74nGnc6Sz.GI/HSSMlcE2lhzgJ3i91a6UtLwSpG5zZIkZV564Lc/uQsy5sWn//TRB0:18134:0:99999:7:::lwq:$6$MQChKuVq$/JNV5IdFxKpZNGiVdHVY74nGnc6Sz.GI/HSSMlcE2lhzgJ3i91a6UtLwSpG5zZIkZV564Lc/uQsy5sWn//TRB0:加密的密码

18134 最后一次修改密码的时间

:0 密码几天之内可以修改

:99999 密码有效天数

:7密码失效前七天提醒用户修改

: 密码失效的宽限天数

: 账号失效日期

: 保留字段，暂时没用

**Group格式**

root​：组名

x: 原本是密码，现在没用

0:组id

adm​：x:4:syslog,lwq后面跟的是组的成员

密码的加密sha 256  需要加密的内容该一丢丢，产生的加密就会全变

su - tom 初始化tom直接进入tom的家目录exit退出		ctrl D

drwxr-xr-x  2 lwq  lwq   4096 8月  26 15:52 桌面/

d是文件类型，后面九位，第一个三位是拥有者（user）的权限，第二个三位是同组的(group)，第三位是其他人(other)

echo -e 'adsd\nasdf'带上-e转义字符才会有用

`>`重定向

jk前后一行

fb一屏

gG开头结尾

ls -N 显示行号

|   管道     接收前面输出的结果，传给后面当参数

history  | awk "{print $1}"把第几列打印出来

awk是独立的系统

![1567066452649](C:\Users\lwq\AppData\Roaming\Typora\typora-user-images\1567066452649.png)

history | grep -A 3 useradd筛选包含useradd的命令

-A 后三行  -B前三行   -C前后三行

-E正则表达式

yy 复制一行 p粘贴

dd

shift+v选中d删除多行 两次esc取消

d+数字+w删除多个单词

u是撤销

ctrl+ r重做

4x    shift+p

