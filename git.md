# Git 分布式版本控制工具

[TOC] 

## 1.简介

Git 是一个分布式版本控制系统，用于跟踪计算机文件的修改，尤其是源代码。它允许多个开发者协作，同时维护项目的历史记录。

应用场景：

1. 场景一：**备份** 小明负责的模块就要完成了，就在即将Release之前的一瞬间，电脑突然蓝屏，硬盘光荣牺牲！几个月 来的努力付之东流 
2. 场景二：**代码还原** 这个项目中需要一个很复杂的功能，老王摸索了一个星期终于有眉目了，可是这被改得面目全非的 代码已经回不到从前了。什么地方能买到哆啦A梦的时光机啊？ 
3. 场景三：**协同开发** 小刚和小强先后从文件服务器上下载了同一个文件：Analysis.java。小刚在Analysis.java 文件中的第30行声明了一个方法，叫count()，先保存到了文件服务器上；小强在Analysis.java文件中的 第50行声明了一个方法，叫sum()，也随后保存到了文件服务器上，于是，count()方法就只存在于小刚的记 忆中了 
4. 场景四：**追溯问题代码的编写人和编写时间！** 老王是另一位项目经理，每次因为项目进度挨骂之后，他都不知道该扣哪个程序员的工资！就拿这 次来说吧，有个Bug调试了30多个小时才知道是因为相关属性没有在应用初始化时赋值！可是二胖、王东、刘 流和正经牛都不承认是自己干的！



![image-20241027213515106](images/image-20241027213515106.png)

![image-20241027215006107](images/image-20241027215006107.png)

## 2.基本命令



```shell
# 配置信息
git config --global user.name “itcast”
git config --global user.email “hello@itcast.cn”



# 1. 打开用户目录，创建.bashrc 文件
# 2. 在.bashrc 文件中输入如下内容：
#用于输出git提交日志
alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'
#用于输出当前目录所有文件及基本信息
alias ll='ls -al'



# 初始化一个新的 Git 仓库(在工作文件夹里新建.git文件)
git init

# 查看当前状态
git status [filename]

# 查看git日志
git log [--option]
    options
    --all 显示所有分支
 	--pretty=oneline 将提交信息显示为一行
 	--abbrev-commit 使得输出的commitId更简短
 	--graph 以图的形式显
git-log

# 从工作区添加到缓存区
git add [filename]
git add .             #或者添加所有修改的文件

# 从缓存区提交到仓库
git commit
git commit -m "message"    #提交暂存区的更改，附上提交信息。
```



## 3.分支



```shell
# 创建本地分支
git branch branchname

# 查看分支
git branch     #本地所有分支
git branch -r  #远程所有分支
git branch -a  #本地和远程所有分支

# 切换分支
git checkout branchname
git checkout -b branchname #创建新分支并切换到该分支

# 合并分支(将其他分支合并到当前分支)
git checkout branchname

# 删除分支
git checkout -d branchname  #本地
git push origin --delete <branchname>  #远程
```



## 4.远程仓库



```shell
```





## 5.工作流程

### 1、克隆仓库

如果你要参与一个已有的项目，首先需要将远程仓库克隆到本地：

```shell
git clone https://github.com/username/repo.git
cd repo
```

### 2、创建新分支

为了避免直接在 main 或 master 分支上进行开发，通常会创建一个新的分支：

```shell
git checkout -b new-feature
```

### 3、工作目录

在工作目录中进行代码编辑、添加新文件或删除不需要的文件。

### 4、暂存文件

将修改过的文件添加到暂存区，以便进行下一步的提交操作：

```shell
git add filename
# 或者添加所有修改的文件
git add .
```

### 5、提交更改

将暂存区的更改提交到本地仓库，并添加提交信息：

```shell
git commit -m "Add new feature"
```

### 6、拉取最新更改

在推送本地更改之前，最好从远程仓库拉取最新的更改，以避免冲突：

```shell
git pull origin main
# 或者如果在新的分支上工作
git pull origin new-feature
```

### 7、推送更改

将本地的提交推送到远程仓库：

```shell
git push origin new-feature
```

### 8、创建 Pull Request（PR）

在 GitHub 或其他托管平台上创建 Pull Request，邀请团队成员进行代码审查。PR 合并后，你的更改就会合并到主分支。

### 9、合并更改

在 PR 审核通过并合并后，可以将远程仓库的主分支合并到本地分支：

```shell
git checkout main
git pull origin main
git merge new-feature
```

### 10、删除分支

如果不再需要新功能分支，可以将其删除：

```shell
git branch -d new-feature
```

或者从远程仓库删除分支：

```shell
git push origin --delete new-feature
```
