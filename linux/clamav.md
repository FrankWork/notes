```bash
$ sudo apt install clamav
$ clamscan --help

$ sudo clamscan -r --bell -i /usr/bin
/usr/bin/wkrhkmvpty: Unix.Trojan.DDoS_XOR-1 FOUND

----------- SCAN SUMMARY -----------
Known viruses: 6495532
Engine version: 0.99.4
Scanned directories: 1
Scanned files: 1716
Infected files: 1
Data scanned: 377.11 MB
Data read: 517.47 MB (ratio 0.73:1)
Time: 59.176 sec (0 m 59 s)

$ sudo clamscan -r --remove /usr/bin

```
## Unix.Trojan.DDoS XOR-1

```bash
$ ll /etc/cron.hourly
总用量 44K
drwxr-xr-x   2 root root 4.0K 5月  10 10:17 ./
drwxr-xr-x 154 root root  12K 5月  10 10:17 ../
-rwxr-xr-x   1 root root  228 5月  10 10:17 gcc.sh*
-rwxr-xr-x   1 root root  150 5月   6 16:01 icrqhdmlcdlan.sh*
-rwxr-xr-x   1 root root  144 5月  10 10:17 ipzmzil.sh*
-rwxr-xr-x   1 root root  145 5月   6 16:01 jebwhfwv.sh*
-rwxr-xr-x   1 root root  144 5月   6 16:01 kcsahdk.sh*
-rw-r--r--   1 root root  102 4月   6  2016 .placeholder
-rwxr-xr-x   1 root root  150 5月   6 16:01 wmujouljbdvsh.sh*

$ sudo chmod -x /etc/cron.hourly/*
$ ll /lib/libudev.so
-rwxr-xr-x 1 root root 612K 5月  10 10:24 /lib/libudev.so*
$ sudo chmod -x /lib/libudev.so
$ cat /etc/crontab
```

