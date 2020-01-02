# Install

Pull docker image

```
# docker pull grafana/grafana
# docker images
```

# Run

```
# docker run -d -p 3000:3000 --name grafana grafana/grafana
```

# Setup

1. Open __Grafana__
    > Input url of `http://<docker-container-IP>:3000/login` in browser

1. Input user name and password
    > default user name and password are `admin`

1. Add data source
    1. Select `Prometheus`
    1. Input URL
    1. `Save & Test`

1. Import templates
    1. Switch to `Dashboards` tab
    1. `Import` the templates

# Show dashboards

1. click __Grafana Logo__ at the up-left corner to go back to `Home`
1. select dashboard from the drop-down list
    > `Prometheus Stats`, `Prometheus 2.0 Stats`, `Grafana metrics`
