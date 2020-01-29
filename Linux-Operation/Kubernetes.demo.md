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
# wget https://nodejs.org/dist/v12.14.1/node-v12.14.1-linux-x64.tar.xz

# tar -xvf node-v12.14.1-linux-x64.tar.xz

# ln -s ~/node-v12.14.1-linux-x64/bin/node /usr/bin/node

# ln -s ~/node-v12.14.1-linux-x64/bin/npm /usr/bin/npm

# npm -v
6.13.4

# node -v
v12.14.1
```

```
# vi /etc/profile
# cat /etc/profile
```

> Add the follow lines at the end of `/etc/profile`
```
export NODE_PATH="/root/node-v12.14.1-linux-x64"
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
# cat >>clone.dockerimages.sh<<EOF
#!/bin/bash 
git clone https://github.com/YunzhiWei/dockerimages.git
EOF
```

### Worker Nodes

#### Pre-requests

- Docker Images: 

```
docker pull busybox
docker pull alpine
docker pull node:12.14.1-alpine
docker pull nginx:1.17.6-alpine
docker pull postgres:12.1-alpine
```

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

1. Remove

    ```
    # docker stop dockerimages_proxy_1 dockerimages_service_1 dockerimages_dbpg_1
    # docker rm dockerimages_proxy_1 dockerimages_service_1 dockerimages_dbpg_1

    # docker network rm dockerimages_bridgenet
    ```

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

# Demo - K8S Service of ClusterIP

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
    # psql -h dbpg -U docker -d docker
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
    # kubectl delete -f dbpg-svc-ci.yaml
    # kubectl delete -f dbpg-deploy.yaml
    # kubectl get deploy
    # kubectl get rs
    # kubectl get po
    ```

    ```
    # cd ../..
    # rm -rf dockerimages
    ```

# Demo - K8S Service of NodePort

## Prerequest

- Required images are ready in Worker Nodes
- Target folders exist in Workder Nodes

## Worker Node

1. update source code to make difference for different version

    ```
    # vi webproxy/www/index.html
    ```

1. update dockerbuild script to set version number

    ```
    # vi webproxy/dockerbuild.sh
    ```

1. build docker images for different version

    ```
    # yarn build:proxy
    # docker images
    ```
> prepare at least 5 images for different versions: `0.0.1` ~ `0.0.5`

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
    # kubectl get all -o wide --all-namespaces
    # watch !!
    ```

    ```
    # kubectl create -f dbpg.yaml
    # kubectl create -f backend.yaml
    # kubectl create -f frontend.yaml
    ```

1. Check - in Hosting Environment

    - Open Web Browser (Chrome) in hosting environment
    - URL: `http://static.office.com:30880`
    - URL: `http://api.office.com:30880`
    - URL: `http://<master-node-ip>:30880`
    - URL: `http://<worker-node-ip>:30880`

    > when frontend-deploy is created without frontend-svc-*, the web pages are still available at the following URL

    - URL: `http://static.office.com`
    - URL: `http://api.office.com`
    - URL: `http://<worker-node-ip>`

1. Upgrade by `update` & `apply` yaml file - in Master Node

    ```
    # kubectl describe deploy frontend-dp
    ```

    > here are some options and commands to upgrade

    ```
    # kubectl apply -f frontend-deploy.yaml
    ```
    ```
    # kubectl edit deploy frontend-dp
    ```
    > add `kubernetes.io/change-cause: "Release Version 0.0.1"` under `annotations`
    ```
    # kubectl set image deploy frontend-dp <container_name>=<image_name>:<version>
    ```

    ```
    # kubectl describe deploy frontend-dp
    # kubectl rollout status deploy frontend-dp
    # kubectl rollout history deploy frontend-dp
    ```

1. Rollback

    ```
    # kubectl rollout undo deploy frontend-dp --to-revision=2
    ```

1. Pause & resume the upgrading

    ```
    # kubectl rollout pause deploy frontend-dp
    ```
    ```
    # kubectl rollout resume deploy frontend-dp
    ```

1. remove

    ```
    # kubectl delete -f frontend.yaml
    # kubectl delete -f backend.yaml
    # kubectl delete -f dbpg.yaml
    ```

    ```
    # cd ../..
    # rm -rf dockerimages
    ```

# Demo - Ingress (Follow the instruction from `[ Kube 32 ] Set up Traefik Ingress on kubernetes Bare Metal Cluster`)

## Reference

[Kubernetes Ingress Controller](https://docs.traefik.io/v1.7/user-guide/kubernetes/)

[Containous 
Traefik](https://github.com/containous/traefik/tree/v1.7/examples/k8s)

## Ingress Controller - Traefik (Step 1)

1. clone traefik

```
# git clone https://github.com/containous/traefik.git
# cd traefik
# git checkout -b v1.7 origin/v1.7
# cd example/k8s
```

1. apply rbac role and role binding

```
# kubectl apply -f traefik-rbac.yaml
```

```
# kubectl describe clusterrole traefik-ingress-controller -n kube-system
```

1. apply daemonset

```
# kubectl apply -f traefik-ds.yaml
```

```
# kubectl get all -n kube-system | grep traefik
```

## Start Nginx (Step 2 - without port setting)

```
# kubectl create -f nginx-demo-ingress.yaml
```

```
# kubectl get po
```

```
# kubectl expose deploy nginx-demo-dp --port 80
```

```
# kubectl describe service nginx-demo-dp
```

## Ingress Resource (Step 3)

```
# kubectl create -f ingress-resource.yaml
```

```
# kubectl get ing
# kubectl describe ing ingress-resource
```

## Clean up

```
# kubectl delete ing ingress-resource
# kubectl delete svc nginx-demo-dp
# kubectl delete deploy nginx-demo-dp

# kubectl delete clusterrole traefik-ingress-controller
# kubectl delete clusterrolebinding traefik-ingress-controller
```

## Ingress Controller - Nginx (replacement option of Traefik)

[nginxinc
/
kubernetes-ingress](https://github.com/nginxinc/kubernetes-ingress)
[Installation with Manifests](https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/)

# Demo - Ingress (Step 1 is same)

## Reference

[Kubernetes Ingress Controller](https://docs.traefik.io/v1.7/user-guide/kubernetes/)

[Containous 
Traefik](https://github.com/containous/traefik/tree/v1.7/examples/k8s)

## Ingress Controller - Traefik (Step 1)

1. clone traefik

```
# git clone https://github.com/containous/traefik.git
# cd traefik
# git checkout -b v1.7 origin/v1.7
# cd example/k8s
```

1. apply rbac role and role binding

```
# kubectl apply -f traefik-rbac.yaml
```

```
# kubectl describe clusterrole traefik-ingress-controller -n kube-system
```

1. apply daemonset

```
# kubectl apply -f traefik-ds.yaml
```

```
# kubectl get all -n kube-system | grep traefik
```

## Start Ingress Resource (with Deployment & clusterIP Service)

```
# kubectl create -f ingress-demo.yaml
```

```
# kubectl get po
# kubectl get svc
# kubectl get ing
# kubectl describe ing ingress-resource
```

## Clean up

```
# kubectl delete -f traefik-ds.yaml
# kubectl delete -f traefik-rbac.yaml
```

```
# kubectl delete ing ingress-resource
# kubectl delete svc ingress-demo-svc-ci
# kubectl delete deploy ingress-demo-dp

# kubectl delete clusterrole traefik-ingress-controller
# kubectl delete clusterrolebinding traefik-ingress-controller
```

# Notice

> Check network if docker compose has any problem.

```
# docker network ls
# docker network rm dockerimages_bridgenet
```

# Comments

> `Docker Compose` is machine based.

> `K8S` is cluster based.

> Compare to `Docker Compose`, `K8S` provides more powerfule abilities (HA, Upgrade/Downgrade with zero downtime), but requires more resources.

> `K8S` needs more yaml files, but will save more long term operation jobs in production environment.
