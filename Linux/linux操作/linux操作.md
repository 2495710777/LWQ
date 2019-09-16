ls -l 以列表的形式列出，详细信息

apt 下载软件的命令

apt install sl   终端里的小火车

下载东西需要用root权限sudo  (super do)

在下载东西时加-y是yes的意思，不需要再次确认

man手册 make 编译 openssl加密库（https） tree 一级一级的目录  vim敲代码的编辑器

curl 在终端里发送http请求 	telnet	检查网络状态，与服务器通不通 

traceroute 追踪到某个服务器的路径  wget下载

lib开头，，，一些软件的源代码

git  mysql-sever  mysql-client   zip   p7zip在linux中解压rar软件，不能压缩回去

rm -r  删除文件夹    tar -xzf 压缩包名   解压    tab键自动补全   cd(change directory)

Ubuntn  的是.deb  linux中默认可执行软件



CentOs  下的软件包是  .rpm

连接云服务器ssh root@x.x.x.x

yum  命令  yum install python36







Hardware   硬件   Kernel 操作系统的核心

shell应用程序，连接用户和Linux内核

操作系统(内核加shell)每个窗口就是一个shell

​	GUI图形用户界面shell

​	CLI命令行式shell

**ctrl:**

​	a  e 开头结尾

​	f  b  左右

​	w 删除单词到终端的粘贴板  y

​	u删除左边全部   k右全部







df -h 查看硬盘的使用 		/dev/sda1本质都在这个里面

tmpfs  虚拟设备挂载点

后面加个/代表是文件夹,增加挂载点，目录树是不会变的，把目录树映射到不同分区里

touch /var/abc.sh    创建一个abc.sh文件，挂载到相应的分区内

boot：引导启动 	整个操作系统的内核在boot里面，不能删除任何东西，会启动不了

切回刚才使用的目录cd -			 cd /   回到根目录

五分钟之内不用重新输入密码

bin普通用户可以用  sbin管理员级别使用

dev 设备目录

echo 'abcdefg'   在屏幕打印字符串

~  家目录  / 根目录

echo "asdasd" > abc  把内容写入abc文件，，文件不存在会创建，会覆盖    	>>  追加

cat abc 查看内容

 echo "xsdsadafg" > /dev/null 直接销毁，不会写入（/dev/null）

/dev/zero   无限的0文件   /dev/random  随机数文件（产生的是真实的随机把生活中的随机场景收集放到熵池中）   python中random的随机是伪随机

/dev/shm   写在这个文件里的是直接写到内存中，重启消失

etc  系统配置文件

proc  进程文件

|连接两个命令

 cat /proc/cpuinfo | **grep** process
processor	: 0
processor	: 1
processor	: 2
processor	: 3

pwd： 显示当前的绝对路径

~ 家目录可以随便操作，各种文件

**sudo  su  -**  进到超级管理员目录

rm -rf  / 格式化硬盘

ctrl+d 注销

ls -l  显示的大小是字节

ls -l h 以k为单位

在文件名前面加   .   变成隐藏文件

查看隐藏文件  ls -a(all)

删除文件  rm  文件名

删除文件夹 rm -r 文件夹名/

mkdir -p a/b/c/d   加一个-p可以创建多层文件夹

tree a  以树状格式显示a文件夹的层级

mkdir -p a/{b/{d,e},c/{f,g}}

touch a/b/d/{x,y,z}

mv移动

cp复制  cp a/c/x/ a/b/d

mv a/c a/b/d  移动文件夹

cp -r a/b/d/c a/   在移动回去

mv x zzz   把x改名为zzz



mv -n zzz pppp  遇到已存在的文件默认不覆盖，不修改		-i是询问是否覆盖

cp也一样

创建快捷方式：

​	ln(link) -s zzz yyy   zzz不存在yyy也不能使用（相对路径）

​	写绝对路径可以创建快捷方式  ln -s a/c/pppp xxx

硬链接只能在一个分区里面，修改硬链接里面的内容，原内容也会修改，给文件产生一个别名，删除源文件，硬链接的内容也不会变

tar -czf(creat zip file)  a.tgz(压缩名)  a/./.（文件名）	压缩

tar -xzf(解压)

find ./ -name "*.txt"  查找匹配

find ./ -type d  文件夹

find ./ -type f  文件

 find ./ -size -1k 查找小于1k的文件

 find ./ -size +1k 查找大于1k的文件

 find ./ -size +1k -size -3k 查找大于1k小于3k的文件

