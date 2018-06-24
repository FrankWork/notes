# install rpm without root

$ mkdir virtualbox
$ mv VirtualBox-5.1-5.1.18_114002_el7-1.x86_64.rpm vb.rpm
$ rpm2cpio vb.rpm | cpio -idv
$ ls
etc/  usr/  vb.rpm
$ mv virtualbox ~/bin/


## download only

```bash
sudo yum install --downloadonly --downloaddir=./ NetworkManager-wifi

```