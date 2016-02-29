# Codeigniter MongoDB library

## 실행 환경
- Ubuntu 14.04
- PHP 7.x
- composer
- Codeigniter 3.x
- MongoDB 2.6.x


먼저 관리가 계정으로 변경 합니다.
``` bash
$ sudo -i
```
## PHP 7 Install
###### PHP install
``` bash
$ apt-get install python-software-properties
$ add-apt-repository ppa:ondrej/php
$ apt-get update
$ apt-get install -y php7.0 build-essential snmp php7.0-fpm php7.0-cli php7.0-common php7.0-json php7.0-opcache php7.0-mysql php7.0-odbc php7.0-sybase php7.0-phpdbg php7.0-dbg php7.0-gd php7.0-imap php7.0-ldap php7.0-pgsql php7.0-pspell php7.0-recode php7.0-snmp php7.0-tidy php7.0-dev php7.0-intl php7.0-gd php7.0-curl php7.0-bz2 php7.0-mcrypt php7.0-dev
```

###### Check PHP Version
``` bash
$ php -v 
PHP 7.0.1-4+deb.sury.org~trusty+1 (cli) ( NTS )
Copyright (c) 1997-2015 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2015 Zend Technologies
```

###### Composer Install
``` bash
$ curl -sS https://getcomposer.org/installer | php
$ mv composer.phar /usr/local/bin/composer
```

###### 참고
* http://tecadmin.net/install-php-7-on-ubuntu/

## MongDB 2.6.x install
1. Import the public key used by the package management system
``` bash
$ apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
```
2. Create a list file for MongoDB.
``` bash
$ echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | tee /etc/apt/sources.list.d/mongodb.list
```
3. Reload local package database.
``` bash
$ apt-get update
```
4. Install the MongoDB packages.
``` bash
$ apt-get install -y mongodb-org
# 또는 버전 지정
$ apt-get install -y mongodb-org=2.6.9 mongodb-org-server=2.6.9 mongodb-org-shell=2.6.9 mongodb-org-mongos=2.6.9 mongodb-org-tools=2.6.9
```
5. 사용자 추가 하기
``` bash
$ mongo
$ use admin
$ db.createUser( { user : "사용자아이디" , pwd : "암호" , roles : [ "readWrite" , "userAdmin" , "dbAdmin" , "clusterAdmin" , "dbAdminAnyDatabase", "userAdminAnyDatabase" ] } )
```
6. MongoDB 연결 설정
``` bash
$ sed -i "s/^bind_ip = 127.0.0.1/bind_ip = 0.0.0.0/" /etc/mongod.conf
$ sed -i "s/^#auth = true/auth = true/" /etc/mongod.conf
```
7. MongoDB restart
``` bash
$ service mongod restart
```


###### 참고
* https://docs.mongodb.org/v2.6/tutorial/install-mongodb-on-ubuntu/