# 参考

[在 Kubernetes集群中 安装 KubeSphere2.1](https://kubesphere.com.cn/forum/d/1272-k8s-kubesphere2-1)
[k8s apiserver证书添加新地址](https://zhuanlan.zhihu.com/p/93015122)

# 环境概述

- 阿里云 ECS (2C 8G) x2
- CentOS 7.8
- xxx.xxx.xxx.150: k8s-m1 (master)
- xxx.xxx.xxx.151: k8s-w1 (worker)

# 准备工作

#### 检查操作系统版本

```
# cat /etc/redhat-release
CentOS Linux release 7.8.2003 (Core)
```

#### 检查并修改机器名称

```
# hostname
# hostnamectl
# cat /etc/hostname
!@#$@%$^#$^#%%#$#^
```

```
# vi /etc/hostname
# systemctl restart systemd-hostnamed
```

```
# reboot
```

#### 配置集群 hosts (私有地址)

```
# vi /etc/hosts
```

```
xxx.xxx.xxx.150 k8s-m1
xxx.xxx.xxx.151 k8s-w1
```

#### 禁用`防火墙`

```
# systemctl stop firewalld && systemctl disable firewalld
# systemctl stop firewalld
```

#### 禁用`selinux`

```
# setenforce 0
# sed -i '7s/enforcing/disabled/' /etc/selinux/config
```

```
# reboot
```

#### 创建`/etc/sysctl.d/k8s.conf`文件

> 创建文件并添加内容

```
# cat >/etc/sysctl.d/k8s.conf <<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
EOF
```

> 执行命令使之生效

```
# modprobe br_netfilter && sysctl -p /etc/sysctl.d/k8s.conf
```

#### 安装ipvs

> 创建文件并添加内容（保证在节点重启后能自动加载所需模块）

```
# cat > /etc/sysconfig/modules/ipvs.modules <<EOF
#!/bin/bash
modprobe -- ip_vs
modprobe -- ip_vs_rr
modprobe -- ip_vs_wrr
modprobe -- ip_vs_sh
modprobe -- nf_conntrack_ipv4
EOF
```

> 修改权限以及查看是否已经正确加载所需的内核模块

```
# chmod 755 /etc/sysconfig/modules/ipvs.modules && bash /etc/sysconfig/modules/ipvs.modules
```

> 查看是否已经正确加载所需的内核模块

```
# lsmod | grep -e ip_vs -e nf_conntrack_ipv4
nf_conntrack_ipv4      15053  0 
nf_defrag_ipv4         12729  1 nf_conntrack_ipv4
ip_vs_sh               12688  0 
ip_vs_wrr              12697  0 
ip_vs_rr               12600  0 
ip_vs                 145497  6 ip_vs_rr,ip_vs_sh,ip_vs_wrr
nf_conntrack          139264  2 ip_vs,nf_conntrack_ipv4
libcrc32c              12644  2 ip_vs,nf_conntrack
```

> 安装 `ipset` 和 `ipvsadm` (便于查看 ipvs 的代理规则)

```
# yum -y install ipset ipvsadm
```

#### 同步服务器时间

> 安装chrony

```
# yum -y install chrony
```

> 修改同步服务器地址为阿里云

```
# sed -i.bak '3,6d' /etc/chrony.conf && sed -i '3cserver ntp1.aliyun.com iburst' /etc/chrony.conf
```

> 启动`chronyd`及加入开机自启

```
# systemctl start chronyd && systemctl enable chronyd
```

> 查看同步结果

```
# chronyc sources
```

#### 关闭`swap`分区

> 手动关闭swap

```
# swapoff -a
```

> 修改fstab文件，注释swap自动挂载 (!!!!!! 此处有些问题：貌似原文件中并没有这句话，因此这个命令实际并未发生作用 !!!!!!)

```
# sed -i '/^\/dev\/mapper\/centos-swap/c#/dev/mapper/centos-swap swap                    swap    defaults        0 0' /etc/fstab
```

> 查看swap是否关闭

```
# free -m
              total        used        free      shared  buff/cache   available
Mem:           7821         123        7395           0         301        7472
Swap:             0           0           0
```

> `swappiness` 参数调整，修改`/etc/sysctl.d/k8s.conf`添加下面一行

```
# cat >>/etc/sysctl.d/k8s.conf <<EOF
vm.swappiness=0
EOF
```

> 使配置生效

```
# sysctl -p /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
vm.swappiness = 0
```

# 安装

#### 安装 Docker18.09.9

> 安装 `yum-utils` 命令包，从而可以使用 `yum-config-manager` 命令

```
yum -y install yum-utils
```

> 添加阿里云yum源

```
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

> 查看可用版本

```
yum list docker-ce --showduplicates | sort -r
已加载插件：fastestmirror, langpacks
可安装的软件包
 * updates: mirrors.aliyun.com
Loading mirror speeds from cached hostfile
 * extras: mirrors.aliyun.com
docker-ce.x86_64            3:19.03.5-3.el7                     docker-ce-stable
docker-ce.x86_64            3:19.03.4-3.el7                     docker-ce-stable
。。。。。。
docker-ce.x86_64            3:18.09.9-3.el7                     docker-ce-stable
docker-ce.x86_64            3:18.09.8-3.el7                     docker-ce-stable
docker-ce.x86_64            3:18.09.7-3.el7                     docker-ce-stable
docker-ce.x86_64            3:18.09.6-3.el7                     docker-ce-stable
。。。。。。
```

> 安装docker18.09.9

```
yum -y install docker-ce-18.09.9-3.el7 docker-ce-cli-18.09.9
```

> 启动docker并设置开机自启

```
systemctl enable docker && systemctl start docker
```

> 配置阿里云docker镜像加速

```
cat > /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://gqk8w9va.mirror.aliyuncs.com"]
}
EOF
```

> 配置完后重启docker

```
systemctl restart docker
```

> 查看加速

```
docker info
```

找到Registry Mirrors一行
Registry Mirrors:
 https://gqk8w9va.mirror.aliyuncs.com/
  
> 查看docker版本

```
docker version

Client:
 Version:           18.09.9
 API version:       1.39
 Go version:        go1.11.13
 Git commit:        039a7df9ba
 Built:             Wed Sep  4 16:51:21 2019
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          18.09.9
  API version:      1.39 (minimum version 1.12)
  Go version:       go1.11.13
  Git commit:       039a7df
  Built:            Wed Sep  4 16:22:32 2019
  OS/Arch:          linux/amd64
  Experimental:     false
```

#### 修改`docker Cgroup Driver`为`systemd`

> 将/usr/lib/systemd/system/docker.service文件中的这一行 ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
> 修改为 ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock --exec-opt native.cgroupdriver=systemd
> 如果不修改，在添加 worker 节点时可能会碰到如下错误
> [WARNING IsDockerSystemdCheck]: detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd". 
Please follow the guide at https://kubernetes.io/docs/setup/cri/

> 使用如下命令修改

```
sed -i.bak "s#^ExecStart=/usr/bin/dockerd.*#ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock --exec-opt native.cgroupdriver=systemd#g" /usr/lib/systemd/system/docker.service
```

> 重启docker

```
systemctl daemon-reload && systemctl restart docker
```

#### 安装`Kubeadm`

> 使用阿里云`yum`源

```
cat >/etc/yum.repos.d/kubernetes.repo <<EOF
[kubernetes]
name=Kubernetes
baseurl=http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=http://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
        http://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF
```

> 安装 `kubeadm`、`kubelet`、`kubectl` (阿里云yum源会随官方更新最新版，因此指定版本)

> 安装1.18.4版本

```
yum -y install kubelet-1.18.4 kubeadm-1.18.4 kubectl-1.18.4
```

> 查看版本

```
kubeadm version

kubeadm version: &version.Info{Major:"1", Minor:"16", GitVersion:"v1.18.4", GitCommit:"a17149e1a189050796ced469dbd78d380f2ed5ef", GitTreeState:"clean", BuildDate:"2020-04-16T11:42:30Z", GoVersion:"go1.13.9", Compiler:"gc", Platform:"linux/amd64"}
```

> 设置`kubelet`开机自启

```
systemctl enable kubelet
```

> 设置`k8s`命令自动补全

```
yum -y install bash-completion
source /usr/share/bash-completion/bash_completion
source <(kubectl completion bash)
echo "source <(kubectl completion bash)" >> ~/.bashrc
```

# 初始化集群

## 初始化 `master` 节点

#### 配置 kubeadm 初始化文件

```
cat <<EOF > ./kubeadm-config.yaml
apiVersion: kubeadm.k8s.io/v1beta2
kind: ClusterConfiguration
kubernetesVersion: v1.18.3
imageRepository: registry.cn-hangzhou.aliyuncs.com/google_containers

#master地址
controlPlaneEndpoint: "172.17.64.150:6443"	
networking:
  serviceSubnet: "10.96.0.0/16"	

  #k8s容器组所在的网段
  podSubnet: "10.20.0.1/16"	
  dnsDomain: "cluster.local"

# 为了让证书包含公网IP，从而允许从外网访问集群
apiServer:
  certSANs:       #填写所有kube-apiserver节点的hostname、IP、VIP
  - k8s-m1        #请替换为hostname
  - 47.95.33.159  #请替换为公网
  - 172.17.64.150 #请替换为私网
  - 10.96.0.1     #不要替换，此IP是API的集群地址，部分服务会用到

EOF
```

#### 初始化master

> ⚠️如果想要重新初始化，需要执行命令 `kubeadm reset -f`

> `kubeadm init --config=kubeadm-config.yaml --upload-certs`

```
# kubeadm init --config=kubeadm-config.yaml

....

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of control-plane nodes by copying certificate authorities
and service account keys on each node and then running the following as root:

  kubeadm join 172.17.64.150:6443 --token ykas96.el7j6myqr38i869k \
    --discovery-token-ca-cert-hash sha256:d417b9f49aa793e0b84c9e7fcf6efa21dedfdaa6fa426cdf4d7ff961d9fe66cf \
    --control-plane 

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 172.17.64.150:6443 --token ykas96.el7j6myqr38i869k \
    --discovery-token-ca-cert-hash sha256:d417b9f49aa793e0b84c9e7fcf6efa21dedfdaa6fa426cdf4d7ff961d9fe66cf 

```

> ⚠️ 保存 token sha256

> 拷贝 `kubeconfig` 文件（这里的路径为 `/root`）

```
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config
```

## 初始化 `worker` 节点

> 将master节点上的 `$HOME/.kube/config` 文件拷贝到 `worker` 节点对应的文件中

```
mkdir -p $HOME/.kube 
scp k8s-m1:~/.kube/config $HOME/.kube
chown $(id -u):$(id -g) $HOME/.kube/config
```

> 将 `worker` 节点加入到集群中

> 这里需要用到2.2中初始化master最后生成的token和sha256值

```
kubeadm join 172.17.64.150:6443 --token ykas96.el7j6myqr38i869k \
    --discovery-token-ca-cert-hash sha256:d417b9f49aa793e0b84c9e7fcf6efa21dedfdaa6fa426cdf4d7ff961d9fe66cf 

... ...

This node has joined the cluster:
* Certificate signing request was sent to apiserver and a response was received.
* The Kubelet was informed of the new secure connection details.

Run 'kubectl get nodes' on the control-plane to see this node join the cluster.
```

> 如果忘记了token和sha256值，可以在master节点使用如下命令查看

```
#kubeadm token list
TOKEN                     TTL       EXPIRES                     USAGES                   DESCRIPTION   EXTRA GROUPS
px979r.mphk9ee5ya8fgy44   20h       2020-03-18T13:49:48+08:00   authentication,signing   <none>        system:bootstrappers:kubeadm:default-node-token
```         
            
> 查看sha256

```
#openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'
5e7c7cd1cc1f86c0761e54b9380de22968b6b221cb98939c14ab2942223f6f51
```

> 同时查看token和sha256

```
#kubeadm token create --print-join-command
kubeadm join 192.168.9.10:6443 --token 9b28zg.oyt0kvvpmtrem4bg     --discovery-token-ca-cert-hash sha256:5e7c7cd1cc1f86c0761e54b9380de22968b6b221cb98939c14ab2942223f6f51
```

> master节点查看node（发现状态都是NotReady，因为还没有安装网络插件，这里我们安装calio官方插件文档）

```
kubectl get nodes
```

## `Master` 节点安装网络插件calio

> 下载文件

```
wget https://docs.projectcalico.org/v3.8/manifests/calico.yaml
```

> 因为在上边kubeadm-config.yaml配置文件中指定了容器组IP，所以需要将文件中的625行改为如下：

```
value: "10.20.0.1/16"
```

> 修改完成后安装calico网络插件

```
kubectl apply -f calico.yaml
```

> 安装完成后稍等一会查看pods状态

```
kubectl get pods -n kube-system
```

> 查看node状态

```
kubectl get nodes 
```

# 准备镜像

#### 镜像列表

- registry.cn-beijing.aliyuncs.com/caskbank/worker:0.2.0-archellis
- registry.cn-beijing.aliyuncs.com/caskbank/service:0.2.0-archellis
- registry.cn-beijing.aliyuncs.com/caskbank/frontend:0.2.0-archellis
- rabbitmq:3.8.2-alpine
- postgres:12.1-alpine
- node:12.14.1-alpine
- redis:5.0.7-alpine
- nginx:1.17.6-alpine
- busybox

#### 命令 - 登录阿里云镜像服务

```
docker login -u [user name] -p [password] registry.cn-hangzhou.aliyuncs.com
```

```
sudo docker login --username=smcc9191 registry.cn-beijing.aliyuncs.com
```

> 可以参考阿里云镜像服务的命令行提示

#### 命令 - 获取镜像

```
docker pull
```

# 安装 Git

```
yum install git
```

# 获取 Demo 脚本

> git repo of dockerimages

```
git clone --depth=1 https://[user name]:[password]@github.com/YunzhiWei/dockerimages.git
```

# 测试 Nginx 容器服务

> 注意阿里云 `ECS` 安全组的安全策略，需要打开 `80` 端口

#### 启动 nginx 容器服务

> 通过暴露 `80` 端口提供服务

```
kubectl create -f nginx-demo-port.yaml
```

#### 等待 nginx 容器服务 `ready`

```
kubectl get po
```

#### 检查 nginx 服务提供的 web page

> 打开浏览器，输入 `http://[Worker Node 的 IP]:80`，可以看到页面

> 打开浏览器，输入 `http://[url]`，可以看到页面（[url] 需要事先在 `hosts` 文件中配置正确）

#### 停止 nginx 容器服务

```
kubectl delete -f nginx-demo-port.yaml
```

# 启动 Ingress 

## Ingress Controller of Traefik

> 切换到 `architecture/traefik` 目录

#### Apply rbac role and role binding

```
# kubectl apply -f traefik-rbac.yaml
# kubectl describe clusterrole traefik-ingress-controller -n kube-system
```

#### Apply daemonset

```
kubectl apply -f traefik-ds.yaml
kubectl get all -n kube-system | grep traefik
```

## Nginx Deployment

> 切换回 `demo` 目录

```
kubectl create -f nginx-demo-ingress.yaml 
```

```
kubectl get po
kubectl get deploy
```

## ClusterIP Service

```
kubectl expose deploy nginx-demo-dp --port 80
```

```
kubectl get service
```

## Ingress Resource

```
kubectl create -f ingress-resource.yaml
```

```
kubectl get ing
kubectl get describe ing ingress-resource
```

> 打开浏览器，输入域名

## Nginx Deployment & ClusterIP Service & Ingress Resource

> 动态监测 `K8S` 集群状态

```
kubectl get all -o wide --all-namespaces
watch !!
```

```
kubectl create -f ingress-demo.yaml
```

> `ingress-demo.yaml` 中包含了：`nginx-demo-ingress.yaml` 和 `ingress-resource` 的内容，并且还包含了 `Cluster IP Service`

```
kubectl get po
kubectl get deploy
kubectl get service
kubectl get ing
kubectl get describe ing ingress-resource
```

> 打开浏览器，输入域名，可以访问页面；输入 IP 则不行 ！！！
