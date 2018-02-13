# dev env setup

## 20180213

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
[root@ ~]# systemctl start postgresql-9.6
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
postgres=# DROP USER awardapply;
postgres=# DROP DATABASE awardapply;
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
awardapply=# create extension ltree;
awardapply=# create extension "pgcrypto";
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

> to make sure the lc_messages, lc_monetary, lc_numeric and lc_time are 'en_US.UTF-8'

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
# descrption: Redis is a persistent key-value database
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
[root@ ~]# wget https://nodejs.org/dist/v8.9.4/node-v8.9.4-linux-x64.tar.xz

[root@ ~]# tar -xvf node-v8.9.4-linux-x64.tar.xz

[root@ ~]# ln -s ~/node-v8.9.4-linux-x64/bin/node /usr/bin/node

[root@ ~]# ln -s ~/node-v8.9.4-linux-x64/bin/npm /usr/bin/npm

[root@ ~]# npm
[root@ ~]# node

[root@ ~]# vim /etc/profile
export NODE_PATH="/root/node-v8.9.4-linux-x64"
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

