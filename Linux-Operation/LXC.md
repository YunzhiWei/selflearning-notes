# Concepts

#### Virtual Machine

|Layer|Components|
|---|---|
|VM|Guest OS|
|Virtualization|Hypervisor|
|Hosting|Linux OS|
|HW|Bare Metal|

#### LXC Machine Container

|Layer|Components|
|---|---|
|VM|Guest OS|
|Virtualization|LXC & LXD API|
|Hosting|Linux OS|
|HW|Bare Metal|

#### Application Container

|Layer|Components|
|---|---|
|App Container|App Image & Bin & Lib|
|Virtualization|Container Runtimer (Docker)|
|Hosting|Linux OS|
|HW|Bare Metal|

# Commands

#### version

```
# lxc version
```

#### help

```
# lxc help
# lxc help | less
# lxc help create
```

#### storage

```
# lxc storage list
```

#### remote

```
# lxc remote list
```

#### image

```
# lxc image list
# lxc image list images:
# lxc image list images:centos
```

#### launch

```
# lxc launch tuna:centos/7 kmaster1 --profile k8s-node
```

#### start

#### stop

#### delete

#### list

#### exec

#### config

#### info

#### profile

#### copy

#### move

#### file

#### snapshot

#### restore

# Config

- limits.cpu
- limits.memory

# Nested Container

- security.
- security.nesting
