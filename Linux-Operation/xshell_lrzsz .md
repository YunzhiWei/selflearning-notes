# 利用 XShell 在 Windows 和 Linux 之间传输文件

* [](https://jingyan.baidu.com/article/3a2f7c2e27e01b26afd611cc.html)

1. 安装

```
[root@.... ~]# yum install  lrzsz -y
```

2. 检查安装结果

```
[root@.... ~]# rpm -qa |grep lrzsz

3. 上传文件（上传到 Linux）

```
[root@.... ~]# rz
```

4. 下载文件（下载到 XShell）

```
[root@.... ~]# sz [filename]
```
