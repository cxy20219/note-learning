## 1. Git?
**&emsp;Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。  
&emsp;Git 是 Linux之父为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。**

* 功能 - 版本控制
* 特点 - 分布式版本控制
* 语法 - linux语法  

## 2. 版本控制
**&emsp;版本控制是在开发过程中管理我们写的文件、目录等内容。保存我们开发过程中的修改历史，方便我们进行查看、备份和恢复到以前版本的技术。**
* 实现多人协同开发
* 统计代码
* 跟踪开发过程
* 提高开发效率

## 3. 特点
### &emsp; 版本控制类别
* 本地版本控制   
保存本地记录的每一次更新，可以对每个版本做一个快照.例如：RCS
* 集中版本控制  
所有版本数据保存在服务器上，开发者需要从服务器更新或上传自己的代码。一旦服务器出现问题会出现数据丢失的风险。例如：SVN 
代表：
* 分布式版本控制  
所有版本信息全部同步到本地的每个用户，可以离线在本地提交，也可以联网远程提交。每个用户都是保存的所有版本的数据，降低了丢失的可能性，但保密性较低。例如：Git
&emsp;  
### &emsp; 原理与使用
&emsp;&emsp;*git有四个区域，文件在四个工作区间转换*

* 工作区 : 平时存放代码的地方
* 暂存区 : 临时存放改动，本质是一个文件
* 仓库区 : 安全存放数据的位置，有所有提交的版本记录
* 远程仓库 : 托管代码的服务器
## 4. 安装
* 官网下载：[https://git-scm.com/](https://git-scm.com/)  
* 阿里镜像下载：[https://npm.taobao.org/mirrors/git-for-windows/](https://npm.taobao.org/mirrors/git-for-windows/)

## 5. 基本语法
### &ensp;linux 小tips
* touch     —— 新建文件
* mkdir     —— 新建文件夹
* rm        —— 删除文件
* rm -r     —— 删除文件夹
* mv        —— 移动文件
* clear     —— 清屏
* history   —— 查看命令历史
* help      —— 帮助
* exit      —— 退出
* reset     —— 初始化终端

### &ensp;Git语法

#### &ensp; &ensp; 仓库
```Git
    # 在当前目录新建一个Git代码库
    $ git init
    
    # 新建一个目录，将其初始化为Git代码库
    $ git init [project-name]
    
    # 下载一个项目和它的整个代码历史
    $ git clone [url]
```

#### &ensp; &ensp; 配置
```Git
    # 显示当前的Git配置
    $ git config --list
    $ git config -l
    
    # 查看系统配置:
    $ git config --system --list
    
    # 查看全局配置
    $ git config --global --list
    
    # 设置提交代码时的用户信息
    $ git config [--global] user.name "[name]"
    $ git config [--global] user.email "[email address]"
```

#### &ensp; &ensp; 增加/删除文件
```Git
    # 添加指定文件到暂存区
    $ git add [file1] [file2] ...
    
    # 添加指定目录到暂存区，包括子目录
    $ git add [dir]
    
    # 添加当前目录的所有文件到暂存区
    $ git add .
    
    # 删除工作区文件，并且将这次删除放入暂存区
    $ git rm [file1] [file2] ...
    
    # 停止追踪指定文件，但该文件会保留在工作区
    $ git rm --cached [file]
```

#### &ensp; &ensp; 代码提交
``` Git
    # 提交暂存区到仓库区
    $ git commit -m [message]
    
    # 提交暂存区的指定文件到仓库区
    $ git commit [file1] [file2] ... -m [message]
    
    # 提交时显示所有diff信息
    $ git commit -v
    
    # 使用一次新的commit，替代上一次提交
    # 如果代码没有任何新变化，则用来改写上一次commit的提交信息
    $ git commit --amend -m [message]
```

#### &ensp; &ensp; 分支
```Git
    # 列出所有本地分支
    $ git branch
    
    # 列出所有远程分支
    $ git branch -r
    
    # 新建一个分支，但依然停留在当前分支
    $ git branch [branch-name]
    
    # 新建一个分支，并切换到该分支
    $ git checkout -b [branch]
    
    # 切换到指定分支，并更新工作区
    $ git checkout [branch-name]
    
    # 切换到上一个分支
    $ git checkout -

    # 合并指定分支到当前分支
    $ git merge [branch]
    
    # 不用Fast forward的合并(有历史记录)
    $ git merge --no--ff -m "message" [branch]
    
    # 删除分支
    $ git branch -d [branch-name]
```

#### &ensp; &ensp; 隐藏本地仓库
```Git
    # 隐藏当前仓库内容
    $ git stash
    
    # 显示隐藏的stash列表
    $ git stash list
    
    # 恢复隐藏的内容到本地仓库
    $ git stash apply [stash列表id]
    
    # 删除stash的内容
    $ git stash drop [stash列表id]
    
    # 恢复的同时删掉stash内容
    $ git stash pop
```

#### &ensp; &ensp; 远程同步
```Git
    # 下载远程仓库的所有变动
    $ git fetch [remote]
    
    # 显示所有远程仓库
    $ git remote -v
    
    # 显示某个远程仓库的信息
    $ git remote show [remote]
    
    # 增加一个新的远程仓库，并命名
    $ git remote add [shortname] [url]
    
    # 取回远程仓库的变化，并与本地分支合并
    $ git pull [remote] [branch]
    
    # 上传本地指定分支到远程仓库
    $ git push [remote] [branch]
    
    # 强行推送当前分支到远程仓库，即使有冲突
    $ git push [remote] --force
    
    # 推送所有分支到远程仓库
    $ git push [remote] --all
```
#### &ensp; &ensp; 版本回退
```Git
# 记录修改历史
$ git log

# 回退到上一个版本
$ git reset --hard HEAD^

# 回退往上两个版本
$ git reset --hard HEAD^^

# 回退往上一百个版本
$ git reset --hard HEAD~100

# 回到指定版本
$ git reset --hard [commit_id]

# 记录每一此命令(便于以后回到新版本)
$ git reflog
```
#### &ensp; &ensp; 标签
```Git
# 查看所有标签信息
$ git tag

#带有说明的标签
$ git tag -a <tagname> -m "message"

# 给当前commit打标签
$ git tag [name]

# 给指定commit打标签
$ git tag [name] [commit_id]

# 删除标签
$ git tag -d [name]

# 推送一个本地标签
$ git push origin [tagname]

# 推送全部未推送过的本地标签
$ git push origin --tags

# 删除一个本地标签
$ git tag -d [tagname]

# 删除一个远程标签
$ git push origin:refs/tags/[tagname]
```

## 6. 基本使用流程
### &emsp;**设置用户**
``` Git
git config --global user.name "名字"`  
git config --global user.email "邮箱"`
```

### &emsp;**初始化**
``` Git
    # 方式一:本地生成一个git
    $ git init
    # 方式二:从远端克隆一个仓库
    $ git clone https://gitee.com/xxxxxx/xx.git
```

1. *将已修改文件添加至暂存区*
```Git
    # 查看文件是否被跟踪
    $ get status 
    # 添加指定文件
    $ git add dir/filename 
    # 添加所有已修改文件
    $ git add . 
```    
2. *将暂存区的改动提交到本地的版本库*  
```Git
    # message就是本次提交的简要说明
    $ git commit -m "message" 
```    
3. *从远程仓库拉取*
```Git
    # master可以更换为其他分支
    $ git pull origin master 
```
4. *本地上传，注意在推送前需要先从远程拉取(clone的不需要)*
```Git
    # master可以更换为其他分支
    $ git push -u origin master 
```
&ensp;**VScode中的Git**
* A 表示文件已经被跟踪
* M 表示该文件存在修改
* D 表示该文件被删除
* U 表示该文件是新添加的

参考：  
[https://zhuanlan.zhihu.com/p/276376558](https://zhuanlan.zhihu.com/p/276376558)  
[https://gitee.com/all-about-git](https://gitee.com/all-about-git)  
[https://www.liaoxuefeng.com/wiki/896043488029600](https://www.liaoxuefeng.com/wiki/896043488029600)