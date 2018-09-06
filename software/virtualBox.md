


cd /etc/sysconfig/network-scripts/
ifup ifcfg-enp0s3
vi ifcfg-enp0s3 
    ONBOOT=yes

firewall-cmd --zone=public --add-port=9042/tcp --permanent
firewall-cmd --reload