## Nth Highest Salary
找出第n高的薪水

|Column Name|Type|
|:----------|:---|
|id         |int |
|salart     |int |

``` MySQL
    CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
    BEGIN
        SET N = N - 1;
        RETURN (
            # Write your MySQL query statement below.
            SELECT DISTINCT salary
            FROM Employee
            ORDER BY salary DESC
            LIMIT N, 1
        );
    END

    /* LIMIT 语句跳过前面N条数据，选取第1条数据 */
```

执行用时：**804ms**

这段SQL的核心思想就是通过存储函数传入的N值，
用ORDER BY语句对薪资排序后，
用LIMIT语句跳过前面的N条，
选取第一条数据。

---

用IFNULL()函数，针对Salary为空值的情况

``` MySQL
    CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
    BEGIN
    SET N := N-1;
    RETURN (
        SELECT IFNULL(
        (SELECT DISTINCT salary
        FROM Employee
        ORDER BY salary DESC
        LIMIT 1 OFFSET N), 
        NULL
        )
    );
    END;
```

执行用时：582ms