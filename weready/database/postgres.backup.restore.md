---
title: 'postgres 数据库的备份与恢复'
author: 'Chris'
contact: '18621569380'
date: '2020-9-19'
keywords: 'postgres, backup, restore, hands on, lab, guide'
brief: 'postgres数据库的备份与恢复'
---

# 参考

- [1](https://www.jianshu.com/p/0602d5c77b8f?tdsourcetag=s_pcqq_aiomsg)

# 备份

#### 命令格式

```
pg_dump -h [host] -U [user] [database] > [output file]
```

```
#!/bin/bash

pg_dump -h dbpg -U postgres archellis > /backup/pgdump.sql
mv -f /backup/pgdump.sql /backup/pg_dump_`date +%Y%m%d%H%M%S`.sql
```

# 恢复

## Option 1

### Steps

1. 进入容器 `dbpg`

1. 进入脚本目录

```
cd script
```

1. 进入数据库

```
psql -d archellis -U postgres
```

1. 清空数据

```
\i clear_all.sql;
```

1. 恢复数据

```
\i pg_dump_xxxxxxx.sql;
```

## Option 2

### Steps

1. 登录数据库

```
psql -U postgres 
```

1. 断开所有连接

```
SELECT pg_terminate_backend(pg_stat_activity.pid) FROM pg_stat_activity WHERE datname = 'archellis' AND pid <> pg_backend_pid();
```

1. 退出登录

```
\q
```

1. 删除数据库

```
dropdb -U postgres archellis
```

1. 创建数据库

```
createdb -U postgres archellis
```

1. 恢复数据

```
psql -d archellis -U postgres -f pg_dump_xxxxxxxx.sql
```
