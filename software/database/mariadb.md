http://dev.mysql.com/doc/refman/5.7/en/tutorial.html
http://www.cnblogs.com/kex1n/archive/2010/03/26/2286504.html

设置MariaDB

$ sudo apt-get install software-properties-common
$ sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xcbcb082a1bb943db
$ sudo add-apt-repository 'deb http://sfo1.mirrors.digitalocean.com/mariadb/repo/10.0/ubuntu trusty main'

安装 MariaDB :

$ sudo apt-get update
$ sudo apt-get install mariadb-server

在安装中，你会被要求设置MariaDB的root密码。

从命令行连接到MariaDB :

sudo mysql

linuxtechi@mail:~$ mysql -u root -p
Enter password:
Welcome to the MariaDB monitor. Commands end with ; or \g.
Your MariaDB connection id is 40
Server version: 10.0.14-MariaDB-1~trusty-log mariadb.org binary distribution
Copyright (c) 2000, 2014, Oracle, SkySQL Ab and others.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
MariaDB [(none)]>

MariaDB 服务

$ sudo /etc/init.d/mysql stop
$ sudo /etc/init.d/mysql start

以上只是在Ubuntu上装完MariaDB,下面要设置MariaDB允许远程访问

1. 如果Ubuntu有设置防火墙或者iptables规则的话,请自行打开
2. 3306端口是不是没有打开？

    使用nestat命令查看3306端口状态：

    ~# netstat -an | grep 3306

    tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN

    从结果可以看出3306端口只是在IP 127.0.0.1上监听，所以拒绝了其他IP的访问。

    解决方法：修改/etc/mysql/my.cnf文件。打开文件，找到下面内容：

    # Instead of skip-networking the default is now to listen only on
    # localhost which is more compatible and is not less secure.
    bind-address  = 127.0.0.1

    把上面这一行注释掉或者把127.0.0.1换成合适的IP，建议注释掉。

    重新启动后，重新使用netstat检测：

    ~# netstat -an | grep 3306
    tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN

 

3. 现在使用下面命令测试：

     ~# mysql -h 192.168.0.101 -u root -p
    Enter password:
    ERROR 1130 (00000): Host 'Ubuntu-Fvlo.Server' is not allowed to connect to this MySQL server

    结果出乎意料，还是不行。

    解决方法：原来还需要把用户权限分配各远程用户。

    登录到mysql服务器，使用grant命令分配权限

    mysql> grant all on *.* to 你的用户名如root@'%' identified by '你的密码';

    完成后使用mysql命令连接，提示成功，为了确保正确可以再远程登陆测试一下。

# mysql 用法：

创建：mysql samp_db < create_member.sql
登陆：mysql -h 127.0.0.1 -u root -p
>show databases;
>use wikidb;
>show tables;
>describe XXtable;

创建表：

CREATE DATABASE IF NOT EXISTS db_name DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

GRANT ALL PRIVILEGES ON wikidb.* TO 'wikiuser'@'localhost' 
IDENTIFIED BY 'password';

创建用户：
MariaDB [(none)]> show databases;
MariaDB [(none)]> use mysql;
MariaDB [mysql]> show tables;
MariaDB [mysql]> describe user;
MariaDB [mysql]> select Host, User, Password from user;
+-----------+------------------+-------------------------------------------+
| Host      | User             | Password                                  |
+-----------+------------------+-------------------------------------------+
| localhost | root             | *3B6E95335E0FD876E9393210F618535CC492D497 |
| g470      | root             | *3B6E95335E0FD876E9393210F618535CC492D497 |
| 127.0.0.1 | root             | *3B6E95335E0FD876E9393210F618535CC492D497 |
| ::1       | root             | *3B6E95335E0FD876E9393210F618535CC492D497 |
| localhost | debian-sys-maint | *E05ECFB4A20AAE9FB318DEDFEDA073E245CCCD5F |
| localhost | drupal           | *87C2D16387BBF6BAD8B735C3BF31B4802B68E3FB |
+-----------+------------------+-------------------------------------------+
6 rows in set (0.00 sec)




2.执行sql脚本,可以有2种方法:
第一种方法:
	$ mysql -h localhost -u root -p123456 < F:\hello world\niuzi.sql
第二种方法:
	mysql>source F:\hello world\niuzi.sql 


```sql
CREATE DATABASE <DATABASE_NAME>;
USE <DATABASE_NAME>;

CREATE TABLE IF NOT EXISTS `runoob_tbl`(
   `runoob_id` INT UNSIGNED AUTO_INCREMENT,
   `runoob_title` VARCHAR(100) NOT NULL,
   `runoob_author` VARCHAR(40) NOT NULL,
   `submission_date` DATE,
   PRIMARY KEY ( `runoob_id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

SHOW TABLES;

INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );

INSERT INTO example (example_id, name, value, other_value)
VALUES
    (100, 'Name 1', 'Value 1', 'Other 1'),
    (101, 'Name 2', 'Value 2', 'Other 2'),
    (102, 'Name 3', 'Value 3', 'Other 3'),
    (103, 'Name 4', 'Value 4', 'Other 4');

DELETE FROM table_name;

select count(*) from tb_name;

SELECT uuid FROM news_tb WHERE uuid in ("fff", "679");

-- 修改字段属性
ALTER TABLE user10 MODIFY email VARCHAR(200) NOT NULL DEFAULT 'a@a.com';
-- 将card移到test后面
ALTER TABLE user10 MODIFY card CHAR(10) AFTER test;


UPDATE 表名 SET 字段名1=值1，[ ，字段名2=值2，…] [ WHERE 条件表达式 ]
```