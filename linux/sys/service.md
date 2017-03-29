# Systemd
(http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html)
$ systemctl --version

$ sudo systemctl reboot# 重启系统
$ sudo systemctl poweroff# 关闭系统，切断电源
$ sudo systemctl halt# CPU停止工作
$ sudo systemctl suspend# 暂停系统
$ sudo systemctl hibernate# 让系统进入冬眠状态
$ sudo systemctl hybrid-sleep# 让系统进入交互式休眠状态
$ sudo systemctl rescue# 启动进入救援状态（单用户状态）

$ systemd-analyze# 查看启动耗时
$ systemd-analyze blame# 查看每个服务的启动耗时
$ systemd-analyze critical-chain# 显示瀑布状的启动过程流
$ systemd-analyze critical-chain atd.service# 显示指定服务的启动流

$ sudo systemctl enable docker # start on boot
$ sudo systemctl disable docker
$ sudo systemctl start docker
$ sudo systemctl stop docker
$ sudo systemctl restart docker






## chkconfig ###################

chkconfig命令主要用来更新（启动或停止）和查询系统服务的运行级信息。但chkconfig不会立即自动禁止或激活一个服务，需要服务器重启才生效。

chkconfig --list

	httpd 0:关闭 1:关闭 2:关闭 3:关闭 4:关闭 5:启用 6:关闭
	bluetooth 0:关闭 1:关闭 2:关闭 3:关闭 4:关闭 5:关闭 6:关闭
	

#让httpd 在机器启动的时候在运行级别上停止

	[root]# chkconfig --level 345 httpd off
	[root]# chkconfig --list |grep httpd
	httpd 0:关闭 1:关闭 2:关闭 3:关闭 4:关闭 5:关闭 6:关闭
	
	php5-fpm  nginx postgresql mongodb mysql redis-server

#让httpd 在机器启动的时候在运行级别上启动

	[root]# chkconfig --level 345 httpd on
	[root]# chkconfig --list |grep httpd
	httpd 0:关闭 1:关闭 2:关闭 3:启用 4:启用 5:启用 6:关闭







#Note: 在Ubuntu中是没有chkconfig命令的，可以用update-rc.d 来代替。

1、删除一个服务
	update-rc.d -f apache2 remove
	
	已执行的命令：
	sudo update-rc.d -f mongodb remove
	sudo update-rc.d -f mysql remove
	sudo update-rc.d -f nginx remove
	sudo update-rc.d -f php5-fpm remove
	sudo update-rc.d -f redis-server remove
	
参数-f是强制删除符号链接，即使/etc/init.d/apache2仍然存在。 
Note：这个命令仅仅禁止该服务，直到该服务被升级。如果你想在服务升级后仍然保持被禁用。应该执行如下的命令：
	update-rc.d apache2 stop 80 0 1 2 3 4 5 6 .
	
2、增加一个服务
如果你想重新添加这个服务并让它开机自动执行，你需要执行以下命令： 
	update-rc.d apache2 defaults
	
	已执行的命令：
	sudo update-rc.d nginx defaults
	sudo update-rc.d php5-fpm defaults
	sudo update-rc.d mongodb defaults
	
并且可以指定该服务的启动顺序：
	update-rc.d apache2 defaults 90
还可以更详细的控制start与kill顺序：
	update-rc.d apache2 defaults 20 80
其中前面的20是start时的运行顺序级别，80为kill时的级别。也可以写成：
	update-rc.d apache2 start 20 2 3 4 5 . stop 80 0 1 6 .
其中0～6为运行级别。 





## service #####################

#停止 HTTPD服务

	[root etc]# service httpd stop
	停止 httpd：[ 确定 ]
	
	sudo service php5-fpm stop
	sudo service nginx stop
	sudo service mongodb stop
	sudo service mysql stop
	sudo service redis-server stop
	sudo service vsftpd stop
	      

#启动httpd服务

	[root]# service httpd start
	启动 httpd：[ 确定 ]
	
	sudo service nginx start
	sudo service php5-fpm start
	sudo service vsftpd start
	
#重起HTTD服务

	[root]# service httpd restart
	停止 httpd：[ 确定 ]
	启动 httpd：[ 确定 ]

查看httpd服务的运行状态

	service httpd status

service --status-all


## 查看运行中的程序 #######################
	$ ps -ef 


## 启动脚本 ############################

	$ ls /etc/init.d/
      php5-fpm  nginx postgresql mongodb mysql redis-server
                
	$ ls /etc/rc.d/init.d/
ls: 无法访问/etc/rc.d/init.d/: 没有那个文件或目录


	





##Linux 运行级别 ####################

0 为停机，机器关闭。（千万不要把initdefault设置为0 ）  
1 为单用户模式，就像Win9x下的安全模式类似。  
2 为多用户模式，但是没有NFS支持。  
3 为完整的多用户模式，是标准的运行级。  
4 一般不用，在一些特殊情况下可以用它来做一些事情。例如在笔记本电脑的电池用尽时，可以切换到这个模式来做一些设置。  
5 就是X11，进到X Window系统了。  
6 为重启，运行init 6机器就会重启。（千万不要把initdefault设置为6 ） 

使用以下命令，可以查看当前的运行级别：
	runlevel显示上次的运行级别和当前的运行级别，“N”表示没有上次的运行级别。
使用以下命令，可以切换运行级别：
	init [123456]  
例如，init 0表示关机，init 6表示重启。

