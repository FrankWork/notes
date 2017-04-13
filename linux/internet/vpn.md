# install 

## centos server 
$ cd /etc/yum.repos.d/
$ wget https://copr.fedoraproject.org/coprs/librehat/shadowsocks/repo/epel-7/librehat-shadowsocks-epel-7.repo
$ yum update
$ yum install shadowsocks-libev

## ubuntu client
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5



# config

/etc/shadowsocks-libev/config.json

{
 "server":"0.0.0.0",
 "server_port":8888,
 "local_address": "127.0.0.1",
 "local_port":1080,
 "password":"mypassword",
 "timeout":300,
 "method":"aes-256-cfb",
}

防火墙开放shadowsocks服务端口:

$ firewall-cmd --permanent --add-port=8888/tcp
$ firewall-cmd --reload


# usage

运行服务端：
$ ss-server -c .ss-config.1.json
$ ss-server -c .ss-config.2.json

# 全局代理

sudo apt-get install polipo
sudo vim /etc/polipo/config

socksParentProxy = "localhost:1080" or "0.0.0.0:1080"
socksProxyType = socks5

sudo service polipo stop
sudo service polipo start

vim ~/.bashrc
alias hp="http_proxy=http://localhost:8123"
source ~/.bashrc

curl ip.gs
当前 IP：118.202.45.132 来自：中国辽宁沈阳东北大学 教育网
hp curl ip.gs
当前 IP：107.181.152.55 来自：美国加利福尼亚州洛杉矶alpharacks.com syn.ltd.uk

export http_proxy=http://localhost:8123
curl ip.gs
unset http_proxy



