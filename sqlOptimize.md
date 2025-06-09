## Department Highest Salary

```
    SELECT Department.name AS Department, Employee.name AS Employee, salary AS Salary
    FROM Employee, Department
    WHERE Employee.departmentId = Department.id AND salary IN (
    SELECT MAX(salary)
    FROM Employee
    GROUP BY departmentId
    )
```

���SQL�����������ڣ���Ա����нˮ���Ӳ�ѯ��**���в���**�����нˮ�б���бȽϣ���δ������Ա�������Ĳ����ڡ�

The problem of this query is that employee's salary against a list of maxinism salaries from **all departments**, without restricting the comparison to the employees' own department.

### �޸ĺ����ȷSQL���

```
    SELECT d.name AS Department, e.name AS Employee, salary AS Salary
    FROM Employee e, Department d
    WHERE e.departmentId = d.id AND (salary, departmentId) IN (
    SELECT MAX(salary), departmentId
    FROM Employee
    GROUP BY departmentId
    )
```

���Ӳ�ѯ���ҳ�**������**����߹��ʡ�

Find out the maxinism salaries from **each departments** in the subquery. 

����ִ��ʱ�䳤��**1177ms**��??

But the execution time of this solution is **1177ms**.??

### �Ż�ִ��ʱ��

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

����WITH��乫�����ʽԤ�ȼ���ÿ�����ŵ����нˮ��������ʱ�������

The `WITH` clause creates a temporary result set (`max_salary`) temporary storing for each department's maximum salary.

Ȼ������������ӣ�����������ظ�ɨ�衣

This avoids recalculating the max salary repeatedly and improves readability.

ִ��ʱ������Ϊ**861ms**��??

The execution time has been reduced to **861ms**.??