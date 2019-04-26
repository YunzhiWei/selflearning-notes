# Environment Setup

## Git

* install git

```
[root@ ~]# yum install git
```

## WGET

* install wget

```
[root@ ~]# yum install -y wget
```

## Nodejs

1. download and install npm binary pakage

```
[root@ ~]# wget https://nodejs.org/dist/v10.15.3/node-v10.15.3-linux-x64.tar.xz

[root@ ~]# tar -xvf node-v10.15.3-linux-x64.tar.xz

[root@ ~]# ln -s ~/node-v10.15.3-linux-x64/bin/node /usr/bin/node

[root@ ~]# ln -s ~/node-v10.15.3-linux-x64/bin/npm /usr/bin/npm

[root@ ~]# npm -v
[root@ ~]# node -v

[root@ ~]# vim /etc/profile
[root@ ~]# cat /etc/profile

export NODE_PATH="/root/node-v10.15.3-linux-x64"
export PATH=$NODE_PATH/bin:$PATH

```

2. restart the server from console

```
[root@ ~]# reboot
```

3. install global npm packages

```
[root@ ~]# npm install -g yarn
[root@ ~]# npm install -g express
[root@ ~]# npm install -g express-generator
```

```
[root@ ~]# npm install -g mocha
[root@ ~]# npm install -g istanbul
```

```
[root@ ~]# npm install -g gulp
[root@ ~]# npm install -g cross-env
[root@ ~]# npm install -g rimraf
[root@ ~]# npm install -g next
```

## PM2

1. install pm2

```
[root@ ~]# npm install -g pm2
```

or

```
[root@ ~]# yarn global add pm2
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

## REDIS

1. install redis

[install redis on CentOS 7](http://www.jb51.net/article/93190.htm)

```
[root@ ~]# wget http://download.redis.io/releases/redis-5.0.4.tar.gz
[root@ ~]# tar xzf redis-5.0.4.tar.gz
[root@ ~]# cd redis-5.0.4
[root@ redis-5.0.4]# make
```

2. start redis server (without **make install**)

```
[root@ redis-5.0.4]# ./src/redis-server
```

3. make install

```
[root@ redis-5.0.4]# cd /src
[root@ src]# make install
[root@ src]# cd /
[root@ src]# redis-server
```

> after make install, redis-server can be invoked anywhere

4. daemonize redis

```
[root@ ~]# vim ./redis-5.0.4/redis.conf
```

> daemonize yes

5. update script to make step 6 work correctly

command: 

```
[root@ ~]# vim /root/redis-5.0.4/utils/redis_init_script
```

content: 

```
#!/bin/sh
# chkconfig: 2345 90 10
# description: Redis is a persistent key-value database
```

6. copy files and make redis start up after system boot

```
[root@ ~]# cd /etc
[root@ etc]# mkdir redis
[root@ etc]# cp /root/redis-5.0.4/redis.conf /etc/redis/6379.conf
[root@ etc]# cp /root/redis-5.0.4/utils/redis_init_script /etc/init.d/redisd
[root@ etc]# chkconfig redisd on
```

7. check if Redis works all right

option 1

```
[root@ ~]# service redisd start 
[root@ ~]# service redisd stop
```

option 2

```
[root@ ~]# /etc/init.d/redisd start 
[root@ ~]# /etc/init.d/redisd stop
```

## PostgreSQL

1. create a new user

```
[root@ ~]# useradd -d /usr/postgres -m postgres
```

2. set group

```
[root@ ~]# usermod -g root postgres
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

11. ( !!! may skip this step !!! ) create a new database, a new user and grant authentication

* Option 1

```
postgres=# CREATE DATABASE universal;
postgres=# CREATE USER universal LOGIN PASSWORD '123456';
postgres=# GRANT ALL ON DATABASE universal TO universal;
```

* Option 2

```
postgres=# DROP DATABASE universal;
postgres=# DROP USER universal;
postgres=# CREATE USER universal WITH PASSWORD '123456';
postgres=# CREATE DATABASE universal OWNER universal;
postgres=# GRANT ALL PRIVILEGES ON DATABASE universal TO universal;
```

12. quit and change back to root

```
postgres=# \q
[postgres@ ~]# su root
```

13. update config

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

> !!! use (password) mode !!!

14. and restart pg service

```
[root@ ~]# systemctl restart postgresql-9.6
```

15. ( !!! may skip this step !!! ) login again (without the last step, this step will fail)

```
[postgres@ root]$ psql -U universal -d universal
```

16. ( !!! may skip this step !!! ) other pg command

```
postgres=# \c postgres
postgres=# \d
```

> \c to change db
> \d to list all tables

17. install other lib

```
[root@ ~]# yum install postgresql96-contrib
```

18. ( !!! may skip this step !!! ) create extension

```
[root@ ~]# psql -U universal -d universal
universal=> \c universal postgres;
universal=# create extension ltree;
universal=# create extension "pgcrypto";
universal=# create extension tablefunc;
universal=# \c universal universal;
universal=> 
```

19. ( !!! may skip this step !!! ) check encoding

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


## RabbitMQ

1. Install ErLang

[Erlang 21.x ==> To use Erlang 21.x on CentOS 7:](https://github.com/rabbitmq/erlang-rpm)

* create repo file for yum

```
cd /etc/yum.repos.d
touch rabbitmq-erlang.repo
vim rabbitmq-erlang.repo
```

* edit the content of the repo file

```
[rabbitmq-erlang]
name=rabbitmq-erlang
baseurl=https://dl.bintray.com/rabbitmq/rpm/erlang/21/el/7
gpgcheck=1
gpgkey=https://dl.bintray.com/rabbitmq/Keys/rabbitmq-release-signing-key.asc
repo_gpgcheck=0
enabled=1
```

* check the repo file content

```
cat rabbitmq-erlang.repo
[rabbitmq-erlang]
name=rabbitmq-erlang
baseurl=https://dl.bintray.com/rabbitmq/rpm/erlang/21/el/7
gpgcheck=1
gpgkey=https://dl.bintray.com/rabbitmq/Keys/rabbitmq-release-signing-key.asc
repo_gpgcheck=0
enabled=1
```

* Installing Erlang

```
sudo yum install erlang
```

* Check Erlang Installation

```
[root@yum.repos.d] # erl -version
Erlang (SMP,ASYNC_THREADS,HIPE) (BEAM) emulator version 10.0.5
```

2. Install RabbitMQ

[article](http://www.cnblogs.com/wang-li/p/9398792.html)

> Option 1

* Download the rpm file:

[Find a rpm to download: Download the Server](http://www.rabbitmq.com/install-rpm.html#downloads)
[For example](https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.7/rabbitmq-server-3.7.7-1.el7.noarch.rpm)

```
[root@yum.repos.d] # cd ~
[root@~] # wget https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.7/rabbitmq-server-3.7.7-1.el7.noarch.rpm
```

* Install with rpm

[install with rpm](http://www.rabbitmq.com/install-rpm.html#with-rpm)

```
rpm --import https://dl.bintray.com/rabbitmq/Keys/rabbitmq-release-signing-key.asc
# this example assumes the CentOS 7 version of the package
yum install rabbitmq-server-3.7.7-1.el7.noarch.rpm
```

> Option 2

* create repo file for yum

```
cd /etc/yum.repos.d
touch bintray-rabbitmq-server.repo
vim bintray-rabbitmq-server.repo
```

* edit the content of the repo file

```
[bintray-rabbitmq-server]
name=bintray-rabbitmq-rpm
baseurl=https://dl.bintray.com/rabbitmq/rpm/rabbitmq-server/v3.7.x/el/7/
gpgcheck=0
repo_gpgcheck=0
enabled=1
```

* check the repo file content

```
cat bintray-rabbitmq-server.repo
[bintray-rabbitmq-server]
name=bintray-rabbitmq-rpm
baseurl=https://dl.bintray.com/rabbitmq/rpm/rabbitmq-server/v3.7.x/el/7/
gpgcheck=0
repo_gpgcheck=0
enabled=1
```

* Installing rabbitmq server

```
sudo yum install rabbitmq-server
```

3. As an administrator, start and stop the server as usual:

[plugin and user](https://blog.csdn.net/alex_bean/article/details/56675694)
[article](https://blog.csdn.net/diyangxia/article/details/77870568)
[article](https://www.cnblogs.com/ylsforever/p/6600925.html)

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

> Note: Forwarding request to 'systemctl enable rabbitmq-server.service'.

5. Check status

```
systemctl status rabbitmq-server.service
rabbitmqctl status
```

6. Enable Web Admin

[article](https://blog.csdn.net/deepblue1024/article/details/79152455)

* enable plugin

```
sudo rabbitmq-plugins enable rabbitmq_management
sudo chown -R rabbitmq:rabbitmq /var/lib/rabbitmq/
```

* add new user for Web Admin

```
sudo rabbitmqctl add_user mqadmin mqadminpassword
sudo rabbitmqctl set_user_tags mqadmin administrator
sudo rabbitmqctl set_permissions -p / mqadmin ".*" ".*" ".*"
```

* 阿里云实例安全组设置：内网入方向规则（15672）

* access web admin from browser

http://[your-vultr-server-IP]:15672/

## Nginx

1. install nginx

```
[root@ ~]# rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
[root@ ~]# yum install -y nginx
```

2. start nginx

```
[root@ ~]# systemctl start nginx.service
[root@ ~]# systemctl status nginx.service
[root@ ~]# systemctl enable nginx.service
```

3. edit config

```
[root@ ~]# cp /etc/nginx/nginx.conf  /etc/nginx/nginx.conf.bak
[root@ ~]# mkdir /etc/nginx/sites-available
[root@ ~]# mkdir /etc/nginx/sites-enabled
[root@ ~]# vi /etc/nginx/nginx.conf
[root@ ~]# cat /etc/nginx/nginx.conf

user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;

events {
    worker_connections  1024;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
    include /etc/nginx/sites-enabled/*.conf;
    server_names_hash_bucket_size 64;
}
```

```
[root@ ~]# nginx -t

```

4. new a site config

```
[root@ ~]# cp /etc/nginx/conf.d/default.conf /etc/nginx/sites-available/atlantis.yg-net.com.conf
[root@ ~]# vim /etc/nginx/sites-available/atlantis.yg-net.com.conf
[root@ ~]# cat /etc/nginx/sites-available/atlantis.yg-net.com.conf

server {
    listen      80;
    server_name atlantis.yg-net.com;
    location / {
        proxy_pass http://localhost:8001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
    error_page  500 502 503 504  /50x.html;
    location = /50x.html {
        root  /usr/share/nginx/html;
    }
}

[root@ ~]# ln -s /etc/nginx/sites-available/atlantis.yg-net.com.conf /etc/nginx/sites-enabled/atlantis.yg-net.com.conf
[root@ ~]# nginx -t
[root@ ~]# systemctl restart nginx

```

5. create other sites config

* PM2: http://localhost:9615
* RabbitMQ: http://localhost:15672

## Install rzsz (for file upload from Windows XShell to Linux)

```
[root@ ~]# yum install  lrzsz -y
```

## prepare runtime dependencies

1. create and execute batch file

```
[root@ ~]# mkdir projects
[root@ ~]# cd projects
[root@ projects]# touch clone.atlantis.sh
[root@ projects]# vim clone.atlantis.sh
[root@ projects]# sh clone.atlantis.sh
```

> clone.atlantis.sh:

```
#!/bin/bash
#publish service and api

git clone https://YunzhiWei@github.com/Clare-Huang/Atlantis.git
```

2. upload certifications for wepay and md file for wechat

start XShell

```
[root@ projects]# mkdir runtime
[root@ projects]# cd runtime
[root@ runtime]# mkdir wechat
[root@ runtime]# mkdir wepay
[root@ runtime]# cd wechat
[root@ wechat]# rz
[root@ runtime]# cd ../wepay
[root@ wechat]# rz
```

## Setup Runtime Environment Variables

1. Edit the profile file

```
[root@ ~]# vim /etc/profile
```

2. content as below

```
export NODE_ENV="production"
```

3. activate the environment variable

```
[root@ ~]# source /etc/profile
```

or 

```
[root@ ~]# reboot
```

## clone projects

1. 

```
[root@ ~]# cd projects
[root@ projects]# sh clone.atlantis.sh
```

2. initial database

```
[root@ projects]# cd Atlantis
[root@ Atlantis]# yarn db:create
[root@ Atlantis]# yarn db:ext
[root@ Atlantis]# yarn db:init
```

3. start production

```
[root@ Atlantis]# yarn production
```

## remove project folder

```
[root@ projects]# rm -rf Atlantis
```

# IT Operations

## rabbitmq

* List all queues and messages

```
[root@ Atlantis]# rabbitmqctl list_queues
```

* reset and clear queues

```
[root@ Atlantis]# rabbitmqctl stop_app
[root@ Atlantis]# rabbitmqctl reset
[root@ Atlantis]# rabbitmqctl start_app
```

## Web Admin

* PM2: http://localhost:9615
* RabbitMQ: http://localhost:15672
