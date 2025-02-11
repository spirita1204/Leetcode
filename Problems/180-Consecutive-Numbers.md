# 180. Consecutive Numbers

Methods: Database
Difficulty: Medium

Medium

Topics

Companies

SQL Schema

---

Pandas Schema

---

Table: `Logs`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| num         | varchar |
+-------------+---------+
In SQL, id is the primary key for this table.
id is an autoincrement column.

```

Find all numbers that appear at least three times consecutively.

Return the result table in **any order**.

The result format is in the following example.

**Example 1:**

```
Input:
Logs table:
+----+-----+
| id | num |
+----+-----+
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |
+----+-----+
Output:
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+
Explanation: 1 is the only number that appears consecutively for at least three times.
```

```sql
# Write your MySQL query statement below

with sub as (
    select id, num,
    lead(num, 1) over (order by id) as num1,
    lead(num, 2) over (order by id) as num2,
    lead(id, 1) over (order by id) as id1,
    lead(id, 2) over (order by id) as id2
    from Logs
)

select distinct num as ConsecutiveNums
from sub
where num = num1 and num1 = num2 
    and id1 = id + 1 and id2 = id + 2;

```