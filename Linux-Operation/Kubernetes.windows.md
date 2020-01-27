# Reference

- [How to setup Kubernetes Cluster Environment with UI Dashboard (From 7:55)](https://www.youtube.com/watch?v=3KupfEUC10Q)

# On Host Machine (Windows 10)

- [通过 curl 命令安装 kubectl 可执行文件](https://kubernetes.io/zh/docs/tasks/tools/install-kubectl/#%e5%9c%a8-windows-%e4%b8%8a%e7%94%a8-chocolatey-%e5%ae%89%e8%a3%85-kubectl)

## 下载 `kubectl.exe`

- [下载地址](https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/windows/amd64/kubectl.exe)

- 保存目录

```
C:\Users\Chris\Downloads\Software\kube
```

- 更新系统环境变量 `Path`，增加 `C:\Users\Chris\Downloads\Software\kube`

## 复制集群配置信息

#### 为当前用户创建目录 `.kube`

```
C:\Users\Chris\.kube
```

#### 将 kubernetes 中的 config 文件复制到上面新创建的文件夹

- 源文件：`/etc/kubernetes/admin.conf`
- 目标文件：`C:\Users\Chris\.kube\config`
