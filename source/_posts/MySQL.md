---
title: MySQL
top: false
cover: false
toc: true
mathjax: true
date: 2020-01-12 15:13:50
password:
summary: 将前段时间学习的MySQL语句进行总结一下，嘻嘻🧐。
tags:
    - MySQL
    - 语言
categories:
    - MySQL
---
<div align="middle"><iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=404375&auto=1&height=66"></iframe></div>

>将前段时间学习的MySQL语句进行总结一下，嘻嘻🧐。

# MySQL分类
---

1. `DDL(Data Definition Language)`数据定义语言
    用来定义数据对象：数据库、表、列等，其中关键字有：create、drop、alter等。
2. `DML(Data Manipulation Language)`数据操纵语言
    用来对数据库中表的数据进行增、删、改，其中关键字有：insert、delete、update等。
3. `DQL(Data Query Language)`数据查询语言
    用来查询数据库中表的数据，其中关键字：select、where等。
4. `DCL(Data Control Language)`数据控制语言
    用来定义数据库的访问权限以及创建用户，关键字：grant、revoke等。

# DDL
---
## 操作数据库
### 创建
```MySQL
# 创建数据库：
create database 数据库名称;
# 创建数据库，判断不存在，再创建：
create database if not exists 数据库名称;
# 创建数据库，并指定字符集：
create database 数据库名称 character set 字符集名;
```

### 查询
```MySQL
# 查询所有数据库的名称
show databases;
# 查询某个数据库的创建语句
show create database 数据库名称;
```

### 修改
```MySQL
# 查询所有数据库的名称
alter database 数据库名称 character set 字符集;
# 例如：
alter database db1 character set utf8;
```

### 删除
```MySQL
# 删除数据库
drop database 数据库名称;
# 判断数据库是否存在，存在再删除
drop database if exists 数据库名称;
```

### 使用数据库
```MySQL
# 使用数据库
use 数据库名称;
# 查询当前正在使用的数据库
select database();
```
## 操作表
### 创建
```MySQL
# 创建表
create table 表名(
    列名1 数据类型1,
    列名2 数据类型2,
    ...
    列名n 数据类型n,
)

```

# DML