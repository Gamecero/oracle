# 实验3：创建分区表

## 实验目的

掌握分区表的创建方法，掌握各种分区方式的使用场景。

## 实验内容

- 本实验使用3个表空间：USERS,USERS02,USERS03。在表空间中创建两张表：订单表(orders)与订单详表(order_details)。

- 使用**你自己的账号创建本实验的表**，表创建在上述3个分区，自定义分区策略。

- 你需要使用system用户给new_zrf分配上述分区的使用权限。你需要使用system用户给new_zrf可以查询执行计划的权限。

- 表创建成功后，插入数据，数据能并平均分布到各个分区。每个表的数据都应该大于1万行，对表进行联合查询。

- 写出插入数据的语句和查询数据的语句，并分析语句的执行计划。

- 进行分区与不分区的对比实验。

  ## 实验步骤

  ### 一、以system身份登录，并给自己的账户权限:

  创建表空间：

  ![create_spacetable](https://github.com/Gamecero/oracle/tree/main/test3/img/create_spacetable.png)

  使得自己用户在表空间（USERS、USERS02、USERS03）不做现额：

  ![change_user](https://github.com/Gamecero/oracle/tree/main/test3/img/change_user.png)

  ## 二、以自己的账号new_zrf身份登录,并运行脚本文件test3.sql:

  获取脚本：
  
  ![cat](https://github.com/Gamecero/oracle/tree/main/test3/img/cat.png)
  
  账号登录：
  
  ![login](https://github.com/Gamecero/oracle/tree/main/test3/img/login.png)
  
  运行该脚本后，进行分区，创建了两个分区表：
  
  ![run_test3](https://github.com/Gamecero/oracle/tree/main/test3/img/run_test3.png)
  
  在分区表orders中插入一万行数据，order_details中插入三万行数据：
  
  ![count](https://github.com/Gamecero/oracle/tree/main/test3/img/count.png)
  
  ![count2](https://github.com/Gamecero/oracle/tree/main/test3/img/count2.png)
  
  ## 三、插入数据的语句和查询数据的语句，并分析语句的执行计划。
  
  查询语句：
  
  ![select1](https://github.com/Gamecero/oracle/tree/main/test3/img/select1.png)
  
  ![select2](https://github.com/Gamecero/oracle/tree/main/test3/img/select2.png)

优化指导：

![instruction1](https://github.com/Gamecero/oracle/tree/main/test3/img/instruction1.png)

![instruction2](https://github.com/Gamecero/oracle/tree/main/test3/img/instruction2.png)

## 实验总结

通过本次实验，我掌握了掌握分区表的创建方法，掌握各种分区方式的使用场景。在本次实验中总共使用3个表空间：USERS,USERS02,USERS03。其中USERS02,USERS03需要我们进行创建，并在表空间中创建两张表：订单表(orders)与订单详表(order_details)。我们需要在给给予自己账号分配上述分区的使用权限。使得自己的账号可以查询执行计划的权限。并且将表创建在上述3个分区，自定义分区策略，再进行插入数据以及查询语句的使用、分析、优化指导。此次实验过程较为复杂，让我们在实验的过程中收获颇多。
