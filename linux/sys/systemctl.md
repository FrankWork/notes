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
