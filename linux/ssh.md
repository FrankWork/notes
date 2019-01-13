# install
sudo apt-get install ssh

# config

/etc/ssh/sshd_config
sudo service ssh restart

# usage: 

ssh [-1246AaCfGgKkMNnqsTtVvXxYy] [-b bind_address] [-c cipher_spec]
           [-D [bind_address:]port] [-E log_file] [-e escape_char]
           [-F configfile] [-I pkcs11] [-i identity_file] [-L address]
           [-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port]
           [-Q query_option] [-R address] [-S ctl_path] [-W host:port]
           [-w local_tun[:remote_tun]] [user@]hostname [command]




# 密钥登录

you@local: $ cat ~/.ssh/id_rsa.pub | ssh you@remote "mkdir -p ~/.ssh && cat >>  ~/.ssh/authorized_keys"
	   $chmod 700 ~/.ssh
	   $chmod 600 ~/.ssh/authorized_keys
you@remote: $ chmod 700 .ssh
	    $ chmod 600 .ssh/authorized_keys

# SSH退出后仍运行程序
$ nohup program &
$ nohup ./hierarchy-phrase.sh &




# SSH命令行上传/下载文件

## 从服务器上下载文件
scp username@servername:/path/filename /var/www/local_dir（本地目录）


## 上传本地文件到服务器
scp /path/filename username@servername:/path

例如
scp /var/www/test.php  root@192.168.0.101:/var/www/
把本机/var/www/目录下的test.php文件上传到192.168.0.101这台服务器上的/var/www/目录中


## 从服务器下载整个目录
scp -r root@192.168.0.101:/var/www/test  /var/www/


## 上传目录到服务器
scp  -r local_dir username@servername:remote_dir
例如：scp -r test  root@192.168.0.101:/var/www/   把当前目录下的test目录上传到服务器的/var/www/ 目录


