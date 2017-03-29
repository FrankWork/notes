# 更改 root 密码

最少 15 个字符，这样的密码强度大概有 90 bit，勉强可以应付密码被“暴力破解”
openssl rand -base64 15
W4IJzqu2Pf3wcTFiKAdC

# 新增一个普通帐号

adduser user-name
passwd user-name

# 禁止 root 使用 ssh 登入

文件/etc/ssh/sshd_config中：
＃PermitRootLogin yes
修改为：
PermitRootLogin no
最后输入以下指令重新启动sshd：
$ systemctl restart sshd.service


# 设定防火墙

过滤封包功能的 netfilter 已经内建在 CentOS 7 的内核，firewalld可以配置 netfilter：
$ yum install firewalld
查看一下防火墙现在开启了哪些服务和端口：
$ firewall-cmd --list-all
出错
$ yum update
启动：	# systemctl start  firewalld
查看状态：# systemctl status firewalld 或者 firewall-cmd --state
停止：	# systemctl disable firewalld
禁用：	# systemctl stop firewalld
查看端口：# firewall-cmd --zone=dmz --list-ports
$ firewall-cmd --list-all
services: dhcpv6-client ssh


# 使用非常规的 ssh 端口

Ssh默认使用端口 22

文件/etc/ssh/sshd_config中：	
＃Port 22
修改为：	
Port 10837
你可以把 10837 改为任何 1024 – 65535 之间的任何数字。
最后输入以下指令重新启动sshd：
$ systemctl restart sshd.service

为ssh设置防火墙
$ cp /usr/lib/firewalld/services/ssh.xml /etc/firewalld/services/
打开/etc/firewalld/services/ssh.xml：
<port protocol="tcp" port="22"/>
修改为：
<port protocol="tcp" port="10837"/>
储存后重新加载 firewalld：
$ firewall-cmd --reload



# 启用公钥验证登入 ssh, failed 

密钥储存在日常使用的电脑，公钥则储存在服务器。

第一步在日常使用的电脑上使用 ssh-keygen 指令建立一对加密钥匙，它会询问储存加密钥匙的档案名称，和把钥匙加密的密码，档案名称使用默认的路径和名称便可以，密码则无需输入

$ ssh-keygen -t rsa

这个指令会创造两个档案，一个名为 id_rsa，是你的 RSA 密钥，另一个是 id_rsa.pub，是你的 RSA 公钥。

公钥必需上传到服务器并且附加于用户帐号里面的 .ssh/authorized_keys 档案中，这个档案储存所有可透过 ssh 登入到这一个帐号的公钥，一行一条公钥。这个档案的存取权限必须是 0700，否则 sshd 不会读取。

设定 ssh 的双重验证法，使用 vim  (或任何文本编辑器) 开启 /etc/ssh/sshd_config，在档案的末端假如这一行：
AuthenticationMethods publickey,password
它告诉服务器用户必须拥有合法的公钥，和输入正确的密码才能成功登入。修改完成后重新启动 sshd：
$ systemctl restart sshd.service

# 更新、更新、每天更新、每天自动更新



