# dev env setup

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
