# Installation on Windows

## Firefox

[download new version here](http://www.firefox.com.cn/)

## 1Passport

[Login and download here](https://1password.com/)

## Shadowsocks

1. Copy exe file to a folder
2. Copy Url (ss:xxxxxxxxxxxxxx) from existing environment
3. Enable SS and test

## Chrome

1. [download here](https://www.google.com/chrome/)
2. Login in gmail account and sync
3. 设置启动页

## Xshell

[download here](https://www.netsarang.com/products/xsh_overview.html)

1. create sessions after installation
2. input username and password for each session

## Git

1. [download latest version here](https://git-scm.com/downloads)
2. [Check GUI clients here](https://git-scm.com/downloads/guis)

## SourceTree

1. [download here](https://www.sourcetreeapp.com/)
2. Login with existing account or register a new one

## VSCode

[download here](https://code.visualstudio.com/)

## 钉钉

1. [download here](https://www.dingtalk.com/)
2. Login with existing account

## Postman

1. [download here](https://www.getpostman.com/apps)
2. Login existing account and sync collections

## Nodejs

[download here](https://nodejs.org/en/download/)
node-v8.11.1-x64

1. npm install -g yarn
2. npm install -g mocha
3. npm install -g istanbul
4. npm install -g express
5. npm install -g express-generator

## postgresql-9.6.7-1-windows-x64.exe

1. Stack Builder may fail. It doesn't matter.
2. 增加环境变量：C:\Program Files\PostgreSQL\9.6\bin
3. 重启 Windows
4. SQL Shell (psql)

```
postgres=# DROP DATABASE awardapply;
postgres=# DROP USER awardapply;
postgres=# CREATE USER awardapply WITH PASSWORD '123456';
postgres=# CREATE DATABASE awardapply OWNER awardapply;
postgres=# GRANT ALL PRIVILEGES ON DATABASE awardapply TO awardapply;
```

5. Command Shell

```
c:\xxx > psql -U awardapply -d awardapply
awardapply=> \c awardapply postgres;
awardapply=# create extension ltree;
awardapply=# create extension "pgcrypto";
awardapply=# create extension tablefunc;
awardapply=# \c awardapply awardapply;
awardapply=> \i initial.sql;
```

## Redis-x64-3.0.504.msi

1. 重启
2. 检查系统驻留服务
3. 检查命令行

```
C:\xxxx > redis-cli
127.0.0.1:6379> get myKey
(nil)
127.0.0.1:6379>
```

## rabbitmq

[Refer to](https://blog.csdn.net/seven_coder/article/details/50946562)

1. otp_win64_20.2.exe
2. rabbitmq-server-3.7.2.exe
3. check installation details report for more information
4. double check

```
C:\xxxxx > C:\Program Files\RabbitMQ Server\rabbitmq_server-3.7.2\sbin
C:\Program Files\RabbitMQ Server\rabbitmq_server-3.7.2\sbin > rabbitmqctl status
Status of node rabbit@Chris-E470 ...
Error: unable to perform an operation on node 'rabbit@Chris-E470'. Please see diagnostics information and suggestions below.

Most common reasons for this are:

 * Target node is unreachable (e.g. due to hostname resolution, TCP connection or firewall issues)
 * CLI tool fails to authenticate with the server (e.g. due to CLI tool's Erlang cookie not matching that of the server)
 * Target node is not running

In addition to the diagnostics info below:

 * See the CLI, clustering and networking guides on http://rabbitmq.com/documentation.html to learn more
 * Consult server logs on node rabbit@Chris-E470

DIAGNOSTICS
===========

attempted to contact: ['rabbit@Chris-E470']

rabbit@Chris-E470:
  * connected to epmd (port 4369) on Chris-E470
  * epmd reports node 'rabbit' uses port 25672 for inter-node and CLI tool traffic
  * TCP connection succeeded but Erlang distribution failed

  * Authentication failed (rejected by the remote node), please check the Erlang cookie


Current node details:
 * node name: 'rabbitmqcli28@Chris-E470'
 * effective user's home directory: C:\Users\Chris
 * Erlang cookie hash: l+SSu57+cRyAQ03AJdwAbQ==
```