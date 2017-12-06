# write 

## hbase

hbase(main):002:0> put 'test', 'row1', 'cf:a', 'value1'
0 row(s) in 0.1590 seconds

hbase(main):006:0> put 'test', 'row2', 'cf:b', 'value2'
0 row(s) in 0.0090 seconds

hbase(main):007:0> put 'test', 'row3', 'cf:c', 'value3'
0 row(s) in 0.0050 seconds

## mysql

insert into test_table(row, cf, value) values ('rowa', 'cf:a', 'value1');
Query OK, 1 row affected (0.04 sec)

MariaDB [test]> insert into test_table(row, cf, value) values ('rowb', 'cf:b', 'value2');
Query OK, 1 row affected (0.06 sec)

MariaDB [test]> insert into test_table(row, cf, value) values ('rowc', 'cf:c', 'value3');
Query OK, 1 row affected (0.03 sec)

## cassandra

INSERT INTO test_table (row_, cf, val) VALUES ('row1', 'cf:1', 'value1');
source_elapsed 6870 Nanosecond, 0.00000686 Second
hh:mm:ss[.fffffffff]
INSERT INTO test_table (row_, cf, val) VALUES ('row2', 'cf:2', 'value2');
source_elapsed 2272 Nanosecond, 0.00000227 Second
INSERT INTO test_table (row_, cf, val) VALUES ('row3', 'cf:3', 'value3');
source_elapsed 1783 Nanosecond





# scan 

## hbase

hbase(main):008:0> scan 'test'
ROW                   COLUMN+CELL                                               
 row1                 column=cf:a, timestamp=1510576073672, value=value1        
 row2                 column=cf:b, timestamp=1510577283481, value=value2        
 row3                 column=cf:c, timestamp=1510577358637, value=value3        
3 row(s) in 0.0260 seconds

## mysql868286

select * from test_table;
+------+------+--------+
| row  | cf   | value  |
+------+------+--------+
| rowa | cf:a | value1 |
| rowb | cf:b | value2 |
| rowc | cf:c | value3 |
+------+------+--------+
3 rows in set (0.00 sec)

## cassandra

SELECT * FROM test_table;

 row_ | cf   | val
------+------+--------
 row1 | cf:1 | value1
 row2 | cf:2 | value2
 row3 | cf:3 | value3

 8 ms


# read 


## hbase

hbase(main):009:0> get 'test', 'row1'
COLUMN                CELL                                                      
 cf:a                 timestamp=1510576073672, value=value1                     
1 row(s) in 0.0100 seconds


## mysql

select * from test_table where row='rowa';
+------+------+--------+
| row  | cf   | value  |
+------+------+--------+
| rowa | cf:a | value1 |
+------+------+--------+
1 row in set (0.00 sec)


## cassandra

SELECT * FROM test_table WHERE row_='row1';
 activity        | timestamp                  | source    | source_elapsed | client
Request complete | 2017-12-06 10:15:32.868286 | 127.0.0.1 |     2286       | 127.0.0.1