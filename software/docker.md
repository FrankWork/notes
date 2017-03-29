## Docker Community Edition for Ubuntu
[Docker Community Edition for Ubuntu](https://store.docker.com/editions/community/docker-ce-server-ubuntu?tab=description)



1. Set up the repository

Set up the Docker CE repository on Ubuntu. The lsb_release -cs sub-command prints the name of your Ubuntu version, like xenial or trusty.

sudo apt-get -y install \
  apt-transport-https \
  ca-certificates \
  curl

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable"

sudo apt-get update

2. Get Docker CE

Install the latest version of Docker CE on Ubuntu:

sudo apt-get -y install docker-ce

3. Test your Docker CE installation

Test your installation:

sudo docker run hello-world
write: connection reset by peer.

hp sudo docker pull hello-world
sudo docker run hello-world


## Manage Docker as a non-root user

[Post-installation steps for Linux](https://docs.docker.com/engine/installation/linux/linux-postinstall/)

To create the docker group and add your user:

    Create the docker group.

    $ sudo groupadd docker

    Add your user to the docker group.

    $ sudo usermod -aG docker $USER

    Log out and log back in so that your group membership is re-evaluated.

    Verify that you can docker commands without sudo.

    $ docker run hello-world

    This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.

## Configure Docker to start on boot

Most current Linux distributions (RHEL, CentOS, Fedora, Ubuntu 16.04 and higher) use systemd to manage which services start when the system boots. Ubuntu 14.10 and below use upstart.
systemd

$ sudo systemctl enable docker

To disable this behavior, use disable instead.

$ sudo systemctl disable docker

If you need to add an HTTP Proxy, set a different directory or partition for the Docker runtime files, or make other customizations, see customize your systemd Docker daemon options.

chkconfig
$ sudo chkconfig docker on
chkconfig：未找到命令

## Control and configure Docker with systemd

### Start manually

Once Docker is installed, you will need to start the Docker daemon. Most Linux distributions use systemctl to start services. If you do not have systemctl, use the service command.

    systemctl:

    $ sudo systemctl start docker

    service:

    $ sudo service docker start


### Custom Docker daemon options

There are a number of ways to configure the daemon flags and environment variables for your Docker daemon. The recommended way is to use the platform-independent daemon.json file, which is located in /etc/docker/ on Linux by default. See [Daemon configuration file](https://docs.docker.com/engine/reference/commandline/dockerd//#daemon-configuration-file).

The default location of the configuration file on Linux is /etc/docker/daemon.json. The --config-file flag can be used to specify a non-default location.

You can configure nearly all daemon configuration options using daemon.json. The following example configures two options. One thing you cannot configure using daemon.json mechanism is a HTTP proxy.

#### Runtime directory and storage driver

sudo docker info

You may want to control the disk space used for Docker images, containers and volumes by moving it to a separate partition.

To accomplish this, set the following flags in the daemon.json file:

{
    "graph": "/mnt/docker-data",
    "storage-driver": "overlay"
}

#### HTTP proxy

DO NOT use the following method, use `hp [command]` instead.

The Docker daemon uses the HTTP_PROXY and NO_PROXY environmental variables in its start-up environment to configure HTTP proxy behavior. You cannot configure these environment variables using the daemon.json file.

This example overrides the default docker.service file.

If you are behind an HTTP proxy server, for example in corporate settings, you will need to add this configuration in the Docker systemd service file.

Create a systemd drop-in directory for the docker service:

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

Step 1: Write a Dockerfile
$ mkdir mydockerbuild
$ cd mydockerbuild
$ nano Dockerfile

Add a FROM statement by copying the following line into the file:

FROM docker/whalesay:latest

The FROM keyword tells Docker which image your image is based on. Whalesay is cute and has the cowsay program already, so we’ll start there.

Add a RUN statement which will install the fortunes program into the image.

RUN apt-get -y update && apt-get install -y fortunes

The whalesay image is based on Ubuntu, which uses apt-get to install packages. These two commands refresh the list of packages available to the image and install the fortunes program into it. The fortunes program prints out wise sayings for our whale to say.

Add a CMD statement, which tells the image the final command to run after its environment is set up. This command runs fortune -a and sends its output to the cowsay command.

CMD /usr/games/fortune -a | cowsay

Check your work. Your file should look just like this:
```
FROM docker/whalesay:latest
RUN apt-get -y update && apt-get install -y fortunes
CMD /usr/games/fortune -a | cowsay
```
Save the file and close the text editor. At this point, your software recipe is described in the Dockerfile file. You are ready to build a new image.

The `docker build -t docker-whale . `command reads the Dockerfile in the current directory and processes its instructions one by one to build an image called docker-whale on your local machine. The command takes about a minute and its output looks really long and complex. In this section, you learn what each message means.


Now you can verify that the new image is on your computer and you can run it.

    In a terminal window or command prompt, type docker images, which lists the images you have locally.

    $ docker images

    REPOSITORY           TAG          IMAGE ID          CREATED             SIZE
    docker-whale         latest       c2c3152907b5      4 minutes ago       275.1 MB
    docker/whalesay      latest       fb434121fc77      4 hours ago         247 MB
    hello-world          latest       91c95931e552      5 weeks ago         910 B

    Run your new image by typing docker run docker-whale.


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
docker pull kalilinux/kali-linux-docker
[meta-package](https://www.kali.org/news/kali-linux-metapackages/)
docker run -i -t 8ececeaf404d /bin/bash 

