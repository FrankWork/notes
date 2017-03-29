设置环境变量PATH

# 1、Ubuntu专有方式
编辑 /etc/ld.so.conf 文件，如果以下语句不存在，则加入：
include /etc/ld.so.conf.d/*.conf
然后在/etc/ld.so.conf.d下边新建一个以 .conf 结尾的文件。
在新建的 .conf 文件中写入需要设置的 path，例如：
~/mypath/bin

# 2、用户目录下的 .bashrc 文件 					#** 推荐用这个 **
在用户主目录下，有一个 .bashrc 文件，编辑该文件：
	$gedit ~/.bashrc
在最后边加入需要设置变量的shell语句，例如：
	export PATH=~/mypath/bin:$PATH
该文件编辑保存后，可立即在新打开的终端窗口内生效。
该方式添加的变量只能当前用户使用。

# 3、系统目录下的 profile 文件
在系统的 etc 目录下，有一个 profile 文件，编辑该文件：
	$sudo gedit /etc/profile
在最后边加入需要设置变量的shell语句，例如：
	export PATH=~/mypath/bin:$PATH
该文件编辑保存后，重启系统，变量生效。
该方式添加的变量对所有的用户都有效。

还有/etc/profile.d目录

# 4、系统目录下的 environment 文件 						# 这个里面定义PATH变量
在系统的 etc 目录下，有一个 environment 文件，编辑该文件：
	$sudo gedit /etc/environment
找到以下的 PATH 变量：
	PATH="<......>"
修改该 PATH 变量，在其中加入自己的path即可，例如：
	PATH="~/mypath/bin:<......>"
各个path之间用冒号分割。该文件也是重启生效，影响所有用户。
