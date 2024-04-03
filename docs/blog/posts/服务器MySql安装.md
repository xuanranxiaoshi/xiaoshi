---
draft: false
date: 2024-03-09
authors:
  - jimi
categories:
  - test
---

# 服务器 MySql 安装

>   2024-03-09

服务器上 mysql 的安装配置流程

<!-- more -->

## 启动命令

```she
./bin/mysqld --defaults-file=./my.cnf --user=chensc
```

```shell
./bin/mysql --defaults-file=./my.cnf -uroot -p -S ./mysql.sock
```

root 密码：123456


## 参考

[1][Linux普通用户安装配置mysql（非root权限）](https://blog.csdn.net/suixinfeixiangfei/article/details/121323984)</br>
[2][MySQL8.0安装配置（Linux版）设置简单密码 &远程访问](https://blog.csdn.net/qq_40932102/article/details/122813604)