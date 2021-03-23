## 从pdborcl创建可插接数据库,简单流程

- 以yourdb为源数据库，yourdb已经打开为read only

- 将zhang改为自己的数据库名称

  ## 步骤

  一、登录

  ![login](https://github.com/Gamecero/oracle/blob/main/%E4%BB%8Epdborcl%E5%88%9B%E5%BB%BA%E5%8F%AF%E6%8F%92%E6%8E%A5%E6%95%B0%E6%8D%AE%E5%BA%93%2C%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/img/login.png)

  二、创建可插接数据库

  ![create](https://github.com/Gamecero/oracle/blob/main/%E4%BB%8Epdborcl%E5%88%9B%E5%BB%BA%E5%8F%AF%E6%8F%92%E6%8E%A5%E6%95%B0%E6%8D%AE%E5%BA%93%2C%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/img/create.png)

  三、打开数据库并查看

  ![open&show](https://github.com/Gamecero/oracle/blob/main/%E4%BB%8Epdborcl%E5%88%9B%E5%BB%BA%E5%8F%AF%E6%8F%92%E6%8E%A5%E6%95%B0%E6%8D%AE%E5%BA%93%2C%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/img/open&show.png)

  四、测试

  创建成功后,退出sys用户，以hr登录到新数据库,测试一下

  ![login-2](https://github.com/Gamecero/oracle/blob/main/%E4%BB%8Epdborcl%E5%88%9B%E5%BB%BA%E5%8F%AF%E6%8F%92%E6%8E%A5%E6%95%B0%E6%8D%AE%E5%BA%93%2C%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/img/login-2.png)

  查看数据库相关文件

  ![show-file](https://github.com/Gamecero/oracle/blob/main/%E4%BB%8Epdborcl%E5%88%9B%E5%BB%BA%E5%8F%AF%E6%8F%92%E6%8E%A5%E6%95%B0%E6%8D%AE%E5%BA%93%2C%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/img/show-file.png)

  删除pdb

  ![delete](https://github.com/Gamecero/oracle/blob/main/%E4%BB%8Epdborcl%E5%88%9B%E5%BB%BA%E5%8F%AF%E6%8F%92%E6%8E%A5%E6%95%B0%E6%8D%AE%E5%BA%93%2C%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/img/delete.png)

  整体代码展示：
  
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
  
  