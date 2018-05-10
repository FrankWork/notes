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
