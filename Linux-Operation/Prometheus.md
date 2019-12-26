# 参考

- [从零搭建Prometheus监控报警系统](https://www.cnblogs.com/chenqionghe/p/10494868.html)
- [Prometheus](https://www.jianshu.com/p/93c840025f01)

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
    - job_name: 'spring'
        metrics_path: '/actuator/prometheus'
        static_configs:
        - targets: ['localhost:9090']
    ```

1. 下载 `prometheus` 镜像

    ```
    # docker pull prom/prometheus:v2.15.1
    ```

1. 运行 `prometheus` 容器

    ```
    # docker run --name prom --hostname prom --ip-forward=true -p 9090:9090 -v /home/monitoring/prometheus.yml:/etc/prometheus/prometheus.yml -d prom/prometheus:v2.15.1 
    ```