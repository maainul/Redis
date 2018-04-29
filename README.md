# Redis
Redis is a free, open source key-value database. It is similar to memcached but the dataset is not volatile and other datatypes (such as lists and sets) are natively supported. Redis comes with redis-cli that provides a simple command-line interface to a Redis server. This tutorial walks you through how to install and configure Redis Server in Ubuntu. However this guide is same for other Ubuntu/Debian-based distros.
# Redis Web Link https://redis.io/

# Install on Linux Mint 
```
sudo apt-get install redis-server
sudo systemctl status redis-server
sudo systemctl enable redis-server
sudo systemctl start redis-server
redis-server -v
```

# REDIS LIST
#### Push value into the list
```
127.0.0.1:6379>	LPUSH num 1234
(integer)4
127.0.0.1:6379>	LRANGE num 0 10
1)"4"
2)"3"
3)"2"
4)"1"
```
#### PUSH new value on the top
```
127.0.0.1:6379>LPUSH num 5
(integer)5	
127.0.0.1:6379>	LRANGE num 0 10
1)"5"
2)"4"
3)"3"
4)"2"
5)"1"
```
#### POP Value from the top
```
127.0.0.1:6379>Lpop num "5"	
127.0.0.1:6379>	LRANGE num 0 10
1)"4"
2)"3"
3)"2"
4)"1"
```
#### PUSH to the bottom using RPUSH
```
127.0.0.1:6379>RPUSH num "6"
127.0.0.1:6379>	LRANGE num 0 10
1)"4"
2)"3"
3)"2"
4)"1"
5)"6"
```
#### POP from the bottom using RPOP
```
127.0.0.1:6379>RPOP num "6"
127.0.0.1:6379>	LRANGE num 0 10
1)"4"
2)"3"
3)"2"
4)"1"
```
#### Length of the list using LLEN
```
127.0.0.1:6379>LLEN num
(integer)5
127.0.0.1:6379>	LRANGE num 0 10
1)"4"
2)"3"
3)"2"
4)"1"
5)"6"
```
#### Get value from specific index using LINDEX
```
127.0.0.1:6379>	LRANGE num 0 10
1)"4"
2)"3"
3)"2"
4)"1"
5)"6"
127.0.0.1:6379>LINDEX num 4
"6"
```
#### Insert value into middle using LSET
```
127.0.0.1:6379>	LSET num 2 8
ok
127.0.0.1:6379>LRANGE num 0 10
1)"4"
2)"3"
3)"8"
4)"1"
5)"6"
```
#### Show all the elements in the list
```
127.0.0.1:6379>LRANGE num 0 -1
1)"4"
2)"3"
3)"8"
4)"1"
5)"6"
```
#### LPUSHX if key exist then this command is successful
```
127.0.0.1:6379>LPUSHX num 7
(integer)6
127.0.0.1:6379>LRANGE num 0 -1
1)"7"
2)"4"
3)"3"
4)"8"
5)"1"
6)"6"
127.0.0.1:6379>LPUSHX sub 12345
(integer)0
```
#### PUSH value befor specific value
```
127.0.0.1.6379>LINSERT num before 1 251
(integer)7
127.0.0.1:6379>LRANGE num 0 -1
1)"7"
2)"4"
3)"3"
4)"8"
5)251
5)"1"
7)"6"
```
#### PUSH value after specific value
```
127.0.0.1.6379>LINSERT num after 1 252
(integer)7
127.0.0.1:6379>LRANGE num 0 -1
1)"7"
2)"4"
3)"3"
4)"8"
5)251
5)"1"
7)"252"
8)"6"
```
# REDIS SETS

#### ADD into set
```
127.0.0.1.6379>SADD myset1 1234
(integer)4
127.0.0.1:6379>SMEMBERS myset1
1)"1"
2)"2"
3)"3"
4)"4"

127.0.0.1.6379>SADD myset1 3//Set doesnot support duplicate key
(integer)0
127.0.0.1:6379>SMEMBERS myset1
1)"1"
2)"2"
3)"3"
4)"4"

127.0.0.1.6379>SADD myset1 5
(integer)1
127.0.0.1:6379>SMEMBERS myset1
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
```
#### How many members in the set
```
127.0.0.1.6379>SCARD myset1
(integer)5
127.0.0.1:6379>SMEMBERS myset1
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
```
#### 1.ADD new set
```
127.0.0.1.6379>SADD myset2 10 11 12 13 14 
(integer)5
127.0.0.1.6379>SMEMBERS myset2
1)"10"
2)"11"
3)"12"
4)"13"
5)"14"
6)"15"
127.0.0.1:6379>SADD my set2 15
(integer)1
1)"10"
2)"11"
3)"12"
4)"13"
5)"14"
6)"15"
127.0.0.1:6379>SADD myset2 1 2 3 
127.0.0.1:6379>SMEMBERS myset2 
1)"1"
2)"2"
3)"3"
4)"10"
5)"11"
6)"12"
7)"13"
8)"14"
9)"15"
```
#### 2.Substructure set from one set to another set (check difference)
```
127.0.0.1:6379>SMEMBERS myset1
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
127.0.0.1:6379>SMEMBERS myset2
(integer)1
1)"1"
2)"2"
3)"3"
4)"10"
5)"11"
6)"12"
7)"13"
8)"14"
9)"15"
127.0.0.1:6379>SDIFF myset1 myset2
1)"4"
2)"5"
127.0.0.1:6379>SDIFF myset2 myset1
1)"10"
2)"11"
3)"12"
4)"13"
5)"14"
6)"15"
```
#### 3.If we want to know the SDIFF snd save it in the third set then..
```
127.0.0.1:6379>SMEMBERS myset1
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
127.0.0.1:6379>SMEMBERS myset2
1)"1"
2)"2"
3)"3"
4)"10"
5)"11"
6)"12"
7)"13"
8)"14"
9)"15"
127.0.0.1:6379>SDIFF myset1 myset2
1)"4"
2)"5"
127.0.0.1:6379>SDIFF myset2 myset1
1)"10"
2)"11"
3)"12"
4)"13"
5)"14"
6)"15"
127.0.0.1:6379>SDIFFSTORE myset3 myset1 myset2
(integer)2
127.0.0.1:6379>SMEMBERS myset3
1)"4"
2)"5"
127.0.0.1:6379>SDIFFSTORE myset4 myset2 myset1
(integer)6
127.0.0.1:6379>SMEMBERS myset3
1)"10"
2)"11"
3)"12"
4)"13"
5)"14"
6)"15"
```
#### 4.Union two set
```
127.0.0.1:6379>SUNION myset1 myset2
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
6)"10"
7)"11"
8)"12"
9)"13"
10)"14"
11)"15"
```
#### 5.Store union set value in another set
```
127.0.0.1:6379>SUNIONSTORE myset5 myset1 myset2
(integer)11
127.0.0.1:6379>SMEMBERS myset5
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
6)"10"
7)"11"
8)"12"
9)"13"
10)"14"
11)"15"
```
Remove members from the set
```
127.0.0.1:6379>SMEMBERS myset5
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
6)"10"
7)"11"
8)"12"
9)"13"
10)"14"
11)"15"
127.0.0.1:6379>SREM myset5 15
(integer)1
127.0.0.1:6379>SMEMBERS myset5
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
6)"10"
7)"11"
8)"12"
9)"13"
10)"14"
```
#### 6.Remove random value from set
```
127.0.0.1:6379>SMEMBERS myset5
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
6)"10"
7)"11"
8)"12"
9)"13"
10)"14"
127.0.0.1:6379>SPOP myset5 "5"
127.0.0.1:6379>SMEMBERS myset5
1)"1"
2)"2"
3)"3"
4)"4"
5)"10"
6)"11"
7)"12"
8)"13"
9)"14"
127.0.0.1:6379>SPOP myset5 3
127.0.0.1:6379>SMEMBERS myset5
1)"1"
2)"2"
4)"4"
5)"10"
6)"11"
7)"12"
8)"13"
9)"14"
```
#### 7.Insertion between two sets
```
127.0.0.1:6379>SMEMBERS set1
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
127.0.0.1:6379>SMEMBERS set2 
1)"1"
2)"2"
3)"3"
4)"10"
5)"11"
6)"12"
7)"13"
8)"14"
9)"15"
127.0.0.1:6379>SINSERT myset1 myset2
1)"1"
2)"2"
3)"3"
```
#### 8.Insertion value store another set
```
127.0.0.1:6379>SINSERT myset1 myset2
1)"1"
2)"2"
3)"3"
127.0.0.1:6379>SINSERTSTORE myset6 myset1 myset2
(integer)3
127.0.0.1:6379>SMMBERS myset6
1)"1"
2)"2"
3)"3"
```
#### 9.SMOVE cmd used to move value from one set to another set
```
127.0.0.1:6379>SMEMBERS set1
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
127.0.0.1:6379>SMEMBERS set2 
1)"1"
2)"2"
3)"3"
4)"10"
5)"11"
6)"12"
7)"13"
8)"14"
9)"15"
127.0.0.1:6379>SMOVE myset1 myset2 5
(integer)1
127.0.0.1:6379>SMEMBERS myset2
1)"1"
2)"2"
3)"3"
4)"4"
5)"5"
6)"10"
7)"11"
8)"12"
9)"13"
10)"14"
11)"15"
```
