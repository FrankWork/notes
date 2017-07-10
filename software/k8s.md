# install


## cubeadm



## centos
$ yum install -y etcd kubernetes # k8s 77M/380M
$ systemctl start etcd
$ systemctl start docker
$ systemctl start kube-apiserver
$ systemctl start kube-controller-manager
$ systemctl start kube-scheduler
$ systemctl start kubelet
$ systemctl start kube-proxy

## ubuntu

sudo apt install snapd
newgrp lxd
sudo usermod -a -G lxd $USER
sudo snap install conjure-up --classic
conjure-up kubernetes  # re-login may be required at that point if you just installed snap utility


## other 
https://github.com/kubernetes/kubernetes/releases

$ tar zxvf kubernetes.tar.gz
$ cd kubernetes
$ ls 
client/   docs/      federation/  README.md  third_party/  version
cluster/  examples/  LICENSES    server/     Vagrantfile
$ cluster/get-kube-binaries.sh
Will download kubernetes-server-linux-amd64.tar.gz from https://storage.googleapis.com/kubernetes-release/release/v1.6.3
Will download and extract kubernetes-client-linux-amd64.tar.gz from https://storage.googleapis.com/kubernetes-release/release/v1.6.3
Is this ok? [Y]/n

Add '/home/frank/bin/kubernetes/client/bin' to your PATH to use newly-installed binaries.


