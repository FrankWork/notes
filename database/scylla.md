C++ Cassandra

fuck! can't compile

```bash
cd /etc/sysconfig/network-scripts/
ifup ifcfg-enp0s3
vi ifcfg-enp0s3 
    ONBOOT=yes

firewall-cmd --zone=public --add-port=9042/tcp --permanent
firewall-cmd --reload


git clone https://github.com/scylladb/scylla.git
cd scylla
git submodule update --init --recursive
sudo ./install-dependencies.sh

./configure.py --mode=release

ninja-build -j8
./build/release/scylla

./build/release/scylla --datadir tmp --commitlog-directory tmp --smp 1
./build/release/scylla --help
```

