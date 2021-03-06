# In_Memory

## 步骤：

### 一、登录

![image-20210309210804757](https://github.com/Gamecero/oracle/blob/main/In_Memory/img/login.png)

### 二、创建表sales，插入100万条记录

![image-20210309210804757](https://github.com/Gamecero/oracle/blob/main/In_Memory/img/table.png)

### 三、插入100万行数据

![image-20210309210804757](https://github.com/Gamecero/oracle/blob/main/In_Memory/img/insert.png)

### 四、进行IN-Memory前后的查询对比

#### in-memory前：

#### 两次执行:

![image-20210309210804757](https://github.com/Gamecero/oracle/blob/main/In_Memory/img/in-memory-before.png)

#### in-memory：

![image-20210309210804757](https://github.com/Gamecero/oracle/blob/main/In_Memory/img/inmemory.png)

#### in-memory后：

#### 两次执行:

![image-20210309210804757](https://github.com/Gamecero/oracle/blob/main/In_Memory/img/inmemory-after.png)

## 具体代码如下：

```sql
--创建表sales，插入100万条记录
CREATE TABLE sales
   (ID NUMBER primary key, 
	NAME VARCHAR2(50 BYTE) not null, 
	QUANTITY NUMBER(8,0), 
	PRICE NUMBER(8,0)
);

--插入100万行数据
declare 
v1 number;
v2 number;
begin
    delete from sales;
    for i in 1..1000000
    loop
        v1:=dbms_random.value(1,90);
        v2:=dbms_random.value(100,900);
        insert into sales(id,name,quantity,price) values (i,'name'||i,v1,v2);
    end loop;
    commit;
end;

插入过程中，如果遇到超出表空间 'USERS' 的空间限额，可以执行：
alter user ZhouRuiFeng quota unlimited on users;

--进行IN-Memory前后的查询对比

--in-memory前：
--两次执行:
set autotrace on TRACEONLY 
select sum(quantity*price) total from sales;

--in-memory：
set autotrace on
alter table sales inmemory;

--in-memory后：
--两次执行:
select sum(quantity*price) total from sales;

观察consistent gets的数量，越少越快。

--查询总金额
```

