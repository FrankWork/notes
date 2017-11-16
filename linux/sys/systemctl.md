# Systemd

## start and stop service
```
sudo systemctl start app.service
sudo systemctl start app

sudo systemctl stop app
```

## restart and reload

```
sudo systemctl restart app
sudo systemctl reload app # reload config file withoud restarting
```

## enable start on boot

```
sudo systemctl enable app
sudo systemctl disable app
```

## check status

```
systemctl status app
systemctl is-active app
systemctl is-enabled app
systemctl is-failed app
```

## custom service

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

$ systemctl enable shadowsocks-server
$ systemctl start shadowsocks-server
```