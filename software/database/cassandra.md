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
$ bin/cassandra -f # -fR as root
$ bin/nodetool status
$ pgrep -f CassandraDaemon # stop
$ kill pid

```

# Inserting and querying

```sql
$ bin/cqlsh localhost
cqlsh> SELECT cluster_name, listen_address FROM system.local;
cqlsh> TRACING ON
```

```SQL
CREATE KEYSPACE Testspace
    WITH replication = {'class': 'SimpleStrategy', 'replication_factor' : 1}
    AND durable_writes = false;

DESCRIBE keyspaces;

USE Testspace;

CREATE TABLE test_table (row_ text PRIMARY KEY, cf text, val text );

INSERT INTO test_table (row_, cf, val) VALUES ('row1', 'cf:1', 'value1');
INSERT INTO users (id, lastname) VALUES (999, 'Sparrow')  IF NOT EXISTS

BEGIN BATCH
  INSERT INTO purchases (user, balance) VALUES ('user1', -8) USING TIMESTAMP 19998889022757000;
  INSERT INTO purchases (user, expense_id, amount, description, paid)
    VALUES ('user1', 1, 8, 'burrito', false);
APPLY BATCH;

SELECT * FROM test_table;

SELECT * FROM test_table WHERE row_='row1';
SELECT * FROM test_table WHERE row_='row1' ALLOW FILTERING;
SELECT count(*) FROM users;


DELETE FROM news_tb where uuid='row1';
TRUNCATE news_tb;
```

# [CQL](http://cassandra.apache.org/doc/latest/cql/index.html)

```SQL

CREATE KEYSPACE Excelsior
    WITH replication = {'class': 'SimpleStrategy', 'replication_factor' : 1}
    AND durable_writes = false;

USE Excelsior;

ALTER KEYSPACE Excelsior
    WITH replication = {'class': 'SimpleStrategy', 'replication_factor' : 4};

DROP KEYSPACE Excelsior;



CREATE TABLE monkeySpecies (
    species text PRIMARY KEY,
    common_name text,
    population varint,SELECT name, occupation FROM users WHERE userid IN (199, 200, 207);
SELECT JSON name, occupation FROM users WHERE userid = 199;
SELECT name AS user_name, occupation AS user_occupation FROM users;

SELECT time, value
FROM events
WHERE event_type = 'myEvent'
  AND time > '2011-02-03'
  AND time <= '2012-01-01'

SELECT COUNT (*) AS user_count FROM users;
    average_size int
) WITH comment='Important biological records'
   AND read_repair_chance = 1.0;

CREATE TABLE timeline (
    userid uuid,SELECT name AS user_name, occupation AS user_occupation FROM users;

    posted_month int,
    posted_time uuid,
    body text,
    posted_by text,
    PRIMARY KEY (userid, posted_month, posted_time)
) WITH compaction = { 'class' : 'LeveledCompactionStrategy' };

CREATE TABLE loads (
    machine inet,
    cpu int,
    mtime timeuuid,
    load float,
    PRIMARY KEY ((machine, cpu), mtime)
) WITH CLUSTERING ORDER BY (mtime DESC);

CREATE TABLE t (
    pk int,
    t int,
    v text,
    s text static,
    PRIMARY KEY (pk, t)
);

INSERT INTO t (pk, t, v, s) VALUES (0, 0, 'val0', 'static0');
INSERT INTO t (pk, t, v, s) VALUES (0, 1, 'val1', 'static1');

SELECT * FROM t;


SELECT name, occupation FROSELECT * FROM test_table WHERE row_='row1';M users WHERE userid IN (199, 200, 207);
SELECT JSON name, occupation FROM users WHERE userid = 199;
SELECT name AS user_name, occupation AS user_occupation FROM users;

SELECT time, value
FROM events
WHERE event_type = 'myEvent'
  AND time > '2011-02-03'
  AND time <= '2012-01-01'

SELECT COUNT (*) AS user_count FROM users;
```