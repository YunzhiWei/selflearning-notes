
#

## [ctrl-z、bg、fg、&、vim](https://blog.csdn.net/yimingsilence/article/details/72724292)

## screen

[Linux——CentOS7之screen安装与命令详解](https://www.imooc.com/article/17788?block_id=tuijian_wz)

* Install

```
[root@VM_183_120_centos ~]# yum install screen -y 
[root@VM_183_120_centos ~]# rpm -qa|grep screen
```

* Start to Use

1.创建一个新的会话

下面命令中test为新建会话的名称

```
[root@VM_183_120_centos ~]# screen -S test
```

2.查看已有会话

```
[root@VM_183_120_centos ~]# screen -ls
```

3.重连会话（在这里我们重连test）

```
[root@VM_183_120_centos ~]# screen  -r test //可以是名字test也可以是session ID
```

4.退出会话

```
[root@VM_183_120_centos ~]#screen -d  <session ID 或者 名字>
```

5.清除dead 会话

如果由于某种原因其中一个会话死掉了（例如人为杀掉该会话），这时screen -list会显示该会话为dead状态。使用screen -wipe命令清除该会话

```
[root@VM_183_120_centos ~]#screen -wipe
```

6.关闭或杀死窗口

* 方法 - 1

退出会话后，使用 screen -X -S [session id] quit 命令，可以结束某个session

```
[root@1core2g201802 ~]# screen -ls
There are screens on:
	14954.test	(Detached)
	27902.frps	(Detached)
2 Sockets in /var/run/screen/S-root.

[root@1core2g201802 ~]# screen -X -S 14954 quit
[root@1core2g201802 ~]# screen -ls
There is a screen on:
	27902.frps	(Detached)
1 Socket in /var/run/screen/S-root.
```

* 方法 - 2

如果已经在某个 screen session 中，可以使用 exit 命令退出当前 session
如下：在 test session 中执行 exit 命令

```
[root@1core2g201802 ~]# screen -ls
There are screens on:
        15419.test      (Attached)
        27902.frps      (Detached)
2 Sockets in /var/run/screen/S-root.

[root@1core2g201802 ~]# exit
```

> 注意
>
> Crtl + a +d     保存进程并退出作业(程序在screen中继续运行，screen -ls 可查看)
>
> exit            退出作业和进程(程序终止，screen -ls 不可查看)