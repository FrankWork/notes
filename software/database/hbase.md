## install

```shell
$ sudo mkdir -p /usr/java/
$ sudo tar xzvf hbase-1.2.6-bin.tar.gz
$ cd hbase-1.2.6/

$ sudo vim conf/hbase-env.sh
JAVA_HOME=/usr/java/jdk1.8.0_152

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
```

### create table and ColumnFamily

```
hbase(main):001:0> create 'test', 'cf'
```

### list

```
hbase(main):002:0> list 'test'
```

### put

```
hbase(main):003:0> put 'test', 'row1', 'cf:a', 'value1'

hbase(main):004:0> put 'test', 'row2', 'cf:b', 'value2'

hbase(main):005:0> put 'test', 'row3', 'cf:c', 'value3'
```

### scan

```
hbase(main):006:0> scan 'test'

```

### get a row

```
hbase(main):007:0> get 'test', 'row1'

```

### disable

```
hbase(main):008:0> disable 'test'

hbase(main):009:0> enable 'test'
```

### Drop the table.

```
hbase(main):011:0> drop 'test'
```

### quit

```
hbase(main):011:0> quit
```

### stop 

```
$ sudo bin/stop-hbase.sh 
$ jps
5330 Jps
```