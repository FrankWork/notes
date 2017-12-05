# install

```
$ java -version # require java 8
$ sudo mkdir -p /usr/java/
$ sudo cp apache-cassandra-3.11.1-bin.tar.gz /usr/java
$ sudo tar -zxvf apache-cassandra-3.11.1-bin.tar.gz # 37M
$ cd apache-cassandra-3.11.1
$ bin/cassandra -f # start
$ bin/nodetool status
$ pgrep -f CassandraDaemon # stop
$ kill pid

```