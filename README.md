# oracle
# 实验一
查询1：

```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
```
## 查询结果：
> ![](https://github.com/chengrui123456/oracle/blob/master/picture1.png)



- 查询2：
```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
HAVING d.department_name in ('IT'，'Sales');
```
## 查询结果：

> ![](https://github.com/chengrui123456/oracle/blob/master/picture2.png)

# 结论：
我认为查询2的SQL语句更好，因为Having是分组（group by）后的筛选条件，分组后的数据组内再筛选。

# 优化指导：
没有 ALL 关键字，包含 GROUP BY 子句的 SELECT 语句将不显示没有符合条件的行的组。

