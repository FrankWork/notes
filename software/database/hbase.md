## install

```shell
$ sudo mkdir -p /usr/java/
$ sudo tar xzvf hbase-1.2.6-bin.tar.gz
$ cd hbase-1.2.6/

$ sudo vim conf/hbase-env.sh
JAVA_HOME=/usr/java/jdk-9.0.1

$ sudo adduser testuser
$ sudo vim conf/hbase-site.xml
```
```xml
<configuration>
  <property>
    <name>hbase.rootdir</name>
    <value>file:///home/testuser/hbase</value>
  </property>
  <property>
    <name>hbase.zookeeper.property.dataDir</name>
    <value>/home/testuser/zookeeper</value>
  </property>
</configuration>
```

```
$ sudo bin/start-hbase.sh 
$ jps
5330 Jps
```

Go to http://localhost:16010 to view the HBase Web UI


## usage

```
$ bin/hbase shell
ArgumentError: wrong number of arguments (0 for 1)
```