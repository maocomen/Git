[TOC]

# 集中式版本控制系统和分布式版本控制系统

集中式版本控制系统，版本库是集中存放在中央服务器的，工作的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，再进行工作。工作完了需要再推送到中央服务器。集中式版本控制系统必须联网才能工作。

分布式版本控制系统没有“中央服务器”，每个人的电脑上都是一个完整的版本库。工作的时候就不需要联网了，因为版本库就在自己的电脑上。多人协作的时候，我们只需要把自己的修改推送给对方就好了。某一个人的电脑坏掉了不要紧，随便从其他人那里复制一个就好了。而集中式版本控制系统的中央服务器要是出了问题，那么所有人都没办法工作了。

在实际使用分布式版本控制系统的时候，通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家一样可以干活，只是交换修改不方便而已。

# 几个基本概念

* 工作区

  我们开发的代码所在的目录，工程所在的目录。

* 暂存区

  当我们执行了 git add 操作之后，我们的修改就会从工作区放到暂存区。

* 版本区

  * 本地仓库

    当我们执行了 git commit 操作之后，就会将修改从暂存区提交到本地仓库。

  * 远程仓库

    当我们执行了 git push 操作之后，就会将本地仓库中的修改提交到远程仓库。

# 命令

## 创建仓库

* git init 

  创建 git 版本库

* git remote add `<remote-name>`  `<remote-url>`

  增加远程仓库

* git remote set-url `<remote-name>` `<remote-url>`

  修改远程仓库的url

* git branch -u `<remote-name>`/`<branch-name>`

  关联远程分支，下次推送到远程仓库直接 git push 就好了，不需要再次关联了

  git push -u `<remote-name>`/`<branch-name>`

  也可以在 push 的时候直接指定远程分支

* git clone `<remote-url>` `<path>`

  克隆到指定目录 也可以直接 cd 到指定目录下执行 git clone 操作

* git clone -b `<branch-name>` —single-branch `<remote-url>`

  克隆指定的某个分支

  ​

## 基本命令

* git add `<file-name>`

  将修改的文件放到暂存区

* git commit -m `<description>`

  将修改提交到本地仓库

* git push 

  将本地仓库的 commit 推送到远程仓库

* git rm `<file-name>`

  删除暂存区中的文件


## 分支

* git checkout `<branch-name>`

  切换分支

* git branch `<branch-name> <remote-branch-name>`

  创建一个关联到远程分支的本地分支 如果远程分支没有填，那么创建一个未关联远程分支的本地分支

* git checkout -b `<branch-name>`

  创建并切换分支

* git branch 

  查看本地分支 当前分支前会有个 * 号标识

* git branch -v

  查看本地分支的最后修改

* git branch -vv

  查看本地分支的最后修改和关联远程分支的情况

* git branch -r

  展示所有的远程分支 -r 代表 --remote

* git branch -a

  展示所有的分支，包括本地的和远程的 -a 代表 —all

* git branch -d `<local-branch-name>`

  删除本地分支

* git branch origin —delete `<remote-branch-name>`

  删除远程分支

  git branch origin :`<remote-branch-name>`

  也可以用这个命令删除远程分支

* git branch -m `<new-branch-name>`

  重命名本地分支

* git merge `<branch-name>`

  合并某分支到前挡分支

* git log —graph

  查看分支合并图

* ​




# 引用

[廖雪峰的官方网站|集中式vs分布式](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374027586935cf69c53637d8458c9aec27dd546a6cd6000)