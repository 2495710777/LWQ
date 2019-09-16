### 基本命令

**Kernel**

kernel是操作系统的核心，直接与硬件打交道，处理底层事情，一般禁止普通用户直接操作，外部程序如果想要调用内核功能需要使用“系统调用的接口”

![1566904309921](C:\Users\lwq\AppData\Roaming\Typora\typora-user-images\1566904309921.png)

**Shell**

shell是有一个应用程序，连接了用户和Linux内核，让用户高效安全低成本的使用Linux内核。。一般分为“用户界面GUI”和“命令行CLI”两种

**常见的GUI Shell**

- Gnome
- KDE
- xface

**常见的CLI Shell**

- sh: Bourne shell, 史蒂夫·伯恩在⻉尔实验室编写.1978年随Version7Unix⾸次发布
- csh:C shell 比尔，乔伊  1979 你那随BSD首次发布
- bash: Bourne-Again shell 1987年由布莱恩·福克斯为了GNU计划⽽编写。能运行于⼤多数类Unix系统的操作系统之上，包括Linux 与 MacOS 都将它作为默认shell。是应⽤最⼴的 Shell。
- zsh:Z shell “The last shell you'll ever need!,对sh进行改进，加入其他功能，强化自动补全功能，加入插件机制，定制性高，功能强大
- 通过cat /etc/shells  查看当前系统安装了哪些shell

#### 主要用的Bash快捷键

```linux
ctrl + f	前进一个字符
ctrl + b	后退一个字符
ctrl + a	光标转到行首
ctrl + e	光标转到行尾
ctrl + w	向左删除一个单词
ctrl + u	向左删除全部
ctrl + k	向右删除全部  垂直制表符
ctrl + y	粘贴u,k删除的内容
ctrl + l	清屏
ctrl + c	终止程序运行
ctrl + d	退出当前终端
ctrl + z	暂停，并放入后台
ctrl + s	暂停屏幕输出
ctrl + q	恢复屏幕输出
ctrl + h	删除一个字符
ctrl + i	水平制表符
ctrl + j	新行
ctrl + t	交换光标位置和光标前一个字符的位置
```

### 目录结构

linux中没有盘符之分，都在一整个根目录中，linux会在根驱动器上创建一些特别的目录，称之为挂载点（mount point），挂载点是虚拟目录中用于额外存储设备的目录，蓄奴目录会让文件和目录出现在这些挂载点目录中，而实际上他们存储在另外一个驱动器中

```linux
/					系统的根目录,不会在这里存储文件  cd /
boot				启动目录

bin					系统的二进制目录，存放普通用户的GNU命令

sbin				系统超级二进制目录，存放管理员级别的GNU命令

usr					资源目录（user system resources）
	bin				用户二进制目录，存放用户级的GNU命令
	sbin			用户超级二进制，存放管理员用户的GNU命令
	local
		bin
		sbin
opt					第三方开发的程序（option），意为选装
dev					设备目录
	null			是一个无底洞（写进此文件夹的数据都会被丢弃）
	zero			无限的 0 数据流（用来产生一个特定大小的空白文件，或者安全销毁文件）
	shm				内存文件夹（写到此文件里是直接写到内存中，重启后消失）
	random			随机数发生器  真正的随机数，在日常生活中收集随机场景的事件，放到熵池中，python中的random随机是伪随机事件
	urandom			非阻塞的随机数发生器
etc					存放系统配置文件目录（et cetera）
proc(process)		存放当前的进程、运行状态信息的目录
        |连接两个命令

         cat /proc/cpuinfo | **grep** process
        processor	: 0
        processor	: 1
        processor	: 2
        processor	: 3
root				管理员家目录（/）cd /
home				用户的家目录(~) cd~/cd  此目录可以随便操作，不会影响到系统，和Windows的user文件夹差不多
pwd					显示当前的额绝对路径
sudo su -     		进到超级管理员目录
media 				媒体⽬录，可移动媒体设备的常⽤挂载点，⼀般是系统⾃动挂载到这⾥
mnt 				挂载⽬录，另⼀个可移动媒体设备的常⽤挂载点，⼀般是留给⽤户⼿动挂载
lib 				系统库⽬录，存放系统和应⽤程序的库⽂件
srv 				服务⽬录，存放本地服务的相关⽂件
sys					系统⽬录，存放系统硬件信息的相关⽂件
run 				运⾏⽬录，存放系统运作时的运⾏时数据
tmp 				临时⽬录，可以在该⽬录中创建和删除临时⼯作⽂件
var					可变⽬录，⽤以存放经常变化的⽂件，⽐如⽇志⽂件	
```

echo "asdasd" > abc  把内容写入abc文件，，文件不存在会创建，会覆盖    	>>  追加

cat abc 查看内容

 echo "xsdsadafg" > /dev/null 直接销毁，不会写入（/dev/null）

#### 目录操作

- 绝对路径 /usr/bin/
- 相对路径 ../a/c
- 命令列表
| Command                      | Description                                                  |
| ---------------------------- | ------------------------------------------------------------ |
| pwd                          | 显示当前目录的绝对路径                                       |
| ls ./                        | 显示当前目录的文件                                           |
| ls -l ./                     | 以列表形式显示文件(文件的大小是字节)                         |
| ls -lh ./                    | 以列表形式显示文件(文件的大小是k)                            |
| ls -a                        | 显示所有的文件，主要是隐藏文件                               |
| cd xxx                       | 切换文件目录                                                 |
| cd -                         | 回到上一次所在位置                                           |
| mkdir abc                    | 创建名为abc的目录文件                                        |
| mkdir -p a/b/c               | 创建多层目录结构  -p                                         |
| mkdir -p a/{b/{d,e},c/{f,g}} | a<br/>├── b<br/>│   ├── d<br/>│   └── e<br/>└── c<br/>    ├── f<br/>    └── g |
| touch a/b/d/{x,y,z}          | 在d文件夹中创建x,y,z文件  touch创建文件用                    |
| rm 文件名                    | 删除文件                                                     |
| rm -r 文件名                 | 删除文件夹                                                   |

#### 文件操作

cp	aa  .. /bb/		将aa文件复制到 ../bb目录中（cp x f  把x文件复制到f文件夹）

mv aa ../bb			 将 aa ⽂件移动到 ../ 并更名为 bb

touch abc				在当前⽂件夹创建⼀个 abc ⽂件, 如果已存在则跳过

ln -s abc def 			为 abc ⽂件创建⼀个软链接

cp/mv/rm 的通用参数

- -i:已存在该文件，覆盖前提示
- -n：如果目标文件已经存在，则停止操作
- -f: 不管目标文件是否存在，强制操作，覆盖前不提示（删除一些删不掉的文件）
- -r:递归对文件夹执行某操作（mv 不需要-r）

**硬链接:ln x zz**（link）

- 只能在同分区创建硬链接
- a/c/x xxx
- 一个文件的多个硬链接相当于一个文件有多个名字，多个硬链接在磁盘上只占用一个文件的大小
- 修改硬链接时，所有同源的硬链接都会发生变化
- 删除源文件后，硬链接依然可以使用

**软链接：ln -s  y yyy**

- 可以跨越分区创建，写创建快捷方式文件的绝对路径，在当前文件夹中创建
- 源文件改变，软链接也改变，
- 源文件被删除，软链接失效

### 压缩文件处理

- tar
  - 压缩：tar -czf abc.tar.gz abc/		(Creat Zip File)
  - abc.tar.gz(压缩包的名字)    abc/压缩的文件
  - 解压：tar -xzf abc.tar.gz

- zip
  - 压缩：zip -r abc.zip abc/（文件夹，普通文件不需要-r）
  - 解压：unzip abc.zip

### 查找文件的find命令

筛选

- 查找当前文件夹下的全部文件： find ./
- 只查找文件： find ./ -type f
- 只查找目录： find ./-type d
- 只查找链接： find ./ -type l
- 按名称查找：find ./ -name "(*.py)"
- 按权限查找：find ./ -perm 0644
- 按大小查找:   find ./ -size +1k -size -5k	   (大于1k小于5k的文件)
- 查找后删除：find ./ -name "(*.py)" -delete

