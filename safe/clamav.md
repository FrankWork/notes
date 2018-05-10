## ClamAV

```bash
$ sudo apt install clamav
$ clamscan --help
$ sudo freshclam 

$ sudo clamscan -r --bell -i /usr/bin
/usr/bin/wkrhkmvpty: Unix.Trojan.DDoS_XOR-1 FOUND

$ sudo clamscan -r --remove /usr/bin
$ cat /root/usrclamav.log |grep FOUND
```
## Unix.Trojan.DDoS XOR-1

/etc/cron.hourly
/etc/init.d
/etc/rc1.d rc2.d ... rc5.d


/bin
/usr/bin
/lib


```bash
$ ll /etc/rc1.d
$ ll /etc/cron.hourly
-rwxr-xr-x   1 root root  228 5月  10 10:17 gcc.sh*

$ sudo chmod -x /etc/cron.hourly/*
$ cat /etc/crontab

$ ll /lib/libudev.so
-rwxr-xr-x 1 root root 612K 5月  10 10:24 /lib/libudev.so*
$ file /lib/libudev.so
/lib/libudev.so: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), statically linked, for GNU/Linux 2.6.9, not stripped

$ sudo chmod -x /lib/libudev.so
```

# 进程

```bash
ll /proc/xxx
lsof /usr/bin/*
pidof /usr/bin/*
```

# 定时任务

```
sudo vi /etc/crontab
sudo chattr +i /etc/crontab
```

## 最近变动文件

$ ls -lt /usr/bin/ | head

## 异常服务

```bash
systemctl | grep LSB
systecmctl stop xxx
vim /etc/systemd/system/xxx
```