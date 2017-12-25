# Getting Started(Git Pro)
## 安装git on Server
	you@server: $ sudo yum install git
### Then add a user for Git.
	you@server: $ sudo useradd git
	you@server: $ passwd git
### First create ssh keys on your local machine:
	you@local: $ ssh-keygen -t rsa
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

# 创建分支
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

`git pull origin other-branch` is equal to `git fetch origin other-branch && git merge other-branch`

# Fork and Syncing a fork

```bash
$ git fetch upstream
$ git checkout master
$ git merge upstream/master
$ git push origin master
```


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
