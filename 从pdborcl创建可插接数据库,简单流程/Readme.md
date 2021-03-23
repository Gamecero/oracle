## 从pdborcl创建可插接数据库,简单流程

- 以yourdb为源数据库，yourdb已经打开为read only

- 将zhang改为自己的数据库名称

  ## 步骤

  一、登录

  ![login](D:\oracle\oracle\oracle\从pdborcl创建可插接数据库,简单流程\img\login.png)

  二、创建可插接数据库

  ![create](D:\oracle\oracle\oracle\从pdborcl创建可插接数据库,简单流程\img\create.png)

  三、打开数据库并查看

  ![open&show](D:\oracle\oracle\oracle\从pdborcl创建可插接数据库,简单流程\img\open&show.png)

  四、测试

  创建成功后,退出sys用户，以hr登录到新数据库,测试一下

  ![login-2](D:\oracle\oracle\oracle\从pdborcl创建可插接数据库,简单流程\img\login-2.png)

  查看数据库相关文件

  ![show-file](D:\oracle\oracle\oracle\从pdborcl创建可插接数据库,简单流程\img\show-file.png)

  删除pdb

  ![delete](D:\oracle\oracle\oracle\从pdborcl创建可插接数据库,简单流程\img\delete.png)

  ```
  $ sqlplus sys/123@202.115.82.8/orcl as sysdba
  CREATE PLUGGABLE DATABASE ZhouRuiFeng FROM yourdb file_name_convert=('/home/student/pdb/yourdb','/home/student/pdb/ZhouRuiFeng');
  --4.打开新数据库
  ALTER PLUGGABLE DATABASE ZhouRuiFeng OPEN;
  --查看新数据库
  show pdbs;
  --6.测试
  --创建成功后,退出sys用户，以hr登录到新数据库,测试一下
  $ sqlplus hr/123@202.115.82.8/ZhouRuiFeng 
  --查看数据库相关文件
  $ ls /home/student/pdb/ZhouRuiFeng
  --7 删除pdb
  ALTER PLUGGABLE DATABASE ZhouRuiFeng close;
  Drop pluggable database ZhouRuiFeng including datafiles;
  ```

  