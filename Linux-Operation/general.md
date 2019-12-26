# 案例

## 检查80端口占用情况并关闭相关服务（Nginx）

### 背景

    > 在 CentOS 7 上安装 Docker 之后，启动 Nginx 镜像，发现 CentOS 7 的 80 端口被占用

### 解决

1. 使用 `lsof -i tcp:80` 命令检查服务器 `80` 端口占用情况
    > 发现服务器已经有了一个本地安装的 `Nginx` 服务

1. 检查服务器的 `/etc` 目录，确实发现存在 `Nginx` 目录
    > `Nginx` 本地服务确实已经安装过

1. 进入 `/etc/init.d` 目录，检查是否有自动启动的脚本文件
    > 未发现和 `Nginx` 相关的自启动脚本

1. 使用 `systemctl list-unit-files` 列出所有系统服务的状态
    > 发现 `nginx.service` 是 `enabled` 状态

1. 使用 `chkconfig nginx off` 命令关闭 `nginx` 自启动

1. 再次使用 `systemctl list-unit-files` 列出所有系统服务的状态
    > 确认 `nginx.service` 是 `disabled` 状态

1. 使用 `nginx -s quit` 命令停止当前正在运行的 `nginx` 服务
    > 其他可以选择用于停止 `Nginx` 服务的命令还有：
    
    ```
    # nginx -s stop
    # systemctl stop nginx.service
    # killall nginx
    ```

1. 再次使用 `lsof -i tcp:80` 命令检查服务器 `80` 端口占用情况
    > 确认 `Nginx` 服务已经停止

1. 使用 `reboot` 命令重启服务器

1. 再次使用 `lsof -i tcp:80` 命令检查服务器 `80` 端口占用情况
    > 确认 `Nginx` 服务没有自动启动

# 命令
