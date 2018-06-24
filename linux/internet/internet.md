
frank@G470:~$ ifconfig
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
