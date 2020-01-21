# 服务发现无法正常工作

## 参考

- [代码库](https://github.com/YunzhiWei/dockerimages.git)
- [环境](https://github.com/YunzhiWei/selflearning-notes/blob/master/Linux-Operation/Kubernetes.install-cluster.md)
- [操作](https://github.com/YunzhiWei/selflearning-notes/blob/master/Linux-Operation/Kubernetes.demo.md)
- [搭建Kubernetes集群踩坑日志之coreDNS 组件出现CrashLoopBackOff问题的解决](https://blog.csdn.net/u011663005/article/details/87937800)
- [使用Kubeadm(1.13+)快速搭建Kubernetes集群](https://www.cnblogs.com/RainingNight/p/using-kubeadm-to-create-a-cluster-1-13.html)
- [coredns pods have CrashLoopBackOff or Error state](https://stackoverflow.com/questions/53075796/coredns-pods-have-crashloopbackoff-or-error-state)
- [Fresh deploy with CoreDNS not resolving any dns lookup](https://github.com/kubernetes/kubeadm/issues/1056)

## 问题说明

> 按照 `Demo - K8S Service of ClusterIP` 中描述的步骤，在启动 `dbpg-svc-ci.yaml` 之后，无法通过服务名称 `dbpg` 来访问数据库服务，只能通过 `<ClusterIP>` 来访问数据库服务

## 调查

### 补充

- 上述问题发生的环境是： `Windows 10` 系统作为 `Hosting`，`VMware` 虚机作为 `Kubernetes Cluster`
- 同样的代码，在办公室服务器组成的 `Kubernetes Cluster` 环境下，没有这个问题

> 结论：应该不是代码的问题，还是集群环境的问题

### 操作

#### 检查当前 Kubernetes 集群状态

> 命令
```
# kubectl get all -n kube-system
```

> 结果
```
NAME                                       READY   STATUS             RESTARTS   AGE
pod/coredns-7f9c544f75-548r5               0/1     CrashLoopBackOff   579        4d1h
pod/coredns-7f9c544f75-mhqhd               0/1     CrashLoopBackOff   579        4d1h
pod/etcd-k8s-master-1                      1/1     Running            2          4d1h
pod/kube-apiserver-k8s-master-1            1/1     Running            2          4d1h
pod/kube-controller-manager-k8s-master-1   1/1     Running            2          4d1h
pod/kube-flannel-ds-amd64-cvm2f            1/1     Running            2          4d1h
pod/kube-flannel-ds-amd64-sbq4k            1/1     Running            2          4d1h
pod/kube-proxy-4cc6n                       1/1     Running            2          4d1h
pod/kube-proxy-szs4s                       1/1     Running            2          4d1h
pod/kube-scheduler-k8s-master-1            1/1     Running            2          4d1h

NAME               TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)                  AGE
service/kube-dns   ClusterIP   10.96.0.10   <none>        53/UDP,53/TCP,9153/TCP   4d1h

NAME                                     DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR                 AGE
daemonset.apps/kube-flannel-ds-amd64     2         2         2       2            2           <none>                        4d1h
daemonset.apps/kube-flannel-ds-arm       0         0         0       0            0           <none>                        4d1h
daemonset.apps/kube-flannel-ds-arm64     0         0         0       0            0           <none>                        4d1h
daemonset.apps/kube-flannel-ds-ppc64le   0         0         0       0            0           <none>                        4d1h
daemonset.apps/kube-flannel-ds-s390x     0         0         0       0            0           <none>                        4d1h
daemonset.apps/kube-proxy                2         2         2       2            2           beta.kubernetes.io/os=linux   4d1h

NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/coredns   0/2     2            0           4d1h

NAME                                 DESIRED   CURRENT   READY   AGE
replicaset.apps/coredns-7f9c544f75   2         2         0       4d1h

```

### 发现

- `pod/coredns-*` （两个） 的状态为 `CrashLoopBackOff`
- `deployment.apps/coredns` AVAILABLE 是 0
- `replicaset.apps/coredns-7f9c544f75` READY 是 0

### 分析

- [coredns pods have CrashLoopBackOff or Error state](https://stackoverflow.com/questions/53075796/coredns-pods-have-crashloopbackoff-or-error-state)

This error

```
[FATAL] plugin/loop: Seen "HINFO IN 6900627972087569316.7905576541070882081." more than twice, loop detected
```

is caused when CoreDNS detects a loop in the resolve configuration, and it is the intended behavior. You are hitting this issue:

> https://github.com/kubernetes/kubeadm/issues/1162

> https://github.com/coredns/coredns/issues/2087

### Hacky solution: Disable the CoreDNS loop detection

#### Edit the CoreDNS configmap:

```
# kubectl -n kube-system edit configmap coredns
```
> Remove or comment out the line with `loop`, save and exit.

#### Remove the CoreDNS pods
> so new ones can be created with new config

```
# kubectl -n kube-system get po
```
> to see all `coredns` nodes in `CrashLoopBackOff`

```
# kubectl -n kube-system delete po coredns-<id-running-in-master-node>
# kubectl -n kube-system delete po coredns-<id-running-in-worker-node>
```
> to delete all `coredns` nodes in `CrashLoopBackOff`

```
# kubectl -n kube-system get po
```
> to make sure all `coredns` nodes are `Running`
