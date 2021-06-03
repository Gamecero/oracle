# 实验6（期末考核） 基于Oracle的逸趣行-列车售票系统数据库设计

## 期末考核要求

- 自行设计一个信息系统的数据库项目，自拟逸趣行-列车售票系统名称。
- 设计项目涉及的表及表空间使用方案。至少5张表和5万条数据，两个表空间。
- 设计权限及用户分配方案。至少两类角色，两个用户。
- 在数据库中建立一个程序包，在包中用PL/SQL语言设计一些存储过程和函数，实现比较复杂的业务逻辑，用模拟数据进行执行计划分析。
- 设计自动备份方案或则手工备份方案。

## 1.项目简介

项目名称：逸趣行-火车售票系统

本项目是基于Oracle的逸趣行-列车售票系统数据库设计。

涉及角色/用户：管理员、普通用户

涉及表：管理员表、普通用户表、订单表、车次表、座位表、车站表、车票信息表

## 2.功能分析

### 车次管理功能

车次管理功能，是由管理员进行的，主要包含车次查询、车次增加、车次修改、车次删除，主要通过操作数据库来实现这些操作。

### 车站管理功能

车站管理功能，是由管理员进行的，主要包含车站查询、车站增加、车站修改、车站删除，主要通过操作数据库来实现这些操作。

### 用户管理功能

用户管理功能主要指两个方面，一个是指管理员和普通用户都可以对自己的用户信息进行管理，包括查看、修改等操作，另一个是指管理员对普通用户的用户管理，包括查询用户、删除用户。

### 订单管理功能

订单管理能，是由管理员进行的，主要包含查看订单、退订、改签，主要通过操作数据库来实现这些操作。

### 票务查询功能

票务查询功能，是由普通用户进行的，主要包含车次查询、车站查询、余票查询，主要通过从数据库匹配关键信息来实现这些操作。

### 登录注册功能

登录注册功能，为使本系统设计符合使用者需求，管理员和普通用户可以进行登录和注册的功能。

## 3.类图设计

![class_img](D:\oracle\oracle\oracle\test6\img\class_img.png)

## 4.数据库设计

![sql_design](D:\oracle\oracle\oracle\test6\img\sql_design.png)

<div id="USERS"></div>

### 4.1manage表（管理员表）

|       字段       |       类型        | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明             |
| :--------------: | :---------------: | :--------: | :------: | :----: | :--: | :--------------- |
|    manage_id     |   Integer（20）   |    主键    |    否    |        |      | 管理员ID         |
|   manage_name    | VARCHAR(100 BYTE) |            |    否    |        |      | 管理员用户名     |
| manage_password  | VARCHAR(100 BYTE) |            |    否    |        |      | 管理员密码       |
|   manage_phone   |   Integer（20）   |            |    否    |        |      | 管理员电话号码   |
| manage_real_name | VARCHAR(100 BYTE) |            |    否    |        |      | 管理员真实姓名   |
| manage_identity  |   Integer（20）   |            |    否    |        |      | 管理员身份证号码 |
|  manage_comment  | VARCHAR(100 BYTE) |            |    是    |   空   |      | 管理员个性签名   |



<div id="TEACHERS"></div>

### 4.2train_user表（普通用户表）

|      字段      |       类型        | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明               |
| :------------: | :---------------: | :--------: | :------: | :----: | :--: | :----------------- |
|    user_id     |   Integer（20）   |    主键    |    否    |        |      | 普通用户ID         |
|   user_name    | VARCHAR(100 BYTE) |            |    否    |        |      | 普通用户姓名       |
| user_password  | VARCHAR(100 BYTE) |            |    否    |        |      | 普通用户密码       |
| user_real_name | VARCHAR(100 BYTE) |            |    否    |        |      | 普通用户真实姓名   |
| user_phone_num |   Integer（20）   |            |    否    |        |      | 普通用户手机号     |
| user_identity  |   Integer（20）   |            |    否    |        |      | 普通用户身份证号码 |
|   user_level   |   Integer（20）   |            |    是    |   空   |      | 普通用户等级       |
|   user_point   |   Integer（20）   |            |    是    |   空   |      | 普通用户积分       |
|  user_comment  | VARCHAR(100 BYTE) |            |    是    |   空   |      | 普通用户个性签名   |

### 4.3station表（车站表）

|     字段     |       类型        | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明     |
| :----------: | :---------------: | :--------: | :------: | :----: | :--: | :------- |
|  station_id  |   Integer（20）   |    主键    |    否    |        |      | 车站ID   |
| station_name | VARCHAR(100 BYTE) |            |    否    |        |      | 车站姓名 |
| station_addr | VARCHAR(100 BYTE) |            |    否    |        |      | 车站地址 |

<div id="GRADES"></div>

### 4.4train_order表（订单表表）

|       字段       |       类型        | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明           |
| :--------------: | :---------------: | :--------: | :------: | :----: | :--: | :------------- |
|     order_id     |   Integer（20）   |    主键    |    否    |        |      | 订单ID         |
|    order_time    |       Date        |            |    否    |        |      | 订单创建时间   |
|     pay_info     | VARCHAR(100 BYTE) |            |    否    |        |      | 订单支付信息   |
|    order_name    | VARCHAR(100 BYTE) |            |    否    |        |      | 订单所属人姓名 |
| order_train_info | VARCHAR(100 BYTE) |            |    否    |        |      | 订单列车信息   |
|    order_seat    | VARCHAR(100 BYTE) |            |    否    |        |      | 订单座位       |
|  order_identity  |   Integer（20）   |            |    否    |        |      | 订单身份证号码 |
|   order_phone    |   Integer（20）   |            |    否    |        |      | 订单电话号码   |

<div id="TESTS"></div>

### 4.5train_num表（车次表）

|      字段      |       类型        | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明     |
| :------------: | :---------------: | :--------: | :------: | :----: | :--: | :------- |
|    train_id    | VARCHAR(100 BYTE) |    主键    |    否    |        |      | 车次编号 |
|   start_time   |       Date        |            |    否    |        |      | 起始时间 |
|  arrive_time   |       Date        |            |    否    |        |      | 到达时间 |
| start_station  | VARCHAR(100 BYTE) |            |    否    |        |      | 起始车站 |
| arrive_station | VARCHAR(100 BYTE) |            |    否    |        |      | 到达车站 |
|   whole_time   | VARCHAR(100 BYTE) |            |    否    |        |      | 全程耗时 |
|  whole_course  | VARCHAR(100 BYTE) |            |    否    |        |      | 全程距离 |

### 4.6seat表（座位表）

|   字段    |       类型        | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明         |
| :-------: | :---------------: | :--------: | :------: | :----: | :--: | :----------- |
| train_id  | VARCHAR(100 BYTE) |    外键    |    否    |        |      | 车次编号     |
| spare_num |   Integer（20）   |            |    否    |        |      | 余座         |
| total_num |   Integer（20）   |            |    否    |        |      | 总共座位数量 |

### 4.7ticket表（车票信息表）

|     字段     |       类型        | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明         |
| :----------: | :---------------: | :--------: | :------: | :----: | :--: | :----------- |
|  ticket_id   |   Integer（20）   |    主键    |    否    |        |      | 车次编号     |
| train_id<FK> | VARCHAR(100 BYTE) |    外键    |    否    |        |      | 余座         |
| ticket_price |    Float（20）    |            |    否    |        |      | 总共座位数量 |

## 5.设计项目涉及的表及表空间使用方案，并插入总共十万条数据。

创建表空间：

表空间总共三个：train_manage、train_user、train_public

表空间中存放的表:

train_manage: manage

train_user: train_num

train_public: station、train_order、train_num、seat、ticket

每个表插入数据：

manage：20000条

train_num：20000条

station：20000条

train_order：10000条

train_num：10000条

seat：10000条

ticket：10000条

```sql
-- 创建表空间
CREATE TABLESPACE train_manage logging DATAFILE '/home/oracle/app/oracle/oradata/orcl/pdborcl/train_data01.dbf' size 64m autoextend on next 65m maxsize 10240m extent management local;
CREATE TABLESPACE train_user logging  DATAFILE '/home/oracle/app/oracle/oradata/orcl/pdborcl/train_data02.dbf' size 64m autoextend on next 65m maxsize 10240m extent management local;
CREATE TABLESPACE train_public logging  DATAFILE '/home/oracle/app/oracle/oradata/orcl/pdborcl/train_data03.dbf' size 200m autoextend on next 65m maxsize 10240m extent management local;
```

表空间创建成功截图：

![creat_table_space](D:\oracle\oracle\oracle\test6\img\create_table_space.png)

![create_table_space2](D:\oracle\oracle\oracle\test6\img\create_table_space2.png)



创建表：

```sql
-- manage表的创建
create table manage
(
manage_id  number(20) primary key,
manage_name VARCHAR2(100 BYTE） not null,
manage_password VARCHAR2(100 BYTE） not null,
manage_phone number(20) not null,
manage_real_name VARCHAR2(100 BYTE） not null,
manage_identity number(20) not null,
manage_comment VARCHAR2(100 BYTE）
)
tablespace train_manage 
pctfree 10 
initrans 1 
maxtrans 255 
storage 
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);
-- train_user表的创建
create table train_user
(
user_id  number(20) primary key,
user_name VARCHAR2(100 BYTE） not null,
user_password VARCHAR2(100 BYTE） not null,
user_real_name VARCHAR2(100 BYTE） not null,
user_phone_num number(20) not null,                          
user_identity number(20) not null,
user_level number(20),
user_point number(20),                        
user_comment VARCHAR2(100 BYTE）
)
tablespace train_user 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);
                          
-- station表的创建
create table station
(
station_id  number(20) primary key,
station_name VARCHAR2(100 BYTE） not null,
station_addr VARCHAR2(100 BYTE） not null
)
tablespace train_public 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);
                      
-- train_order表的创建
create table train_order
(
order_id  number(20) primary key,
order_time Date not null,
pay_info VARCHAR2(100 BYTE） not null,
order_name VARCHAR2(100 BYTE） not null,
order_train_info VARCHAR2(100 BYTE) not null,                    
order_seat VARCHAR2(100 BYTE) not null,
order_identity number(20) not null,
order_phone number(20) not null                        
)
tablespace train_public 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);
                        
-- train_num表的创建
create table train_num
(
train_id  VARCHAR2(100 BYTE） primary key,
start_time Date not null,
arrive_time Date not null,
start_station VARCHAR2(100 BYTE） not null,
arrive_station VARCHAR2(100 BYTE） not null,
whole_time VARCHAR2(100 BYTE） not null,                       
whole_course VARCHAR2(100 BYTE） not null   
)
tablespace train_public 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);                  

-- seat表的创建
create table seat
(
train_id  VARCHAR2(100 BYTE） not null references train_num(train_id),
spare_num number(20) not null,
total_num number(20) not null     
)
tablespace train_public 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);                      

-- ticket表的创建
create table ticket
(
ticket_id  number(20) primary key,
train_id  VARCHAR2(100 BYTE） not null references train_num(train_id),
ticket_price number(20,2) not null    
)
tablespace train_public 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);                           
 -- 查询表空间的数据库 
select TABLE_NAME from dba_tables where TABLESPACE_NAME='TRAIN_MANAGE';
select TABLE_NAME from dba_tables where TABLESPACE_NAME='TRAIN_USER';
select TABLE_NAME from dba_tables where TABLESPACE_NAME='TRAIN_PUBLIC';
```

创建表截图：

![create_table_manage](D:\oracle\oracle\oracle\test6\img\create_table_manage.png)

![create_table_train_user](D:\oracle\oracle\oracle\test6\img\create_table_train_user.png)

![create_table_station](D:\oracle\oracle\oracle\test6\img\create_table_station.png)

![create_table_train_order](D:\oracle\oracle\oracle\test6\img\create_table_train_order.png)

![create_table_train_num](D:\oracle\oracle\oracle\test6\img\create_table_train_num.png)

![create_table_seat](D:\oracle\oracle\oracle\test6\img\create_table_seat.png)

![create_table_ticket](D:\oracle\oracle\oracle\test6\img\create_table_ticket.png)

验证表是否创建在对应的表空间：

![select_table](D:\oracle\oracle\oracle\test6\img\select_table.png)

插入数据：

```sql
总共插入数据：100000条
manage：20000条
train_num：20000条
station：20000条
train_order：10000条
train_num：10000条
seat：10000条
ticket：10000条
-- manage表的数据插入20000条
declare 
i int;
manage_id number(20);
manage_name VARCHAR2(100);
manage_password VARCHAR2(100);
manage_phone number(20);
manage_real_name VARCHAR2(100);
manage_identity number(20);
manage_comment VARCHAR2(100);
begin
i:=1;
while i<=20000 
loop
manage_id:=i;
manage_name:= 'manage'|| i;
manage_password := '123'|| i;
manage_phone := '180810'|| i;
manage_real_name := '周睿锋'||i;
manage_identity := '51323120'||i;
manage_comment := '个人签名'||i;
insert into manage(MANAGE_ID,MANAGE_NAME,MANAGE_PASSWORD,MANAGE_PHONE,MANAGE_REAL_NAME,MANAGE_IDENTITY,MANAGE_COMMENT) values (manage_id,manage_name,manage_password,manage_phone,manage_real_name,manage_identity,manage_comment);
i:=i+1;
end loop;
commit;
end;
/


-- train_user表数据插入20000
declare 
i int;
user_id number(20);
user_name VARCHAR2(100);
user_password VARCHAR2(100);
user_phone_num number(20);
user_real_name VARCHAR2(100);
user_identity number(20);
user_level number(20);
user_point number(20);
user_comment VARCHAR2(100);
begin
i:=1;
while i<=20000 
loop
user_id:=i;
user_name:= 'user'|| i;
user_password := '123'|| i;
user_phone_num := '180810'|| i;
user_real_name := 'zrf'||i;
user_identity := '51323120'||i;
user_level := '1'||i;
user_point := '1'||i;
user_comment := '个人签名'||i;
insert into train_user(user_id,user_name,user_password,user_real_name,user_phone_num,user_identity,user_level,user_point,user_comment) values (user_id,user_name,user_password,user_real_name,user_phone_num,user_identity,user_level,user_point,user_comment);
i:=i+1;
end loop;
commit;
end;
/


                        
-- station表的数据插入20000条
declare 
i int;
station_id number(20);
station_name VARCHAR2(100);
station_addr VARCHAR2(100);
begin
i:=1;
while i<=20000 
loop
station_id:=i;
station_name:= '地点'|| i;
station_addr := '地址'|| i;
insert into station(station_id,station_name,station_addr) values (station_id,station_name,station_addr);
i:=i+1;
end loop;
commit;
end;
/

                      
-- train_order表的数据插入10000条
declare 
i int;
order_id number(20);
order_time Date ;
pay_info VARCHAR2(100);
order_name VARCHAR2(100);
order_train_info VARCHAR2(100) ;              
order_identity number(20);
order_seat VARCHAR2(100);
order_phone number(20);
begin
i:=1;
while i<=10000 
loop
order_id:=i;
if i mod 6 =0 then
  order_time:=to_date('2015-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =1 then
  order_time:=to_date('2016-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =2 then
  order_time:=to_date('2017-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =3 then
  order_time:=to_date('2018-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =4 then
  order_time:=to_date('2019-3-2','yyyy-mm-dd')+(i mod 60);
else
  order_time:=to_date('2020-3-2','yyyy-mm-dd')+(i mod 60);
end if;
pay_info:= '已支付';
order_name := 'zrf'||i;
order_train_info :=i;
order_identity := '51323120'||i;
order_phone := '180810'||i;
order_seat :='B'||i mod 60;
insert into train_order(order_id,order_time,pay_info,order_name,order_train_info,order_identity,order_seat,order_phone) values (order_id,order_time,pay_info,order_name,order_train_info,order_identity,order_seat,order_phone);
i:=i+1;
end loop;
commit;
end;
/

                        
-- train_num表的数据插入10000条
declare 
i int;
train_id  VARCHAR2(100);
start_time Date;
arrive_time Date;
start_station VARCHAR2(100);
arrive_station VARCHAR2(100);
whole_time VARCHAR2(100);                     
whole_course VARCHAR2(100);
begin
i:=1;
while i<=10000 
loop
train_id:=i;
if i mod 6 =0 then
  start_time:=to_date('2015-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =1 then
  start_time:=to_date('2016-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =2 then
  start_time:=to_date('2017-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =3 then
  start_time:=to_date('2018-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =4 then
  start_time:=to_date('2019-3-2','yyyy-mm-dd')+(i mod 60);
else
  start_time:=to_date('2020-3-2','yyyy-mm-dd')+(i mod 60);
end if;
if i mod 6 =0 then
  arrive_time:=to_date('2015-3-4','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =1 then
  arrive_time:=to_date('2016-3-4','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =2 then
  arrive_time:=to_date('2017-3-4','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =3 then
  arrive_time:=to_date('2018-3-4','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =4 then
  arrive_time:=to_date('2019-3-4','yyyy-mm-dd')+(i mod 60);
else
  arrive_time:=to_date('2020-3-4','yyyy-mm-dd')+(i mod 60);
end if;
start_station:= '起始站'||i;
arrive_station := '终点站'|| i;
whole_time := (TO_NUMBER(arrive_time - start_time));
whole_course := '200'||i mod 6;
insert into train_num(train_id,start_time,arrive_time,start_station,arrive_station,whole_time,whole_course) values (train_id,start_time,arrive_time,start_station,arrive_station,whole_time,whole_course);
i:=i+1;
end loop;
commit;
end;
/
           
-- seat表的数据的插入10000条
declare 
i int;
train_id  VARCHAR2(100);
spare_num number(20);
total_num number(20);
begin
i:=1;
while i<=10000 
loop
train_id:=i;
spare_num:= i mod 60;
total_num := 60;
insert into seat(train_id,spare_num,total_num) values (train_id,spare_num,total_num);
i:=i+1;
end loop;
commit;
end;
/

-- ticket表的数据插入10000条
declare 
i int;
ticket_id  number(20);
train_id  VARCHAR2(100);
ticket_price number(20,2);
begin
i:=1;
while i<=10000 
loop
ticket_id:=i;
train_id:=i;
ticket_price:=dbms_random.value(400,100);
insert into ticket(ticket_id,train_id,ticket_price) values (ticket_id,train_id,ticket_price);
i:=i+1;
end loop;
commit;
end;
/ 

-- 查询是否插入成功
select count(*) from manage;
select count(*) from train_user;
select count(*) from station;
select count(*) from train_order;
select count(*) from train_num;
select count(*) from seat;
select count(*) from ticket;
select count(*) from train_order where pay_info = '已支付';
```



验证数据是否插入成功：

![select_count1](D:\oracle\oracle\oracle\test6\img\select_count1.png)

![select_count2](D:\oracle\oracle\oracle\test6\img\select_count2.png)

## 6.设计权限及用户分配方案,两类角色，两个用户

用户：

c##train_manage 

拥有角色：c##t_manage 

分配表空间：train_manage、train_user、train_public

c##train_user 

拥有角色：c##t_user 

分配表空间：train_user、train_public

角色：

c##t_manage 

拥有角色：connect、resource、dba

c##t_user 

拥有角色：connect、resource

```sql
-- 创建角色
CREATE ROLE c##t_manage;
CREATE ROLE c##t_user;
-- 授权角色
GRANT connect,resource,dba, create table,create view,create trigger, create procedure,create sequence TO c##t_manage;
GRANT connect,resource, create table,create view,create trigger, create procedure,create sequence TO c##t_user;
-- 创建用户
CREATE USER  c##train_manage  IDENTIFIED BY 123 DEFAULT TABLESPACE train_manage;
-- 指定用户额外表空间
ALTER USER c##train_manage QUOTA UNLIMITED ON train_user;
ALTER USER c##train_manage QUOTA UNLIMITED ON train_public;
-- 创建用户
CREATE USER  c##train_user   IDENTIFIED BY 123 DEFAULT TABLESPACE train_user;
-- 指定用户额外表空间
ALTER USER c##train_user QUOTA UNLIMITED ON train_public ;
-- 分配角色给用户
GRANT  c##t_manage TO  c##train_manage;
GRANT  c##t_user TO  c##train_user;
```

成功截图如下：

![create_role](D:\oracle\oracle\oracle\test6\img\create_role.png)

![grant_role](D:\oracle\oracle\oracle\test6\img\grant_role.png)

![create_user](D:\oracle\oracle\oracle\test6\img\create_user.png)

## 7.在数据库中建立一个程序包，在包中用PL/SQL语言设计一些存储过程和函数，实现比较复杂的业务逻辑，用模拟数据进行执行计划分析

建立的包：

包名： TrainPack

函数：

函数名：Get_count(order_id_t NUMBER)

功能：

输入订单ID，查询订单表和车次表，返回与该订单相关的车次对应的起始车站

过程：

过程名：Get_orders(train_id_t VARCHAR2)

功能：

输入订单id，输出与该订单相关的车次的起始车站，以及统计同一时间段的车次数量并输出与订单相关的车票价格

```sql
-- 创建包
create or replace PACKAGE TrainPack IS
  FUNCTION Get_count(order_id_t NUMBER) RETURN VARCHAR2;
  PROCEDURE Get_orders(train_id_t VARCHAR2);
END TrainPack;
-- 创建函数和过程
create or replace PACKAGE BODY TrainPack IS
    FUNCTION Get_count(order_id_t NUMBER) RETURN VARCHAR2
    AS
     M VARCHAR2(100);
     N VARCHAR2(100);
     BEGIN
       select order_train_info into N from train_order where order_id=order_id_t;
       select start_station into M from train_num where train_id=N;
       RETURN M;
     END;
    PROCEDURE Get_orders(train_id_t VARCHAR2)
    AS
        N NUMBER(20);
        L date;
        S VARCHAR2(20);
        R VARCHAR2(100);
    begin
        --使用游标
        DBMS_OUTPUT.PUT_LINE('输出起始站：');
        select start_station into R from train_num where train_id = train_id_t;
        DBMS_OUTPUT.PUT_LINE(R);
         select start_time into L from train_num where train_id = train_id_t;
        select count(*) into N from train_num where start_time = L;
        DBMS_OUTPUT.PUT_LINE('输出车次数量：');
        DBMS_OUTPUT.PUT_LINE(N);
        select ticket_price into S from ticket where train_id = train_id_t;
        DBMS_OUTPUT.PUT_LINE('输出票价：');
        DBMS_OUTPUT.PUT_LINE(S);
    END;
END TrainPack;
/
```

创建成功：

![package_success](D:\oracle\oracle\oracle\test6\img\package_success.png)

测试：

```sql
-- 测试函数
select TrainPack.Get_count(11) AS 订单11起始车站,TrainPack.Get_count(12) AS 订单12起始车站 from dual;
-- 测试过程
DECLARE
  train_id_t VARCHAR2(100);    
BEGIN
  train_id_t := 1;
  TrainPack.Get_orders (train_id_t) ;  
  train_id_t := 2;
  TrainPack.Get_orders (train_id_t) ;    
END;
```

测试结果：

![test_function](D:\oracle\oracle\oracle\test6\img\test_function.png)

![success_PROCEDURE](D:\oracle\oracle\oracle\test6\img\success_PROCEDURE.png)

## 8.设计手动备份方案

本项目设置手动备份方案——即采用Rman备份

### 8.1创建恢复目录

```sql
-- 创建恢复目录：用来存储RMAN资料库的
create tablespace bp datafile '/home/oracle/app/oracle/oradata/bp.dbf' size 20m autoextend on next 5m maxsize unlimited;
-- 在恢复目录数据库中创建RMAN用户并授权
create user c##zrf_r identified by 123 default tablespace bp quota unlimited on bp;
grant connect,resource,recovery_catalog_owner to c##zrf_r;
```

![rman_create_table](D:\oracle\oracle\oracle\test6\img\rman_create_table.png)

![rman_create_user](D:\oracle\oracle\oracle\test6\img\rman_create_user.png)

### 8.2连接RMAN恢复目录数据库

```sql
-- 连接RMAN恢复目录数据库
rman catalog c##zrf_r/123
-- 创建恢复目录
create catalog tablespace bp;
-- 退出
quit
-- 确认环境信息
echo $ORACLE_SID
-- 连接到目标数据库、连接到恢复目录数据库
rman catalog c##zrf_r/123 target /
-- 向恢复目录注册数据库ORCL——此时就可以使用RMAN的恢复目录对目标数据库进行备份和恢复操作
register database;
```

![rman_conn](D:\oracle\oracle\oracle\test6\img\rman_conn.png)

![rman_conn_target](D:\oracle\oracle\oracle\test6\img\rman_conn_target.png)

### 8.3通道分配

```sql
-- 手动通道配置
run
{
allocate channel ch1 device type disk;
allocate channel ch2 device type disk;
allocate channel ch3 device type disk;
}

-- 显示已经配置过的有默认值的参数，其中包括通道参数
show all;
```

![rman_disk](D:\oracle\oracle\oracle\test6\img\rman_disk.png)

![rman_show](D:\oracle\oracle\oracle\test6\img\rman_show.png)

### 8.4归档模式下备份与恢复

```sql
-- 查看数据库是否处于归档模式下
archive log list;
-- 关闭数据库
shutdown immediate
-- 重启并设置成归档模式
startup mount;
alter database archivelog;
archive log list;
alter database open;
-- 连接到目标数据库、连接到恢复目录数据库
rman catalog c##zrf_r/123 target /
-- 备份和恢复整个数据库
backup database;
```

![archiv_no](D:\oracle\oracle\oracle\test6\img\archiv_no.png)

![archiv_yes](D:\oracle\oracle\oracle\test6\img\archiv_yes.png)

![rman_backup_1](D:\oracle\oracle\oracle\test6\img\rman_backup_1.png)

![rman_backup_2](D:\oracle\oracle\oracle\test6\img\rman_backup_2.png)

### 8.5测试备份情况

```sql
-- 切换到保存路径
cd /home/oracle/app/oracle/recovery_area/ORCL/backupset/
-- 查看文件
ls
```

![rman_ls](D:\oracle\oracle\oracle\test6\img\rman_ls.png)

### 8.6测试恢复功能

```sql
-- 关闭数据库
shutdown immediate;
-- 退出数据库
exit
-- 切换到数据文件存储路径
cd /home/oracle/app/oracle/oradata/orcl/pdborcl
-- 查看数据文件
ls
-- 删除train_data01.dbf
rm -rf train_data01.dbf
-- 再次确认
ls
-- 启动数据库
sqlplus /nolog
conn /as sysdba
startup
-- 此时因为缺少数据文件无法启动
-- 检查此时数据库状态
select status from v$instance;
-- 连接RMAN
rman target sys/123
-- 恢复数据库
restore database;
-- 同步恢复
recover database;
-- 打开数据库
alter database open resetlogs;
-- 再次启动数据库，启动成功，检查此时数据库状态，此时状态已经打开
startup
select status from v$instance;
-- 再次切换到数据文件存储路径
cd /home/oracle/app/oracle/oradata/orcl/pdborcl
-- 查看数据文件，删除的已经还原
ls
```

测试截图：

1、删除文件并查看删除成功与否：

![rman_rm_1](D:\oracle\oracle\oracle\test6\img\rman_rm_1.png)

![rman_ls_2](D:\oracle\oracle\oracle\test6\img\rman_ls_2.png)

2、尝试打开数据库，此时由于删除了数据文件已经打不开了：

![rman_rm_file](D:\oracle\oracle\oracle\test6\img\rman_rm_file.png)

3、查看数据库状态：

![rman_sql_select](D:\oracle\oracle\oracle\test6\img\rman_sql_select.png)

4、执行恢复操作：

![rman_restore](D:\oracle\oracle\oracle\test6\img\rman_restore.png)

![rman_recover](D:\oracle\oracle\oracle\test6\img\rman_recover.png)



![rman_open](D:\oracle\oracle\oracle\test6\img\rman_open.png)

5、验证文件是否已经恢复成功

![rman_ls_again](D:\oracle\oracle\oracle\test6\img\rman_ls_again.png)

![rman_open_success](D:\oracle\oracle\oracle\test6\img\rman_open_success.png)

## 9.项目总结

​	本次项目，是对我们本学期所有Oracle学习的总结，在本次期末项目中，我自行设计了一个信息系统的数据库项目，自拟题目为逸趣行-列车售票系统名称。并且设计了项目涉及的表及表空间使用方案，总共设计了三个表空间、七张表，共插入了十万条数据。在设计权限及用户分配方案阶段，我设计了两类角色，两个用户。并且在数据库中建立一个程序包，在包中用PL/SQL语言设计了存储过程和函数，实现比较复杂的业务逻辑，用模拟数据进行执行计划分析，并且设计了手动备份方案，是基于RMAN设计的备份。

​	本次项目每个阶段，老师都在课程讲过相关的知识，因此在本次项目制作过程中，我的进展较为顺利。其中最有挑战性的部分，我认为是备份部分，在该部分，我尝试过自动备份，通过expdp编写脚本，并设置自动运行时间来进行备份，但是备份完毕之后的恢复过程并不理想，因此我又尝试了老师在课堂上最开始讲过的脱机备份，但是总体效率不高，需要人主动将每一个数据文件复制以作恢复。因此最后，我选择了RMAN设计的备份方案，RMAN支持多种备份手段，并且备份、恢复简单。

​	此次项目，我对Oracle数据库操作有了更进一层的理解。



