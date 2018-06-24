# 查看cpu
$ lscpu
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                24

$ cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c 
24  Intel(R) Xeon(R) CPU E5-2620 0 @ 2.00GHz

# 查看内存信息 
$ free -g # 46G 内存
             total       used       free     shared    buffers     cached
Mem:            46          4         42          0          0          3

$ cat /proc/meminfo 
MemTotal:       49272616kB = 46GB 

# 查看硬盘信息
$ lsblk
sda      8:0    0 931.5G  0 disk 

$ df -h
文件系统	      容量  已用  可用 已用%% 挂载点
/dev/sda3             9.9G  456M  8.9G   5% /
tmpfs                  24G  420K   24G   1% /dev/shm
/dev/sda2             797G  757G  284K 100% /home
/dev/sda6             9.9G  151M  9.2G   2% /opt
/dev/sda5              50G  181M   47G   1% /tmp
/dev/sda7             9.9G  6.4G  3.1G  68% /usr
/dev/sda8             9.9G  522M  8.9G   6% /var


# 查看显卡
lspci  | grep -i vga    


# 查看操作系统版本
$ lsb_release -a
LSB Version:	:core-4.0-amd64:core-4.0-noarch:graphics-4.0-amd64:graphics-4.0-noarch:printing-4.0-amd64:printing-4.0-noarch
Distributor ID:	CentOS
Description:	CentOS release 6.3 (Final)
Release:	6.3
Codename:	Final

# 其他
$ dmidecode -q

# 检查某个进程是否存在

$ cat /proc/pid/status
这里pid是你的进程ID，看看输出结果，有一栏是State 

# 其他设备

```bash
# uname -a # 查看内核/操作系统/CPU信息
# head -n 1 /etc/issue # 查看操作系统版本
# cat /proc/cpuinfo # 查看CPU信息
# hostname # 查看计算机名
# lspci -tv # 列出所有PCI设备
# lsusb -tv # 列出所有USB设备
# lsmod # 列出加载的内核模块
# env # 查看环境变量 资源
# free -m # 查看内存使用量和交换区使用量
# df -h # 查看各分区使用情况
# du -sh <目录名> # 查看指定目录的大小
# grep MemTotal /proc/meminfo # 查看内存总量
# grep MemFree /proc/meminfo # 查看空闲内存量
# uptime # 查看系统运行时间、用户数、负载
# cat /proc/loadavg # 查看系统负载 磁盘和分区
# mount | column -t # 查看挂接的分区状态
# fdisk -l # 查看所有分区
# swapon -s # 查看所有交换分区
# hdparm -i /dev/hda # 查看磁盘参数(仅适用于IDE设备)
# dmesg | grep IDE # 查看启动时IDE设备检测状况

网络

# ifconfig # 查看所有网络接口的属性
# iptables -L # 查看防火墙设置
route -n # 查看路由表
# netstat -lntp # 查看所有监听端口
# netstat -antp # 查看所有已经建立的连接
# netstat -s # 查看网络统计信息

进程

# ps -ef # 查看所有进程
# top # 实时显示进程状态


用户

# w # 查看活动用户
# id <用户名> # 查看指定用户信息
# last # 查看用户登录日志
# cut -d: -f1 /etc/passwd # 查看系统所有用户
# cut -d: -f1 /etc/group # 查看系统所有组
# crontab -l # 查看当前用户的计划任务 服务
# chkconfig --list # 列出所有系统服务
# chkconfig --list | grep on # 列出所有启动的系统服务 
```