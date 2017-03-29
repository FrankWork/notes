1. download wordpress
	https://cn.wordpress.org/wordpress-4.4.2-zh_CN.tar.gz
2. sudo cp wordpress-*-zh_CN.tar.gz /usr/share/nginx/html/wordpress-*-zh_CN.tar.gz
3. sudo tar xvzf  wordpress-*-zh_CN.tar.gz 
4. sudo rm wordpress-4.4.2-zh_CN.tar.gz
5. 浏览http://localhost/wordpress/readme.html
6. 必要信息
	数据库名：wordpress
	用户名：root
	密码：
	数据库主机：localhost
	表前缀：wp_

我们能够连接到数据库服务器（这意味着您的用户名和密码正确），
但未能选择$s数据库。

您确定它存在吗？
用户root有权限使用数据库wordpress吗？
在部分系统中您的数据库名称前缀是您的用户名，如是username_wordpress。
可能是这种问题吗？

7. mysql新建数据库

$ mysql -u root -p
$ sudo vim create_database.sql
$ source /usr/share/nginx/html/wordpress/create_database.sql

这意味着您在wp-config.php文件中指定的用户名和密码信息不正确，或我们未能在
localhost联系到数据库服务器。这可能意味着您主机的数据库服务器未在运行。

注意：密码不正确

抱歉，我不能写入wp-config.php文件。

注意：没有写入权限
sudo vim wp-config.php

8 安装
站点名称：Hackerhub
用户名：frank
密码： ^hv%!Lo0U4i#Y!mw9P
邮箱：lzh00776@163.com


自定义模板
	1 打开网页，选择“外观”，点击“编辑”
	2 在右侧找到自己需要编辑的模块

forbidden Google fonts
	on wordpress site ,打开主题 functions.php文件。找到 ‘Register Google 
	fonts’字样, edit it and save.
	Note: I dit NOT change it.

forbidden Gravatar img
	on your wordpress site, click 'settings', click 'discuss', disable 
	'show images'.
