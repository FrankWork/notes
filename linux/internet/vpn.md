# install 

# shadowsocks-go

mkdir -p ~/bin/socks/
go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server 	# on server
go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-local 	# on client
cd $GOPATH/src/github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server
go build
mv shadowsocks-server ~/bin/socks
cd $GOPATH/src/github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-local 
go build
mv shadowsocks-local ~/bin/socks


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

防火墙开放shadowsocks服务端口(server side):

$ firewall-cmd --permanent --add-port=8888/tcp
$ firewall-cmd --reload


# usage

$ ./shadowsocks-server -c server.json # on server

$ ./shadowsocks-local -c client.json # on client
$ alias hp="http_proxy=socks5://127.0.0.1:1080"
$ hp curl ip.gs



