
## sudo nmap -O 202.118.18.60 （neu nlp lab）

Starting Nmap 7.01 ( https://nmap.org ) at 2016-09-24 14:59 CST
Nmap scan report for IP-202-118-18-60.neu.edu.cn (202.118.18.60)
Host is up (0.0011s latency).
Not shown: 988 closed ports
PORT     STATE SERVICE
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
1025/tcp open  NFS-or-IIS
1026/tcp open  LSA-or-nterm
1027/tcp open  IIS
1030/tcp open  iad1
1031/tcp open  iad2
1688/tcp open  nsjtp-data
3306/tcp open  mysql
3389/tcp open  ms-wbt-server
Device type: general purpose
Running: Microsoft Windows Vista|7|8.1
OS CPE: cpe:/o:microsoft:windows_vista cpe:/o:microsoft:windows_7::sp1 cpe:/o:microsoft:windows_8.1
OS details: Microsoft Windows Vista, Windows 7 SP1, or Windows 8.1 Update 1

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 37.71 seconds

## $ whois 202.118.18.60 

% [whois.apnic.net]
% Whois data copyright terms    http://www.apnic.net/db/dbcopyright.html

% Information related to '202.118.0.0 - 202.118.31.255'

inetnum:        202.118.0.0 - 202.118.31.255
netname:        NEU-CN
descr:          Northeastern University, China
descr:          Box 308, Northeastern University
descr:          Shenyang, Liaoning 110006
country:        CN
admin-c:        GC1-CN
tech-c:         QW1-CN
tech-c:         CER-AP
remarks:        origin AS4538
mnt-irt:        IRT-CERNET-AP
changed:        hm-changed@net.edu.cn 19950122
mnt-by:         MAINT-CERNET-AP
status:         ASSIGNED NON-PORTABLE
source:         APNIC

irt:            IRT-CERNET-AP
address:        Network Research Center,
address:        Main Bldg, Tsinghua Univ
address:        Beijing 100084, China
phone:          +86-10-62784301
fax-no:         +86-10-62785933
e-mail:         abuse@net.edu.cn
abuse-mailbox:  abuse@net.edu.cn
admin-c:        CER-AP
tech-c:         CER-AP
auth:           # Filtered
remarks:        timezone GMT+8
remarks:        http://www.ccert.edu.cn
mnt-by:         MAINT-CERNET-AP
changed:        hm-changed@net.edu.cn 20101126
source:         APNIC

role:           CERNET Helpdesk
address:        Room 224, Main Building
address:        Tsinghua University
address:        Beijing 100084, China
country:        CN
phone:          +86-10-6278-4049
fax-no:         +86-10-6278-5933
e-mail:         cernet-helpdesk-ip@net.edu.cn
remarks:        abuse@net.edu.cn
admin-c:        XL1-CN
tech-c:         SZ2-AP
nic-hdl:        CER-AP
remarks:        Point of Contact for admin-c
mnt-by:         MAINT-CERNET-AP
changed:        cernet-helpdesk-ip@net.edu.cn 20010903
source:         APNIC
changed:        hm-changed@apnic.net 20111114

person:         Guiran Chang
address:        Northeastern University, China
address:        Box 308, Northeastern University
address:        Shenyang, Liaoning 110006
address:        CN
country:        CN
phone:          +86-24-3841748
fax-no:         +86-24-3890817
e-mail:         chang@neu.edu.cn
nic-hdl:        GC1-CN
notify:         dbmon@apnic.net
mnt-by:         MAINT-NULL
changed:        hostmaster@apnic.net 19950122
source:         APNIC
changed:        hm-changed@apnic.net 20111122

person:         Quan Wang
address:        Northeastern University, China
address:        Box 308, Northeastern University
address:        Shenyang, Liaoning 110006
address:        CN
country:        CN
phone:          +86-24-3841748
fax-no:         +86-24-3890817
e-mail:         wang@neu.edu.cn
nic-hdl:        QW1-CN
notify:         dbmon@apnic.net
mnt-by:         MAINT-NULL
changed:        hostmaster@apnic.net 19950122
source:         APNIC
changed:        hm-changed@apnic.net 20111122

% This query was served by the APNIC Whois Service version 1.69.1-APNICv1r6-SNAPSHOT (UNDEFINED)

## frank@G470:~$ curl -I  202.118.18.60 
HTTP/1.1 200 OK
Date: Sat, 24 Sep 2016 12:22:12 GMT
Server: Apache/2.2.8 (Win32) PHP/5.2.3
Last-Modified: Sat, 20 Nov 2004 06:16:26 GMT
ETag: "6000000005f72-2c-3e94a902f4280"
Accept-Ranges: bytes
Content-Length: 44
Content-Type: text/html

# frank@G470:~$ nmap -A -T4  202.118.18.60 

Starting Nmap 7.01 ( https://nmap.org ) at 2016-09-24 20:22 CST
Nmap scan report for IP-202-118-18-60.neu.edu.cn (202.118.18.60)
Host is up (0.0011s latency).
Not shown: 988 closed ports
PORT     STATE SERVICE            VERSION
80/tcp   open  http               Apache httpd 2.2.8 ((Win32) PHP/5.2.3)
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.2.8 (Win32) PHP/5.2.3
|_http-title: Site doesn't have a title (text/html).
135/tcp  open  msrpc              Microsoft Windows RPC
139/tcp  open  netbios-ssn        Microsoft Windows 98 netbios-ssn
445/tcp  open  microsoft-ds       Microsoft Windows 10 microsoft-ds
1025/tcp open  msrpc              Microsoft Windows RPC
1026/tcp open  msrpc              Microsoft Windows RPC
1027/tcp open  msrpc              Microsoft Windows RPC
1030/tcp open  msrpc              Microsoft Windows RPC
1031/tcp open  msrpc              Microsoft Windows RPC
1688/tcp open  msrpc              Microsoft Windows RPC
3306/tcp open  mysql              MySQL (unauthorized)
3389/tcp open  ssl/ms-wbt-server?
| ssl-cert: Subject: commonName=XZ-20131011VSMZ
| Not valid before: 2016-05-27T13:11:32
|_Not valid after:  2016-11-26T13:11:32
|_ssl-date: 2016-09-24T12:24:52+00:00; +1m31s from scanner time.
Service Info: OSs: Windows, Windows 98, Windows 10; CPE: cpe:/o:microsoft:windows, cpe:/o:microsoft:windows_98, cpe:/o:microsoft:windows_10

Host script results:
|_nbstat: NetBIOS name: XZ-20131011VSMZ, NetBIOS user: <unknown>, NetBIOS MAC: 78:ac:c0:b9:13:ce (Hewlett Packard)
| smb-os-discovery: 
|   OS: Windows 7 Ultimate 7601 Service Pack 1 (Windows 7 Ultimate 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1
|   Computer name: XZ-20131011VSMZ
|   NetBIOS computer name: XZ-20131011VSMZ
|   Workgroup: WORKGROUP
|_  System time: 2016-09-24T20:24:52+08:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smbv2-enabled: Server supports SMBv2 protocol

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 70.84 seconds



# frank@G470:~$ sudo nmap -sS  202.118.18.60 

Starting Nmap 7.01 ( https://nmap.org ) at 2016-09-24 20:25 CST
Nmap scan report for IP-202-118-18-60.neu.edu.cn (202.118.18.60)
Host is up (0.0093s latency).
Not shown: 988 closed ports
PORT     STATE SERVICE
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
1025/tcp open  NFS-or-IIS
1026/tcp open  LSA-or-nterm
1027/tcp open  IIS
1030/tcp open  iad1
1031/tcp open  iad2
1688/tcp open  nsjtp-data
3306/tcp open  mysql
3389/tcp open  ms-wbt-server

Nmap done: 1 IP address (1 host up) scanned in 48.73 seconds

