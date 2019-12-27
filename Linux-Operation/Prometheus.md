# 参考

- [从零搭建Prometheus监控报警系统](https://www.cnblogs.com/chenqionghe/p/10494868.html)
- [Prometheus](https://www.jianshu.com/p/93c840025f01)
- [Prometheus Docs](https://prometheus.io/docs/introduction/overview/)
- [How To Install Prometheus with Docker on Ubuntu 18.04](https://devconnected.com/how-to-install-prometheus-with-docker-on-ubuntu-18-04/)

# 安装日志

## 准备工作

1. 创建目录 `/home/monitoring`

    ```
    # cd /home
    # mkdir monitoring
    # cd monitoring
    # pwd
    /home/monitoring
    ```

1. 准备 `yml` 文件

    > `prometheus.yml`

    ```
    global:
      scrape_interval: 15s
      evaluation_interval: 15s
        
    rule_files:
      # - "first.rules"
      # - "second.rules"

    scrape_configs:
      - job_name: 'prometheus'
        # metrics_path defaults to '/metrics'
        # schema defaults to 'http'
        static_configs:
          - targets: ['local_host_ip:9090', 'local_host_ip:9100']
            labels:
              my: mylabel
    ```

## 安装 `Prometheus`

1. 下载 `prometheus` 镜像

    ```
    # docker pull prom/prometheus:v2.15.1
    ```

1. 运行 `prometheus` 容器

    ```
    # docker run --name prom --hostname prom --ip-forward=true -p 9090:9090 -v /home/monitoring/prometheus.yml:/etc/prometheus/prometheus.yml -d prom/prometheus:v2.15.1 
    ```

1. 使用浏览器远程访问 `prometheus` 服务
    > http://[hosting server IP]:9090

1. 使用浏览器远程访问 `prometheus` 服务的 `job`
    > http://[hosting server IP]:9090/metrics

## 安装 `node-exporter`

1. 下载 `prom/node-exporter` 镜像

    ```
    # docker pull prom/node-exporter
    ```

1. 运行 `node-exporter` 容器

    ```
    # docker run -d -p 9100:9100 -v "/:/hostfs" prom/node-exporter 
    ```