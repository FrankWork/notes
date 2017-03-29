# Install 

$ sudo apt install vsftpd


# 上传下载


get remote-file [local-file]
put local-file [remote-file]

mget remote-files
mput local-files



$ ftp 127.0.0.1 21
Connected to 127.0.0.1.
220 (vsFTPd 3.0.3)
Name (127.0.0.1:frank): frank
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> dir
drwxr-xr-x    2 1000     1000         4096 May 08 11:07 ??????
ftp> pwd
257 "/home/frank" is the current directory
ftp> quit
221 Goodbye.






# 启动与停止

## 启动
$ service vsftpd start

## 停止
$ service vsftpd stop

## 重启
$ service vsftpd restart




# 配置

/etc/ftpusers
/etc/vsftpd.conf

## 字符编码
utf8_filesystem=YES

## vsftpd.conf-用户登录控制

anonymous_enable=YES，允许匿名用户登录。
no_anon_password=YES，匿名用户登录时不需要输入密码。
local_enable=YES，允许本地用户登录。
deny_email_enable=YES，可以创建一个文件保存某些匿名电子邮件的黑名单，以防止这些人使用Dos攻击。
banned_email_file=/etc/vsftpd/banned_emails，保存电子邮件黑名单的目录（默认）

## 用户权限控制：


write_enable=YES，开启全局上传
local_umask=022，本地文件上传的umask设置为022，系统默认。
anon_upload_enable=YES，允许匿名用户上传，当然要在write_enable=YES的情况下。同时必须建立一个允许ftp用户读写的目录。
anon_mkdir_write_enable=YES，允许匿名用户创建目录
chown_uploads=YES，匿名用户上传的文件属主转换为别的用户，一般建议为root。
chown_username=whoever，改此处的whoever为要转换的属主，建议root
chroot_list_enable=YES，用一个列表来限定哪些用户只能在自己目录下活动。
chroot_list_enable=/etc/vsftpd/chroot_list，指定用户列表文件
nopriv_user=ftpsecure，指定一个安全账户，让ftp完全隔离和没有特权的账户

## 用户连接和超时设置：

idle_session_timeout=600，默认的超时时间
data_connection_timeout=120，设置默认数据连接的超时时间

## 服务器日志和欢迎信息

dirmessage_enable=YES，允许为配置目录显示信息
ftpd_banner=Welcome to blah FTP service. ftp的欢迎信息
xferlog_enable=YES 打开日志记录功能
xferlog_file=/var/log/xferlog  日志记录文件的位置
