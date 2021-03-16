# 实验2：用户及权限管理

## 实验目的

掌握用户管理，角色管理，权根维护与分配的能力，掌握用户之间共享对象的操作技能。

## 实验内容

Oracle有一个开发者角色资源，可以创建表，过程，诸如此类的对象，但是不能创建视图。

在pdborcl插接式数据中创建一个新的本地角色con_res_view，该角色包含连接和资源角色，同时也包含CREATE VIEW权限，这样任何拥有con_res_view的用户就同时拥有这三种权限。

创建角色之后，再创建用户new_user，给用户分配表空间，设置限制为50M，授予con_res_view角色。

最后测试：用新用户new_user连接数据库，创建表，插入数据，创建视图，查询表和视图的数据。

## 实验步骤

1. 第1步：

- 登录

![login](img\login.png)

- 创建角色con_res_zrf并授权：

![role&grant](img\role&grant.png)

- 创建用户new_zrf，并授权和分配空间

![role&grant](img\role&grant.png)

2.第2步：

- 新用户new_user连接到pdborcl

![login_zrf](img\login_zrf.png)

- 创建表mytable

![mytable](img\mytable.png)

- 创建视图myview

![view](img\view.png)

- 插入数据

![insert](img\insert.png)

- 将myview的SELECT对象权限授予hr用户。

![grant_view](img\grant_view.png)

3.第3步：

- 用户hr连接到pdborcl，查询new_zrf授予它的视图myview

![select_view](img\select_view.png)

- 查询其他用户的视图，进行共享测试

![share_ww](img\share_ww.png)

- 向其他用户写入数据并查询



## 查看数据库的使用情况

- 登录

![login_system](img\login_system.png)

- 查看表空间的数据库文件

![pace_data](img\pace_data.png)

- 查看每个文件的磁盘占用情况

![cipan](img\cipan.png)

## 实验总结

通过本次实验我掌握了用户管理、角色管理、权根维护与分配的能力，并学会了如何运用用户之间共享对象的操作技能。此次实验，为我们之后的实践打下了坚实的基础。









