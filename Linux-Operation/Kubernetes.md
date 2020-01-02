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
    cat <<EOF > /etc/sysctl.d/k8s.conf
    net.bridge.bridge-nf-call-ip6tables = 1
    net.bridge.bridge-nf-call-iptables = 1
    EOF
    ```

    ```
    sysctl --system　　# 是配置生效
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
    apiVersioin: v1
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
    > HA

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

# Deployments

# Services

# NodePort Service

# Load Balancing

# Cluster IP

# Storage Volume

## emptyDir volume
## HostPath volume
## Persistent Volume & Persistent Volume Claim
## Static Volume vs Dynamic Volume

# ConfigMap

# DaemonSet

# Secrets

# Jobs
