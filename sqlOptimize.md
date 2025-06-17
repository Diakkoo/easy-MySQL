## Department Highest Salary📊

```
    SELECT Department.name AS Department, Employee.name AS Employee, salary AS Salary
    FROM Employee, Department
    WHERE Employee.departmentId = Department.id AND salary IN (
    SELECT MAX(salary)
    FROM Employee
    GROUP BY departmentId
    )
```

这个SQL语句问题出现在：将员工的薪水与子查询中**所有部门**的最高薪水列表进行比较，而未限制在员工所属的部门内。

The problem of this query is that employee's salary against a list of maxinism salaries from **all departments**, without restricting the comparison to the employees' own department.

### 修改后的正确SQL语句🛠️🛠

```
    SELECT d.name AS Department, e.name AS Employee, salary AS Salary
    FROM Employee e, Department d
    WHERE e.departmentId = d.id AND (salary, departmentId) IN (
    SELECT MAX(salary), departmentId
    FROM Employee
    GROUP BY departmentId
    )
```

在子查询中找出**各部门**的最高工资。

Find out the maxinism salaries from **each departments** in the subquery. 

但是执行时间长达**1177ms**。🤯🤯

But the execution time of this solution is **1177ms**.🤯🤯

### 优化执行时间⌛

```
    WITH max_salary AS (
    SELECT departmentId, max(salary) AS Salary
    FROM Employee
    GROUP BY departmentId
    )
    SELECT d.name AS Department, e.name AS Employee, m.salary AS Salary
    FROM Employee e, Department d, max_salary m
    WHERE e.departmentId = m.departmentId AND e.departmentId = d.id
        AND e.salary >= m.salary
```

运用WITH语句公共表达式预先计算每个部门的最高薪水，创建临时结果集。

The `WITH` clause creates a temporary result set (`max_salary`) temporary storing for each department's maximum salary.

然后进行三表连接，避免对主表重复扫描。

This avoids recalculating the max salary repeatedly and improves readability.

执行时间缩减为**861ms**。🦾🤖

The execution time has been reduced to **861ms**.🦾🤖
