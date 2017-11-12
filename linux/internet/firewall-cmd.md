firewall-cmd --list-all
sudo firewall-cmd --permanent --add-port=21/tcp
sudo firewall-cmd --reload

为ssh设置防火墙
$ cp /usr/lib/firewalld/services/ssh.xml /etc/firewalld/services/
打开/etc/firewalld/services/ssh.xml：
<port protocol="tcp" port="22"/>
修改为：
<port protocol="tcp" port="10837"/>
储存后重新加载 firewalld：
$ firewall-cmd --reload


