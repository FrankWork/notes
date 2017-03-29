# 查看进程占用哪个端口

$  netstat -anp | grep 8080


# IP: 
    ifconfig

# gateway:

[root@localhost ~]# netstat -rn
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window irtt Iface
172.16.44.0     0.0.0.0          255.255.255.0    U         0      0          0 vmnet8
172.16.10.0     0.0.0.0          255.255.255.0        U         0      0          0 vmnet1
172.16.0.0       0.0.0.0          255.255.252.0        U         0      0          0 eth0
169.254.0.0     0.0.0.0          255.255.0.0           U         0      0          0 eth0
0.0.0.0         172.16.0.254    0.0.0.0           UG        0      0          0 eth0

(以0.0.0.0开始的行的gateway是默认网关)


# DNS:
[root@localhost ~]# cat /etc/resolv.conf
search               localdomain
nameserver 172.16.0.250

如果共享访问互联网，查看出口IP

curl  http://members.3322.org/dyndns/getip 
