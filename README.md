Description
===========

For use with Ubuntu 20.04 and Nomp as stratum https://github.com/cbunting99/node-open-mining-portal

### Please see the original page for the description and information regarding MPOS. 

https://github.com/MPOS/php-mpos


### Installation (May not be 100%) Ubuntu 20.04 + Nomp: (Link Above)

The original install information contains various sets of the same files, just different versions. I am trying to simplify the install and will update anything below as needed.

```
cd ~

sudo apt-get update

sudo apt-get dist-upgrade

sudo apt-get install git

sudo apt-get install build-essential libboost-all-dev libcurl4-openssl-dev libdb-dev libdb++-dev mysql-server

sudo apt-get install memcached php-memcached php-mysqlnd php-curl php-json php-curl libapache2-mod-php

sudo apt-get install php-mbstring php-dom php-zip zip

sudo apache2ctl -k stop; sleep 2; sudo apache2ctl -k start

cd

cd /var/www

sudo git clone https://github.com/cbunting99/php-mpos MPOS

cd MPOS

php composer.phar install (May need to run sudo php composer.phar install)

```

### (If you get connection issues below with mysql, try this then continue.) 
Replace password with a password.

```
sudo mysql

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

exit
```

### Then Continue:

```
sudo mysql -p -e "create database mpos"

sudo mysql -p mpos < sql/000_base_structure.sql

sudo chown -R www-data templates/compile templates/cache

sudo cp include/config/global.inc.dist.php include/config/global.inc.php
```

## Other stuff you may need for building coins.
```
sudo apt-get install libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils python3
```

## Berkley DB 4.8 
* For Ubuntu 20.04 and possibly newer versions:

```
sudo add-apt-repository ppa:luke-jr/bitcoincore

sudo apt-get update && sudo apt-get install libdb4.8-dev libdb4.8++-dev -y
```

* If you need to compile Berkeley DB;

```
wget http://download.oracle.com/berkeley-db/db-4.8.30.zip
unzip db-4.8.30.zip
cd db-4.8.30
cd build_unix/
../dist/configure --prefix=/usr/local --enable-cxx
make
make install
cd ..
```

### You can find a lot of info here, https://github.com/MPOS/php-mpos/wiki/Config-Setup