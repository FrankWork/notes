# install

//================================================================================
 Package            架构             版本                  源              大小
//================================================================================
正在安装:
 redis              x86_64           3.2.3-1.el7           epel           527 k
为依赖而安装:
 jemalloc           x86_64           3.6.0-1.el7           epel           105 k

事务概要
//================================================================================
安装  1 软件包 (+1 依赖软件包)

总下载量：631 k
安装大小：2.6 M


## ubuntu
sudo apt-get install redis-server
sudo systemctl start redis

## centos
$ yum install redis
$ systemctl start redis

## config

$ redis-cli
> info
config_file:

$ vim /etc/redis/redis.conf # ubuntu
$ vi /etc/redis.conf        # centos
```
 #bind 127.0.0.1
requirepass your_redis_master_password

```
$ systemctl restart redis

$ firewall-cmd --permanent --add-port=6379/tcp
$ firewall-cmd --reload
阿里云设置安全组


# 命令行客户端

$redis-cli -h 127.0.0.1 -p 6379
$redis-cli PING
$redis-cli

# set get

>PING
> echo hi
>incr foo
>get foo
> get noexists
>keys *
>select 1 # 切换到数据库1

?	匹配一个字符
*	匹配任意个（包括０个）字符
[]	匹配括号间的任一字符，可以用“-”号表示一个范围
\x	匹配字符x，x为转义字符

>set bar 1
>keys *
>exists bar
>exists no
>del bar
>type foo
string, hash, list, set, zset
>lpush bar 1
>incrby bar 2
>decr bar
>decrby bar 5
>incrbyfloat bar 2.7
>incrbyfloat bar 5e+4
>append key " world!"
>strlen key
>set key 你好
>mset key1 v1 key2 v2 key3 v3
>get key2
>mget key1 key3
>set foo bar
>getbit foo 0
>getbit foo 6
>getbit foo 10000000000
>setbit foo 6 0
>setbit foo 7 1
>setbit nofoo 10 1
>bitcount foo
>bitcount foo 0 1
>set foo1 bar
>set foo2 aar
>bitop or res foo1 foo2
>get res

## 散列类型
>hset car price 500
>hset car name BMW
>hget car name
>hmset car price 500 name BMW
>hmget car price name
>hgetall car
>hexists car model
>hsetnx key field value
>hincrby person score 60
>hdel car price
>hkeys car
>hvals car
>hlen car

## 列表类型
>lpush numbers 1
>lpush numbers 2 3
>rpush numbers 0 -1
>lpop numbers
>rpop numbers
>llen numbers
>lrange numbers 0 2
>lrange numbers -2 -1
>lrange numbers 1 999
>lrem numbers -1 2
>lrange numbers 0 -1
>lindex numbers 0
>lindex numbers -1
>lset numbers 1 7
>lindex numbers 1 7
>ltrim numbers 1 2
>lrange numbers 0 1
>linsert numbers after 7 3
>linsert numbers before 2 1
>rpoplpush source destination
## 集合类型
>sadd letters a
>sadd letters a b c
>srem letters c d
>smembers letters
>sismember letters a
>sadd setA 1 2 3
>sadd setB 2 3 4
>sdiff setA setB
>sdiff setB setA
>sadd setC 2 3
>sdiff setA setB setC
>sinter setA setB
>sinter setA setB setC
>sunion setA setB
>sunion setA setB setC
>smembers letters
>scard letters
>sdiffstore dest key [key ...]
>sINTERstore dest key [key ...]
>sunionstore dest key [key ...]
>srandmember letters
>srandmember letters 2
>srandmembers letters -2
>spop letters
## 有序集合
>zadd score 89 tom 67 peter 100 david
>zadd score 76 peter
>zadd test 17e+307 a
>zadd test 1.5 b
>zadd test +inf c
>zadd test -inf d
>zscore score tom
>zrange score 0 2
> zrange score 1 -1
>zrange score 0 -1 withscores
>zadd chinese 0 马华 0 刘墉 0 司马光 
>zrevrange chinese 0 -1
>zrangebyscore key min max [withscores] [limit offset count]
>zrangebyscore score 80 (100
>zrangebyscore score 60 +inf limit 1 3
>zrevrangebyscore score 100 0 limit 0 3
>zincrby score 4 jerry
>zcard score
>zount score 90 100
>zrem score wendy
>zremrangebyrank score 0 2
>zremrangebyscore score (4 5
>zrank score peter
>zrevrank peter
>zinterstore destination numkeys key [key ...] [weights weight [weight ...]] [aggregate sum|min|max]
>zunionstore destination numkeys key [key ...] [weights weight [weight ...]] [aggregate sum|min|max]
## 事物
>multi
>sadd "user:1:following" 2
>sadd "user:2:following" 1
>exec

>set key 1
>watch key
>set key 2
>multi
>set key 3
>exec

>watch key 
>unwatch
## 生存时间，单位秒
>set session:29e3d uid1314
>expire session:29e3d 900
>ttl session:29e3d
>set foo bar
>expire foo 20
>persist foo
>ttl foo
pexpire, expireat, pexpireat

>sort tag:ruby:posts
>sort mylist
>sort mylistalpha alpha
>sort tag:ruby:posts desc
>sort tag desc limit 1 2
>sort tag:ruby:posts by post:*->time desc
>sort tag:ruby:posts by post:*->time desc get post:*->title
>sort tag:ruby:posts by post:*->time desc get post:*->title get post:*->time
>sort tag:ruby:posts by post:*->time desc get post:*->title get #
>sort mylist store sort.result
>brpop queue 0
>blpop queue 0
>llen queue

>PUBLISH channel.1 hi
>SUBSCRIBE channel.1
>PSUBSCRIBE channel.?*
>SET foo bar
>OBJECT ENCODING foo

## 备份

> SAVE
> CONFIG GET dir
$ systemctl stop redis
$ scp /var/lib/redis/dump.rdb $ali:/var/lib/redis/
$ systemctl restart redis


