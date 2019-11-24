# Software Download

- [v2ray core](https://github.com/v2ray/v2ray-core/releases)

# Installation Instruction

- [一键安装脚本](https://github.com/wulabing/V2Ray_ws-tls_bash_onekey)

# Installation Options

## Option 1: Vmess+websocket+TLS+Nginx+Website

```
bash <(curl -L -s https://raw.githubusercontent.com/wulabing/V2Ray_ws-tls_bash_onekey/master/install.sh) | tee v2ray_ins.log
```

## Option 2: Vmess + HTTP2 over TLS

```
bash <(curl -L -s https://raw.githubusercontent.com/wulabing/V2Ray_ws-tls_bash_onekey/master/install_h2.sh) | tee v2ray_ins_h2.log
```

# Command Line


## Start V2ray：

```
systemctl start v2ray
```

## Stop V2ray：

```
systemctl stop v2ray
```

## Start Nginx

```
systemctl start nginx
```

## Stop Nginx

```
systemctl stop nginx
```

# 相关目录


## Web 目录

```
/home/wwwroot/levis
```

## V2ray 服务端配置

```
/etc/v2ray/config.json
```

## V2ray 客户端配置

```
执行安装时所在目录下的 v2ray_info.txt
```

## Nginx 目录

```
/etc/nginx
```

## 证书目录

```
/data/v2ray.key 和 /data/v2ray.crt
```

# Installation Log

1. Try option 1: failed
2. Try option 2: succeeded
3. Installation Log

```
[Sat Nov 23 23:54:56 CST 2019] Your cert is in  /root/.acme.sh/www.weready.online_ecc/www.weready.online.cer 
[Sat Nov 23 23:54:56 CST 2019] Your cert key is in  /root/.acme.sh/www.weready.online_ecc/www.weready.online.key 
[Sat Nov 23 23:54:56 CST 2019] The intermediate CA cert is in  /root/.acme.sh/www.weready.online_ecc/ca.cer 
[Sat Nov 23 23:54:56 CST 2019] And the full chain certs is there:  /root/.acme.sh/www.weready.online_ecc/fullchain.cer 
[OK]  SSL 证书生成成功 

[Sat Nov 23 23:54:56 CST 2019] Installing key to:/data/v2ray.key
[Sat Nov 23 23:54:56 CST 2019] Installing full chain to:/data/v2ray.crt
[OK]  证书配置成功 
[OK]  Nginx systemd ServerFile 添加 完成 
[OK]  V2ray+ws+tls 安装成功

[OK]  Nginx 启动 完成 
Created symlink from /etc/systemd/system/multi-user.target.wants/nginx.service to /usr/lib/systemd/system/nginx.service.
[OK]  设置 Nginx 开机自启 完成 
[OK]  V2ray 启动 完成 
[OK]  设置 v2ray 开机自启 完成 
[OK]  cron 计划任务更新 完成 
```
