
# Shadowsocks Server

## VPS

Log in: https:\/\/50vz.net
User: yunzhi.wei@live.com
Password: wife 10 digital complex
Server Name:  OpenVZVPS-20161025611
IP:  172.247.39.100
SSH Port: ChinaNetCloud Standard\
40022

**搬瓦工** 也提供虚机

## SSH 登陆 Xshell

* user: root
* password: wife 10 digital

## Install ShadowSocks Service

Copy from [here](http://www.centoscn.com/image-text/install/2015/0510/5399.html)

### 1、查看系统

    [root@localhost ~]# cat /etc/issue
    CentOS release 6.6` `(Final)
    [root@localhost ~]# uname -a
    Linux localhost.localdomain 2.6.32-042stab106.6` `#1 SMP Mon Apr 20 14:48:47 MSK 2015 x86_64 x86_64 x86_64 GNU/Linux

### 2、安装ShadowSocks

```
# yum install python-setuptools && easy_install pip
# pip install shadowsocks
```

### 3、创建配置文件\/etc\/shadowsocks.json

```
[root@localhost /]# touch /etc/shadowsocks.json
[root@localhost /]# vi /etc/shadowsocks.json
{
"server":"xxx.xxx.xx.xxx",
"server_port":8989,
"local_address": "127.0.0.1",
"local_port":1080,
"password":"******",
"timeout":600,
"method":"rc4-md5"
}
```

备注：加密方式官方默认使用aes-256-cfb，推荐使用rc4-md5，因为 RC4比AES速度快好几倍。

**各字段说明：**

> * server:服务器IP
> * server\_port:服务器端口
> * local\_port:本地端端口
> * password:用来加密的密码
> * timeout:超时时间（秒）
> * method:加密方法，可选择 “bf-cfb”, “aes-256-cfb”, “des-cfb”, “rc4″等
> * ?KID@bJCln$

### 4、使用配置文件在后台运行shadowsocks服务

```
[root@localhost /]# ssserver -c /etc/shadowsocks.json -d start
```

备注：若无配置文件，在后台可以使用以下命令运行

```
[root@localhost \/\]\# ssserver -p 443 -k MyPass -m rc4-md5 -d start
```

### 5、停止服务

```
[root@localhost /]# ssserver -c /etc/shadowsocks.json -d stop
```

## 参考

* https://github.com/shadowsocks/shadowsocks/wiki/Shadowsocks-使用说明
* http://wuchong.me/blog/2015/02/02/shadowsocks-install-and-optimize/
