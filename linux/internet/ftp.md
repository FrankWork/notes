## 简介

### 身份

- user
- guest
- anonymous

### 记录

/var/log/

### 用户活动目录

chroot环境变量为用户活动目录，只能访问活动目录下的内容

### 端口

- 命令通道
  * 客户端会随机选择一个大于1024的端口A与服务器端的21端口链接，查询、下载、上传等命令是通过这个通道来进行的。
- 数据通道
  * 在主动模式下，客户端通过命令通道告知服务器自己所需数据及另一个端口B
  * 服务器由命令通道了解客户端的需求后，会主动由20端口向客户端另一个端口联机，进行数据传输

### 防火墙

```
firewall-cmd --permanent --add-port=21/tcp
firewall-cmd --permanent --add-service=ftp
firewall-cmd --reload
```


## 安装与使用

```
$ sudo apt install vsftpd
$ sudo vim /etc/vsftpd.conf # ubuntu
$ sudo vim /etc/vsftpd/vsftpd.conf
anon_root=/srv/ftp
local_root=/

$ sudo systemctl enable vsftpd
$ sudo systemctl start vsftpd
$ sudo systemctl restart vsftpd
$ sudo systemctl stop vsftpd

$ sudo netstat -lnp | grep ftp
tcp6       0      0 :::21     :::*   LISTEN      21191/vsftpd
```

### 上传下载

```
$ ftp 127.0.0.1 21
Name (127.0.0.1:frank): frank
Password:
ftp> dir
ftp> pwd
ftp> quit

ftp> get remote-file [local-file]
ftp> put local-file [remote-file]

ftp> mget remote-files
ftp> mput local-files

```

```
ftp://user:passwd@ip:/filename
ftp://user:passwd@ip/filename
ftp://lzh:.@127.0.0.1/home/lzh/examples.desktop
```



## 配置

```
/etc/ftpusers
/etc/vsftpd.conf
```

### 字符编码

```
utf8_filesystem=YES
```

### vsftpd.conf-用户登录控制

```
anonymous_enable=YES，允许匿名用户登录。
no_anon_password=YES，匿名用户登录时不需要输入密码。
local_enable=YES，允许本地用户登录。
deny_email_enable=YES，可以创建一个文件保存某些匿名电子邮件的黑名单，以防止这些人使用Dos攻击。
banned_email_file=/etc/vsftpd/banned_emails，保存电子邮件黑名单的目录（默认）
```

### 用户权限控制：

```
write_enable=YES，开启全局上传
local_umask=022，本地文件上传的umask设置为022，系统默认。
anon_upload_enable=YES，允许匿名用户上传，当然要在write_enable=YES的情况下。同时必须建立一个允许ftp用户读写的目录。
anon_mkdir_write_enable=YES，允许匿名用户创建目录
chown_uploads=YES，匿名用户上传的文件属主转换为别的用户，一般建议为root。
chown_username=whoever，改此处的whoever为要转换的属主，建议root
chroot_list_enable=YES，用一个列表来限定哪些用户只能在自己目录下活动。
chroot_list_enable=/etc/vsftpd/chroot_list，指定用户列表文件
nopriv_user=ftpsecure，指定一个安全账户，让ftp完全隔离和没有特权的账户
```

### 用户连接和超时设置：

```
idle_session_timeout=600，默认的超时时间
data_connection_timeout=120，设置默认数据连接的超时时间
```

### 服务器日志和欢迎信息

```
dirmessage_enable=YES，允许为配置目录显示信息
ftpd_banner=Welcome to blah FTP service. ftp的欢迎信息
xferlog_enable=YES 打开日志记录功能
xferlog_file=/var/log/xferlog  日志记录文件的位置
```
