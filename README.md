# Redis
Redis is a free, open source key-value database. It is similar to memcached but the dataset is not volatile and other datatypes (such as lists and sets) are natively supported. Redis comes with redis-cli that provides a simple command-line interface to a Redis server. This tutorial walks you through how to install and configure Redis Server in Ubuntu. However this guide is same for other Ubuntu/Debian-based distros.
# Redis Web Link
https://redis.io/
# Install on Linux Mint 
```
sudo apt-get install redis-server
sudo systemctl status redis-server
sudo systemctl enable redis-server
sudo systemctl start redis-server
redis-server -v
```
