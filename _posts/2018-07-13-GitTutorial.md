---
layout: post
title: "Git教程"
date: 2018-07-13   
tag: 工具 
---

### 介绍       

　　Git是做项目的版本管理，你也可以称它们为版本管理工具。假如现在你有一个文件夹，里面可以是项目，也可以是你的个人笔记(如我这个博客)，或者是你的简历、毕业设计等等，都可以使用git来管理。

　　目前常用的版本控制器有Git和SVN，即使这两个你没有全用过，至少也会听过，我这里以Git为例，个人比较喜欢Git，你也可以看看这篇文章：[为什么Git比SVN好](http://www.worldhello.net/2012/04/12/why-git-is-better-than-svn.html)。我使用的是Mac，Mac上没自带Git环境，但是作为iOS开发者，我安装Xcode的时候，Xcode里是有自带Git的，所以我不需要考虑怎么去安装Git了。          

### 简介说明

![GIT主要概念及工作流程图](/images/posts/tmp/GIT主要概念及工作流程图.png)

> - Remote：远程仓库
> - Repository：本地仓库
> - Index / Stage：暂存区
> - Workspace：工作区

![GIT主要概念及工作流程图](/images/posts/tmp/GIT协作开发1.png)

![GIT主要概念及工作流程图](/images/posts/tmp/GIT协作开发2.png)

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

>* 执行  `cd ~/.ssh ` `ls`查看是否已配置SSH（是否已经存在 id_rsa.pub 或 id_dsa.pub 文件，可删除后，重新生成新的密钥）
>
>* 执行 `ssh-keygen -t rsa` 一直回车执行后，可生成私钥 *id_rsa* 和 公钥 *id_rsa.pub*
>
>* 公钥一般在  **C:\Users\Administrator** 目录下 ，如果看不到.ssh文件，可以使用`ls -ah`指令查看隐藏文件夹即可 
>
>* 执行查看公钥的命令`cat ~/.ssh/id_rsa.pub` 
>
>* 添加 `SSH key` 到 `github` 上（首先copy `id_rsa.pub`文件内容）
>
>* 登录你的 `github` 账号，右上角进入 `setting - Account settings` ，选择 `SSH and GPG keys` 
>
>* 点击 Add SSH key 按钮添加一个 SSH key 。把你复制的 SSH key 代码粘贴到 key 所对应的输入框中
>
>* ### 测试一下该SSH key
>
>* ```shell
>  $ ssh -T git@github.com
>  $ yes
>  $ 输入密码
>  ```
>
>  

### 命令大全

> - `git clone <远程仓库的网址>` 【默认在当前目录下从远程仓库克隆一个版本库到本地】
>
>   ```shell
>   $ git clone <远程仓库的网址> <本地目录>
>   
>   # -b 指定要克隆的分支，默认master分支
>   $ git clone <远程仓库的网址> -b <分支名称> <本地目录>
>   ```
>
> - `git init` 【初始化本地仓库，在当前目录下生成 **.git** 文件夹】
>
>   
>
> - `git status` 【查看本地仓库的状态】
>
>   
>
> - `git remote` 【操作远程库】
>
>   ```shell
>   # 列出远程仓库的详细信息，别名后展示URL地址
>   $ git remote -v
>   
>   # 添加远程仓库：别名默认origin
>   $ git remote add <远程仓库的别名> <远程仓库的URL地址>
>   
>   # 修改远程仓库的别名
>   $ git remote rename <原远程仓库的别名> <新的别名>
>   
>   # 删除指定名称的远程仓库
>   $ git remote remove <远程仓库的别名>
>   
>   # 修改远程仓库的URL地址
>   $ git remote set-url <远程仓库的别名> <新的远程仓库URL地址>
>   ```
>
>   
>
> - `git branch`【操作GIT的分支命令】
>
>   ```shell
>   # 列出本地的所有分支，当前所在分支以“*” 标出
>   $ git branch
>   
>   # 列出本地的所有分支并显示最后一次提交，当前所在分支以“*” 标出
>   $ git branch -v
>   
>   # 创建新分支，新的分支基于上一次提交建立
>   $ git branch <分支名>
>   
>   # 修改分支名称，如不指定原分支名称则为当前所在分支
>   $ git branch -m [<原分支名>] <新的分支名>
>   
>   # 强制修改分支名称
>   $ git branch -M [<原分支名>] <新的分支名>
>   
>   # 删除指定的本地分支
>   $ git branch -d <分支名>
>   
>   # 强制删除指定的本地分支
>   $ git branch -D <分支名>
>   ```
>
> - `git checkout` 【检出命令，用于创建、切换分支等】
>
>   ```shell
>   # 切换到已存在的指定分支
>   $ git checkout <分支名>
>   
>   # 创建并切换到指定的分支，保留所有提交记录，等同【git branch 和 git checkout】
>   $ git checkout -b <分支名>
>   
>   # 创建并切换到指定的分支，删除所有的提交记录
>   $ git checkout --orphan <分支名>
>   
>   # 替换掉本地的改动，新增的文件和已经添加到暂存区的内容不受影响
>   $ git checkout <文件路径>
>   ```
>
> - `git cherry-pick` 【把已经提交的记录合并到当前分支】
>
>   ```shell
>   # 把已经提交的记录合并到当前分支
>   $ git cherry-pick <commit ID>
>   ```
>
> - `git add` 【把要提交的文件的信息添加到暂存区中】
>
>   ```shell
>   # 把指定的文件添加到暂存区中
>   $ git add <文件路径>
>   
>   # 添加所有修改、已删除的文件到暂存区中
>   $ git add -u [<文件路径>]
>   $ git add --update [<文件路径>]
>   
>   # 添加所有修改、已删除、新增的文件到暂存区中，省略<文件路径>即为当前目录
>   $ git add -A [<文件路径>]
>   $ git add --all [<文件路径>]
>   
>   # 查看所有修改、已删除但没有提交的文件，进入一个子命令系统
>   $ git add -i [<文件路径>]
>   $ git add --interactive [<文件路径>]
>   ```
>
> - `git commit` 【将暂存区中的文件提交到本地仓库中】
>
>   ```shell
>   # 把暂存区中的文件提交到本地仓库，调用文本编辑器输入该次提交的描述信息
>   $ git commit
>   
>   # 把暂存区中的文件提交到本地仓库中并添加描述信息
>   $ git commit -m "描述信息"
>   
>   # 把所有修改、已删除的文件提交到本地仓库中[不包括未被版本库跟踪的文件，等同先调用git add -u]
>   $ git commit -a -m "描述信息"
>   
>   # 修改上次提交的描述信息
>   $ git commit --amend
>   ```
>
> - `git fetch` 【从远程仓库获取最新的版本到本地的tmp分支上】
>
>   ```shell
>   # 将远程仓库所有分支的最新版本全部拉取回本地
>   $ git fetch <远程仓库的别名>
>   
>   # 将远程仓库指定分支的最新版本拉取回本地
>   $ git fetch <远程主机名> <分支名>
>   ```
>
> - `git merge` 【合并分支】
>
>   ```shell
>   # 把指定的分支合并到当前所在的分支下
>   $ git merge <分支名>
>   ```
>
> - `git diff` 【比较版本之间的差异】
>
>   ```shell
>   # 比较当前文件和暂存区中文件的差异，显示没有暂存起来的更改
>   $ git diff
>   
>   # 比较暂存区中的文件和上次提交时的差异
>   $ git diff --cached
>   $ git diff --staged
>   
>   # 比较当前文件和上次提交时的差异
>   $ git diff HEAD
>   
>   # 查看从指定的版本之后改动的内容
>   $ git diff <commit ID>
>   
>   # 比较两个分支之间的差异
>   $ git diff <分支名> <分支名>
>   
>   # 查看两个分支分开后各自的改动内容
>   $ git diff <分支名>...<分支名>
>   ```
>
> - `git pull` 【从远程仓库获取最新版本并合并到本地（首先执行 `git fetch`，然后执行 `git merge`，把获取的分支的HEAD合并到当前分支）】
>
>   ```shell
>   # 从远程仓库获取最新版本
>   $ git pull
>   ```
>
> - `git push` 【把本地仓库的提交推送到远程仓库】
>
>   ```shell
>   # 把本地仓库的分支推送到远程仓库的指定分支
>   $ git push <远程仓库的别名> <本地分支名>:<远程分支名>
>   
>   # 删除指定的远程仓库的分支
>   $ git push <远程仓库的别名>:<远程分支名>
>   $ git push <远程仓库的别名> --delete <远程分支名>
>   ```
>
> - `git log` 【显示提交的记录】
>
>   ```shell
>   # 打印所有的提交记录
>   $ git log
>   
>   # 打印从第一提交到指定的提交的记录
>   $ git log <commit ID>
>   
>   # 打印指定数量的最新提交的记录
>   $ git log -<指定的数量>
>   ```
>
> - `git reset` 【还原提交记录】
>
>   ```shell
>   # 重置暂存区，但文件不受影响
>   # 相当于将用 git add 命令更新到暂存区的内容撤出暂存区，可以指定文件
>   # 没有指定 commit ID 则默认为当前 HEAD
>   $ git reset [<文件路径>]
>   $ git reset --mixed [<文件路径>]
>   
>   # 将 HEAD 的指向改变，撤销到指定的提交记录，文件未修改
>   $ git reset <commit ID>
>   $ git reset --mixed <commit ID>
>   
>   # 将 HEAD 的指向改变，撤销到指定的提交记录，文件未修改
>   # 相当于调用 git reset --mixed 命令后又做了一次 git add
>   $ git reset --soft <commit ID>
>   
>   # 将 HEAD 的指向改变，撤销到指定的提交记录，文件也修改了
>   $ git reset --hard <commit ID>
>   ```
>
> - `git revert` 【生成一个新的提交来撤销某次提交，此次提交之前的所有提交都会被保留】
>
>   ```shell
>   # 生成一个新的提交来撤销某次提交
>   $ git revert <commit ID>
>   ```
>
> - `git tag` 【操作标签的命令】
>
>   ```shell
>   # 打印所有的标签
>   $ git tag
>   
>   # 添加轻量标签，指向提交对象的引用，可以指定之前的提交记录
>   $ git tag <标签名称> [<commit ID>]
>   
>   # 添加带有描述信息的附注标签，可以指定之前的提交记录
>   $ git tag -a <标签名称> -m <标签描述信息> [<commit ID>]
>   
>   # 切换到指定的标签
>   $ git checkout <标签名称>
>   
>   # 查看标签的信息
>   $ git show <标签名称>
>   
>   # 删除指定的标签
>   $ git tag -d <标签名称>
>   
>   # 将指定的标签提交到远程仓库
>   $ git push <远程仓库的别名> <标签名称>
>   
>   # 将本地所有的标签全部提交到远程仓库
>   $ git push <远程仓库的别名> -tags
>   ```
>
> - `git mv` 【重命名文件或者文件夹】
>
>   ```shell
>   # 重命名指定的文件或文件夹
>   $ git mv <源文件/文件夹> <目标文件/文件夹>
>   ```
>
> - `git rm` 【删除文件或者文件夹】
>
>   ```shell
>   # 移除跟踪指定的文件，并从本地仓库的文件夹中删除
>   $ git rm <文件路径>
>   
>   # 移除跟踪指定的文件夹，并从本地仓库的文件夹中删除
>   $ git rm -r <文件夹路径>
>   
>   # 移除跟踪指定的文件，在本地仓库的文件夹中保留该文件
>   $ git rm --cached
>   ```

### 实战场景

1、配置SSH密钥，避免每次提交代码都要输入用户名/密码

```shell
# 查看当前 clone 地址
$ git remote -v

# 如果是https方式，需要移除，并换成ssh方式
$ git remote rm origin

# 添加新的 git 方式【ssh方式，github上赋值SSH方式的仓库地址】
$ git remote add origin <git地址>

# 查看 push 方式是否修改成功
$ git remote -v

# 重新push一下
$ git push origin master
```

2、撤销与恢复

```shell
# 恢复暂存区的指定文件到工作区
$ git checkout [file]

# 恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]

# 恢复暂存区的所有文件到工作区
$ git checkout .

# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]

# 重置暂存区与工作区，与上一次commit保持一致
$ git reset --hard

# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
$ git reset [commit]

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]

# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]

# 新建一个commit，用来撤销指定commit
# 后者的所有变化都将被前者抵消，并且应用到当前分支
$ git revert [commit]

# 暂时将未提交的变化移除，稍后再移入
$ git stash
$ git stash pop
```

3、远程同步

```shell
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

4、保存和恢复工作进度（git stash）

注：<u>stash只能保存处于git下的文件，未add到git的文件无法生效</u>

```shell
# 保存当前工作进度，将工作区和暂存区恢复到修改之前
$ git stash

# 同上，message为此次进度保存的说明
$ git stash save <message>

# 显示保存的工作进度列表，编号越小代表保存进度的时间越近
$ git stash list

# 恢复工作进度到工作区，其中stash@{num}是可选项，在多个工作进度中可选择恢复，默认恢复最近的一次进度，相当于 stash@{0}
$ git stash pop stash@{num}

# 恢复工作进度到工作区且可重复恢复，其中stash@{num}是可选项，在多个工作进度中可选择恢复，默认恢复最近的一次进度，相当于 stash@{0}
$ git stash apply stash@{num}

# 删除指定的工作进度，其中stash@{num}是可选项，在多个工作进度中可选择删除，默认删除最近的一次进度，相当于 stash@{0}
$ git stash drop stash@{num}

# 删除所有保存的工作进度
$ git stash clear
```





