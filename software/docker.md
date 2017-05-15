## Install Docker Community Edition for Ubuntu
[Docker Community Edition for Ubuntu](https://store.docker.com/editions/community/docker-ce-server-ubuntu?tab=description)


```
$ lsb_release -cs
$ sudo apt-get -y install apt-transport-https ca-certificates curl
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) stable"
$ sudo apt-get update

$ sudo apt-get -y install docker-ce

sudo docker run hello-world
write: connection reset by peer.

hp sudo docker pull hello-world
sudo docker run hello-world
```

## Manage Docker as a non-root user

[Post-installation steps for Linux](https://docs.docker.com/engine/installation/linux/linux-postinstall/)

```
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
$ Log out and log back in so that your group membership is re-evaluated.
$ docker run hello-world
```
## Configure Docker to start on boot

```
$ sudo systemctl enable docker  # start on boot
$ sudo systemctl disable docker # disable this behavior

If you need to add an HTTP Proxy, set a different directory or partition for the Docker runtime files, or make other customizations, see customize your systemd Docker daemon options.

$ sudo chkconfig docker on
chkconfig：未找到命令

$ sudo systemctl start docker
or
$ sudo service docker start
```

## Control and configure Docker with systemd

### Custom Docker daemon options

configuration file: /etc/docker/daemon.json

[Daemon configuration file](https://docs.docker.com/engine/reference/commandline/dockerd//#daemon-configuration-file)

#### Runtime directory and storage driver

$ sudo docker info

You may want to control the disk space used for Docker images, containers and volumes by moving it to a separate partition.

To accomplish this, set the following flags in the daemon.json file:
{
    "graph": "/mnt/docker-data",
    "storage-driver": "overlay"
}

#### HTTP proxy

DO NOT use the following method, use `hp [command]` instead.

```bash

$ mkdir -p /etc/systemd/system/docker.service.d
$ touch /etc/systemd/system/docker.service.d/http-proxy.conf 

```

Create a file that adds the HTTP_PROXY environment variable:

    [Service]
    Environment="HTTP_PROXY=http://proxy.example.com:80/"

If you have internal Docker registries that you need to contact without proxying you can specify them via the NO_PROXY environment variable:

    Environment="HTTP_PROXY=http://proxy.example.com:80/" "NO_PROXY=localhost,127.0.0.1"

Flush changes:

    $ sudo systemctl daemon-reload

Verify that the configuration has been loaded:

$ systemctl show --property=Environment docker
    Environment=HTTP_PROXY=http://proxy.example.com:80/

Restart Docker:

$ sudo systemctl restart docker




## Docker Engine user guide
[Docker Engine user guide](https://docs.docker.com/engine/userguide/)

Find and run the whalesay image
$ [docker pull docker/whalesay]
$ docker run docker/whalesay cowsay boo
$ docker images
 REPOSITORY           TAG         IMAGE ID            CREATED            SIZE
 docker/whalesay      latest      fb434121fc77        3 hours ago        247 MB
 hello-world          latest      91c95931e552        5 weeks ago        910 B
$ sudo docker run docker/whalesay cowsay where are you from?

## build your own image
[see](https://docs.docker.com/engine/getstarted/step_four/)

$ mkdir mydockerbuild
$ cd mydockerbuild
$ gedit Dockerfile

FROM docker/whalesay:latest
RUN apt-get -y update && apt-get install -y fortunes
CMD /usr/games/fortune -a | cowsay

$ docker build -t docker-whale ./ 
$ docker images
    REPOSITORY           TAG          IMAGE ID          CREATED             SIZE
    docker-whale         latest       c2c3152907b5      4 minutes ago       275.1 MB
    docker/whalesay      latest       fb434121fc77      4 hours ago         247 MB
    hello-world          latest       91c95931e552      5 weeks ago         910 B
$ docker run docker-whale

## Create a Docker Hub account and repository

Tag and push the image

$ docker images
$ docker tag 7d9495d03763 maryatdocker/docker-whale:latest
$ docker images
$ docker login
$ docker push frankwork/docker-whale

remove 
$ docker rmi -f 7d9495d03763


## Kali Linux
$ docker pull kalilinux/kali-linux-docker
[meta-package](https://www.kali.org/news/kali-linux-metapackages/)
$ docker run -i -t 8ececeaf404d /bin/bash 

## swift 

$ docker build -t swift31 ./ # it took times

or 

$ docker pull swiftdocker/swift
$ docker run --privileged -i -t --name swiftfun swiftdocker/swift:latest /bin/bash
$ docker start swiftfun
$ docker attach swiftfun

