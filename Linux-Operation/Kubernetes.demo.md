# Environment

## Hosting Environment 

- Windows 10
- VMware Workstation 15 Player

### Setup Hosting Windows

#### Open `C:\Windows\System32\drivers\etc` and add the following lines

```
192.168.153.130    master1.k8s.com
192.168.153.131    worker1.k8s.com
192.168.153.131    static.office.com
192.168.153.131    api.office.com
```

#### check

```
> ping worker1.k8s.com
> ping static.office.com
```

## Cluster Environment

### Nodes

|Role|Hostname|FQDN|IP|OS|RAM|CPU|Storage|
|----|----|----|----|----|----|----|----|
|Master|k8s-master-1|master1.k8s.com|192.168.153.130|CentOS 7|4G|2|20GB|
|Worker|k8s-worker-1|worker1.k8s.com|192.168.153.131|CentOS 7|4G|2|20GB|
  
### Worker Nodes

#### Pre-requests

- Docker Images: `Alpine`, `Nodejs`, `Nginx`, `Postgres`
- Docker Compose
- Nodejs
- Git

#### Prepare `~/projects/clone.athena.sh`

```
# cd ~
# mkdir projects
# cd projects
# vi clone.dockerimages.sh
# cat clone.dockerimages.sh
```

> `clone.dockerimages.sh`
```
#!/bin/bash 
#publish service and api

git clone https://github.com/YunzhiWei/dockerimages.git
```

# Demo - Docker Compose

## Worker Node

1. Clone

    ```
    # cd ~/projects
    # sh clone.dockerimages.sh
    # ls
    # cd dockerimages
    # ls
    ```
    > Source code should be ready

1. Build

    ```
    # yarn build
    # docker images
    ```
    > Docker images should be built

1. Run

    ```
    # yarn start
    ```
    > 

## Hosting Machine

1. Open Web Browser (Chrome)

1. URL: http://static.office.com

1. URL: http://api.office.com

## Source Code

> details for each image and whole structure

## Comments

### Why docker compose?

> DevOps 1.0

- No need to manage each docker image manually
- All infra arch and configurations are under management
- Each to setup production environment
- and more ...

