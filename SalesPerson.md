# 607. Sales Person

Table: `SalesPerson`

| Column Name     | Type    |
|:----------------|:--------|
| sales_id        | int     |
| name            | varchar |
| salary          | int     |
| commission_rate | int     |
| hire_date       | date    |

`sales_id` is the primary key (column with unique values) for this table.<br>
Each row of this table indicates the name and the ID of a salesperson alongside their salary, commission rate, and hire date.
 
Table: `Company`

| Column Name | Type    |
|:------------|:--------|
| com_id      | int     |
| name        | varchar |
| city        | varchar |

`com_id` is the primary key (column with unique values) for this table.<br>
Each row of this table indicates the name and the ID of a company and the city in which the company is located.
 
Table: `Orders`

| Column Name | Type |
|:------------|:-----|
| order_id    | int  |
| order_date  | date |
| com_id      | int  |
| sales_id    | int  |
| amount      | int  |

`order_id` is the primary key (column with unique values) for this table.<br>
`com_id` is a foreign key (reference column) to `com_id` from the Company table.<br>
`sales_id` is a foreign key (reference column) to `sales_id` from the SalesPerson table.<br>
Each row of this table contains information about one order. This includes the ID of the company, the ID of the salesperson, the date of the order, and the amount paid.

### Solution-1

```
# 思路：JOIN 连接
        NOT EXISTS 排除公司为“RED”的销售人员

SELECT sa.name
FROM SalesPerson sa
WHERE NOT EXISTS(
    SELECT 1
    FROM Orders o JOIN Company c ON o.com_id = c.com_id
    WHERE c.name = "RED" AND o.sales_id = sa.sales_id
)
```

### Solution-2

```
思路：嵌套子查询

SELECT name
FROM SalesPerson
WHERE sales_id NOT IN (
                        SELECT sales_id
                        FROM Orders
                        WHERE com_id =(
                                        SELECT com_id
                                        FROM Company
                                        WHERE name = "RED"
                                    )   
                    )                  
```