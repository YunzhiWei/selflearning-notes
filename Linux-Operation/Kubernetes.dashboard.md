# Reference

- [kubadm安装kubernetes集群和Dashboard UI v2.0.0-beta1](https://www.jianshu.com/p/521600428701)
- [从零开始搭建Kubernetes集群（四、搭建K8S Dashboard）](https://www.jianshu.com/p/6f42ac331d8a)
- [Readme](https://github.com/kubernetes/dashboard/blob/master/README.md)
- [Manefest](https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-rc2/aio/deploy/recommended.yaml)

# Download yaml file

```
https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-rc2/aio/deploy/recommended.yaml
```

# Update yaml file

```
kind: Service
... ...
metadata:
  labels:
    k8s-app: kubernetes-dashboard
... ...
spec:
  type: NodePort
  ports:
    - port: 443
      targetPort: 8443
      nodePort: 30443
... ...
```

```
... ...
imagePullPolicy: IfNotPresent
... ...
imagePullPolicy: IfNotPresent
... ...
```

# Start

```
# kubectl apply -f recommended.yaml
```

# Create Service Account

```
# kubectl apply -f sa-cluster-admin.yaml
```

# Get token

```
kubectl get namespace
kubectl get secret -n kube-system
kubectl describe secret -n kube-system dashboard-admin-token-`<xxxxx>`
```

# Copy the Token

# Access from Firefox

```
https://192.168.83.132:30443
```

# Clear Up

```
# kubectl delete -f recommended.yaml
# kubectl delete -f sa-cluster-admin.yaml
```
