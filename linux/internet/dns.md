## 查询

```
$ whois google.com
$ whois baidu.com

$ host www.google.com
www.google.com has address 202.118.0.248
www.google.com has IPv6 address 2001:da8:9000:b255::248

$ nslookup google.com
Name:   google.com
Address: 172.217.24.14   # dns server

$ dig www.163.com

```


## dns缓存服务器

bind: The Berkeley Internet Name Domain (BIND) implements an Internet domain name server.

```
$ sudo apt install bind9     # ubuntu
$ sudo systemctl start bind9 # unable to connect to google !!!

# yum install bind           # centos
# systemctl start named

$ dig @localhost www.google.com
$ edit /etc/resolv.conf

nameserver 127.0.0.1  # 設定第一台 DNS
search neu6.edu.cn    # 設定 search domain 
```

use dnsmasq !