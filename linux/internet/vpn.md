## install shadowsocks-go

```
mkdir -p ~/bin/socks/
go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server 	# on server
go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-local 	# on client

cd $GOROOT/src/github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server
go build
mv shadowsocks-server ~/bin/socks

cd $GOROOT/src/github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-local 
go build
mv shadowsocks-local ~/bin/socks
```

## config

```
$ vim server.json
{
  "port_password": {
    "8888": "mypassword"
  },
  "timeout":300,
  "method":"aes-256-cfb"
}

$ vim client.json
{
  "server_password": [
    ["[x:x:ipv6::x:x]:8888", "mypassword", "aes-256-cfb"],
    ["x.x.x.x:8888", "mypassword", "aes-256-cfb"]
  ]
  "local_port":1080,

  "timeout":300,
}
```

## usage

```
$ ./shadowsocks-server -c server.json # on server

$ ./shadowsocks-local -c client.json # on client
$ alias hp="http_proxy=socks5://127.0.0.1:1080"
$ hp curl ip.gs
```

## optional

### start on boot

```
$ vim /etc/systemd/system/shadowsocks-server.service

[Unit]
Description=Shadowsocks Server
After=network.target

[Service]
ExecStart=/usr/local/bin/ssserver -c /etc/shadowsocks/ss-config.json
Restart=always

[Install]
WantedBy=multi-user.target

$ sudo systemctl enable shadowsocks-server
$ sudo systemctl start shadowsocks-server
$ systemctl status shadowsocks-server
```

### firewall

防火墙开放shadowsocks服务端口(server side):
```
$ firewall-cmd --permanent --add-port=8888/tcp
$ firewall-cmd --reload
```




