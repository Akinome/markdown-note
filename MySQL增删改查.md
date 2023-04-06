# MySQL增删改查

## 1. 创建查看 数据库、表

```mysql
create batabase *;
show databases;
create table * ();
show tables;
desc / describe *;
# 查看数据库的编码
show variables like 'char%';

```

## 2. 修改(table * 是表名,[] 属性可省略)

```mysql
alter table * rename to *; # 修改表名
alter table * modify *(属性) [after] *; # 修改字段属性,位置
alter table * change * *(属性); # 修改字段名称
alter table * add *(属性) [after/first]; # 添加字段
alter table * drop *; # 删除字段

alter table * character set utf8mb4; # 修改字符集
```

## 4. 录入信息

```mysql
insert into * () values();
# 例子,user是表名，
insert into user (uid,uname) 
values(101,"steven");
#查看表信息
select * from user; # 这里的*号是通配符
```

## 5. 约束

```mysql
# 非空约束
create table *
(name varchar(10) not null
);
# 主键约束
create table *
(name varchar(10) primary key
);
# 外键约束
create table *
(name varchar(10) not null
);
# UNIQUE唯一约束
create table *
(name varchar(10) unique
);
# 默认
create table *
(name varchar(10) default '用户'
);
# 多字段组合
create table *
(name varchar(10),
 primary key(sid,sclass)
);


# 例子
create table *
(
    id int primary key,
    name varchar(10) not null,
    sex char(1) default 'boy'
);
```

### 5.1.外键约束

#### 外键创建规则

1. 必须有主表才可以设置从表
2. 主表必须实际存在
3. 必须为主表定义主键
4. 外键列的数据类型必须和主键列的数据类型相同
5. 外键列的数量必须和主键列的数量相同
6. 外键可以不是外表中的主键，但必须和主表关联字段相对应
7. 主从表创建时，存储引擎必须是InnoDB

------

##### 参数说明

CONSTRAINT : 用于设置外键约束名称，可以省略

FOREIGN KEY : 外键设置，用于指定外键字段

REFERENCES : 主表及主键设置，用于指定主表和主键

##### 属性说明

CASCADE : 主表删除或修改记录时，从表也会对关联记录的外键字段进行修改。

RESTRICT : 删除或修改主表记录，子表中若有关联记录，则不允许主表删除或修改。

SET NULL : 主表删除或修改主表记录时，从表会将关联记录的外键字段设为null。

ON UPDATE CASCADE : 主表修改记录时，从表关联记录的外键字段也会修改。(将CASCADE改为RESTRICT，意思相反)

ON DELETE CASCADE : 主表删除记录时，从表关联记录的外键字段也会删除。(将CASCADE改为RESTRICT，意思相反)

#### 外键约束创建

```mysql
# 主表
create table class(
xuehao int primary key,
name varchar(6))engine=innodb;
```

```mysql
# 从表
create table students(
id int auto_increment primary key,
uid int not null,
name varchar(6) not null,
foreign key(uid) references class(xuehao) on update cascade on delete cascade)engine=innodb;
```

```mysql
# 插入数据，进行测试
insert into class values(111,'张三'),(222,'李四'),(333,'王五');
insert into students values(1,111,'张三'),(2,222,'李四'),(3,333,'王五');
```

## 6.删库跑路

```mysql
drop table|database *; # 删表|删库
drop table if exists *; # 删表
drop database if exists * # 删库
truncate table *; # 只清除表数据，保留表结构
# 删除表的数据
delete from * # delete可以删除一行，也可以删除多行；如果不加where条件是很危险的！不建议这样做

```

```mysql
create table user
(
    uid int primary key not null,
    ulogin varchar(20) not null,
    uname varchar(30) not null,
    upwd varchar(50) not null,
    ugender varchar(4) default '男',
    ubithday date,
    ucity varchar(50),
    uemail varchar(50),
    ucredit int default 0 not null
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```
