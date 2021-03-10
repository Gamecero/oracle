# 实验1：SQL语句的执行计划分析与优化指导

## 实验目的

  分析SQL执行计划，执行SQL语句的优化指导。理解分析SQL语句的执行计划的重要作用。

## 实验内容

- 对Oracle12c中的HR人力资源管理系统中的表进行查询与分析。
- 首先运行和分析教材中的样例：本训练任务目的是查询两个部门('IT'和'Sales')的部门总人数和平均工资，以下两个查询的结果是一样的。但效率不相同。
- 设计自己的查询语句，并作相应的分析，查询语句不能太简单。

## 教材中的查询语句

查询1：

```SQL
set autotrace on

SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
from hr.departments d,hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT','Sales')
GROUP BY d.department_name;
```

- 查询2

```SQL
set autotrace on

SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
FROM hr.departments d,hr.employees e
WHERE d.department_id = e.department_id
GROUP BY d.department_name
HAVING d.department_name in ('IT','Sales');
```

执行上面两个比较复杂的返回相同查询结果数据集的SQL语句，通过分析SQL语句各自的执行计划，判断哪个SQL语句是最优的。最后将你认为最优的SQL语句通过sqldeveloper的优化指导工具进行优化指导，看看该工具有没有给出优化建议



## 教材查询语句运行结果

### 查询一

![image-20210309191104552](D:\oracle\oracle\oracle\test1\img\image-20210309191104552.png)

### 查询一的自动跟踪的执行计划：

![image-20210309210804757](D:\oracle\oracle\oracle\test1\img\image-20210309210804757.png)

### 查询二：

![image-20210309191032280](D:\oracle\oracle\oracle\test1\img\image-20210309191032280.png)

### 查询二的自动跟踪的执行计划

![image-20210309210609262](D:\oracle\oracle\oracle\test1\img\image-20210309210609262.png)

## 查询语句分析结果

根据查询结果所耗时间以及自动跟踪的执行计划进行分析，查询一的语句比查询二更优。

### 优化指导

我对查询一进行优化指导，具体结果如下：

![image-20210310152212006](D:\oracle\oracle\oracle\test1\img\image-20210310152212006.png)

根据优化指导的建议，我开始创建索引：

![image-20210310190714327](D:\oracle\oracle\oracle\test1\img\image-20210310190714327.png)

## 个人设计的查询语句

我根据查询了工作为AD_PRES、AD_VP、IT_PROG的工作人员的总人数，以及他们的平均工资，并且得出结果如下：

```sql
--查询工作为AD_PRES和工作为AD_VP的人员总人数以及他们的平均工资
SELECT (j.job_id)as "工作名称",count(e.job_id)as "工作总人数",
avg(e.salary)as "平均工资"
from hr.jobs j,hr.employees e
where j.job_id = e.job_id
and j.job_id in ('AD_PRES','AD_VP','IT_PROG')
GROUP BY j.job_id;
```

![image-20210310215949226](D:\oracle\oracle\oracle\test1\img\image-20210310215949226.png)