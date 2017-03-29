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
