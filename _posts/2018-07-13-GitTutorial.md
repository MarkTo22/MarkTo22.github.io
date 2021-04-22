---
layout: post
title: "Git教程"
date: 2018-07-13   
tag: 工具 
---

### 介绍       

　　Git是做项目的版本管理，你也可以称它们为版本管理工具。假如现在你有一个文件夹，里面可以是项目，也可以是你的个人笔记(如我这个博客)，或者是你的简历、毕业设计等等，都可以使用git来管理。

　　目前常用的版本控制器有Git和SVN，即使这两个你没有全用过，至少也会听过，我这里以Git为例，个人比较喜欢Git，你也可以看看这篇文章：[为什么Git比SVN好](http://www.worldhello.net/2012/04/12/why-git-is-better-than-svn.html)。我使用的是Mac，Mac上没自带Git环境，但是作为iOS开发者，我安装Xcode的时候，Xcode里是有自带Git的，所以我不需要考虑怎么去安装Git了。          

### 安装Git

**在Mac OS X上安装Git**      

提供两种方法参考：      

> 1、通过homebrew安装Git，具体方法请参考[homebrew的文档](http://brew.sh/)      
> 2、直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode。     

**在Windows上安装Git**      

> 从[https://git-for-windows.github.io](https://git-for-windows.github.io) 下载，然后按默认选项安装即可，安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！


### 配置Git      

安装完成后，还需要最后一步设置，在命令行输入：

>* $ git config --global user.name "Your Name"
>* $ git config --global user.email "email@example.com"

"Your Name"： 是每次提交时所显示的用户名，因为Git是分布式版本控制系统，当我们push到远端时，就需要区分每个提交记录具体是谁提交的，这个"Your Name"就是最好的区分。          

"email@example.com"： 是你远端仓库的email       

--global：用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然我们也可以对某个仓库指定不同的用户名和Email地址【global：表示系统用户级别，登陆当前操作系统的用户范围；而没有global参数，表示项目级别/仓库级别，仅在当前本地库范围内有效（优先级更高）】。         



### 开始使用-建立仓库：

你在目标文件夹下使命令：    

>* git init  （创建.git文件）      

就会创建一个 `.git` 隐藏文件，相当于已经建立了一个本地仓库。

### SSH 配置：

业务场景（需要信任你的机器，避免每次提交远程仓库都输入用户名/密码）：    
**打开git bash**      
>* 执行  `cd ~/.ssh `查看是否已配置SSH（如已配置，可删除后，重新生成新的密钥）
>* 执行 `ssh-keygen -t rsa` 一直回车执行后，可生成私钥 *id_rsa* 和 公钥 *id_rsa.pub*
>* 公钥一般在  **C:\Users\Administrator** 目录下 ，如果看不到.ssh文件，可以使用`ls -ah`指令查看隐藏文件夹即可 
>* 执行查看公钥的命令`cat ~/.ssh/id_rsa.pub` 


### 其它   

git branc 查看时如出现

>*  (HEAD detached at analytics_v2)   
>*  dev
>*  master

代表现在已经进入一个临时的HEAD，可以使用 `git checkout -b temp` 创建一个 temp branch，这样临时HEAD上修改的东西就不会被丢掉了。
然后切换到 dev 分支上，在使用 git branch merge temp，就可以把 temp 分支上的代码合并到 dev 上了。

<br>
### 详情Git使用指南
**小明--Git使用教程**
> [江湖人称---小明](http://itrain.top/2016/11/git_tutorial/)

