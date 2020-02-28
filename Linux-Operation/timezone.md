#  问题描述

程序运行时，前端应用、后端服务、数据库服务、数据表字段，都有各自的时间设置，包括时间日期、时区设置，如果不匹配，有可能会造成时间判断上的错误。

# 背景

## 数据表

```
created_when        timestamp DEFAULT current_timestamp,
updated_when        timestamp DEFAULT current_timestamp,
```

> 目前数据库的时间字段，采用的是 `timestamp`，是不带时区信息的时间戳。因此，字段保存的时间信息，由写入时的时间决定。字段读出的信息，就是写入时的当前时间（由当时的时间，和时区设置决定）

## 数据库服务器（或容器）

- 由数据库服务器的时间和单独数据库的时区设置决定
- 通过 `ALTER DATABASE [database-name] SET timezone TO 'Asia/Shanghai';`

## 服务器

- 服务器的时间，由服务器的时间和时区决定
- 通过 `date` 命名可以查看
- 通过 `cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime` 可以改变

## 容器

- 容器运行时的时间，由宿主机的时间和容器的时区决定
- 通过 `date` 命名可以查看
- 如果是自定义镜像，可以在 `Dockerfile` 中通过增加 `RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime` 改变镜像时区
- 如果是标准镜像，可以通过注册表项 `TZ=Asia/Shanghai` 改变镜像时区

# 解决方案

## 宿主机

### 服务器时间自动定时同步更新

```
yum install -y ntpdate
ntpdate -u 210.72.145.44
```

### 设置正确的时区

```
cp /etc/localtime /etc/localtime.bak
cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

## 自定义容器镜像

### 基于 `Nginx` 的前端镜像

`Dockerfile`

```
FROM nginx:1.17.6-alpine

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
ADD ./runtime/nginx /etc/nginx
ADD ./runtime/www /www

... ...
```

### 基于 `Nodejs` 的后端镜像

`Dockerfile`

```
FROM node:12.14.1-alpine

# RUN apk update \
#     && apk add tzdata \
#     && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
#     && echo "Asia/Shanghai" > /etc/timezone
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
RUN apk add --no-cache tzdata \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    &&rm -rf /var/cache/apk/* /tmp/* /var/tmp/* $HOME/.cache

ADD ./node_modules /node_modules

... ...
```

## 标准镜像（`redis`，`postgres`）

`docker-compose.yml`

```
version: '2'

services:
  redis:
    container_name: redis
    image: 'redis:5.0.7-alpine'
    restart: always
    networks:
      - bridgenet
    ports:
      - '6379:6379'
    environment: 
      - TZ=Asia/Shanghai

... ...
```

## 数据库

### 服务器

> 确保服务器自动生成时间的正确性

`timezone.sh`

```
psql -v ON_ERROR_STOP=1 --username postgres --dbname [database-name] <<-EOSQL
  ALTER DATABASE [database-name] SET timezone TO 'Asia/Shanghai';
EOSQL
```

`docker-entrypoint-initdb.d/initial.sh`

```
#!/bin/bash
set -e

cd /script
sh create_db.sh
sh create_ext.sh
sh timezone.sh
sh initial.sh

... ...

```

### 客户端

> 确保客户端执行的相关命令，所使用的时间的正确性（如果没有明确设置，缺省会使用数据库的时区设置）

`timezone.sql`

```
show timezone;
set timezone='Asia/Shanghai';
select current_timestamp;
show timezone;
```

`initial.sql`

```
\i timezone.sql;
\i ecset.sql;

... ...

```

# 参考内容

## 服务器时间同步

> [【Linux】- 同步网络时间](https://www.cnblogs.com/wangwust/p/11330718.html)

|时间同步服务|主机|
|--:|---|
|中国国家授时中心|210.72.145.44|
|NTP服务器(上海) |ntp.api.bz|
|美国|time.nist.gov|
|复旦|ntp.fudan.edu.cn|
|微软公司授时主机(美国) |time.windows.com|
|台警大授时中心(台湾)|asia.pool.ntp.org|

## Linux CentOS

- timedatectl

```
# timedatectl
```

- date

```
# date
```

- set timezone

```
# cp /etc/localtime /etc/localtime.bak
# cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

# Postgres

## 客户端

- localtimestamp, current_timestamp, now()

```
select localtimestamp, current_timestamp, now();
```

- show timezone

```
=> show timezone;
```

- set timezone

```
=> set timezone='Asia/Shanghai';
```

> by default the timezone is 'UTC'

## 服务端

```
ALTER DATABASE [database-name] SET timezone TO 'Asia/Shanghai
```
