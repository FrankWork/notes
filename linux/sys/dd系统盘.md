# 查看文件系统类型

		frank@G470:~$ df -hT
文件系统       类型      容量  已用  可用 已用% 挂载点
udev           devtmpfs  2.9G     0  2.9G    0% /dev
tmpfs          tmpfs     592M  8.9M  583M    2% /run
/dev/sda6      ext4      102G   65G   32G   68% /
tmpfs          tmpfs     2.9G  128K  2.9G    1% /dev/shm
tmpfs          tmpfs     5.0M  4.0K  5.0M    1% /run/lock
tmpfs          tmpfs     2.9G     0  2.9G    0% /sys/fs/cgroup
tmpfs          tmpfs     592M   88K  592M    1% /run/user/1000


# 制作系统盘

##查看UUID
	frank@G470:~$ ls -la /dev/disk/by-id | grep usb
lrwxrwxrwx 1 root root   9  5月 22 09:47 usb-General_USB_Flash_Disk_0416IO00000076B7-0:0 -> ../../sdb
lrwxrwxrwx 1 root root  10  5月 22 09:47 usb-General_USB_Flash_Disk_0416IO00000076B7-0:0-part1 -> ../../sdb1
lrwxrwxrwx 1 root root  10  5月 22 09:47 usb-General_USB_Flash_Disk_0416IO00000076B7-0:0-part2 -> ../../sdb2
lrwxrwxrwx 1 root root   9  5月 22 09:47 usb-Generic_USB2.0-CRW_20100201396000000 -> ../../sdc

## 查看系统分区
		$ cat /proc/partitions 插U盘前
major minor  #blocks  name

   8        0  488386584 sda
   8        1  156434563 sda1
   8        2     850944 sda2
   8        3          1 sda3
   8        5  217121792 sda5
   8        6  107742208 sda6
   8        7    6232064 sda7
  11        0    1048575 sr0

		$ cat /proc/partitions 插U盘后
major minor  #blocks  name

   8        0  488386584 sda
   8        1  156434563 sda1
   8        2     850944 sda2
   8        3          1 sda3
   8        5  217121792 sda5
   8        6  107742208 sda6
   8        7    6232064 sda7
  11        0    1048575 sr0
   8       32    3915776 sdb	*
   8       33     987136 sdb1	*
   8       34       2336 sdb2	*


		frank@G470:~$ ls -l /dev | grep sdb
brw-rw----  1 root disk      8,  32  5月 22 00:14 sdb
brw-rw----  1 root disk      8,  33  5月 22 00:14 sdb1
brw-rw----  1 root disk      8,  34  5月 22 00:14 sdb2


		$ sudo fdisk -l

Disk /dev/sda: 931.5 GiB, 1000204886016 bytes, 1953525168 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x2bd2c32a

设备       启动      Start     末尾    扇区   Size Id 类型
/dev/sda1  *          2048     206847    204800   100M  7 HPFS/NTFS/exFAT
/dev/sda2           206848  209922047 209715200   100G  7 HPFS/NTFS/exFAT
/dev/sda3        209922048 1029122047 819200000 390.6G  7 HPFS/NTFS/exFAT
/dev/sda4       1029124094 1953523711 924399618 440.8G  5 扩展
/dev/sda5       1029124096 1936863231 907739136 432.9G 83 Linux
/dev/sda6       1936865280 1953523711  16658432     8G 82 Linux 交换 / Solaris

Disk /dev/sdb: 3.8 GiB, 4009754624 bytes, 7831552 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x0e0e8e70

设备       启动   Start  末尾  扇区  Size Id 类型
/dev/sdb1  *          0 2902111 2902112  1.4G  0 空
/dev/sdb2       2888004 2892739    4736  2.3M  1 FAT12

## 格式化U盘
$ sudo umount /dev/sdb1
$ sudo umount /dev/sdb2

$ sudo mkfs.vfat /dev/sdb1
$ sudo mkfs.vfat /dev/sdb2

Disk /dev/sdb: 3.8 GiB, 4009754624 bytes, 7831552 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000

## 修复U盘 read only

sudo umount /dev/sdb1
sudo hdparm -r0 /dev/sdb

id frank

sudo mount -o uid=1000 /dev/sdb1 /mnt/usb

sudo hdparm -r0 /dev/sdb1
sudo mount -o remount,rw /dev/sdb1

## 格式化U盘

sudo fsck.vfat /dev/sdb1
sudo wipefs -a "/dev/sdb1"

## 卸载U盘
		frank@G470:~$ ls -l /media/frank	卸载前
总用量 18
dr-xr-xr-x 1 frank frank  2048  4月 17  2014 Ubuntu 14.04 LTS amd64
drwx------ 3 frank frank 16384  1月  1  1970 Ubuntu 14.04 LTS amd641

		$ sudo umount /dev/sdb1
		$ sudo umount /dev/sdb2

		frank@G470:~$ ls -l /media/frank	卸载后
总用量 0

# 写入U盘
	复制系统进U盘
		$ sudo dd if=ubuntu-17.04-desktop-amd64.iso of=/dev/sdb
		$ sudo dd if=~/下载/ubuntu-16.04-desktop-amd64.iso of=/dev/sdb1

	基本命令格式
		dd if=xxx of=xxx
	例如你的系统iso文件叫做123.iso，放在home的downloads文件夹下，并且只有一块u盘
		sudo dd if=~/downloads/123.iso of=dev/sdb4
	基本就上面那样，如果有多块u盘，制作前要先确认下，别弄错了。

	如果是of=/dev/sdb，则从U盘的最初一个字节开始写，即破坏原有分区表；如果是of=/dev/sdb1，则保留分区表，从U盘
	的第一个分区开始写。


