# Getting Started(Git Pro)
## 安装git on Server
	you@server: $ sudo yum install git
### Then add a user for Git.
	you@server: $ sudo useradd git
	you@server: $ passwd git
### First create ssh keys on your local machine:
	you@local: $ ssh-keygen -t rsa -C your-email
### copy these keys to the server
	you@local: $ cat ~/.ssh/id_rsa.pub | ssh git@remote-server "mkdir -p ~/.ssh && cat >>  ~/.ssh/authorized_keys"
	           $chmod 700 ~/.ssh
	           $chmod 600 ~/.ssh/authorized_keys
    git@server: $ chmod 700 .ssh
    git@server: $ chmod 600 .ssh/authorized_keys
### set up a remote repository
	git@server: $ mkdir ~/command-note.git
	git@server: $ cd ~/command-note.git
	git@server: $ git init --bare
### Then Setup a Local Repository
	you@local: $ git remote set-url origin git@e.com:/home/git/my-project.git
	you@local: $ git remote set-url origin ssh://git@e.com:port/home/git/my-project.git
	or
	you@local: $ git init && git remote add origin git@e.com:/home/git/my-project.git
	you@local: $ git push origin master
	
## 安装git和ssh on PC:
	sudo apt-get install git
	sudo apt-get install ssh
## 配置文件
```bash
	~/.gitconfig
```

## git设置Identity：
	git config --global user.name FrankWork
	git config --global user.email lzh00776@163.com

## Check Your Settings
	git config --list
	git config user.name

## Your Editor
	git config --global core.editor gedit

## Getting Help
	git help <verb>
	git <verb> --help
	man git-<verb>
	
	git help add
	
# Git Basics

## Getting a Git Repository

### Initializing a Repository in an Existing Directory
	git init

### Initial commit
	git add *.c
	git add LICENSE
	git commit -m 'initial project version'

### Cloning an Existing Repository
	git clone https://github.com/libgit2/libgit2
	git clone https://github.com/libgit2/libgit2 <another-name>

## Recording Changes to the Repository

### Checking the Status of Your Files
	git status

### Tracking New Files
	git add README
### Staging Modified Files
	git add README(modified)
### Ignoring Files
	$ cat .gitignore
	*.[oa]
	*~
### diff
	git diff
	git diff --staged
	git diff --cached
### Committing Your Changes
	git commit
	git commit -m "Story 182: Fix benchmarks for speed"
### Viewing the Commit History
	git log
		
## 列出文件
	git ls-files
## Git远程更新
$ git remote -v
origin	https://github.com/dmlc/mxnet.git (fetch)
origin	https://github.com/dmlc/mxnet.git (push)
$ git fetch origin master
$ git fetch --recurse-submodules origin master
从远程的origin仓库的master分支下载代码到本地的origin master


创建SSH Key
	ssh-keygen -t rsa -C "youremail@example.com"
	登陆GitHub，打开“Account settings”，“SSH Keys”页面,然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴.ssh目录里id_rsa.pub文件的内容
远程库克隆
	git clone git@github.com:FrankWork/LeetCode.git
提交
	git add readme.txt
	git commit -m "append GPL"
列出远程分支
	git remote
	git remote -v | --verbose 列出详细信息
推送
	git push -u origin master第一次推送master分支的所有内容；
	git push origin master推送最新修改；

## git log

git log --pretty=oneline --graph
git log --abbrev-commit --pretty=oneline --graph

# 本地master与远程master同步
git pull --rebase



## 创建分支
创建并切换到新分支
$ git checkout -b iss53
这相当于执行下面这两条命令：
$ git branch iss53
$ git checkout iss53
合并分支
$ git checkout master
$ git merge iss53
删掉已经合并的分支
$ git branch -d iss53
$ git push origin --delete <branch_name>
sha: ceea27c51d624e692aeb236c9ba1eb01d59d20cb
https://github.com/FrankWork/LeetCode.git
远程获取多个分支
$ git branch -r
  origin/baseline
  origin/master
$ git checkout baseline
更新到分支
git push origin [branch-name]:refs/for/[branch-name]

把master内容更新到分支
#git checkout master
#git fetch upstream
#
#git checkout branch-1
#git merge master 合并master到分支(当前分支与master同步)
#git push....



`git pull origin other-branch` is equal to `git fetch origin other-branch && git merge other-branch`

# Fork and Syncing a fork

```bash
$ git remote -v
$ git remote add upstream https://github.com/tensorflow/tensorflow.git
$ git fetch upstream
$ git checkout master
$ git merge upstream/master
$ git push origin master
```

## 代码撤销、回滚

撤销：未进行git push前的所有操作，都是在“本地仓库”中执行的。我们暂且将“本地仓库”的代码还原操作叫做“撤销”
回滚: 已进行git push，即已推送到“远程仓库”中。我们将已被提交到“远程仓库”的代码还原操作叫做“回滚”

git reset、git checkout和git revert
git stash: 代码写了一部分，需要切换到另一分支，但不想为当前工作创建一次提交
git commit --amend 修改最后一次提交

HEAD	上一次提交的快照，下一次提交的父结点
Index	预期的下一次提交的快照–“暂存区域”，运行git add后，代码就进入“暂存区域”
Working Directory	沙盒

重置

将当前的分支重设（reset）到指定的<commit>或者HEAD（默认是HEAD，即最新的一次提交），并且根据[mode]有可能更新index和working directory（默认是mixed）

git reset [--hard|soft|mixed|merge|keep] [commit|HEAD]
 
 –hard：重设index和working directory，从<commit>以来在working directory中的任何改变都被丢弃，并把HEAD指向<commit>。彻底回退到某个版本，本地的源码也会变为上一个版本的内容。 

 –soft：index和working directory中的内容不作任何改变，仅仅把HEAD指向<commit>。自从<commit>以来的所有改变都会显示在git status的“Changes to be committed”中。回退到某个版本，只回退了commit的信息。如果还要提交，直接commit即可。

–mixed：仅重设index，但是不重设working directory。这个模式是默认模式，即当不显示告知git reset模式时，会使用mixed模式。这个模式的效果是，working directory中文件的修改都会被保留，不会丢弃，但是也不会被标记成“Changes to be committed”，但是会打出什么还未被更新的报告

回退add操作
	$ git add test
	$ git reset HEAD test
回退最后一次提交
	$ git add test
	$ git commit -m"Add test"
	$ git reset --soft HEAD^
回退最近几次提交，并把这几次提交放到新分支上
	$ git branch topic #已当前分支为基础，新建分支topic
	$ git reset --hard HEAD~2 #在当前分支上回滚提交
	$ git checkout topic
	说明：通过临时分支来保留提交，然后在当前分支上做硬回滚。 
将本地的状态回退到和远程一样
	$ git reset --hard origin/devlop
回退到某个版本提交
	$ git reset 497e350
	497e350为某commitID。当前HEAD会指向497e350，在497e350其之后提交的内容会被回退到初始状态。 
要想在develop分支，但错误地提交到了maser分支
	git checkout master
	git add .
	git commit -m"..."
	git reset --mixed HEAD~1
	git stash
	git checkout develop
	git stash pop

# 撤销branch合并

$ git log
commit 885ecaff2132c42008f4703766aceed2dd8715c4
Date:   Tue May 9 09:59:19 2017 +0800

    embeddings

commit aa5592ab474962da40b5266cf3ee6befebfd8c64
Merge: d4065f2 ac0e432
Date:   Tue May 9 09:54:56 2017 +0800

    merge baseline

commit d4065f2672cc542b0d21ce144dcb9e1929544ea3
Date:   Mon May 8 23:48:12 2017 +0800

    readme

$ git reset d4065f2672cc542b0d21ce144dcb9e1929544ea3
$ git checkout *.py
$ git add.. && git commit ..
$ git push -f origin master远程库克隆


## read src

$ git checkout -b read-src
$ git log --reverse
$ git revert 388c115956a06267aeb71b24e467dafd3d968931 # to init commit


# 例子 
$ cd '/home/frank/work/Coursera/Machine Learning'
$ git init
初始化空的 Git 仓库于 /home/frank/work/Coursera/Machine Learning/.git/
$ gedit .gitignore
*~
token
token.mat
lib/
$ git add -A
 git commit -m "Programming exercies of Andrew Ng's Machine Learning"
[master （根提交） bbc81b2] Programming exercies of Andrew Ng's Machine Learning
 165 files changed, 11123 insertions(+)
$ git rm K_means_Image_Compress/ -r -f
rm 'K_means_Image_Compress/README.md'
...
$ git commit -m "rm private dir"
[master a4281ed] rm private dir
 23 files changed, 368 deletions(-)
$ git branch -a
* master
$ git log
commit a4281ed9d52408e8058bed069979ce5ad8eba0e2
Author: FrankWork <lzh00776@163.com>
Date:   Sat Dec 17 21:08:54 2016 +0800

    rm private dir

commit bbc81b2cd073294333f962c86d8e5e63b32191ef
Author: FrankWork <lzh00776@163.com>
Date:   Sat Dec 17 21:02:41 2016 +0800

    Programming exercies of Andrew Ng's Machine Learning
$ git status
位于分支 master
无文件要提交，干净的工作区
$ git diff
$ git remote add origin https://github.com/FrankWork/CourseraMachineLearning.git
$ git push -u origin master
Username for 'https://github.com': FrankWork
Password for 'https://FrankWork@github.com': 
对象计数中: 166, 完成.
Delta compression using up to 4 threads.
压缩对象中: 100% (165/165), 完成.
写入对象中: 100% (166/166), 22.01 MiB | 3.74 MiB/s, 完成.
Total 166 (delta 8), reused 0 (delta 0)
remote: Resolving deltas: 100% (8/8), done.
To https://github.com/FrankWork/CourseraMachineLearning.git
 * [new branch]      master -> master
分支 master 设置为跟踪来自 origin 的远程分支 master。

参考资料：
	http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
	http://www.git-scm.com/doc
