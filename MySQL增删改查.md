## MySQL增删改查

### 1. 创建查看 数据库、表

```mysql
create batabase *;
show databases;
create table * ();
show tables;
desc / describe *;

```

### 2. 修改(table * 是表名,[] 属性可省略)

```mysql
alter table * rename to *; # 修改表名
alter table * modify *(属性) [after] *; # 修改字段属性,位置
alter table * change * *(属性); # 修改字段名称
alter table * add *(属性) [after/first]; # 添加字段
alter table * drop *; # 删除字段

alter table * character set utf8mb4; # 修改字符集
```

### 4. 录入信息

```mysql
insert into * () values();
# 例子,user是表名，
insert into user (uid,uname) 
values(101,"steven");
#查看表信息
select * from user; # 这里的*号是通配符
```

### 5. 约束	

```mysql
# 非空约束
create table *
(name varchar(10) not null
);
# 主键约束
create table *
(name varchar(10) primary key
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

### 6.删库跑路

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
