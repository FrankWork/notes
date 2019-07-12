# [cli](https://www.sqlite.org/cli.html)

```
$ sqlite3 data.db
sqlite> .databases
sqlite> .fullschema
sqlite> .read ex1.sql
sqlite> .separator "\t"
sqlite> .import ex1.tsv tableA
sqlite> select * from table;

sqlite>.open ex1.db
sqlite>.save ex1.db
sqlite> create table tbl1(one varchar(10), two smallint);
sqlite> insert into tbl1 values('hello!',10);
sqlite> insert into tbl1 values('goodbye', 20);
sqlite> .headers on
sqlite> select * from tbl1;

sqlite> CREATE TABLE tbl2 (
   ...>   f1 varchar(30) primary key,
   ...>   f2 text,
   ...>   f3 real
   ...> );

CREATE TABLE artist(
  artistid    INTEGER PRIMARY KEY, 
  artistname  TEXT
);

CREATE TABLE track(
  trackid     INTEGER, 
  trackname   TEXT, 
  trackartist INTEGER,
  FOREIGN KEY(trackartist) REFERENCES artist(artistid)
);

CREATE TABLE parent(a PRIMARY KEY, b UNIQUE, c, d, e, f);
CREATE UNIQUE INDEX i1 ON parent(c, d);
CREATE INDEX i2 ON parent(e);
CREATE UNIQUE INDEX i3 ON parent(f COLLATE nocase);

```
 
# [data type](https://www.sqlite.org/datatype3.html)

- NULL. The value is a NULL value.
- INTEGER. The value is a signed integer, stored in 1, 2, 3, 4, 6, or 8 bytes depending on the magnitude of the value.
- REAL. The value is a floating point value, stored as an 8-byte IEEE floating point number.
- TEXT. The value is a text string, stored using the database encoding (UTF-8, UTF-16BE or UTF-16LE).
- BLOB. The value is a blob of data, stored exactly as it was input.

## date time 


- TEXT as ISO8601 strings ("YYYY-MM-DD HH:MM:SS.SSS").
- REAL as Julian day numbers, the number of days since noon in Greenwich on November 24, 4714 B.C. according to the proleptic Gregorian calendar.
- INTEGER as Unix Time, the number of seconds since 1970-01-01 00:00:00 UTC. 

