## 一、Shell脚本概述

通过Shell中的各种命令，开发者和运维人员可以对服务器进行维护工作

为了能够对服务器批量执行操作，我们可以将需要执行的命令写入文件，执行批量，这种文件便是Shell脚本。

## 二、Shell 脚本首行

在Shell脚本中，#开头的文本是注释，但第一行 #！开头的这句话比较特殊，他会告诉Shell应该使用哪个程序来执行当前脚本。

常见的方式有：

- `#!/bin/sh`
- `#!/bin/bash`
- `#!/usr/bin/env bash`

对于python脚本的第一句一般是 `#!/usr/bin/env python`

 ## 三、创建脚本

1.创建cpu-count.sh文件

2.![1567339937437](C:\Users\lwq\AppData\Roaming\Typora\typora-user-images\1567339937437.png)

- 创建脚本之后还不能执行，因为创建出来的文件的权限都是644，所以第一步先修改文件的权限为775	即 chmod 775(a+x) cpu-count.sh

- 输入 ./cpu-count.sh 执行脚本
- 查看上一条命令的退出状态：`echo $?`
  - linux中的所有程序执行结束后都装状态码
  - 状态为**0**表示正常，状态码只要不是0代表执行异常

**知识点**

- 在脚本中 `export A=123`定义全局变量
-    echo输出 echo “abc\ndef” ==> 不会换行
-    echo输出 echo -e “abc\ndef” ==> 加个-e会换行
- 在普通文件夹中的脚本程序执行需要用 `./cpu-count.sh`当把脚本程序移动到 /usr/local/bin 目录下时可以直接使用  `cpu-count.sh`
- /usr/bin 是存放系统级脚本的地方

## 四、变量

1、定义

- 如果像在python中定义变量的方式 `a = 123`  在linux中会报错,在linux中定义变量的时候，**`=前后都没有空格  a=123`**
- 输出查看变量  ：**echo "$a"** 
- 输出还可以使用:**printf  "$a"**  linux不自带，需要安装
- 在脚本中使用变量：**echo "a is $a"**  a is 123
  - echo后面跟的是单引号： 里面的内容会原样输出
  - 双引号：**如果有$会转变成对应变量的值**
  - 利用`expr`可以进行变量的算数运算（+、-）
    - ![1567342267076](C:\Users\lwq\Desktop\Linux\linux操作5\img\1567342267076.png)

![1567343043319](C:\Users\lwq\Desktop\Linux\linux操作5\img\1567343043319.png)

**echo $[$a * $b]   ==>只有在[] 以数字的形式运算，其他情况是变量的拼接**

- **全局变量**
  - `export A=123`   定义当前Shell全局变量（在脚本中编辑的）
  - `source  脚本`   ==>终端重新加载脚本,才可以使用

- **常用的系统环境变量**
  - echo $PATH  可执行文件的目录
  - echo $PWD  当前目录的绝对路径
  - echo $HOME  目录
  -  echo $USER  当前的用户名
  - echo $UID  当前用户的UID

- whoami     可以查看当前登陆的用户名

## 五、分支语句：if

分支控制语句完整格式：

```linux
if 命令
then
	语句1
elif 命令
then
	语句2
else
	语句3
fi  ==>标志着if语句的结束  
linux对于缩进没有讲究
```

- if 语句 判断的是后面跟的命令的状态码： **0为true，其他值为false**

- if 语句 后面跟条件测试命令： [ ... ]

  - shell 提供了⼀种专⽤做条件测试的语句 [ ... ]
  - 这⼀对⽅括号本质上是⼀个命令, ⾥⾯的条件是其参数, 所以 [ 的后⾯和 ]的前⾯必须有空格, 否则会报错。
  - 他可以进⾏三种⽐较
    - 数值⽐较
    - 字符串⽐较
    - ⽂件⽐较

  **注意**  if 后面需要空格，中括号也是命令(-f 是前半中括号的参数)，是个测试命令，中括号里面内容前后都需要空格，不然会认为整体为一个命令

```linux
if [ -f abc.md ];分号是把命令拼接成一行使用的，不重要
then   // 如果
	echo 'it is a file';
else
	echo 'it is not a file';
fi  

//把if后面改成  if ls abcd;   ==> 意思：ls是命令，查看ls有没有abcd文件

if后面是判断状态码是否为正常，如果为0，执行then中语句，否则执行else
```

- 数值比较
  - `[ n1 -eq n2 ]`   ==> 判断n1 与 n2 是否相等
  - 同理 `-ge`大于或等于、`-gt`大于、`-le`小于或等于、`-lt`小于、`-ne`不等于

```linux
//实例：
a=123
b=123
[ $a -eq $b]; echo $?    ==>成立返回0，否则返回1
如果我想直接输入符号，那么需要在加个[]，如果不加会认为是字符串比较
[[ $a == $b ]];echo $?
```

- 字符串比较
  - `=` 是否相等、`!=`不相等、`<`、`>`
  - `-n`检查长度是否不为0
  - `-z`检查长度是否为0

![1567344803240](C:\Users\lwq\Desktop\Linux\linux操作5\img\1567344803240.png)

```linux
a='qwer'
b='qwer'
c='poiu'
[ $a = $b ];echo $?
[ $a > $c ];echo $?  ==> 0  ，按照ASCII值进行比较
[ -n $a ];echo $?  ==> -n检查该字符串是否为 非空
[ -z $a ];echo $?  ==> -z检查该字符串的是否为 空 0 z指zero
```

- 文件的比较
  - `-d`是否存在并且是一个目录
  - `-e`是否存在
  - `-f`是否存在并且为一个文件
  - `-r`是否可读
  - `-w`是否可写
  - `-x`是否执行
  - `-s`是否非空
  - `-O`是否属于当前用户
  - `-G`默认组与当前组是否相同
  - `-nt`比较前者是否比后者新
  - `-ot`比较前者是否比后者旧

```linux
[ -d $1 ];echo $?   ==>如果我传的是个文件夹，那么返回0，否则返回1。
同理其他的语句
```

## 六、循环语句：for

Shell 中的循环结构有三种: for 、 while 和 until , 这⾥重点介绍 for 循环。

1. for 循环的基本格式:

   ```linux
   for 变量 in 序列 do
    要执⾏的命令
   done
   ```

2. 练习: 打印 1 到 10 中的偶数

   ```linux
   for i in `seq 1 10`    //与python中的range不同，seq 是双闭区间
   do  //开始执行
    	if [[ $[ $i % 2] == 0 ]]
   	then
    		echo "偶数: $i"
    	else
    		echo "奇数: $i"
    	fi
    done //结束
   ```

   1. seq START END 语句⽤来产⽣⼀个数字序列
   2. $[ NUM1 + NUM2 ] 语句⽤来进⾏基本的数学运算
   3. [[ ... ]] 语句⽤来更⽅便的进⾏⽐较判断

3. C语⾔⻛格的 for 循环

  ```python
  for ((i=0; i<10; i++))  //双层小括号，里面不需要$符号，i也不需要声明
  do
   echo "num is $i"
  done
  ```

  ![](C:\Users\lwq\Desktop\Linux\linux操作5\img\1567345429085.png)

## 七、函数 function

linux的函数定义时参数不写在括号内，因为在Linux环境下，任何一个字符都代表是一个命令，在调用时也不需要写括号，所以无法在括号内传参数

定义时 function 不是必须的，可以省略

```python
//定义函数
function foo(){   （）都为空
	echo 'i am foo'
}
foo     //函数调用，不需要括号

//如果里面不写foo调用函数，在外部调用应该如何操作？
需要在终端 
source 脚本文件   ==>相当于python中import    . 也可以代替source
foo   直接在终端就可以直接调用了
```

那么如何传参数呢：

![1567346420484](C:\Users\lwq\Desktop\Linux\linux操作5\img\1567346420484.png)

当把参数都写在函数体的外部，会接收来自脚本本身传进来的参数

![1567346712419](C:\Users\lwq\Desktop\Linux\linux操作5\img\1567346712419.png)

在调用脚本函数的时候需要在外部重载`source 脚本文件`或者`. 脚本文件`然后再调用函数以及传入参数

**获取用户的输入**

- read  -p  '请输入一个数字：'  num `    ==> -p 是提示语句
- echo  '您的输入：$num ' 
- ![1567348893034](C:\Users\lwq\Desktop\Linux\linux操作5\img\1567348893034.png)



练习：利用MD5加密判断两个文件是否相等

![1567348134320](C:\Users\lwq\Desktop\Linux\linux操作5\img\1567348134320.png)