#查看自己的进程：
	ps -x

#杀死进程：
	kill pid	

#查看占用某个端口的进程
	netstat -anp | grep 8080
	
# show active process

	$ ps -ef
运行的进程：
   53 ?        00:00:00 md
  966 ?        00:00:08 mongod
 1043 ?        00:00:00 mysqld_safe
 1400 ?        00:00:01 mysqld
 1463 ?        00:00:00 php5-fpm
 1466 ?        00:00:00 php5-fpm
 1467 ?        00:00:00 php5-fpm
 2011 ?        00:00:00 nginx
 2012 ?        00:00:00 nginx
 2013 ?        00:00:00 nginx
 2014 ?        00:00:00 nginx
 2015 ?        00:00:00 nginx
 
# To see every process running as root (real & effective ID) in user format:
          ps -U root -u root u

	
	
