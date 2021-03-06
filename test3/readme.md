# 实验3：创建分区表

## 实验目的

掌握分区表的创建方法，掌握各种分区方式的使用场景。

## 实验内容

- 本实验使用3个表空间：USERS,USERS02,USERS03。在表空间中创建两张表：订单表(orders)与订单详表(order_details)。

- 使用new_zrf创建本实验的表，表创建在上述3个分区，自定义分区策略。

- 你需要使用system用户给new_zrf分配上述分区的使用权限。你需要使用system用户给new_zrf可以查询执行计划的权限。

- 表创建成功后，插入数据，数据能并平均分布到各个分区。每个表的数据都应该大于1万行，对表进行联合查询。

- 写出插入数据的语句和查询数据的语句，并分析语句的执行计划。

- 进行分区与不分区的对比实验。

  ## 实验步骤

  ### 一、以system身份登录，并给自己的账户权限:

  创建表空间：

  ![create_spacetable](https://github.com/Gamecero/oracle/raw/main/test3/img/create_spacetable.png)

  使得自己用户在表空间（USERS、USERS02、USERS03）不做限额：

  ![change_user](https://github.com/Gamecero/oracle/raw/main/test3/img/change_user.png)

  ## 二、以自己的账号new_zrf身份登录,并运行脚本文件test3.sql:

  获取脚本：
  
  ![cat](https://github.com/Gamecero/oracle/raw/main/test3/img/cat.png)
  
  脚本具体代码：
  
  ```sql
  /*
  实验三脚本文件:
  首先创建自己的账号new_zrf然后以system身份登录:
  
  [student@deep02 ~]$sqlplus system/123@localhost/pdborcl
  SQL>ALTER USER new_zrf QUOTA UNLIMITED ON USERS;
  SQL>ALTER USER new_zrf QUOTA UNLIMITED ON USERS02;
  SQL>ALTER USER new_zrf QUOTA UNLIMITED ON USERS03;
  SQL>exit
  
  然后以自己的账号new_zrf身份登录,并运行脚本文件test3.sql:
  [student@deep02 ~]$cat test3.sql
  [student@deep02 ~]$sqlplus new_zrf/123@localhost/pdborcl
  SQL>@test3.sql
  SQL>exit
  
  该脚本在你的账号下创建了两个分区表，orders（一万行数据），order_details（三万行数据）。
  
  
  参考：
  1. oracle分区技术-- interval parition实验及总结
     http://blog.chinaunix.net/uid-23284114-id-3304525.html
  */
  
  declare
        num   number;
  begin
        select count(1) into num from user_tables where TABLE_NAME = 'ORDER_DETAILS';
        if   num=1   then
            execute immediate 'drop table ORDER_DETAILS cascade constraints PURGE';
        end   if;
  
        select count(1) into num from user_tables where TABLE_NAME = 'ORDERS';
        if   num=1   then
            execute immediate 'drop table ORDERS cascade constraints PURGE';
        end   if;
  end;
  /
  
  CREATE TABLE ORDERS
  (
    ORDER_ID NUMBER(10, 0) NOT NULL
  , CUSTOMER_NAME VARCHAR2(40 BYTE) NOT NULL
  , CUSTOMER_TEL VARCHAR2(40 BYTE) NOT NULL
  , ORDER_DATE DATE NOT NULL
  , EMPLOYEE_ID NUMBER(6, 0) NOT NULL
  , DISCOUNT NUMBER(8, 2) DEFAULT 0
  , TRADE_RECEIVABLE NUMBER(8, 2) DEFAULT 0
  , CONSTRAINT ORDERS_PK PRIMARY KEY
    (
      ORDER_ID
    )
    USING INDEX
    (
        CREATE UNIQUE INDEX ORDERS_PK ON ORDERS (ORDER_ID ASC)
        LOGGING
        TABLESPACE USERS
        PCTFREE 10
        INITRANS 2
        STORAGE
        (
          BUFFER_POOL DEFAULT
        )
        NOPARALLEL
    )
    ENABLE
  )
  TABLESPACE USERS
  PCTFREE 10
  INITRANS 1
  STORAGE
  (
    BUFFER_POOL DEFAULT
  )
  NOCOMPRESS
  NOPARALLEL
  PARTITION BY RANGE (ORDER_DATE)
  (
    PARTITION PARTITION_2015 VALUES LESS THAN (TO_DATE(' 2016-01-01 00:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN'))
    NOLOGGING
    TABLESPACE USERS
    PCTFREE 10
    INITRANS 1
    STORAGE
    (
      INITIAL 8388608
      NEXT 1048576
      MINEXTENTS 1
      MAXEXTENTS UNLIMITED
      BUFFER_POOL DEFAULT
    )
    NOCOMPRESS NO INMEMORY
  , PARTITION PARTITION_2016 VALUES LESS THAN (TO_DATE(' 2017-01-01 00:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN'))
    NOLOGGING
    TABLESPACE USERS
    PCTFREE 10
    INITRANS 1
    STORAGE
    (
      BUFFER_POOL DEFAULT
    )
    NOCOMPRESS NO INMEMORY
  , PARTITION PARTITION_2017 VALUES LESS THAN (TO_DATE(' 2018-01-01 00:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN'))
    NOLOGGING
    TABLESPACE USERS
    PCTFREE 10
    INITRANS 1
    STORAGE
    (
      BUFFER_POOL DEFAULT
    )
    NOCOMPRESS NO INMEMORY
  , PARTITION PARTITION_2018 VALUES LESS THAN (TO_DATE(' 2019-01-01 00:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN'))
    NOLOGGING
    TABLESPACE USERS02
    PCTFREE 10
    INITRANS 1
    STORAGE
    (
      BUFFER_POOL DEFAULT
    )
    NOCOMPRESS NO INMEMORY
  , PARTITION PARTITION_2019 VALUES LESS THAN (TO_DATE(' 2020-01-01 00:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN'))
    NOLOGGING
    TABLESPACE USERS02
    PCTFREE 10
    INITRANS 1
    STORAGE
    (
      BUFFER_POOL DEFAULT
    )
    NOCOMPRESS NO INMEMORY
  , PARTITION PARTITION_2020 VALUES LESS THAN (TO_DATE(' 2021-01-01 00:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN'))
    NOLOGGING
    TABLESPACE USERS02
    PCTFREE 10
    INITRANS 1
    STORAGE
    (
      BUFFER_POOL DEFAULT
    )
    NOCOMPRESS NO INMEMORY
  , PARTITION PARTITION_2021 VALUES LESS THAN (TO_DATE(' 2022-01-01 00:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN'))
    NOLOGGING
    TABLESPACE USERS03
    PCTFREE 10
    INITRANS 1
    STORAGE
    (
      BUFFER_POOL DEFAULT
    )
    NOCOMPRESS NO INMEMORY
  );
  
  CREATE TABLE order_details
  (
  id NUMBER(10, 0) NOT NULL
  , order_id NUMBER(10, 0) NOT NULL
  , product_name VARCHAR2(40 BYTE) NOT NULL
  , product_num NUMBER(8, 2) NOT NULL
  , product_price NUMBER(8, 2) NOT NULL
  , CONSTRAINT order_details_fk1 FOREIGN KEY  (order_id)
  REFERENCES orders  (  order_id   )
  ENABLE
  )
  TABLESPACE USERS
  PCTFREE 10 INITRANS 1
  STORAGE (BUFFER_POOL DEFAULT )
  NOCOMPRESS NOPARALLEL
  PARTITION BY REFERENCE (order_details_fk1);
  
  declare
    dt date;
    m number(8,2);
    V_EMPLOYEE_ID NUMBER(6);
    v_order_id number(10);
    v_name varchar2(100);
    v_tel varchar2(100);
    v number(10,2);
    v_order_detail_id number;
  begin
  /*
  system login:
  ALTER USER "TEACHER" QUOTA UNLIMITED ON USERS;
  ALTER USER "TEACHER" QUOTA UNLIMITED ON USERS02;
  ALTER USER "TEACHER" QUOTA UNLIMITED ON USERS03;
  */
    v_order_detail_id:=1;
    delete from order_details;
    delete from orders;
    for i in 1..10000
    loop
      if i mod 6 =0 then
        dt:=to_date('2015-3-2','yyyy-mm-dd')+(i mod 60); --PARTITION_2015
      elsif i mod 6 =1 then
        dt:=to_date('2016-3-2','yyyy-mm-dd')+(i mod 60); --PARTITION_2016
      elsif i mod 6 =2 then
        dt:=to_date('2017-3-2','yyyy-mm-dd')+(i mod 60); --PARTITION_2017
      elsif i mod 6 =3 then
        dt:=to_date('2018-3-2','yyyy-mm-dd')+(i mod 60); --PARTITION_2018
      elsif i mod 6 =4 then
        dt:=to_date('2019-3-2','yyyy-mm-dd')+(i mod 60); --PARTITION_2019
      else
        dt:=to_date('2020-3-2','yyyy-mm-dd')+(i mod 60); --PARTITION_2020
      end if;
      V_EMPLOYEE_ID:=CASE I MOD 6 WHEN 0 THEN 11 WHEN 1 THEN 111 WHEN 2 THEN 112
                                  WHEN 3 THEN 12 WHEN 4 THEN 121 ELSE 122 END;
      --插入订单
      v_order_id:=i;
      v_name := 'aa'|| 'aa';
      v_name := 'zhang' || i;
      v_tel := '139888883' || i;
      insert /*+append*/ into ORDERS (ORDER_ID,CUSTOMER_NAME,CUSTOMER_TEL,ORDER_DATE,EMPLOYEE_ID,DISCOUNT)
        values (v_order_id,v_name,v_tel,dt,V_EMPLOYEE_ID,dbms_random.value(100,0));
      --插入订单y一个订单包括3个产品
      v:=dbms_random.value(10000,4000);
      v_name:='computer'|| (i mod 3 + 1);
      insert /*+append*/ into ORDER_DETAILS(ID,ORDER_ID,PRODUCT_NAME,PRODUCT_NUM,PRODUCT_PRICE)
        values (v_order_detail_id,v_order_id,v_name,2,v);
      v:=dbms_random.value(1000,50);
      v_name:='paper'|| (i mod 3 + 1);
      v_order_detail_id:=v_order_detail_id+1;
      insert /*+append*/ into ORDER_DETAILS(ID,ORDER_ID,PRODUCT_NAME,PRODUCT_NUM,PRODUCT_PRICE)
        values (v_order_detail_id,v_order_id,v_name,3,v);
      v:=dbms_random.value(9000,2000);
      v_name:='phone'|| (i mod 3 + 1);
  
      v_order_detail_id:=v_order_detail_id+1;
      insert /*+append*/ into ORDER_DETAILS(ID,ORDER_ID,PRODUCT_NAME,PRODUCT_NUM,PRODUCT_PRICE)
        values (v_order_detail_id,v_order_id,v_name,1,v);
      --在触发器关闭的情况下，需要手工计算每个订单的应收金额：
      select sum(PRODUCT_NUM*PRODUCT_PRICE) into m from ORDER_DETAILS where ORDER_ID=v_order_id;
      if m is null then
       m:=0;
      end if;
      UPDATE ORDERS SET TRADE_RECEIVABLE = m - discount WHERE ORDER_ID=v_order_id;
      IF I MOD 1000 =0 THEN
        commit; --每次提交会加快插入数据的速度
      END IF;
    end loop;
  end;
  /
  select count(*) from orders;
  select count(*) from order_details;
  
  --以system用户运行：
  set autotrace on
  
  select * from new_zrf.orders where order_date
  between to_date('2017-1-1','yyyy-mm-dd') and to_date('2018-6-1','yyyy-mm-dd');
  
  select a.ORDER_ID,a.CUSTOMER_NAME,
  b.product_name,b.product_num,b.product_price
  from new_zrf.orders a,new_zrf.order_details b where
  a.ORDER_ID=b.order_id and
  a.order_date between to_date('2017-1-1','yyyy-mm-dd') and to_date('2018-6-1','yyyy-mm-dd');
  ```
  
  账号登录：
  
  ![login](https://github.com/Gamecero/oracle/raw/main/test3/img/login.png)
  
  运行该脚本后，进行分区，创建了两个分区表：
  
  ![run_test3](https://github.com/Gamecero/oracle/raw/main/test3/img/run_test3.png)
  
  在分区表orders中插入一万行数据，order_details中插入三万行数据：
  
  ![count](https://github.com/Gamecero/oracle/raw/main/test3/img/count.png)
  
  ![count2](https://github.com/Gamecero/oracle/raw/main/test3/img/count2.png)
  
  ## 三、插入数据的语句和查询数据的语句，并分析语句的执行计划。
  
  查询语句：
  
  sql_1
  
  ![select1](https://github.com/Gamecero/oracle/raw/main/test3/img/select1.png)
  
  sql_2
  
  ![select2](https://github.com/Gamecero/oracle/raw/main/test3/img/select2.png)根据sql_1，sql_2比较，在orders数据量为10000,order_details数据量为30000时，有分区比无分区查找数据优势更大。

优化指导：

![instruction1](https://github.com/Gamecero/oracle/raw/main/test3/img/instruction1.png)

![instruction2](https://github.com/Gamecero/oracle/raw/main/test3/img/instruction2.png)

## 实验总结

通过本次实验，我掌握了掌握分区表的创建方法，掌握各种分区方式的使用场景。在本次实验中总共使用3个表空间：USERS,USERS02,USERS03。其中USERS02,USERS03需要我们进行创建，并在表空间中创建两张表：订单表(orders)与订单详表(order_details)。我们需要在给给予自己账号分配上述分区的使用权限。使得自己的账号可以查询执行计划的权限。并且将表创建在上述3个分区，自定义分区策略，再进行插入数据以及查询语句的使用、分析、优化指导。此次实验过程较为复杂，让我们在实验的过程中收获颇多。
