# Git 学习总结

> 特别声明：本文档内容总结自廖雪峰老师博客出品的Git教程，欢迎大家移步过去膜拜：
>
> <https://www.liaoxuefeng.com/wiki/896043488029600>

## 1. 集中式 VS 分布式

### 1.1 集中式

版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆。典型的代表就是：**CVS** 和 **SVN**

![集中式](C:\Users\Amstrong\AppData\Roaming\Typora\typora-user-images\1564493020076.png)

### 1.2 分布式

布式版本控制系统根本没有 “中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件 A，你的同事也在他的电脑上改了文件 A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

> 在实际使用分布式版本控制系统的时候，其实很少在两人之间的电脑上推送版本库的修改，因为可能你们俩不在一个局域网内，两台电脑互相访问不了，也可能今天你的同事病了，他的电脑压根没有开机。因此，分布式版本控制系统通常也有一台充当 “中央服务器” 的电脑，但这个服务器的作用仅仅是用来方便 “交换” 大家的修改，没有它大家也一样干活，只是交换修改不方便而已。

![1564493260183](C:\Users\Amstrong\AppData\Roaming\Typora\typora-user-images\1564493260183.png)

### 1.3 分布式版本管理的优势

- **无需联网**

集中式版本控制系统最大的毛病就是必须联网才能工作，如果在局域网内还好，带宽够大，速度够快，可如果在互联网上，遇到网速慢的话，可能提交一个 10M 的文件就需要 5 分钟

- **安全性更高**

集中式版本控制系统依赖中央服务器，如果中央服务器宕机或者其他意外，那么将无法正常工作，并且会导致文件丢失。而分布式版本控制系统，只需要从其他人那里再复制一个即可。

- **分支管理**

Git中关于版本控制中的分支管理概念，是其他版本控制系统所没有的

- **免费**



##  2. Git 安装



### 2.1 在Linux上安装

最简便的方法，试着输入`git` ，看看系统有没有安装 Git，现在的 Linux 都会提示你是否安装，并且如何安装

```bash
$ git
The program 'git' is currently not installed. You can install it by typing:
sudo apt-get install git
```

### 2.2 在 Windows 上安装

1. 官网下载：<https://git-scm.com/downloads>
2. 傻瓜式安装
3. 安装过程中一定记得勾选安装 Git bash（一个能让你在Windows上使用Linux指令操作电脑的shell）





## 3. Git常用命令总结



### 3.1 全局配置

- 在本机上全局配置用户名

```bash
$ git config --global user.name "Your Name"
```

- 在本机上全局配置用户邮箱

```bash
$ git config --global user.email "email@example.com"
```

### 3.2 创建版本库并向版本库中添加文件

- 初始化版本库

> 版本库又名仓库，英文名**repository**，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

```bash
$ git init
Initialized empty Git repository in F:/A-Python学习教程/Git使用文档/.git/
```

- 添加文件到版本库（可以同时add 多个文件）

```bash
$ git add README.md README1.md
```

- 提交文件更改

```bash
$ git commit -m <message>  # commit 命令会自动提交所有add到版本库中的文件
```

> ![1564495328535](C:\Users\Amstrong\AppData\Roaming\Typora\typora-user-images\1564495328535.png)
>
> 简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。
>
> 嫌麻烦不想输入`-m "xxx"`行不行？确实有办法可以这么干，但是强烈不建议你这么干，因为输入说明对自己对别人阅读都很重要。实在不想输入说明的童鞋请自行Google，我不告诉你这个参数。
>
> `git commit`命令执行成功后会告诉你，`1 file changed`：1个文件被改动（我们新添加的readme.txt文件）；`84 insertions`：插入了84行内容（readme.md有84行内容）。

### 3.3 文件修改后更新版本

- 查看当前版本库中的文件状态

```bash
$ git status
```

> ![1564495711807](C:\Users\Amstrong\AppData\Roaming\Typora\typora-user-images\1564495711807.png)
>
> `git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令 **modified** 输出告诉我们，`README.md`被修改过了，但还没有准备提交修改。

- 查看文件修改内容

```bash
$ git diff
```

> ![1564495828621](C:\Users\Amstrong\AppData\Roaming\Typora\typora-user-images\1564495828621.png)
>
> `git diff`顾名思义就是查看difference，显示的格式正是Unix通用的diff格式，`---`表示相对于上一版本删除的内容，`+++`表示当前版本相比上一版本增加的内容，可以从上面的命令输出看到文件修改的内容。

- 提交新版本

提交修改和提交新文件是一样的两步：

1. 第一步是`git add`

```bash
$ git add readme.txt
```

2. 第二步是`git commit -m <说明内容>`



> 我们再来对比下，这些操作之间，如果我们查看版本库状态分别显示的内容：
>
> ###### 1. 文件改动后查看 `git status`
>
> ![1564496500168](C:\Users\Amstrong\AppData\Roaming\Typora\typora-user-images\1564496500168.png)
>
> `git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令 **modified** 输出告诉我们，`README.md`被修改过了，但还没有准备提交修改。
>
> ###### 2. 使用 `git add README.md` 和 `git commit -m '说明信息' ` 完成版本提交后
>
> ![1564496711642](C:\Users\Amstrong\AppData\Roaming\Typora\typora-user-images\1564496711642.png)
>
> Git告诉我们当前没有需要提交的修改，而且，工作目录是干净（working tree clean）的。



### 3.4  版本回退

> 你不断对文件进行修改，然后不断提交修改到版本库里，就好比玩RPG游戏时，每通过一关就会自动把游戏状态存盘，如果某一关没过去，你还可以选择读取前一关的状态。有些时候，在打Boss之前，你会手动存盘，以便万一打Boss失败了，可以从最近的地方重新开始。Git也是一样，每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在Git中被称为`commit`。一旦你把文件改乱了，或者误删了文件，还可以从最近的一个`commit`恢复，然后继续工作，而不是把几个月的工作成果全部丢失。

- 查看所有文件版本

```bash
$ git log   # 由上到下为新版本--老版本 commit：版本号 author:作者 Date：提交日期 最后一行为我们在comit -m 指令后写的版本信息
```

![1564498086897](C:\Users\Amstrong\AppData\Roaming\Typora\typora-user-images\1564498086897.png)

如果我们需要精简显示版本日志：

```bash
$ git log --pretty=oneline  # 以单行精简模式显示
```

![1564498261745](C:\Users\Amstrong\AppData\Roaming\Typora\typora-user-images\1564498261745.png)

- 版本回退

`--hard` 参数的含义后面会说明

```bash
$ git reset --hard <版本号>
# 版本号的常用格式：
# 1. 回退一个版本：head^
# 2. 回退2个版本：head^^
# 3. 回退多个版本：head~100
```

