# 操作系统检测

frank@G470:~$ sudo apt-get install nmap

远程探测操作系统 
	sudo nmap -O ip

精准检测操作系统
	nmap -O –osscan-guess ip
	Failed to resolve "–osscan-guess".

详细检测操作系统
	sudo nmap -O -osscan_limit  ip


# 检测SQL注入点

sqlmap -u url


cookie检测注入点


sqlmap -u url --cookie "id=230" --level 2

# whois



# 测试



## 其他测试

Note： http://172.16.0.86 是登陆页面


	frank@G470:~$ ping -c 4 172.16.0.86
PING 172.16.0.86 (172.16.0.86) 56(84) bytes of data.
64 bytes from 172.16.0.86: icmp_seq=1 ttl=64 time=27.9 ms
64 bytes from 172.16.0.86: icmp_seq=2 ttl=64 time=18.6 ms
64 bytes from 172.16.0.86: icmp_seq=3 ttl=64 time=3.19 ms
64 bytes from 172.16.0.86: icmp_seq=4 ttl=64 time=20.0 ms

--- 172.16.0.86 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 3.197/17.439/27.911/8.953 ms
	
	frank@G470:~$ curl -I http://172.16.0.86
	
HTTP/1.1 200 OK
Server: DrcomServer1.0
Accept-Ranges: bytes
Connection: keep-alive
Content-type: text/html
Cache-Control: no-cache
Content-length: 5660


	frank@G470:~$ sudo nmap -O 172.16.0.86

Starting Nmap 6.40 ( http://nmap.org ) at 2016-05-25 00:11 CST
Nmap scan report for bogon (172.16.0.86)
Host is up (0.097s latency).
Not shown: 987 closed ports
PORT     STATE    SERVICE
22/tcp   open     ssh
23/tcp   open     telnet
80/tcp   open     http
82/tcp   open     xfer
443/tcp  open     https
801/tcp  open     device
1723/tcp open     pptp
2601/tcp filtered zebra
2602/tcp filtered ripd
2604/tcp filtered ospfd
3128/tcp filtered squid-http
8080/tcp open     http-proxy
9002/tcp open     dynamid
Device type: general purpose
Running: Linux 2.6.X
OS CPE: cpe:/o:linux:linux_kernel:2.6.9
OS details: Linux 2.6.9
Network Distance: 1 hop

OS detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 71.58 seconds


cmcc wifi网关： 10.255.223.254

	frank@G470:~$ ping -c 4 10.255.223.254
	
PING 10.255.223.254 (10.255.223.254) 56(84) bytes of data.
64 bytes from 10.255.223.254: icmp_seq=1 ttl=64 time=27.3 ms
64 bytes from 10.255.223.254: icmp_seq=2 ttl=64 time=47.3 ms
64 bytes from 10.255.223.254: icmp_seq=3 ttl=64 time=133 ms
64 bytes from 10.255.223.254: icmp_seq=4 ttl=64 time=2.14 ms

--- 10.255.223.254 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 2.145/52.700/133.925/49.556 ms

	$ sudo nmap -Pn -O -osscan_limit 10.255.223.254
	$ sudo nmap -O 10.255.223.254
	
Starting Nmap 6.40 ( http://nmap.org ) at 2016-05-25 00:17 CST
Nmap scan report for bogon (10.255.223.254)
Host is up (0.017s latency).
Not shown: 999 filtered ports
PORT     STATE SERVICE
1723/tcp open  pptp
MAC Address: 00:0D:48:06:4F:1B (Aewin Technologies Co.)

OS detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.11 seconds


快通宿舍宽带


		frank@G470:~$ ping -c 4 10.248.28.1
		
PING 10.248.28.1 (10.248.28.1) 56(84) bytes of data.
64 bytes from 10.248.28.1: icmp_seq=1 ttl=64 time=0.279 ms
64 bytes from 10.248.28.1: icmp_seq=2 ttl=64 time=0.282 ms
64 bytes from 10.248.28.1: icmp_seq=3 ttl=64 time=0.308 ms
64 bytes from 10.248.28.1: icmp_seq=4 ttl=64 time=0.463 ms

--- 10.248.28.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 2997ms
rtt min/avg/max/mdev = 0.279/0.333/0.463/0.075 ms

		frank@G470:~$ sudo nmap -O 10.248.28.1
					  sudo nmap -O -osscan_limit  10.248.28.1

Starting Nmap 6.40 ( http://nmap.org ) at 2016-05-25 07:06 CST
Nmap scan report for 10.248.28.1
Host is up (0.00034s latency).
All 1000 scanned ports on 10.248.28.1 are filtered
Too many fingerprints match this host to give specific OS details

OS detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.03 seconds
		


快通宿舍宽带+netcore无线路由器
		
		frank@G470:~$ ping -c 4 192.168.1.1
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=30 time=0.339 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=30 time=0.465 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=30 time=0.345 ms
64 bytes from 192.168.1.1: icmp_seq=4 ttl=30 time=0.482 ms

--- 192.168.1.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3000ms
rtt min/avg/max/mdev = 0.339/0.407/0.482/0.070 ms


		frank@G470:~$ sudo nmap -O 192.168.1.1
Starting Nmap 6.40 ( http://nmap.org ) at 2016-05-25 11:57 CST
Nmap scan report for 192.168.1.1
Host is up (0.0010s latency).
Not shown: 999 filtered ports
PORT   STATE SERVICE
80/tcp open  http
MAC Address: 08:10:79:74:53:F2 (Unknown)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
No OS matches for host
Network Distance: 1 hop

OS detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 24.68 seconds

			$ curl -I http://192.168.1.1
			
HTTP/1.1 200 OK
Server: HTTP Software 1.1
Date: Sat, 21 Dec 1996 12:00:00 GMT
Connection: close
Content-encoding: gzip
Content-type: text/html


		frank@G470:~/work/unixc$ sudo nmap -O 192.168.1.2		

Starting Nmap 6.40 ( http://nmap.org ) at 2016-05-25 12:25 CST
Nmap scan report for 192.168.1.2
Host is up (0.016s latency).
All 1000 scanned ports on 192.168.1.2 are filtered
MAC Address: A0:86:C6:9F:35:25 (Unknown)
Too many fingerprints match this host to give specific OS details
Network Distance: 1 hop

OS detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 24.45 seconds


		frank@G470:~/work/unixc$ sudo nmap -O 192.168.1.3

Starting Nmap 6.40 ( http://nmap.org ) at 2016-05-25 12:26 CST
Nmap scan report for 192.168.1.3
Host is up (0.000063s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
No exact OS matches for host (If you know what OS is running on it, see http://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=6.40%E=4%D=5/25%OT=22%CT=1%CU=41121%PV=Y%DS=0%DC=L%G=Y%TM=5745299
OS:B%P=x86_64-pc-linux-gnu)SEQ(SP=106%GCD=1%ISR=107%TI=Z%CI=I%TS=8)SEQ(SP=1
OS:06%GCD=1%ISR=107%TI=Z%CI=I%II=I%TS=8)OPS(O1=MFFD7ST11NW7%O2=MFFD7ST11NW7
OS:%O3=MFFD7NNT11NW7%O4=MFFD7ST11NW7%O5=MFFD7ST11NW7%O6=MFFD7ST11)WIN(W1=AA
OS:AA%W2=AAAA%W3=AAAA%W4=AAAA%W5=AAAA%W6=AAAA)ECN(R=Y%DF=Y%T=40%W=AAAA%O=MF
OS:FD7NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T
OS:4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+
OS:%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y
OS:%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%
OS:RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 0 hops

OS detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 31.13 seconds
			
			






