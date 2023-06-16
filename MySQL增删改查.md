# MySQL 增删改查

## 1. 创建查看 数据库、表

```mysql
create database *;
create database * default character set=utf8;
show databases;
create table * ();
show tables;
desc / describe *;
# 查看数据库的编码
show variables like 'char%';

```

### 1.1.自增数据表

可以使主键自增，避免频繁的输入id主键

```mysql
# 只能在 int 类型中使用
# 例子
create table t3
(
    id int primary key auto_increment,# 自增主键
    name varchar(10)
);
```

### 数据类型

#### 常用的数据类型有

- 整型 int
- 位类型 bit
- 浮点型 float 和 double、real
- 定点数 decimal、numeric
- 日期时间类型 date、time、 datetime、year
- 字符串 char、varchar、text
- 二进制数据 Blob、xxbinary
- 枚举 enum
- 集合 set

| 数据类型     | 字节 | 最小值(有符号/无符号)  | 最大值(有符号/无符号)                    |
| ------------ | ---- | ---------------------- | ---------------------------------------- |
| TINYINT      | 1    | -128/0                 | 127/255                                  |
| SMALLINT     | 2    | -32768/0               | 32767/65535                              |
| MEDIUMINT    | 3    | -8388608/0             | 8388607/1677215                          |
| INT、INTEGER | 4    | -2147483648/0          | 2147483647/4294967295                    |
| BIGINT       | 8    | -9223372036854775808/0 | 9223372036854775807/18446744073709551615 |

## 2. 修改(table * 是表名,[] 属性可省略)

```mysql
alter table * rename to *; # 修改表名
alter table * modify *(属性) [after] *; # 修改字段属性,位置
alter table * change * *(属性); # 修改字段名称
alter table * add *(属性) [after/first]; # 添加字段
alter table * drop *; # 删除字段

alter table * character set utf8mb4; # 修改字符集
```

## 3.查询信息

```mysql
select * from [table] #查询表中的所有信息
select [字段名],[Field name] from [table] # 只查询字段所在列的信息
select distinct [字段名] from [table] # 只查询字段所在列所包含的不同信息(相同数值的只显示一次)

# 支持 where 条件
select * from [table] where [Field name]=10;
```

### 3.1 模糊查询

```mysql
# % 代表一个或多个字符，_ 代表一个字符
# 示例：查询名字里带'k'的用户的所有信息
select * from [table] where [Field name] like '%k%';
# 示例：查询名字里'k'结尾的用户的所有信息
select * from [table] where [Field name] like '%k';
# 示例：查询名字里第二个字符为'k'的用户的所有信息
select * from [table] where [Field name] like '_k%';
```

### 3.2 排序查询

```mysql
# score 分数
# 升序排序
select * from [table] order by [Field name];
select * from [table] order by [Field name] asc;
# 降序排序
select * from [table] order by [Field name] desc;
```

### 3.3 分页查询

```mysql
# 显示开头的三条数据
select * from [table] limit 3;
# 跳过前两条记录，查看第三条到第六条记录
select * from [table] limit 2,4; # 2 跳过前两条记录，4 查询之后的四条记录
select * from [table] limit 4 offset 2; # 另一种方法

# 查询数值最高的三条信息
select * from [table] order by [Field name] desc limit 3;
```

### 3.4 分组查询

| id   | name  | sex  | score | grade | teacher |
| ---- | ----- | ---- | ----- | ----- | ------- |
| 101  | lily  | 女   | 85    | 1     | 李老师  |
| 102  | kate  | 女   | 92    | 1     | 张老师  |
| 103  | mike  | 男   | 87    | 2     | 王老师  |
| 104  | jack  | 男   | 88    | 2     | 李老师  |
| 105  | lucky | 女   | 95    | 3     | 张老师  |
| 106  | happy | 女   | 100   | 3     | 王老师  |
| 107  | sunny | 男   | 90    | 4     | 李老师  |
| 108  | alen  | 女   | 94    | 4     | 张老师  |

```mysql
# 查询每个老师，所带学生的数量
select teacher,count(id) from t2 group by teacher;
# 查询每个老师，所带学生的最高分
select teacher,max(score) from t2 group by teacher;
# 查询每个年级的平均分
select grade,avg(score) from t2 group by grade;
# 查询每个老师所带的学生数量，及姓名
select teacher, count(id),group_concat(name) from t2 group by teacher;
# 查询每个年级的学生数量及姓名
select grade,count(id),group_concat(name) from t2 group by grade;
# 查询男生女生的最高分
select gender,max(score) from t2 group by gender;
# 查询每为老师所带学生中，女同学的最高分
select teacher,max(score) from t2 where sex='女' group by teacher;

select count(tgender teacher) from t2;
```

### 3.5 查询多表数据

b表

| id   | name | age  |
| ---- | ---- | ---- |
| 1    | kate | 18   |
| 2    | jack | 19   |
| 3    | lily | 17   |
| 4    | tom  | 20   |

c表

| c_id | c_name | id   |
| ---- | ------ | ---- |
| 101  | php    | 1    |
| 102  | mysql  | 2    |
| 103  | web    | 3    |
| 104  | php    | 2    |

d表

| d_id | c_id | id   | score |
| ---- | ---- | ---- | ----- |
| 201  | 101  | 1    | 95    |
| 202  | 102  | 2    | 85    |
| 203  | 103  | 3    | 96    |

```mysql
# 交叉连接。笛卡尔机错误示范，会匹配所有数据，数据量大时会卡机
select name,c_id from b,c;

select name,c_id from b cross join c;

# 内连接查询，显示有效匹配数据
# 查询以b表中的id,对应c表中的id匹配的专业数据
select name,c_name from b inner join c where b.id=c.id;
# 查询以c表中的id，对应c表中的id匹配的成绩数据
select c_name,score from c inner join d on c.c_id=d.c_id;

# 左外连接查询，显示有效匹配数据
select * from b left join c on b.id=c.id;

# 子查询,in 是一个运算符
where [Field name] in (select gid from orders);
```

## 4. 录入信息

```mysql
insert into * () values();
# 例子,user是表名，
insert into user (uid,uname) 
values(101,"steven");

# 更新数据
update [table] set name='' [where id=*]

# 查看表信息
select * from user; # 这里的*号是通配符
```

### 4.1. 更新数据

```mysql
update 表名 set name='更新的数据' [where id=*]
# 有条件的更新指定一个字段数据
update user set name='lily' where id=1;
# 没有条件更新所以匹配字段的数据
update user set name='lily'
# 指定更新的区间
update user set name='lily' where id between 1 and 5; # 更新表中第一条到五条的记录
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
# UNSIGNED无符号约束
create table *
(name varchar(10) unsigned
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

#### 1. 外键约束创建

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
# 从表
create table students(
id int auto_increment primary key,
uid int not null,
name varchar(6) not null,
constraint * foreign key(*)# 从表的字段
    references class(xuehao)# 主表和字段
);
```

```mysql
# 插入数据，进行测试
insert into class values(111,'张三'),(222,'李四'),(333,'王五');
insert into students values(1,111,'张三'),(2,222,'李四'),(3,333,'王五');
```

#### 2.添加外键约束

```mysql
# 添加外键约束
alter table odersitem add constraint fk_odersitem_orders_cid foreign key(oid) references orders(oid);

# 为users表中的ulogin添加唯一性（ulogin）约束
alter table users add constraint uq_ulogin unique(ulogin);
alter table users modify ulogin varchar(20) unique;

# 添加default约束，默认值为当前系统时间
alter table users modify uregtime datetime default current_timestamp;
```

## 6.复制数据表

```mysql
# 1.复制表结构
#复制表结构到新表，主键和自增方式是不会复制的
create table 新表 select * from 旧表;
create table 新表 select * from 旧表 where false; #这个where条件将跳过数据的复制;
# 把旧表的所有字段类型都复制到新表
create table 新表 like 旧表;

create table onlinedb.t1 like student.t1;

# 2.复制表结构及数据到新表
create into 新表 select * from 旧表;

# 3.复制旧表的数据到新表(新旧表结构一样)
insert into 新表 select * 旧表;

# 4.赋值旧表数据到新表(新旧表结构不一样)
insert into 新表(字段1,字段2,..) select 字段1,字段2,... from 旧表;

```

## 7.删除表的数据

```mysql
delete from * # delete可以删除一行，也可以删除多行；如果不加where条件是很危险的！不建议这样做

delete from 表名 where id=5; # 通过指定条件删除

# 指定唯一键的范围删除
delete from 表名 where id between 1 and 5; # 删除表中第一条到五条的记录

# 排序后删除指定条件的数据
delete from 表名 order by id desc limit 5; # 倒序排序的前五条记录
delete from 表名 order by id asc limit 5; # 正序排序的前五条记录

```

## 8.删库跑路

通过delete删除，优点：数据可恢复 缺点：速度慢

通过truncate删除，优点：速度极快 缺点：数据不可恢复

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

```mysql
create table goods
(
    id int primary key auto_increment,
    type varchar(30) not null,
    name varchar(30) unique,
    price decimal(7,2) unsigned,
    num int default 0,
    add_time datetime
)DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;

insert into goods1(type,name,price,num,add_time)
values('书籍','西游记',50.40,20,'2018-01-01 13:40:40'),
('糖类','牛奶糖',7.50,200,'2018-02-02 13:40:40'),
('糖类','水果糖',2.50,0,''),
('服饰','休闲西服',800.00,'','2016-04-04 13:40:40'),
('饮品','果汁',3.00,70,'2016-05-05 13:40:40'),
('书籍','论语',109,50,'2016-06-06 13:40:40');

create table zc
(
    id int primary key auto_increment,
    name varchar(30) not null,
    sex enum('w','m'),
    hobby enum('basketball','football','bolleybal'),
    score float(3,1) unique,
    mobile varchar(11),
    entry_time date
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

## 9. where 条件

```mysql
# 直接选择
where [Filed name]=1;
where [Filed name] in ('1','2');
where [Filed name] not in ('1','2');

select tgrade as '年级' from table where tgrade in (2,4,5);


# 区间选择
where [Filed name] between 1 and 10;

# 或运算
where [Filed name]=10 or [Filed name]=11; # or == &
where [Filed name]=10 and [Filed name]=11; # and == &&

# 子查询
where [Field name] in (select gid from orders);
select * from goods where id in (select gid from orders);
where add_time1 > '2020-01-01';
select * from goods where id = any(select gid from orders where add_time1 > '2020-01-01')

```

## 10. 聚合函数

having 和 where 功能类似，但是一般不单独使用，而是和group by 一起使用。而且，having 后面可以直接使用聚合函数作为筛选条件，where 是不可以的。

```mysql
# 求和函数 返回字段的和
select sum([Field name]) from [table];
# 计数函数 返回选择中被选的函数
select count([Field name]) from [table];
# 聚合函数 进行分组查询
select group_concat([Field name]) from [table]

# 最大值和最小值
select max/min([Field name]) from [table];
# having 查询每个类别的最高值大于10的类别
select max([Field name]) from [table] group by [class] having max([Field name])>10;
# 查询每个类别商品类目小于2的商品类别
select max([Field name]) from [table] group by [class] having count([Field name])<2;

# 时间函数 now()，查询年龄
select year(now())-year(birthday) from [table]
```

## 11
