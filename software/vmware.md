# centos7最小化安装

$ vi /etc/sysconfig/network-scripts/ifcfg-ens33
    ONBOOT=yes
$ service network restart
$ ip addr


# 虚拟机联网
https://blog.csdn.net/qq_28090573/article/details/78730552

1. birdge
    VMware虚拟出来的操作系统就像是局域网中的一台独立的主机，它可以访问网内任何一台机器，手工配置它的TCP/IP配置信息，以实现通过局域网的网关或路由器访问互联网。
    适用情况：在局域网中有1个以上的IP地址可以自由分配使用。
    https://blog.csdn.net/qq_28817739/article/details/77604505
    虚拟机的子网掩码，默认网关，DNS服务器要和本地主机的一样，虚拟机的ip地址要和本地ip地址在一个网段
2.  NAT 
    让虚拟系统借助NAT(网络地址转换)功能，通过宿主机器所在的网络来访问公网, 无法和本局域网中的其他真实主机进行通讯，宿主机器和虚拟机可以双向通信
    需要在本地操作系统将本地网卡共享给VMnet8(NAT模式用的虚拟交换机)
    适用情况：只有1 个外网的IP地址可以使用
    要用SSH连虚拟机，得使用端口转发
    https://blog.csdn.net/jiuduan2009/article/details/51737004
    配置虚拟机本地静态ip
    $ vi /etc/sysconfig/network-scripts/ifcfg-ens33
        DEVICE=eth0 
        TYPE=Ethernet 
        ONBOOT=yes 
        BOOTPROTO=static 
        IPADDR=192.168.148.1 #注意虚拟机的IP与宿主机的内网IP不能相同 
        NETMASK=255.255.255.0 
        GATEWAY=192.168.148.2 
        DNS1=202.118.1.29
        DNS2=202.118.1.53
    $ service network restart
3. HostOnly
    虚拟网络是一个全封闭的网络，它唯一能够访问的就是主机。想要虚拟机上外网则需要主机联网并且网络共享
    所有的虚拟系统是可以相互通信的，虚拟系统和宿主机器系统是可以相互通信的

# 安装 VMware Tools
https://docs.vmware.com/cn/VMware-Workstation-Pro/15.0/com.vmware.ws.using.doc/GUID-08BB9465-D40A-4E16-9E15-8C016CC8166F.html


$ yum update
$ yum upgrade
$ yum install perl gcc
$ yum install "kernel-devel-uname-r == $(uname -r)"

$ mkdir /mnt/cdrom
$ mount /dev/cdrom /mnt/cdrom
$ cd /tmp
$ tar zxpf /mnt/cdrom/VMwareTools-x.x.x-yyyy.tar.gz
$ umount /dev/cdrom 
$ cd vmware-tools-distrib
$ ./vmware-install.pl


yum install gcc-c++

