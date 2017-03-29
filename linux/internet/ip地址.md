# 查看本地IP（inet 地址）
$ ifconfig
enp7s0    Link encap:以太网  硬件地址 dc:0e:a1:e8:8e:28  
          inet 地址:192.168.1.2  广播:192.168.1.255  掩码:255.255.255.0
          inet6 地址: fe80::463e:bf50:ccb5:5d41/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  跃点数:1
          接收数据包:13671 错误:0 丢弃:0 过载:0 帧数:0
          发送数据包:14809 错误:0 丢弃:0 过载:0 载波:1
          碰撞:0 发送队列长度:1000 
          接收字节:10499617 (10.4 MB)  发送字节:2262234 (2.2 MB)

lo        Link encap:本地环回  
          inet 地址:127.0.0.1  掩码:255.0.0.0
          inet6 地址: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  跃点数:1
          接收数据包:2829 错误:0 丢弃:0 过载:0 帧数:0
          发送数据包:2829 错误:0 丢弃:0 过载:0 载波:0
          碰撞:0 发送队列长度:1 
          接收字节:381410 (381.4 KB)  发送字节:381410 (381.4 KB)

wlp8s0    Link encap:以太网  硬件地址 08:ed:b9:5a:80:a2  
          UP BROADCAST MULTICAST  MTU:1500  跃点数:1
          接收数据包:0 错误:0 丢弃:0 过载:0 帧数:0
          发送数据包:0 错误:0 丢弃:0 过载:0 载波:0
          碰撞:0 发送队列长度:1000 
          接收字节:0 (0.0 B)  发送字节:0 (0.0 B)
          中断:17 

# 查看出口IP

$ wget http://members.3322.org/dyndns/getip
$ cat getip


