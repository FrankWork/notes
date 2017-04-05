apt-cache search package 搜索软件包
apt-cache show package  获取包的相关信息，如说明、大小、版本等
sudo apt-get install package 安装包
sudo apt-get install package --reinstall   重新安装包
sudo apt-get -f install   修复安装
sudo apt-get remove package 删除包
sudo apt-get remove package --purge 删除包，包括配置文件等
sudo apt-get update  更新源
sudo apt-get upgrade 更新已安装的包
sudo apt-get dist-upgrade 升级系统
apt-cache depends package 了解使用该包依赖那些包
apt-cache rdepends package 查看该包被哪些包依赖
sudo apt-get build-dep package 安装相关的编译环境
apt-get source package  下载该包的源代码
sudo apt-get clean && sudo apt-get autoclean 清理无用的包
sudo apt-get autoremove 自动卸载
sudo apt-get check 检查是否有损坏的依赖

# 强制解锁
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock

# 编辑源：
sudo gedit /etc/apt/sources.list

## source.list 格式说明
例如：
deb     http://mirrors.163.com/debian/ wheezy                  main non-free contrib
deb     http://mirrors.163.com/debian/ wheezy-proposed-updates main non-free contrib
deb-src http://mirrors.163.com/debian/ wheezy                  main non-free contrib
deb-src http://mirrors.163.com/debian/ wheezy-proposed-updates main non-free contrib
其中可以把每一行分为四个部分：
deb	  ftp地址                            版本代号    限定词
deb	  http://mirrors.163.com/debian/    wheezy     main non-free contrib
（1）第一部分为deb或者deb-src，其中前者代表软件的位置，后者代表软件的源代码的位置
（2）第二部分为你的ftp镜像的url，
	/dists/ 目录包含"发行版"(distributions), 此处是获得 Debian 发布版本(releases)和已发布版本(pre-releases)的软件包的正规途径。
	/pool/ 目录为软件包的物理地址, 目录下按属性再分类("main", "contrib" 和 "non-free"), 分类下面再按源码包名称的首字母归档。
	/indices/:维护人员文件和重载文件.
	/project/:大部分为开发人员的资源
（3）第三部分表示你的debian版本号，可以查看dists/里的内容来填写，如 Trusty（14.04），Xenial（16.04）
（4）第四部分为dists/版本号/下的内容，
	main     		这些软件可以被自由地重新分发，并且被 Ubuntu 团队完全支持
	restricted		有些常用软件虽然没有一个完全的自由软件许可证，但是 Ubuntu 团队仍然支持它们。
	universe		几乎可以找到每一种开源软件，但是它们得不到安全补丁和支持

## sources.list的写法
	1)找到ftp主目录，把地址记下来，比如http://mirror.neu.edu.cn/ubuntu/
	2)打开dists，里面包含的目录名字，记下来。xenial,xenial-backports, xenial-security xenial-updates
	3)打开pool目录，看看里面包含哪些组件目录，比如main、multiverse、restricted,universe
	4)书写格式：deb <1记下来的地址> <2记下来的目录名> <3记下来的名字>， 如：
		deb http://mirrors.163.com/debian wheezy man contrib non-free 
		
		deb http://mirror.neu.edu.cn/ubuntu/ xenial main multiverse restricted universe
		deb http://mirror.neu.edu.cn/ubuntu/ xenial-backports main multiverse restricted universe
		deb http://mirror.neu.edu.cn/ubuntu/ xenial-security main multiverse restricted universe
		deb http://mirror.neu.edu.cn/ubuntu/ xenial-updates main multiverse restricted universe
# 更新软件

## 更新软件源
sudo apt-get update
## 更新软件
sudo apt-get install 软件名
