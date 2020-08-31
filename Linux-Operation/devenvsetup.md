# dev env setup

## 20180522

> tried but fail

```
CREATE EXTENSION postgis;
CREATE EXTENSION postgis_topology;
```

## 20180518

### login to remove Linux server as root without password

1. [easy way](https://blog.csdn.net/oLiHongMing/article/details/79951603)
2. [more complete way](https://blog.csdn.net/universe_hao/article/details/52296811)
3. Here is my way

> Login to local Linux server as root
> generate private and public key

```
[root@SHYG ~]# ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
95:50:b9:b0:63:a5:aa:61:3a:28:49:a6:2f:3e:6f:8e root@SHYG.CentOS
The key's randomart image is:
+--[ RSA 2048]----+
|        ....     |
|        ..o.     |
|         =o.     |
|        =..      |
|       oS.       |
| o  o .          |
|+o o o           |
|*.+..            |
|oE*+             |
+-----------------+
[root@SHYG ~]# ^C
[root@SHYG ~]# 
```

> check the generated key

```
[root@SHYG ~]# cd .ssh
[root@SHYG .ssh]# ls
id_rsa  id_rsa.pub  known_hosts
```

> copy public key to remove server

```
[root@SHYG .ssh]# ssh-copy-id 39.106.193.149
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@39.106.193.149's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh '39.106.193.149'"
and check to make sure that only the key(s) you wanted were added.
```

> login to remove server as root and check

```
[root@1core2g201802 ~]# cd .ssh
[root@1core2g201802 .ssh]# cat authorized_keys 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDJZltn44S6Ry4gJwWkiPELDwoCYCH9cFaUUQAhYkWRdWXqO0Kc6UrC5O53n7IzLif0S6xKGSR4W8Sq82sIwRsagjTfolaSUjkajP8gn2XbCFoj0hJpQBGs5pAzJnwLq/DKkvwLfVEUAuaQhPiY9dhNqOKBasq22XRleYH7um2EBNd+brcUEa6PtCE+R0lAp70FouTnifKUBmUcZgK+6G+N2wy29r3yDdJxCnLBcO4mxy04pV8YFVrvzufU5BsvLxts7DdVQxFO3pgj+icoV9DvQHC9GbBqfuNJ7sPpmZy75vsjaTs2kEHGFcvl4aF/oZk3oeN5dprgIkCmn5JHvGcV root@SHYG.CentOS
[root@1core2g201802 .ssh]# 
```

> try to login from local to remove without password

```
[root@SHYG .ssh]# ssh '39.106.193.149'
Last login: Fri May 18 13:36:33 2018 from 101.81.137.116

Welcome to Alibaba Cloud Elastic Compute Service !

[root@1core2g201802 ~]# 
[root@1core2g201802 ~]# 
[root@1core2g201802 ~]# 
[root@1core2g201802 ~]# ls
dump.rdb                           node-v8.9.4-linux-x64         projects                                redis-4.0.8
erlang-solutions-1.0-1.noarch.rpm  node-v8.9.4-linux-x64.tar.xz  rabbitmq-server-3.7.4-1.el7.noarch.rpm  redis-4.0.8.tar.gz
[root@1core2g201802 ~]# 
```

### Jenkins

[Reference](https://blog.csdn.net/tragedyxd/article/details/51861526)

> ***remember to 'Test Configuration' during configuring 'Publish over SSH'***

## 20180517

1. Copy folder from 192.168.1.30 (Linux CentOS) to Aliyun Linux

```
[root@SHYG reactadmin]# scp -r ./build root@39.106.193.149:/home
```

## 20180430

1. create extension

```
[root@ ~]# psql -U awardapply -d awardapply
awardapply=> \c awardapply postgres
Password for user postgres: 
You are now connected to database "awardapply" as user "postgres".
awardapply=# create extension tablefunc;
CREATE EXTENSION
awardapply=# \c awardapply awardapply
Password for user awardapply: 
You are now connected to database "awardapply" as user "awardapply".
```

## 20180412

1. Install Jenkins (in office desktop - CentOS 7)

[](https://www.cnblogs.com/woshimrf/p/6103366.html)
[](https://www.jianshu.com/p/b524b151d35f)

```
$ sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
$ sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
$ sudo yum -y install jenkins
```

2. Install Java

```
$ sudo yum install java-1.8.0-openjdk
$ java -version
openjdk version "1.8.0_161"
OpenJDK Runtime Environment (build 1.8.0_161-b14)
OpenJDK 64-Bit Server VM (build 25.161-b14, mixed mode)
```

if Java is installed before, may need to remove it before install

```
$ java -version
java version "1.5.0"
$ sudo yum remove java
```

3. start jenkins vervice

```
$ sudo service jenkins start/stop/restart
$ sudo chkconfig jenkins on
```

4. Open Jenkins

Browser: IP:8080

5. Install plugin

6. Create the first user

> username: admin
> password: Jenkins
> email: yunzhi.wei@yg-net.com

7. User root user with permission (not user 'jenkins' by default)


> 修改jenkins执行用户

```
vi /etc/sysconfig/jenkins
```

> 修改JENKINS_USER值：

```
## Type:        string
## Default:     "jenkins"
## ServiceRestart: jenkins
#
# Unix user account that runs the Jenkins daemon
# Be careful when you change this, as you need to update
# permissions of $JENKINS_HOME and /var/log/jenkins.
#
JENKINS_USER="root"
```

> 这里我们把JENKINS_USER值改为root用户。
> 注意：这里不一定就要修改为root用户，可以根据实际情况分配一个可执行相应命令的用户即可。

> 修改目录的相应权限：

```
sudo chown -R root /var/log/jenkins 
sudo chgrp -R root /var/log/jenkins

sudo chown -R root /var/lib/jenkins  
sudo chgrp -R root /var/lib/jenkins

sudo chown -R root /var/cache/jenkins 
sudo chgrp -R root /var/cache/jenkins
```

> Update

```
vim /etc/sudoers
```

```
## Allow root to run any commands anywhere
root      ALL=(ALL)      ALL
jenkins   ALL=(ALL)      ALL
```

> restart

```
service jenkins restart
```

> add the following line at the beginning of the Execute Shell

```
#!/bin/bash -ilex
```

## 20180401

1. Install ErLang

[Introduction from RabbitMQ](http://www.rabbitmq.com/install-rpm.html)
[Download from ErLang](https://www.erlang-solutions.com/resources/download.html)
[Article](https://blog.csdn.net/qq_22075041/article/details/78855708)

* Adding repository entry

```
wget https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm
rpm -Uvh erlang-solutions-1.0-1.noarch.rpm
```

* Installing Erlang

```
sudo yum install erlang
```


2. Install RabbitMQ

[Find a download address from this page](http://www.rabbitmq.com/install-rpm.html)
[For example](https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.4/rabbitmq-server-3.7.4-1.el7.noarch.rpm)
And use the following command to install.

```
wget https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.4/rabbitmq-server-3.7.4-1.el7.noarch.rpm
rpm --import https://dl.bintray.com/rabbitmq/Keys/rabbitmq-release-signing-key.asc
# this example assumes the CentOS 7 version of the package
yum install rabbitmq-server-3.7.4-1.el7.noarch.rpm
```


3. As an administrator, start and stop the server as usual:

```
/sbin/service rabbitmq-server start
```

```
/sbin/service rabbitmq-server stop
```

4. To start the daemon by default when the system boots, as an administrator run

```
chkconfig rabbitmq-server on
```

5. Enable Web Admin

```
sudo rabbitmq-plugins enable rabbitmq_management
```


## 20180223

1. Edit the profile file

```
[root@ ~]# vim /etc/profile
```

2. content as below

```
export AWARDAPPLY_SECRET="XXXXXXXXXX"
```

3. activate the environment variable

```
[root@ ~]# source /etc/profile
```

## 20180216

```
[root@ projects]# npm install -g mocha
[root@ projects]# npm install -g istanbul
```

## 20180213

1. create batch file

```
[root@ ~]# cd projects
[root@ projects]# touch clb.sh
[root@ projects]# vim clb.sh
[root@ projects]# sh clb.sh
```

> clb.sh:

```
#!/bin/bash
#publish service and api

git clone https://YunzhiWei@github.com/Clare-Huang/awardapply-backend.git
```

2. invoke batch file and install packages

```
[root@ awardapply]# yarn install
```

## 20180212

1. create a new user

```
[root@ ~]# useradd –d /usr/postgres -m postgres
```

2. set group

```
[root@ ~]# usermod –g root postgres
```

3. change password

```
[root@ ~]# passwd postgres
```

4. change user

```
[root@ ~]# su postgres
[postgres@ root]$ su root
```

5. install postgresql

[valuable to read about initdb](https://www.cnblogs.com/think8848/p/5877076.html)
[CentOS 7 with PG 9.6](http://www.linuxidc.com/Linux/2017-10/147536.htm)

```
[root@ ~]# yum install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-centos96-9.6-3.noarch.rpm
[root@ ~]# yum install postgresql96
[root@ ~]# yum install postgresql96-server
[root@ ~]# 
```

> postgresql will be installed in the folder of '/usr/pgsql-9.6'.
> postgresql will use the folder '/var/lib/pgsql/9.6/data' as database data folder.

6. initial postgresql

```
[root@ ~]# /usr/pgsql-9.6/bin/postgresql96-setup initdb
[root@ ~]# systemctl enable postgresql-9.6
[root@ ~]# systemctl start postgresql-9.6
```

7. check postgresql status

```
[root@ ~]# systemctl status postgresql-9.6
```

8. go into interactive mode with user account of 'postgres'

```
[root@ ~]# su postgres
[postgres@ root]$ psql
```

9. list all database

```
postgres=# \l
```

10. change postgres password

```
postgres=# alter user postgres with password '123456';
```

11. create a new database, a new user and grant authentication

* Option 1

```
postgres=# CREATE DATABASE awardapply;
postgres=# CREATE USER awardapply LOGIN PASSWORD '123456';
postgres=# GRANT ALL ON DATABASE awardapply TO awardapply;
```

* Option 2

```
postgres=# DROP DATABASE awardapply;
postgres=# DROP USER awardapply;
postgres=# CREATE USER awardapply WITH PASSWORD '123456';
postgres=# CREATE DATABASE awardapply OWNER awardapply;
postgres=# GRANT ALL PRIVILEGES ON DATABASE awardapply TO awardapply;
```

12. quit

```
postgres=# \q
```

13. update config and restart pg service

```
[root@ ~]# vim /var/lib/pgsql/9.6/data/postgresql.conf
```

```
listen_addresses = '*'
port = 5432
password_encryption = on
```

```
[root@ ~]# vim /var/lib/pgsql/9.6/data/pg_hba.conf
```

> original config:

```
local	all          all                                     peer
```

> new config (trust):

```
local   all             all                                     trust
```

> new config (password):

```
local   all             all                                     md5
```

> original config:

```
host    all             all           127.0.0.1/32              Ident
```

> new config (trust):

```
host    all             all           127.0.0.1/0               trust
```

> new config (password):

```
host    all             all           127.0.0.1/0               md5
```

> use (password) mode!!!

```
[root@ ~]# systemctl restart postgresql-9.6
```

14. login again (without the last step, this step will fail)

```
[postgres@ root]$ psql -U awardapply -d awardapply
```

15. other pg command

```
postgres=# \c postgres
postgres=# \d
```

> \c to change db
> \d to list all tables

16. install other lib

```
[root@ ~]# yum install postgresql96-contrib
```

17. create extension

```
[root@ ~]# psql -U awardapply -d awardapply
awardapply=> \c awardapply postgres;
awardapply=# create extension ltree;
awardapply=# create extension "pgcrypto";
awardapply=# create extension tablefunc;
awardapply=# \c awardapply awardapply;
awardapply=> 
```

18. check encoding

```
awardapply=# show client_encoding;
```

```
[root@ ~]# vim /var/lib/pgsql/9.6/data/postgresql.conf
```

```
C:\Program Files\PostgreSQL\9.6\data
```

[to understand pg encoding](https://www.cnblogs.com/winkey4986/p/6279243.html)

## 20180211

1. install pm2

```
[root@ ~]# npm install -g pm2
```

2. test pm2

```
[root@ ~]# cd projects
[root@ projects]# express exp
[root@ projects]# cd exp
[root@ exp]# npm install
[root@ exp]# pm2 start ./bin/www --name 'welcome express'
[root@ exp]# pm2 monit
[root@ exp]# pm2 list
[root@ exp]# pm2 logs
[root@ exp]# pm2 startup centos
[root@ exp]# pm2 save
```

> There are some error message for 'pm2 startup centos'.
> Just ignore and restart the server.
> PM2 works fine.

```
[root@ exp]# pm2 unstartup
[root@ exp]# pm2 save
```

> No http response after server restart.


```
[root@ exp]# pm2 start ./bin/www
[root@ exp]# pm2 stop 0
[root@ exp]# pm2 delete 0
```

```
[root@ exp]# pm2 start ./bin/www --name 'welcome express'
[root@ exp]# pm2 startup
[root@ exp]# pm2 save
```

> PM2 works after server restart.


```
[root@ exp]# pm2 web
```

> http://localhost:9615
> Get Server status in JSON format

3. keymetrics.io

```
[root@ exp]#  pm2 link [secret key] [public key]
```

> https://app.keymetrics.io/#/bucket/5a7faf922d51188490bc7ced/dashboard

4. install redis

[install redis on CentOS 7](http://www.jb51.net/article/93190.htm)

```
[root@ ~]# wget http://download.redis.io/releases/redis-4.0.8.tar.gz
[root@ ~]# tar xzf redis-4.0.8.tar.gz
[root@ ~]# cd redis-4.0.8
[root@ redis-4.0.8]# make
```

5. start redis server (without **make install**)

```
[root@ redis-4.0.8]# ./src/redis-server
```

6. make install

```
[root@ redis-4.0.8]# cd /src
[root@ src]# make install
[root@ src]# cd /
[root@ src]# redis-server
```

> after make install, redis-server can be invoked anywhere

7. daemonize redis

```
[root@ ~]# vim ./redis-4.0.8/redis.conf
```

> daemonize yes

8. 

```
[root@ etc]# vim /root/redis-4.0.8/utils/redis_init_script
```

```
#!/bin/sh
# chkconfig: 2345 90 10
# description: Redis is a persistent key-value database
```

```
[root@ ~]# cd /etc
[root@ etc]# mkdir redis
[root@ etc]# cp /root/redis-4.0.8/redis.conf /etc/redis/6379.conf
[root@ etc]# cp /root/redis-4.0.8/utils/redis_init_script /etc/init.d/redisd
[root@ etc]# chkconfig redisd on
```

## 20180210

1. install git

```
[root@ ~]# yum install git
```

2. install wget

```
[root@ ~]# yum install -y wget
```

3. download and install npm binary pakage

```
[root@ ~]# wget https://nodejs.org/dist/v12.14.1/node-v12.14.1-linux-x64.tar.xz

[root@ ~]# tar -xvf node-v12.14.1-linux-x64.tar.xz

[root@ ~]# ln -s ~/node-v12.14.1-linux-x64/bin/node /usr/bin/node

[root@ ~]# ln -s ~/node-v12.14.1-linux-x64/bin/npm /usr/bin/npm

[root@ ~]# npm
[root@ ~]# node

[root@ ~]# vim /etc/profile
export NODE_PATH="/root/node-v12.14.1-linux-x64"
export PATH=$NODE_PATH/bin:$PATH
```

4. restart the server from aliyun console

5. install global npm packages

```
[root@ ~]# npm install -g yarn
[root@ ~]# npm install -g express
[root@ ~]# npm install -g express-generator
```



. generate ssh key

```
[root@ ~]#  ssh-keygen -t rsa -C "yunzhi.wei@live.com"
```


# vi 基础命令

* v - 从命令模式进入视图模式
* i - 从命令模式进入插入模式
* Esc - 从插入模式退回命令模式
* : - 命令模式下进入【Last Line Mode】
* :w [file name] - 以 file name 为文件名存盘
* :wq 存盘并退出
* :q! 强制退出不存盘

# Linux

## User & Group

```
[root@ ~]# groups
[root@ ~]# groups [user name]
[root@ ~]# whoami
```

```
[root@ ~]# less /etc/group
[root@ ~]# less /etc/shadow
[root@ ~]# less /etc/passwd
```

