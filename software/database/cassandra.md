# install

```
$ java -version # require java 8
$ sudo mkdir -p /usr/java/
$ sudo cp apache-cassandra-3.11.1-bin.tar.gz /usr/java
$ sudo tar -zxvf apache-cassandra-3.11.1-bin.tar.gz # 37M
```


# configuration

conf/cassandra.yaml

runtime 

- cluster_name: the name of your cluster.
- seeds: a comma separated list of the IP addresses of your cluster seeds.
- storage_port: make sure that there are no firewalls blocking this port.
- listen_address: the IP address of your node, this is what allows other nodes to communicate with this node so it is important that you change it. Alternatively, you can set listen_interface to tell Cassandra which interface to use, and consecutively which address to use. Set only one, not both.
- native_transport_port: as for storage_port, make sure this port is not blocked by firewalls as clients will communicate with Cassandra on this port.

directories

- data_file_directories: one or more directories where data files are located.
- commitlog_directory: the directory where commitlog files are located.
- saved_caches_directory: the directory where saved caches are located.
- hints_directory: the directory where hints are located.


# start 

```
$ cd apache-cassandra-3.11.1
$ bin/cassandra -f # start
$ bin/nodetool status
$ pgrep -f CassandraDaemon # stop
$ kill pid

```

# Inserting and querying

```
$ bin/cqlsh localhost
cqlsh> SELECT cluster_name, listen_address FROM system.local;
```
