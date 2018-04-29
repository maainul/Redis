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
