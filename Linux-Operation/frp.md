# Background Knowledge

[一分钟实现内网穿透（ngrok服务器搭建）](https://blog.csdn.net/zhangguo5/article/details/77848658?utm_source=5ibc.net&utm_medium=referral)

# Source Code and Readme Document

[github](https://github.com/fatedier/frp/blob/master/README_zh.md)

# Server Install

[frp简易安装配置说明](https://blog.csdn.net/e_wsq/article/details/79405512)

1. download

```
wget https://github.com/fatedier/frp/releases/download/v0.21.0/frp_0.21.0_linux_amd64.tar.gz
```

2. unzip

```
tar zxvf frp_0.21.0_linux_amd64.tar.gz
```

3. config frps.ini

* command

```
vim frps.ini
```

* content

```
# frps.ini
[common]
bind_port = 7000
vhost_http_port = 80
```

4. start service

```
./frps -c ./frps.ini
```

> You may want to save above command as a sh batch file.

```
#!/bin/bash
# start frp service

./frps -c ./frps.ini
```

# Aliyun Config

> 设置阿里云 ECS（xxx.xxx.xxx.xxx） 安全组规则：允许 7000 端口 以及 80 端口
> 阿里云域名解析 增加 A 记录：www.[domainname].com ==>xxx.xxx.xxx.xxx

# Client Install

1. download
2. config frpc.ini

```
# frpc.ini
[common]
server_addr = xxx.xxx.xxx.xxx
server_port = 7000

[web]
type = http
local_port = 3000
custom_domains = www.[domainname].com
```

> Above is the configuration about web server. Below is the configuration about the tcp (from Xiaoyi Zhu).

```
# frpc.ini
[common]
server_addr = xxx.xxx.xxx.xxx
server_port = 7000

[unix_domain_socket]
type = tcp
remote_port = 3000
plugin = unix_domain_socket
plugin_unix_path = /var/run/docker.sock
```

3. start frp client

```
frpc -c frpc.ini
```

> You may want to save above command as a bat file in the same folder of frpc.ext and frpc.ini.

# Test

1. Start Web Server from local machine and listen port 3000

```
node app
```

2. Open Web Site from Browser

> Input 'http://www.[domainname].com:80' in browser url address box.

# Subdomain

If you want to use sub domain, here is the case:

```
# frps.ini
[common]
bind_port = 7000
vhost_http_port = 80
subdomain_host = [sub domain name].com
```

```
# frpc.ini
[common]
server_addr = xxx.xxx.xxx.xxx
server_port = 7000

[web]
type = http
local_port = 3000
subdomain = [site name]
```

Example

```
# frps.ini

[common]
bind_port = 7000
vhost_http_port = 80
subdomain_host = frp.yg-net.com
```

```
# frpc.ini

[common]
server_addr = 107.151.172.73
server_port = 7000

[web]
type = http
local_port = 3000
subdomain = atlantis
```


# 注意

> 如果服务器版本和客户端版本不一致，会引发报错，导致客户端无法启动
