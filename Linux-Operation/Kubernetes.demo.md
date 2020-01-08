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

### Master & Worker Nodes

#### Git

```
# yum install git
```

#### WGET

```
# yum install -y wget
```

#### Node & NPM

> download and install npm binary pakage
```
# wget https://nodejs.org/dist/v10.15.3/node-v10.15.3-linux-x64.tar.xz

# tar -xvf node-v10.15.3-linux-x64.tar.xz

# ln -s ~/node-v10.15.3-linux-x64/bin/node /usr/bin/node

# ln -s ~/node-v10.15.3-linux-x64/bin/npm /usr/bin/npm

# npm -v
# node -v

# vim /etc/profile
# cat /etc/profile
```

> `/etc/profile`
```
export NODE_PATH="/root/node-v10.15.3-linux-x64"
export PATH=$NODE_PATH/bin:$PATH
```

#### reboot the server

```
# reboot
```

#### install global npm packages

```
# npm install -g yarn gulp cross-env rimraf
```

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

### Worker Nodes

#### Pre-requests

- Docker Images: `Alpine`, `Nodejs`, `Nginx`, `Postgres`
- Docker Compose

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

# Demo - K8S Pod

## Prerequest

- Required images are ready in Worker Nodes
- Target folders exist in Workder Nodes

## Master Node

1. Clone

    ```
    # cd ~/projects
    # sh clone.dockerimages.sh
    # ls
    # cd dockerimages/devops
    # ls
    ```
    > Source code should be ready

1. Run

    ```
    # kubectl create -f dbpg-pod.yaml
    ```

1. Check

    ```
    # kubectl get po
    # kubectl exec -it dbpg-pod sh
    ```

    ```
    # ls /var/lib/postgresql/data
    # ls /docker-entrypoint-initdb.d
    ```

    ```
    # psql -U docker -d docker
    ```

    ```
    # \d
    # \l
    # select * from dbt_maindata;
    ```

    ```
    # \q
    ```

    ```
    # exit
    ```

1. remove

    ```
    # kubectl delete -f dbpg-pod.yaml
    # kubectl get po
    ```

    ```
    # cd ../..
    # rm -rf dockerimages
    ```

# Demo - K8S Deployment

## Prerequest

- Required images are ready in Worker Nodes
- Target folders exist in Workder Nodes

## Master Node

1. Clone

    ```
    # cd ~/projects
    # sh clone.dockerimages.sh
    # ls
    # cd dockerimages/devops
    # ls
    ```
    > Source code should be ready

1. Run

    ```
    # kubectl create -f dbpg-deploy.yaml
    ```

1. Check

    ```
    # kubectl get deploy
    # kubectl get rs
    # kubectl get po
    # kubectl exec -it dbpg-pod-<POD-ID> sh
    ```

    ```
    # ls /var/lib/postgresql/data
    # ls /docker-entrypoint-initdb.d
    ```

    ```
    # psql -U docker -d docker
    ```

    ```
    # \d
    # \l
    # select * from dbt_maindata;
    ```

    ```
    # \q
    ```

    ```
    # exit
    ```

1. remove

    ```
    # kubectl delete -f dbpg-deploy.yaml
    # kubectl get deploy
    # kubectl get rs
    # kubectl get po
    ```

    ```
    # cd ../..
    # rm -rf dockerimages
    ```

# Demo - K8S Service

## Prerequest

- Required images are ready in Worker Nodes
- Target folders exist in Workder Nodes

## Master Node

1. Clone

    ```
    # cd ~/projects
    # sh clone.dockerimages.sh
    # ls
    # cd dockerimages/devops
    # ls
    ```
    > Source code should be ready

1. Update Pod's port

    ```
    # vi dbpg-pod.yaml
    ```

    > remove the following lines
    ```
    ports:
    - containerPort: 5432
      hostPort: 5432
      protocol: TCP
    ```

1. Run

    ```
    # kubectl create -f dbpg-deploy.yaml
    # kubectl create -f dbpg-svc-ci.yaml
    # kubectl create -f dbpg-pod.yaml
    ```

1. Check

    ```
    # kubectl get service
    # kubectl get deploy
    # kubectl get rs
    # kubectl get po
    # kubectl exec -it dbpg-pod sh
    ```

    ```
    # psql -h dbpg-svc-ci -U docker -d docker
    ```

    ```
    # \d
    # \l
    # select * from dbt_maindata;
    ```

    ```
    # \q
    ```

    ```
    # exit
    ```

1. remove

    ```
    # kubectl delete -f dbpg-pod.yaml
    # kubectl delete -f dbpg-service.yaml
    # kubectl delete -f dbpg-deploy.yaml
    # kubectl get deploy
    # kubectl get rs
    # kubectl get po
    ```

    ```
    # cd ../..
    # rm -rf dockerimages
    ```
