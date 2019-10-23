## install shadowsocks-go

wget https://github.com/shadowsocks/shadowsocks-go/releases/download/1.2.1/shadowsocks-server.tar.gz

```
mkdir -p ~/bin/socks/
go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server 	# on server
go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-local 	# on client

cd $GOPATH/src/github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server
go build
mv shadowsocks-server ~/bin/socks

cd $GOPATH/src/github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-local 
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
sudo apt install firewalld
$ firewall-cmd --permanent --add-port=8888/tcp
$ firewall-cmd --reload
```



# install v2ray

wget https://install.direct/go.sh
sudo bash go.sh
systemctl start v2ray

vi /etc/v2ray/config.json

{
  "inbounds": [
    {
      "port": 40827,
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "505f001d-4aa8-4519-9c54-6b65749ee3fb",
            "alterId": 64
          }
        ]
      },
      "streamSettings": {
        "network": "mkcp",
        "kcpSettings": {
          "uplinkCapacity": 5,
          "downlinkCapacity": 100,
          "congestion": true,
          "header": {
            "type": "none"
          }
        }
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    }
  ]
}


systemctl restart v2ray
firewall-cmd --zone=public --add-port=24556/udp --permanent
firewall-cmd --reload
vi /etc/rc.local
	systemctl restart v2ray

