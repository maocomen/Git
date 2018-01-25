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

* git remote

  列出所有的远程仓库

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

* git fetch

  本地远程分支的记录更新到最新的版本，但是本地当前分支代码并不与远程分支做合并

* git pull

  将当前分支的代码与远程分支的代码进行合并，类似于 git fetch 之后再做一次 git merge

* ​


## 分支

* git checkout `<branch-name>`

  切换分支

* git branch `<branch-name> <remote-branch-name>`

  创建一个关联到远程分支的本地分支 如果远程分支没有填，那么创建一个未关联远程分支的本地分支

* git checkout -b `<branch-name>`

  创建并切换分支

* git checkout -b `<branch-name>` `<remote-branch-name>`

  创建并切换到一个已经关联到远程分支的本地分支

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

  合并某分支到当前分支

* git log —graph

  查看分支合并图




## 标签

* git checkout  `<tag-name>`

  切换标签

* git checkout -b `<branch-name>` `<tag-name>`

  切换到本地标签，并创建一个对应的分支。

* git tag `<tag-name>` `<commit-id>`

  对指定的 commit 创建一个标签，如果 commit-id 没有指定，那么对当前最新的 commit 创建一个标签

* git tag -a `<tag-name>`  -m `<description>`  `<commit-id>`

  对指定的 commit 创建一个标签，如果 commit-id 没有指定，那么对当前最新的 commit 创建一个标签。

* git tag

  查看所有的标签

* git show `<tag-name>`

  展示某个 tag 的详细信息

* git tag -s `<tag-name>` -m `<description>` `<commit-id>`

  对指定的 commit 创建一个标签，并进行签名。如果 commit-id 没有指定，那么对当前最新的 commit 创建一个标签。

  签名采用PGP签名，因此，必须首先安装 GPG（GnuPG），如果没有找到 GPG，或者没有 GPG 密钥对，就会报错

* git tag -d `<tag-name>`

  删除标签

* git push `<remote-name>` `<tag-name>`

  将本地标签推送到远程服务器

* git push `<remote-name>` —tags

  将本地未推送到远程服务器的标签一次性全部推送到远程服务器

* git push `<remote-name>` :refs/tags/`<tag-name>`

  删除远程服务器的标签 例如: git push origin :refs/tags/v0.9 删除远程服务器上名为 v0.9 的标签。

  要删除远程服务器的标签，必须先删除本地的标签。

* git describe 

  显示离当前提交最近的标签 只显示注释标签

  V2.1-1-gf1a3f0b

  V2.1 是标签名称，后面的 1 是打标签后有多少次提交，g代表 git ，后面的是 commit id。

* git describe —tags

  显示离当前提交最近的标签

  ​

## 存储

* git stash

  将当前工作区的修改保存起来。

* git stash list

  查看所有的 stash。

* git stash pop stash@{`number`}

  回到某一个 stash 的状态，并删除这个 stash。如果不加 stash 编号，默认回到最后一个 stash。

* git stash drop stash@{`number`}

  丢弃某一个 stash。如果不加 stash 编号，默认丢弃最后一个 stash。

* git stash apply stash@{`number`}

  回到某个 stash 的状态。该命令并不会删除该 stash ，需要我们手动清除。如果不加 stash 编号，默认回到最后一个 stash。

* git stash save `<description>`

  添加 stash 的时候加上描述。

* git stash -u

  添加一个 stash。包括新建的，未在版本库索引中的文件。

* git stash clear

  删除所有的 stash



## 其他

- git diff

  输出工作区和暂存区的不同

- git diff —cached

  输出暂存区和本地最近的版本( commit )的不同

- git diff HEAD

  输入工作区、暂存区与本地最近的版本( commit )的不同

- git checkout `<file_name>`

  放弃工作区某个文件的修改

- git checkout .

  放弃工作区的全部修改

- git revert `<commit-id>` 

  工作区回到某个 commit 上个 commit 时候的内容，并新加一个 commit 。

- git reset `<commit-id>` 

  版本库完全回退到某个 commit 时候的内容，并与当前工作区的修改进行合并。

- git commit —amend

  修改当前最新的 commit 的描述。会进入到一个 vim 编辑界面。

- git commit --amend —author='`Author Name <email@address.com>`'

  修改作者名

- git log

  查看提交历史

- git reflog

  查看本地执行过的 git 命令。

- git whatchanged —since='`<time horizon>`'

  查看指定时间范围内的提交记录 时间范围可以是 2 weeks ago，1 day ago ，2 months ago，2 years ago 等

- git cherry-pick `<commit-id>`

  将别的分支的 commit 提交到当前分支

- git config --global alias.`<handle>` `<command>`

  给 git 命令起别名

  我们可以使用 git confit —global alias.st status 来给 status 命令起一个叫 st 的别名，那么我们以后就可以把 git status 命令简写为 git st。

# 引用

[廖雪峰的官方网站|集中式vs分布式](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374027586935cf69c53637d8458c9aec27dd546a6cd6000)

[Git的奇技淫巧🙈](https://www.cnblogs.com/xueweihan/p/5703144.html)