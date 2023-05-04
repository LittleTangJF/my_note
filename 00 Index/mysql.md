## 前言


- 关系型数据库
- 二维数据表
- 关联表，一对一、一对多、多对多
- sql语句

## 连接数据库


方式1 宝塔面板终端

```js
mysql -u username -p  // 连接某个数据库
```

方式2 navicat

```js
主机：119.91.156.37
端口： 3306
用户名： root
密码： 从宝塔面板复制
```

## SQL语句分类

>条件： where、order by、limit、offset

- DDL：数据定义语言； 创建 、 删除、 修改
- DML：数据操作语言； 添加、删除、 修改
- DQL：数据库查询语言
- DCL：数据控制语言；数据库、表格的权限

## DDL常用命令

>注意事项
>关键字大写 CREATE TABLE SHOW等，然后表名用 ``包裹
>分号；结尾

- 重启： **sudo systemctl restart mysqld**
- 数据库增删改查：
	- create database name;
	- show databases;
	- drop database： 删除
	- alter database： 修改
- 使用： use name;
- 表增删改查
	- create table  name();
	- show tables;
	- insert： 插入
	- select： 选择数据
	- desc： 描述
	- alter：修改
		- rename
		- add
		- change： value
		- modify：类型

## DML语句


- 插入数据： insert into...values
- 删除数据： delete from 
	- where
- 修改数据：update name set

## DQL语句


- select： 选择数据

## 查询条件

1.和where搭配使用

- &&、and
- or
- between and
- brand in 包含
- like 模糊查询
	- v%
	- %v%
	- \_v%: 下划线代表一个字符

2.和order by配合使用

- desc： 降序
- asc：升序

3.和limit配合使用

- offset：偏移

## 数据类型


- 数字类型：
	- 整数：tinyint： 1、amallint: 2、mediumint: 3、int 4、bigint 8
	- 浮点数：float 4、double 8
	- 精度：decimal 、 numeric
- 日期和时间
	- year
	- date
	- datetime： 日期时间
	- timestamp： 时间戳： 范围UTC
- 字符串（字符和字节）
	- char: 1-255
	- varchar: 0-65535
	- binary、varbinary: 二进制形式
	- blob： 视频、图片
	- text：比65535大的字符串
- 空间类型
- json

## 表约束


- 主键primarykey

  - 唯一性、是表中索引
  - 默认值：defualt
  - 默认增长
  - 外键
  - 联合主键：多个key

## 聚合表函数


- avg(): 平均
- max(): 最高
- min
- sum
- count(\*)


## 分组


配合聚合函数使用，group by

和group by配合使用的是having

## 多表关系


如果一张表保存的信息过于冗余，存在相同的信息，可建多表

1.创建外键
- foreign key(id) references table(id)

2.外键更新和删除

在有外键约束的情况下修改外键 on update \  on  delete
- 默认restrict严格模式
- cascade： 跟随
- setnull：更新 删了就set  null


## 多表查询


表与表之间的连接

 - 左连接：left [outer]  join table on 条件
	 - 可以查询到有交集和没有交集的数据
 - 右连接： right join 
	 - 以右为主，没有就是null
 - 内连接： cross/inner join on
	 - 左右都要有数据
 - 全连接： mysql没有，需要用union
	 - (左连接) union (右连接)


## 多对多表关系


1.建立一张关系表

- 用外键关联创建关系表
- 插入数据，给关联的外键

2.查询多对多表

- 内连接： 有数据的情况
- 左连接： 可查右边没数据的情况
- 右连接：可查左边没数据的情况