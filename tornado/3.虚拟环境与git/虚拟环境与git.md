## 虚拟环境与Git

### 一、MVC网站架构

为了更好的开发我们的服务器，我们需要对我们的程序进行一些规划。通常使用的 

​		![1568202269833](C:\Users\lwq\Desktop\tornado\3.虚拟环境与git\1568202269833.png)

MVC模式(Model-view-controller)是软件工程中的一种软件架构模式，把软件系统分为三个基本部分：

- 模型(Model),它是程序需要操作的数据或信息
- 视图(View),它提供给用户的操作界面，是程序的外壳
- 控制器(Controller),它负责根据用户从’视图层‘输入的指令，选取“数据层”中的数据，然后对其进行相应的操作，产生最终结果

这种模式的特点是构建简单, 层次清晰, 代码可复⽤性好, 模块之间耦合度低

对应到我们的服务器程序，简单来说，就是⼀些模块只负责前端⻚⾯显示，另⼀些模块只负责数据模型
的定义和数据的操作，其他模块负责连接这两部分，并进⾏必要的逻辑处理。

对应到程序细节
我们可以按照程序功能不同，分为 3 个模块。

```shell
├── main.py  --> Controller
├── models.py -->Model层
├── view.py -->View层
├── requirements.txt
├── statics
│   └── img
│       └── logo.png
├── templates
    ├── all.html
    ├── base.html
    ├── info.html
    └── modify.html

```

## 二、虚拟环境

实际⼯作中，我们可能同时要维护若⼲个项⽬，每个项⽬使⽤的软件包、版本可能都不⼀样，⽐如项⽬A 使⽤ tornado 4.3，⽽项⽬ B 使⽤ tornado 6.0 版，这时如果将两个版本同时装到全局的 Python 环境下就会冲突。

所以我们要为不同的项⽬单独设置它运⾏所需的环境，这就需要借助虚拟环境管理

1、安装

```python
pip install virtualenv
```

2、在项目文件中创建虚拟环境

```shell
cd ~/项目文件夹
# 创建虚拟环境
# 虚拟环境可以创建到任何位置，但⼀般与项⽬⽂件夹放到⼀起
virtualenv env # 名字可以任意取
```

3、加载虚拟环境

```shell
# 在创建好之后还不能使用，需要加载激活
source ~/项目文件夹/env/bin/activate
加载成功后会在开头出现虚拟环境文件env的名字
```

共享虚拟环境：

​    pip freeze  > requirements.txt 运行环境所需要的所有包

把所有的东西发给另一个用户

另一个用户在项目所在的文件中创建一个虚拟环境，然后加载

然后把打包过的txt文件中的包全部下载，就创建个完全相同的虚拟环境

```
pip install -r requirements.txt
```

此时就可以正常运行了

4、退出虚拟环境

```shell
deactivate  # 当开发完成后，可以退出当前虚拟环境
```

## 三、版本控制工具与Git

### 版本控制工具的作用

- 能够追踪全部代码的状态

- 找出不同版本代码之间的差异

- 能够进行版本回滚
- 能够协助多个开发者进行代码合并（有冲突的代码需要开发者手动合并）

diff 能够比较两个文件有什么不同，但是非常的不直观

### 常见的版本控制工具

- CVS：基本退出了历史舞台
- svn：中心化的版本控制工具，需要有一台中心服务器

（当服务器崩溃时，所有的操作都会停止，文件也会丢失）

​		![1568204910554](C:\Users\lwq\Desktop\tornado\3.虚拟环境与git\1568204910554.png)

- git：分布式的版本控制工具，中心服务器不再是必需的（可以有，每个人都是一个服务器，可以上传，可以下载）

  ​	

![1568204995236](C:\Users\lwq\Desktop\tornado\3.虚拟环境与git\1568204995236.png)

- hg: 纯python开发的版本控制工具
- Github：依托Git而创建的一个平台，有独立的公司在运作
- 备注：所有的文本类的东西都可以交由版本控制工具来管理

### git的历史

Git 最初由 Linus 为了维护 Linux 内核源码⽽开发。
Linus 当时因不堪忍受早期版本控制⼯具的各种问题，最终决定⾃⼰开发了⼀个，并且将它开源出来，
供所有⼈使⽤。
历史详情可点击这⾥：[全球最大同性交友平台的“黑历史”](https://mlog.club/article/34876)

#### 1、起步

- 先下载git包

```shell
sudo apt install git
```

- 之后配置绑定自己的账号和邮箱

  ```shell
  git config --global user.name '你的名字'
  git config --global user.name '你的邮箱'
  绑定后自动生成ls ~/.gitconfig
  ```

- 设置要忽略的文件

- git init 对仓库进行初始化，产生了一个 `.git`的目录，这个文件夹就是本地的仓库

- 对于不需要让Git追踪的文件（比如虚拟环境文件）可以在项目目录下创建`.gitignore`文件

  ```shell
  touch .gitignore
  ```

  `.gitignore`文件中可以写需要忽略的文件名，或是某一类文件的通配符， 如下

  ```shell
  *.pyc
  *.log
  *.sqlite3
  .DS_Store
  .venv/
  .idea/
  __pycache__/
  ```

- 把需要提交到文件添加到暂存区

  ```shell
  git add .  (aaa bbb ccc)
  ```

- 将暂存区的文件拿出暂存区

  ```shell
  git reset .  <文件名 文件名> 或者 git rm --cached 文件名1 文件名2
  ```

- 将暂存区的文件提交到本地仓库

  ```shell
  git commit -m '对提交的文件的描述'
  ```

- 在github上创建仓库，拿到仓库的地址

   git remote add origin https://github.com/2495710777/day3.git  使用HTTP协议每次push上传都要输入密码，推荐使用ssh的协议

  git remote add origin git@github.com:2495710777/day3.git

  在本地添加一个配置，告知我要提交到哪个仓库

  最好是用这个，在提交上来时不需要输入密码

  在首次使用github时，需要在执行一步，在家目录执行

  `ssh-keygen`

  cd ~/.ssh

  id_rsa 密钥 id_rsa.pub 公钥  他们两个相互制约 公钥可以公开，私钥绝对不能公开

  然后把公钥复制添加到github的ssh密钥的位置

  在执行下面的代码

  在首次提交时：git push -u origin master

  以后更新文件提交直接：git push

- 其他人第一次拿github库中的项目

  把GitHub的文件克隆下来（一个仓库只执行一次）

  git clone git@github.com:2495710777/day3.git

- 再次取出更新的文件用pull就可以

  git pull git@github.com:2495710777/day3.git

**随笔**

git log --graph 查看多个提交的状态

`回退到某个版本：git checkout 9c4f66405ef55f34dbe89df3796eb858f650e186`

`在返回现在的版本：git checkout master`

git checkout <文件名>  还原修改的代码，前提是被修改的代码没有被add添加到暂存区，和没有被提交的。从暂存区中取出（reset,rm --cached），还可以还原

git blame <文件名> 该文件的每行代码的最后一次修改人



git branch <分支名> 创建一个新的分支

git checkout <分支名> 切换到新的分支工作

git checkout -b <分支名> 创建之后直接选择

#### 2、必须要掌握的Git命令

| Command                                           | Description                                                  | 与远程通信 | 操作示例                                        |
| ------------------------------------------------- | ------------------------------------------------------------ | ---------- | ----------------------------------------------- |
| init                                              | 在本地初始化一个新的仓库,会生成一个.git的文件                | —          | `git init`                                      |
| add                                               | 把需要上传的文件添加到暂存区                                 | —          | `git add aaa bbb`                               |
| commit                                            | 将暂存区的文件提交到本地仓库                                 | —          | `git commit -m '注释'`                          |
| push                                              | 将本地仓库的内容推送到远程仓库中（比如github）               | 有         | `git push`                                      |
| pull                                              | 将远程仓库的更新拉取到本地仓库                               | 有         | git pull                                        |
| clone                                             | 将远程仓库克隆到本地                                         | 有         | `git clone git@github.com: 2495710777/day3.git` |
| branch                                            | 管理分支                                                     | —          | git branch 分支名                               |
| checkout                                          | 切换分支/代码回滚/代码还原                                   | —          | git checkout 分支名 / 提交ID                    |
| diff                                              | 不同版本之间进⾏差异对⽐,可以直接比较这种修改过  但还没有添加到暂存区的文件做了什么修改 | —          | git diff 版本1 版本2                            |
| merge:把某个分支合并过来 rebase：合并到某个分支上 | 合并两个分支                                                 | —          | git merge 其他分支名                            |
| status                                            | 查看当前分支的状态                                           | —          | git status                                      |
| log                                               | 查看提交历史                                                 | —          | git log/git log --graph                         |
| reset                                             | 代码重置/代码回滚                                            | —          | git reset                                       |
| blame                                             | 检查文件的每行代码最后一次是谁修改的                         | —          | git blame 文件名                                |

git log --graph 查看多个提交的状态

`回退到某个版本：git checkout 9c4f66405ef55f34dbe89df3796eb858f650e186`

`在返回现在的版本：git checkout master`

git checkout <文件名>  还原修改的代码，前提是被修改的代码没有被add添加到暂存区，和没有被提交的。从暂存区中取出（reset,rm --cached），还可以还原

git blame <文件名> 该文件的每行代码的最后一次修改人

#### 3、⽤游戏的⽅式练习 Git
请点击 https://learngitbranching.js.org/

#### 4、练习

1. 在 Github.com 上建⽴⾃⼰的账号，将前⼏天写的代码提交并推送上去
2. 每次代码更新后，提交、推送