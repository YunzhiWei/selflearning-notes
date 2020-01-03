# Reference

- [kubernetes安装（基于CentOS7，kubeadm）](https://www.cnblogs.com/pascall/p/10675545.html)
- [kubernetes1.13.5安装部署](https://www.cnblogs.com/doufy/p/10730812.html)

# What is Kubernetes

- A HA Cluster and Management System

# Kubernetes Architecture & Terminology

- Node
    + Master
        * API Server ( Expose API )
        * ETCD (Key-Value Database)
        * Scheduler
        * Controller Manager
        > `Node Controller`, `Replication Controller`, `Endpoint Controller`, `Service Token Controller`,

    + Worker
        * Kubelet (Communicate with __*API Server*__)
        * Kube-Proxy
        * Pod

- Pod
    > Kubernetes 管理的对象，群集中的基本调度单元

- Container

- Tools (Invoke __*API*__)
    + Command Line (kubectl)
    + UI 

# Installation

- [Play-wth-k8s (PWK)](https://labs.Play-wth-k8s.com) (online version playground)
    + out of box, no need to install
    + max 5 instances (nodes)
    + 4 hours time limit

- Options
    + Minikube (all in one setup with limited resource)
    + Kubeadm (full function cluster and HA)

## Prepare

### Pre-reqs

- 3GB or more RAM
- 3 CPU Core or more
- Full network connectivity among all machines in the cluster
- Disable SWAP on all nodes
- Disable SELinux on all nodes
- Check & rename all nodes' hostname (to make it easy in future when managing the cluster)

### Prepare

- Prepare Master & Worker nodes ( CentOS 7 or above )

- Disable firewall & SWAP & SELinux on __*ALL NODES*__

    + disable firewall
        ```
        # systemctl stop firewalld
        # systemctl disable firewalld
        ```

    + disable SWAP temporary
        ```
        # swapoff -a
        ```

    + disable SWAP forever
        ```
        # sed -i 's/.\\*swap.\\*/#&/' /etc/fstab
        ```

    + disable SELinux
        ```
        # setenforce 0
        # getenforce
        # sed -i 's/enforcing/disabled/g' /etc/selinux/config
        # grep disabled /etc/selinux/config | grep -v '#'
        SELINUX=disabled
        ```

    + reboot
        ```
        # reboot
        ```

- Install Docker if Docker is absent
- Start and enable docker on all nodes

- Kubeadm, Kubelet, Kubectl on all nodes

    > baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
    > gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg

    ```
    # cat <<EOF > /etc/yum.repos.d/kubernetes.repo
    [kubernetes]
    name=Kubernetes
    baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
    enabled=1
    gpgcheck=1
    repo_gpgcheck=1
    gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
    exclude=kube*
    EOF
    ```

    ```
    # yum install -y kubeadm kubelet kubectl --disableexcludes=kubernetes
    ```

- Start and enable kubelet on all nodes

    ```
    # systemctl enable kubelet
    # systemctl start kubelet
    ```

- 将桥接的IPV4流量传递到iptables链：

    > !!! __ONLY__ adapt to __*RHEL/CentOS 7*__ !!!

    ```
    # cat <<EOF > /etc/sysctl.d/k8s.conf
    net.bridge.bridge-nf-call-ip6tables = 1
    net.bridge.bridge-nf-call-iptables = 1
    EOF
    ```

    ```
    # sysctl net.bridge.bridge-nf-call-iptables=1
    # sysctl net.ipv4.ip_forward=1
    ```

    ```
    # sysctl --system　　# 使配置生效
    ```

- Restart the systemd daemon and the kubelet service

    ```
    # systemctl daemon-reload
    # systemctl restart kebelet
    ```

## Setup

### master node

- Initialize the master nodes

    ```
    # kubeadm init --pod-network-cidr=10.240.0.0/16
    ```

    or

    ```
    # kubeadm init --pod-network-cidr=10.244.0.0/16 --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers --ignore-preflight-errors=swap --ignore-preflight-errors=SystemVerification

    Your Kubernetes control-plane has initialized successfully!

    To start using your cluster, you need to run the following as a regular user:

    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config

    You should now deploy a pod network to the cluster.
    Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
    https://kubernetes.io/docs/concepts/cluster-administration/addons/

    Then you can join any number of worker nodes by running the following on each as root:

    kubeadm join 192.168.30.216:6443 --token oeuhau.b3t5vakibrd8frdv \
        --discovery-token-ca-cert-hash sha256:a27fd47fd0a0c77ecb10a53582a76434c6fdeb35833115901dcb93d907b49e4f 
    ```

    > --pod-network-cidr使用flannel网络解决方案，默认10.244.0.0/16，如不指使用flannel时则会失败
    
    > --image-repository  使用阿里云镜像源
    
    > --ignore-preflight==SystemVerification 忽略内核版本

    > --ignore-preflight-errors=swap 忽略swap设备警告，建议禁止swap设备

    > __*!!!注意初始化命令的执行结果!!!*__

- 根据 kubeadm init 命令结果，运行脚本（__*!!!本步骤所需脚本来自上一步的执行结果!!!*__）

    > Here to save the command result from previous step

    ```
    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
    ```

    ```
    # kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
    ```

    > 服务器上运行 `kubectl apply -f` 可能会因为服务器无法访问到 `yml` 文件而导致失败
    
    > 尝试各种方法，比如在个人电脑上先访问 `https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml` , 获取到文件内容
    
    > 然后在服务器上，手动创建一个服务器本地的 `kube-flannel.yml` 文件，把个人电脑上，浏览器里访问到的内容，复制到服务器的本地文件中

    > 然后服务器上执行：`kubectl apply -f kube-flannel.yml`，可以成功

- 检查 Kubernetes 安装结果

    ```
    # kubectl get pods --all-namespaces
    ```

- 如果上面初始化命令的结果没有做记录，忘记了 `token`，可以通过如下命令：

    ```
    # kubeadm token create --print-join-command
    ```

### worker node

- Join cluster

    ```
    # kubeadm join 192.168.30.216:6443 --token oeuhau.b3t5vakibrd8frdv --discovery-token-ca-cert-hash sha256:a27fd47fd0a0c77ecb10a53582a76434c6fdeb35833115901dcb93d907b49e4f 
    ```

- Check all nodes

```
# kubectl get no
```

# Kubectl

- create, get
- describe, delete
- exec, logs

## Syntax

```
kubectl [command] [TYPE] [NAME] [flags]
```
>　command: create, get, describe, delete, logs, exec, edit, run, apply, scale, ...

>　TYPE: pod(s), deployment(s), replicaset(s), replicationcontroller(s), service(s), daemonset(s), namespace(s), persistentvolume(s), persistentvolumeclaim(s), job(s), Cronjob(s)

> flags: -w

## Example

1. create a resource from a file

    ```
    # kubectl create -f pod-example.yml
    # kubectl create -f deploy-example.yml
    # kubectl create -f <directory>
    ```

1. list one or more resources

    ```
    # kubectl get pods
    # kubectl get pods -o wide
    # kubectl get pods, deploy
    ```

1. display details

    ```
    # kubectl describe nodes <node-name>
    # kubectl describe pods <pod-name>
    # kubectl describe pods
    ```

1. delete resources

    ```
    # kubectl delete -f pod.yml
    # kubectl delete pods --all
    # kubectl delete pods, services -l name=<label-name>
    ```

1. execute a command against a container in a pod

    ```
    # kubectl exec <pod-name> date
    # kubectl exec <pod-name> -c <container-name> date
    # kubectl exec -it <pod-name> /bin/bash
    ```

1. print the logs from a container in a pod

    ```
    # kubectl logs <pod-name>
    ```
    > 输出已有日志

    ```
    # kubectl logs <pod-name> -f
    ```
    > 持续输出日志

# Pod

## Concept

- What is Pod
    > __Kubernetes__ 体系下最小的调度单元

- Multi-container
- Pod networking
    > Each Pod has its uniq IP
    > Each container inside the same Pod share the Pod IP and has its uniq port
- Inter-Pod & Intra-Pod communication
    > Each Pod can be reached by its Pod IP + its container Port
    > Pods inside the same Pod can reach each other with localhost + its container Port

- Pod lifecycle
    + Pending
    + Running
    + Succeeded
    + Failed
    
    > After `Succeeded` or `Failed`, the Pod life is finished. No one can take the Pod back from `Succeeded` or `Failed` states.

- Pod manifest file
- Pod deployment

## Demo

- Manifest file example

    ```
    # nginx-pod.yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: nginx-pod
      labels:
        app: nginx
        tier: dev
    spec:
      containers:
      - name: nginx-container
        image: nginx
    ```

- kind & apiVersion

    |Kind |apiVersion|
    |-:   | :-:|
    | Pod | v1 |
    | ReplicationController | v1 |
    | Service    | v1 |
    | ReplicaSet | apps/v1 |
    | Deployment | apps/v1 |
    | DaemonSet  | apps/v1 |
    | Job        | batch/v1 |

- Deploy with kubectl command

    ```
    # kubectl create -f nginx-pod.yaml
    pod/nginx-pod created
    ```

- Check with kubectl command

    ```
    # kubectl get pod
    # kubectl get pod -o wide
    # kubectl get pod nginx-pod -o yaml
    # kubectl describe pod nginx-pod
    ```

- Check by to ping the Pod

    ```
    # ping <Pod-IP>
    ```

- Execute command insided the Pod

    ```
    # kubectl exec -it nginx-pod -- /bin/sh
    ```

- delete the Pod with Kubectl

    ```
    # kubectl delete pod nginx-pod
    ```

# Replication Controller

## Concept

- What is Replication Controller
    
    > Ensure that a specified number of pods are running at any time

- What the senario is RC for
    
    + High Availability
    + Load Balancing

- labels
    > Replication Controller and Pods are associated with 'lables'

## Demo

- Manifest file example

    ```
    # nginx-rc.yaml
    apiVersioin: v1
    kind: ReplicationController
    metadata:
      name: nginx-rc
    spec:
      replicas: 3
      selector:
        app: nginx-app
      template:
        metadata:
          name: nginx-pod
          labels:
            app: nginx-app
        spec:
          containers:
          - name: nginx-container
            image: nginx
            ports:
            - containerPort: 80
    ```

- Deploy with kubectl command

    ```
    # kubectl create -f nginx-rc.yaml
    replicationcontroller/nginx-rc created
    ```

- Check with kubectl command

    ```
    # kubectl get pods
    # kubectl get po -l app=nginx-app
    # kubectl get po -o wide
    # kubectl describe rc nginx-rc
    # kubectl get nodes
    ```

- Scaling up with kubectl command

    ```
    # kubectl scale rc nginx-rc --replicas=5
    # kubectl get rc nginx-rc
    # kubectl get po -o wide
    ```

- Scaling down with kubectl command

    ```
    # kubectl scale rc nginx-rc --replicas=3
    # kubectl get rc nginx-rc
    # kubectl get po -o wide
    ```

- delete with Kubectl

    ```
    # kubectl delete -f nginx-rc.yaml
    # kubectl get rc nginx-rc
    # kubectl get po -o wide
    ```

# ReplicaSet

## Concept

- What is ReplicaSet
    > Ensure that a specified number of pods are running at any time

- What the senario is ReplicaSet for
    > Next generation of RC
    
    + High Availability
    + Load Balancing

- labels
    > ReplicaSet and Pods are associated with 'lables'

- selector
    + Equality-based

        * Syntax
            > `=`, `==`, `!=`
        
        * Example
            > `env = production`, `tier != frontend`

        * command line
            > `# kubectl get pods -l env=production`

        * Used in
            > Services & Replication Controller
    
    + Set-based

        * Syntax
            > `in`, `notin`, `exists`
        
        * Example
            > `env in (production, qa)`, `tier notin (frontend, backend)`

        * command line
            > `# kubectl get pods -l 'env in (production)'`

        * Used in
            > ReplicaSet, Deployment, DaemonSet, Job

## Demo

- Manifest file example

    ```
    # nginx-rs.yaml
    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
      name: nginx.rs
    spec:
      replicas: 3
      selector:
        matchLabels:
            app: nginx-app
        matchExpressions:
            - {key: tier, operator: In, values: [frontend]}
      template:
        metadata:
          name: nginx-pod
          labels:
            app: nginx-app
            tier: frontend
        spec:
          containers:
          - name: nginx-container
            image: nginx
            ports:
            - containerPort: 80
    ```

- Deploy with kubectl command

    ```
    # kubectl create -f nginx-rs.yaml
    replicaset/nginx-rs created
    ```

- Check with kubectl command

    ```
    # kubectl get pods
    # kubectl get po -o wide
    # kubectl get po -l tier=frontend
    # kubectl get rs nginx.rs -o wide
    # kubectl describe rs nginx.rs
    # kubectl get nodes
    ```

- Scaling up with kubectl command

    ```
    # kubectl scale rs nginx.rs --replicas=5
    # kubectl get rs nginx.rs
    # kubectl get po -o wide
    ```

- Scaling down with kubectl command

    ```
    # kubectl scale rs nginx.rs --replicas=3
    # kubectl get rs nginx.rs
    # kubectl get po -o wide
    ```

- delete with Kubectl

    ```
    # kubectl delete -f nginx-rs.yaml
    # kubectl get rs nginx.rs
    # kubectl get po -o wide
    ```

# Deployments

## Concept

> Pods can be managed manually

> Pods can be managed by __*Replication Controller*__ or __*ReplicaSet*__

> Pods can be managed by __*Deployments*__

- What is __*Deployments*__
    > Ensure zero downtime when upgrade and rollback

- What the senario is __*Deployments*__ for
    + Upgrade & Rollback
    + Sequentially in order
    + Zero downtime
    + Pause & Resume

- Types
    + Recreate
    + RollingUpdate
    + Canary
    + Blue / Green

## Demo 1

- Manifest file example

    ```
    # nginx-deploy.yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-deployment
      labels:
        app: nginx-app
    spec:
      replicas: 3
      selector:
        matchLabels:
            app: nginx-app
        matchExpressions:
            - {key: tier, operator: in, values: [frontend]}
      template:
        metadata:
          name: nginx-pod
          labels:
            app: nginx-app
            tier: frontend
        spec:
          containers:
          - name: nginx-container
            image: nginx
            imagePullPolicy: IfNotPresent
            ports:
            - containerPort: 80
    ```

- Deploy with kubectl command

    ```
    # kubectl create -f nginx-deploy.yaml
    deployment.apps/nginx-deployment created
    ```

- Check with kubectl command

    > One __*ReplicaSet*__ will be created automatically backend

    ```
    # kubectl get rs -l app=nginx-app
    ```

    ```
    # kubectl get deploy -l app=nginx-app
    # kubectl describe deploy nginx-deployment
    ```

    ```
    # kubectl get po -l app=nginx-app
    # kubectl get nodes
    ```

- Upgrade with kubectl command

    + `set` command
        ```
        # kubectl set image deploy nginx-deployment nginx-container=nginx:1.9.1
        deployment.extensions/nginx-deployment image updated
        ```

    + `edit` command
        ```
        # kubectl edit deploy nginx-deployment
        deployment.extensions/nginx-deployment image updated
        ```

- Rollback with kubectl command
    + `set` command with wrong version number
        ```
        # kubectl set image deploy nginx-deployment nginx-container=nginx:2020 --record
        ```

    + check status & history
        ```
        # kubectl rollout status deployment/nginx-deployment
        # kubectl rollout history deployment/nginx-deployment
        ```

    + rollback
        ```
        # kubectl rollout undo deployment/nginx-deployment
        ```
    
    + double check
        ```
        # kubectl rollout status deployment/nginx-deployment
        ```

- Scaling up with kubectl command

    ```
    # kubectl scale deployment nginx-deployment --replicas=5
    # kubectl get deploy
    # kubectl get po -o wide
    ```

- Scaling down with kubectl command

    ```
    # kubectl scale deployment nginx-deployment --replicas=1
    # kubectl get deploy
    # kubectl get po -l app=nginx-app
    ```

- delete with Kubectl

    ```
    # kubectl delete -f nginx-deploy.yaml
    # kubectl get rs nginx-rs
    # kubectl get po -o wide
    ```

## Demo 2

- 准备一个自己的 Docker Image
    > Dockerfile
    ```
    FROM nginx:1.17.6-alpine

    ADD ./www /www
    ```

- 创建 `www` 目录，并在该目录下创建 `index.html`
    > index.html
    ```
    version # 1.0.0
    hello world
    ```

- 构建自己的镜像
    > 镜像需要存在于 worker node，而不是 master node
    ```
    # docker build ./ -t chris/demo
    ```

- 使用自己的镜像 `chris/demo`，重复 __*Demo 1*__

- 创建 `demo-deploy.yaml`

    ```
    # cp nginx-deploy.yaml demo-deploy.yaml
    ```

- 更新 `demo-deploy.yaml`
    > 为了让 kuburnetes 能够使用本地的镜像（`chris/demo`），而不是从网上拉取镜像

    ```
    imagePullPolicy: IfNotPresent
    ```

- deploy 创建之后，进入 Pod，检查 `www/index.html`
    ```
    # kubectl exec -it demo-deployment-xxxxxxxx -- /bin/sh
    ```

- 更新 `www/index.html` 的内容，重新构建 `chris/demo`
    > 通过 `docker images` 可以看到，镜像的 `IMAGE ID` 发生了变化

- 通过 `edit` 方式，编辑 `demo-deploy.yaml`，然后 `demo-deployment` 自动完成升级

- 检查 Pods
    > 原有的 Pods 被终止了，新的 Pods 被创建了；新 Pods 用到了最新的镜像内容

- Rollback
    > 如果之前的升级，没有带版本号的话，rollback 无法发挥作用
    
    > 所以，如果希望回滚有效，镜像必须要有明确的版本号

# Services

## Concept

- What is __*Services*__
    > Permanent access point of the Pod(s)

- What the senario is __*Services*__ for
    + After Pods are deleted and created dynamicly, they will have new IP address, how to access these Pods within the cluster
    + How to expose Pods service outside of the cluster

- Types
    + ClusterIP (within the cluster)
    + NodePort (expose to outside world)
    + LoadBalancer

# NodePort Service

## Concept

- What is __*NodePort Services*__
    > Permanent access point of the __*Pod(s)*__ from outside world in `<IP>:<Port>` format

- __*NodeIP*__ & __*NodePort*__
    >- Outside world will access `<NodeIP>:<NodePort>`
    >- __*NodePort*__ range: `30000` ~ `32767`

- __*NodePort Service*__
    >- When outside world request on `<NodeIP>:<NodePort>`, __*NodePort Service*__ will response.
    >- __*NodePort Service*__ will foreward the request to the __*Pod*__ which is associated to it
    >- __*Port*__ on __*NodePort Service*__ is `80`
    >- __*TargetPort*__ on __*Pod*__ is `80`

- Types
    + NodePort (from outside world point of view)
    + Port (Port on the NodePort Service)
    + TargetPort (Port on the Pod)

- 注意事项

    >- 对一个 K8S 群集（cluster）来说，某一个端口（NodePort），只能有一个 NodePort Service
    >- NodePort Service 根据 labels 来关联到一个或多个 Pods
    >- 如果是多个 Podes，无论 Pods 是在同一个 Node 上，还是分布在不同的 Node 上，外界都可以通过`<NodeIP>:<NodePort>`来访问到对应的 Pods
    
## Demo

- Manifest file example

    ```
    # nginx-svc-np.yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: proxy-service
      labels:
        app: nginx-app
    spec:
      selector:
        app: nginx-app
      type: NodePort
      ports:
        - nodePort: 31000
          port: 80
          targetPort: 80
    ```

- Deploy with kubectl command

    ```
    # kubectl create -f nginx-deploy.yaml
    # kubectl create -f nginx-src-np.yaml
    ```

- Check with kubectl command

    ```
    # kubectl get service -l app=nginx-app
    ```

- Check with browser
    > 通过 __*NodePort*__，无论是 Master Node IP，还是 Worker Node 的IP，都可以访问到 EndPoint

- delete with Kubectl

    ```
    # kubectl delete svc proxy-service
    # kubectl get pods
    ```

# LoadBalancer

## Concept

- What is __*LoadBalancer Services*__
    > Permanent access point of the __*Pod(s)*__ from outside world in `URL` format

- sernario
    >- 如果有多个 Pods 运行在不同的 Nodes 上面，__*NodePort service*__ 会使得通过任何一个 Node 的 `<NodeIP>:<NodePort>`，都可以访问到 __*NodePort Service*__
    >- 如何能通过一个统一的 Access Point 发布这个 Service

## Demo

> LoadBalancer 能否成功创建，取决于云服务提供商

- Manifest file example

    ```
    # nginx-svc-lb.yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: lb-service
      labels:
        app: nginx-app
    spec:
      selector:
        app: nginx-app
      type: LoadBalancer
      ports:
        - nodePort: 31000
          port: 80
          targetPort: 80
    ```

- Deploy with kubectl command

    ```
    # kubectl create -f nginx-deploy.yaml
    # kubectl create -f nginx-src-lb.yaml
    ```

- Check with kubectl command

    ```
    # kubectl get service -l app=nginx-app
    ```

- delete with Kubectl

    ```
    # kubectl delete svc lb-service
    # kubectl get pods
    ```

# ClusterIP

## Concept

- What is __*ClusterIP Services*__
    > Access point ONLY within the cluster internal

## Demo

- Manifest file example

    ```
    # redis-master-deployment.yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: redis-master
      labels:
        app: redis
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: redis
          role: master
          tier: backend
      template:
        metadata:
          labels:
            app: redis
            role: master
            tier: backend
      spec:
        containers:
        - name: master
          image: k8s.gcr.io/redis:e2e
          resources:
            requests:
              memeory: 100Mi
          ports:
          - containerPort: 6379
    ```

    ```
    # redis-slave-deployment.yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: redis-slave
      labels:
        app: redis
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: redis
          role: slave
          tier: backend
      template:
        metadata:
          labels:
            app: redis
            role: slave
            tier: backend
      spec:
        containers:
        - name: slave
          image: gcr.io/google_samples/gb-redisslave:v1
          resources:
            requests:
              memeory: 100Mi
          ports:
          - containerPort: 6379
    ```

    ```
    # redis-master-service.yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: redis-master-svc
      labels:
        app: nginx-app
        role: master
        tier: backend
    spec:
      selector:
        app: redis
        role: master
        tier: backen
      type: ClusterIP
      ports:
        - port: 6379
          targetPort: 6379
    ```

- Deploy with kubectl command

    ```
    # kubectl create -f nginx-deploy.yaml
    # kubectl create -f nginx-src-lb.yaml
    ```

- Check with kubectl command

    ```
    # kubectl get service -l app=nginx-app
    ```

- delete with Kubectl

    ```
    # kubectl delete svc lb-service
    # kubectl get pods
    ```

# Storage Volume

## emptyDir volume
## HostPath volume
## Persistent Volume & Persistent Volume Claim
## Static Volume vs Dynamic Volume

# ConfigMap

# DaemonSet

# Secrets

# Jobs
