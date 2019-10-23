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

## hdfs shell

http://hadoop.apache.org/docs/r1.0.4/cn/hdfs_shell.html

```
查看文件
hadoop fs -ls url
cat文件到本地
hadoop fs -cat url > output
查看文件夹大小
hadoop fs -dus url
新建文件夹
hadoop fs -mkdir /test
删除文件夹
hadoop fs -rmr dir
本地文件复制到目标文件
hadoop fs -put localfile /user/hadoop/hadoopfile
hadoop fs -put localfile1 localfile2 /user/hadoop/hadoopdir
hadoop fs -put localfile hdfs://host:port/hadoop/hadoopfile
hadoop fs -put - hdfs://host:port/hadoop/hadoopfile

用户合并一个文件夹下面的所有文件至一个本地文件中
hadoop fs -getmerge <src> <localdst> [addnl]

跨集群ugi拷贝文件
hadoop distcp -su user,passwd -du user,passwd src dist


hadoop job -list
hadoop job -kill job_201212111628_11166
```

## hive

    INSERT OVERWRITE DIRECTORY
    '${HDFS_FILE_PRE}/${day}'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

	select * from 
