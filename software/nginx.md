 $sudo apt-get install nginx
      Nginx的版本是1.2.1
      ubuntu安装Nginx之后的文件结构大致为：
      所有的配置文件都在/etc/nginx下，并且每个虚拟主机已经安排在了/etc/nginx/sites-available下
      启动程序文件在/usr/sbin/nginx
      日志放在了/var/log/nginx中，分别是access.log和error.log
      并已经在/etc/init.d/下创建了启动脚本nginx
      默认的虚拟主机的目录设置在了/usr/share/nginx/www

修改nginx配置文件
$ sudo vim /etc/nginx/nginx.conf

安装php
sudo apt-get install php5-fpm

然后编辑配置文件。
代码如下:
sudo gedit /etc/nginx/sites-available/default

注意，如果是用gedit而不是用vi编辑，那应该编辑sites-available下的default文件，如果是编辑site-enabled下的default，因为gedit保存时默认会生成一个“default~”的备份，这个备份也会被nginx当成启用的配置文件而出错无法启动。保险的做法是，编辑site-available下的文件后仍手动删除备份文件。
找到location ~ \.php$的地方，5行取消注释，变成这样：

location ~ \.php$ {
# fastcgi_split_path_info ^(.+\.php)(/.+)$;
# # NOTE: You should have "cgi.fix_pathinfo = 0;" in php.ini
#
# # With php5-cgi alone:
# fastcgi_pass 127.0.0.1:9000;
# # With php5-fpm:
 fastcgi_pass unix:/var/run/php5-fpm.sock;
 fastcgi_index index.php;
 include fastcgi_params;
}
这就成了！
启动nginx：
sudo service nginx start
重启：sudo service nginx restart

扩展：
1. default文件中，找到
index index.html index.htm;

这行，加入成
index index.html index.htm index.php;

这就可以用php文件做默认主页
2.default文件中，在server{}指示符的 location / {} 指示符内，加入
autoindex on;

当文件夹内没有index文件，就会自动索引文件。
3. server{} 指示符的 root 行是文件根目录，自行修改就能把那个文件夹作为网站根目录

#1 - Configure PHP5-FPM
PHP5-FPM configuration file is located at /etc/php5/fpm/php.ini. Open it with your text editor
$ sudo vi /etc/php5/fpm/php.ini

Change this parameter, from:
cgi.fix_pathinfo=1

to:
cgi.fix_pathinfo=0

Save and close the file and then restart php5-fpm service, type:
$ sudo service php5-fpm restart

After the configuration section is done, now we need to test them to make sure that our configuration is working as required. On Ubuntu 14.04 the root document folder is located in /usr/share/nginx/html. 
$ sudo gedit /usr/share/nginx/html/phpinfo.php
So create the file  with the following code:
	<?php echo phpinfo(); ?>

http://localhost/phpinfo.php



