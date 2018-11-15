# 查看网卡

$ cat /proc/net/dev
  lo
  ens33
$ ethtool -i ens33
  driver:

# 查看ip地址

$ ip addr
$ ip addr show 
$ ip addr show ens33 # ens33为网卡设备

# 网络配置

配置本地静态ip

$ vi /etc/sysconfig/network-scripts/ifcfg-ens33
        DEVICE=eth0
        TYPE=Ethernet
        ONBOOT=yes
        BOOTPROTO=static
        IPADDR=192.168.148.1   #注意虚拟机的IP与宿主机的内网IP不能相同
        NETMASK=255.255.255.0
        GATEWAY=192.168.148.2
        DNS1=202.118.1.29
        DNS2=202.118.1.53

配置本地动态ip

$ vi /etc/sysconfig/network-scripts/ifcfg-ens33
	BOOTPROTO=dhcp

$ service network restart



# 计算机网络


- 分组交换
	背景：战争期间，一旦正在通信的电路有一个交换机或链路被炸，则整个通信电路就要中断
	分组交换是采用存储转发技术。把欲发送的报文分成一个个的“分组”，在网络中传送。分组的首部是重要的控制信息，因此分组交换的特征是基于标记的。分组交换网由若干个结点交换机和连接这些交换机的链路组成。从概念上讲，一个结点交换机就是一个小型的计算机，但主机是为用户进行信息处理的，结点交换机是进行分组交换的。每个结点交换机都有两组端口，一组是与计算机相连，链路的速率较低。一组是与高速链路和网络中的其他结点交换机相连。

- 协议分层
	为了减少网络设计的复杂性，绝大多数网络采用分层设计方法。所谓分层设计方法，就是按照信息的流动过程将网络的整体功能分解为一个个的功能层，不同机器上的同等功能层之间采用相同的协议，同一机器上的相邻功能层之间通过接口进行信息传递。

- 协议体系结构
	OSI七层：物理层、   数据链路层、  网络层、   运输层、   会话层、   表示层、   应用层
	         比特流     帧            数据包      段        访问次序   ASCII,JEPG    
			 线路       MAC           IP         TCP,UDP                          HTTP,FTP
	TCP/IP四层：网络接口层、网际层ip、运输层（TCP,UDP），应用层
	五层：物理层、数据链路层、网络层、运输层、应用层

- 网关
	Gateway,又称网间连接器、协议转换器。网关在网络层以上实现网络互连，是最复杂的网络互连设备，仅用于两个高层协议不同的网络互连。网关既可以用于广域网互连，也可以用于局域网互连。从一个房间走到另一个房间，必然要经过一扇门。同样，从一个网络向另一个网络发送信息，也必须经过一道“关口”，这道关口就是网关。

- 交换机
	Switch,意为“开关”是一种用于电（光）信号转发的网络设备。它可以为接入交换机的任意两个网络节点提供独享的电信号通路。
	应用在数据链路层。交换机有多个端口，每个端口都具有桥接功能，可以连接一个局域网或一台高性能服务器或工作站。实际上，交换机有时被称为多端口网桥

- 路由器
	Router 作用在网络层，根据信道的情况自动选择和设定路由，以最佳路径，按前后顺序发送信号，实现各种骨干网内部连接、骨干网间互联和骨干网与互联网互联互通业务

- 网桥
	（Bridge）是早期的两端口二层网络设备，用来连接不同网段，后来被交换机取代

- 局域网和广域网
	局域网（Local Area	Network，LAN），是指在某一区域内由多台计算机互联成的计算机组，
		局域网是封闭的，传输速度更快
	广域网（Wide Area Network，WAN），就是我们通常所说的Internet，它是一个遍及全世界的网络。
		传输速度慢

- ip地址分类
	ip地址由两部分组成：网络ID和主机ID，同一个物理网络上的所有主机都使用同一个网络ID，网络上的一个主机（包括网络上工作站，服务器和路由器等）有一个主机ID与其对应
	ip地址分为公网ip和私有ip，前者可以直接连上internet，后者不可以，后者用于局域网内。
	上网时，局域网机器将请求发送给路由器，路由器将数据发给internet

	A: 0xxxxxxx | host | host | host |  
	B: 10xxxxxx | net  | host | host |  
	C: 110xxxxx | net  | net  | host |
	D: 1110xxxx | mc   | mc   |

	   最大网络数       ip地址范围                 最大主机数      私有ip地址范围
	A  2^7-2 = 126      0.0.0.0-127.255.255.255     16777214	10.0.0.0-10.255.255
	B  2^14  = 16384    128.0.0.0-191.255.255.255   65534   	172.16.0.0-172.31.255.255
	C  2^21  = 2097152  192.0.0.0-223.255.255.255   254         192.168.0.0-192.168.255.255

- 子网划分
	目的：减少跨网段的网络流量，使大部分流量待在本地网络中，优化网络性能
	      将多个小网络连接起来，更易维护，也更容易覆盖大型地理区域

	确定子网数目，确定每个子网主机数目



# 其他

frank@G470:~$ ifconfig # 此命令已被废弃，不再维护
eth0      Link encap:以太网  硬件地址 dc:0e:a1:e8:8e:28  
          UP BROADCAST MULTICAST  MTU:1500  跃点数:1
          接收数据包:0 错误:0 丢弃:0 过载:0 帧数:0
          发送数据包:0 错误:0 丢弃:0 过载:0 载波:0
          碰撞:0 发送队列长度:1000 
          接收字节:0 (0.0 B)  发送字节:0 (0.0 B)

lo        Link encap:本地环回  
          inet 地址:127.0.0.1  掩码:255.0.0.0
          inet6 地址: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  跃点数:1
          接收数据包:482 错误:0 丢弃:0 过载:0 帧数:0
          发送数据包:482 错误:0 丢弃:0 过载:0 载波:0
          碰撞:0 发送队列长度:0 
          接收字节:41665 (41.6 KB)  发送字节:41665 (41.6 KB)

wlan0     Link encap:以太网  硬件地址 08:ed:b9:5a:80:a2  
          inet 地址:192.168.43.159  广播:192.168.43.255  掩码:255.255.255.0
          inet6 地址: fe80::aed:b9ff:fe5a:80a2/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  跃点数:1
          接收数据包:9832 错误:0 丢弃:0 过载:0 帧数:213805
          发送数据包:4245 错误:0 丢弃:0 过载:0 载波:0
          碰撞:0 发送队列长度:1000 
          接收字节:3743295 (3.7 MB)  发送字节:664523 (664.5 KB)
          中断:17 





		frank@G470:~$ sudo mii-tool -v
		
eth0: negotiated 100baseTx-FD flow-control, link ok
  product info: vendor 00:13:74, model 2 rev 5
  basic mode:   autonegotiation enabled
  basic status: autonegotiation complete, link ok
  capabilities: 100baseTx-FD 100baseTx-HD 10baseT-FD 10baseT-HD
  advertising:  100baseTx-FD 100baseTx-HD 10baseT-FD 10baseT-HD flow-control
  link partner: 100baseTx-FD 100baseTx-HD 10baseT-FD 10baseT-HD flow-control
		
		
		
		
		
		frank@G470:~$ ethtool eth0
		
Settings for eth0:
	Supported ports: [ TP ]
	Supported link modes:   10baseT/Half 10baseT/Full 
	                        100baseT/Half 100baseT/Full 
	Supported pause frame use: No
	Supports auto-negotiation: Yes
	Advertised link modes:  Not reported
	Advertised pause frame use: No
	Advertised auto-negotiation: Yes
	Speed: 100Mb/s
	Duplex: Full
	Port: Twisted Pair
	PHYAD: 0
	Transceiver: internal
	Auto-negotiation: on
	MDI-X: Unknown
Cannot get wake-on-lan settings: Operation not permitted
	Current message level: 0x0000003f (63)
			       drv probe link timer ifdown ifup
	Link detected: yes
	
	
	
	
		frank@G470:~$ ethtool -i wlan0
	
driver: wl0
version: 6.30.223.141 (r415941)
firmware-version: 
bus-info: 
supports-statistics: no
supports-test: no
supports-eeprom-access: no
supports-register-dump: no
supports-priv-flags: no


                    

$ vim /etc/hosts                    

          
# centos wifi

TL-WN725N V1

```bash
lspci |grep -i network 查看无线网卡型号
lsusb -v               查看外置无线网卡

Bus 001 Device 018: ID 148f:2878 Ralink Technology, Corp.


nmcli general status # 查看wifi enabled
nmcli device status

rpm -q NetworkManager-wifi
yum install NetworkManager-wifi
systemctl restart NetworkManager

nmcli dev wifi list
nmcli --ask dev wifi connect <wifi-name>

systemctl is-enabled NetworkManager
systemctl is-active NetworkManager

chkconfig network off
chkconfig wpa_supplicant off

sudo yum install NetworkManager-wifi
```
