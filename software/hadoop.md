# install

```
$ mkdir -p /usr/java/
$ tar zxvf hadoop-2.7.4.tar.gz
$ cd hadoop-2.7.4/
$ sudo vim etc/hadoop/hadoop-env.sh
JAVA_HOME=/usr/java/jdk1.8.0_152
```

```
$ bin/hadoop
```

## config

```
$ sudo vim etc/hadoop/core-site.xml
```
```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
```

```
$ sudo vim etc/hadoop/hdfs-site.xml
```
```xml
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```

```
# log-in without password
$ ssh localhost

$ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
$ chmod 0600 ~/.ssh/authorized_keys
```

## start

```
$ bin/hdfs namenode -format
$ sbin/start-dfs.sh
```
NameNode - http://localhost:9870/

```
$ bin/hdfs dfs -mkdir input
$ bin/hdfs dfs -put etc/hadoop/*.xml input

$ bin/hdfs dfs -get output output
$ cat output/*
$ bin/hdfs dfs -cat output/*

$ sbin/stop-dfs.sh
```


