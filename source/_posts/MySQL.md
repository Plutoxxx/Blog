---
title: MySQL
img: /medias/featureimages/7.jpg
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
<div align="middle"><iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=413834822&auto=1&height=66"></iframe></div>

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

# DDL-操作数据库、表
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
    列名n 数据类型n
)
```
### 查询
```MySQL
# 查询某个数据库中的所有表名称
show tables;
# 查询表结构
desc 表名;
```
### 修改
```MySQL
# 修改表名
alter table 表名 rename to 新的表名;
# 查询表结构
alter table 表名 character set 字符集名称;
# 添加一列
alter table 表名 add 列名 数据类型;
# 修改列名称 类型
alter table 表名 change 列名 新列别 新数据类型;
alter table 表名 modify 列名 新数据类型;
# 删除列
alter table 表名 drop 列名;
```
### 删除
```MySQL
# 删除表
drop table 表名;
# 判断表是否存在，存在再删除
drop table if exists 表名;
```
# DML-增删改表中数据
## 添加
```MySQL
# 添加数据
insert into 表名(列名1,列名2,...列名n) values(值1,值2,...值n);
```
>1. 列名和值要一一对应。
2. 表名后不定义列名，则给所有列添加值`insert into 表名 values(值1,值2,...值n);`。
3.除了数字类型，其他类型需要使用引号（单双都可以）引起来。

## 删除
```MySQL
# 删除数据
delete from 表名 [where 条件];
# 删除所有记录
1. delete from 表名; -- 不推荐使用。有多少条记录就会执行多少次删除操作
2. TRUNCATE TABLE 表名; -- 推荐使用，效率更高 先删除表，然后再创建一张一样的表。
```
## 修改
```MySQL
# 修改数据
update 表名 set 列名1 = 值1, 列名2 = 值2,...[where 条件];
```
# DQL-查询表中记录
## 语法
```MySQL
select
    字段列表
from
    表名列表
where
    条件列表
group by
    分组字段
having
    分组之后的条件
order by
    排序
limit
    分页限定
```
## 基础查询
### 简单查询
```MySQL
# 查询所有列
select * from 表名;
# 查询指定列
select 字段名1，字段名2... from 表名;
```