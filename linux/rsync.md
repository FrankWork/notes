# install

```
$ sudo apt install rsync # debian、ubuntu
$ yum install rsync      # Fedora、Redhat
```

# usage

$ rsync -avh from to
$ rsync -avzh /mypath/myfile.gz pi@192.168.1.12:/mybackup/
$ rsync -avzh -e 'ssh -p 12345' /mypath/myfile.gz pi@192.168.1.12:/mybackup/
$ rsync -avh --delete myfolder/ backup/

