
# 发行版

- Community Edition
- Enterprise Edition

# 安装

## 参考

- [Get Docker Engine - Community for CentOS](https://docs.docker.com/install/linux/docker-ce/centos/)

## 安装日志（Install using the repository）

1. SET UP THE REPOSITORY

```
# sudo yum install -y yum-utils device-mapper-persistent-data lvm2
# sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

2. INSTALL DOCKER ENGINE - COMMUNITY

```
# sudo yum install docker-ce docker-ce-cli containerd.io
```

3. Start Docker

```
$ sudo systemctl start docker
```

4. Verify that Docker Engine - Community is installed correctly by running the hello-world image.

```
$ sudo docker run hello-world
```

5. Verify that Docker Engine - Community is installed correctly by running the whalesay image. (Optional)

- [docker/whalesa](https://hub.docker.com/r/docker/whalesay)

```
$ docker run docker/whalesay cowsay boo
```

# 基本命令

## run - Run a container

- tag

```
# docker run redis:4.0
```

- STDIN
- -it (interactive mode, attach terminal)

- attach / detach (-d)

- Port Mapping (external:internal)

```
# docker run -p 8001:3000 xxxxx
# docker run -p 8002:3000 xxxxx
# docker run -p 8003:3000 xxxxx
# docker run -p 8004:3000 xxxxx
```

- Volume Mapping

```
# docker run --name db_pg_1 -v /my/own/datadir:/var/lib/postgresql/data -d postgres
```

- Environment Variables

```
# docker run -e APP_COLOR=blue XXXX
```

## ps - List containers

## stop - Stop a container

## rm - Remove a container

## rmi - Remove images

## pull - Download an image

## exec - Execute a command

## attach - attach a container

## inspect - inspect a container

## logs - show container's log

## 示例

```
# docker run centos
# docker run -it centos bash
# docker ps
# docker ps -a
# docker run centos sleep 20
# docker run -d --name thistest centos sleep 100
# docker exec thistest cat /etc/*release*
# docker stop thistest
# docker rm xxx xxx xxx
# docker images
# docker rmi xxxx
# docker pull centos
# docker inspect thistest
# docker logs thistest
```

# 典型镜像

## 使用 Node:alpine 启动 js 脚本

```
# docker run -it --rm --name node_main_1 -v "$PWD":/usr/src/app -w /usr/src/app node:11.10.1-alpine node main.js
```

## 使用 postgres:alpine 管理数据库

1. 下载镜像

```
# docker pull postgres:alpine
```

2. 启动容器

```
# docker run --name dbpg -e POSTGRES_PASSWORD=123456 -p 54320:5432 -d postgres:alpine
```

3. 进入容器

```
# docker exec -it dbpg /bin/bash
```

4. 启动 psql 

```
psql -U postgres -d postgres
```


# 参考

- [Docker for the Absolute Beginner - Hands On](https://kodekloud.com/courses/296044)
- [Docker Documents](https://docs.docker.com/)
- [docker实现postgresql](https://www.jianshu.com/p/9ab7b89637e7)