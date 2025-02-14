# 626. Exchange Seats

Methods: Database
Difficulty: Medium

Medium

Topics

Companies

SQL Schema

---

Pandas Schema

---

Table: `Seat`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| student     | varchar |
+-------------+---------+
id is the primary key (unique value) column for this table.
Each row of this table indicates the name and the ID of a student.
id is a continuous increment.

```

Write a solution to swap the seat id of every two consecutive students. If the number of students is odd, the id of the last student is not swapped.

Return the result table ordered by `id` **in ascending order**.

The result format is in the following example.

**Example 1:**

```
Input:
Seat table:
+----+---------+
| id | student |
+----+---------+
| 1  | Abbot   |
| 2  | Doris   |
| 3  | Emerson |
| 4  | Green   |
| 5  | Jeames  |
+----+---------+
Output:
+----+---------+
| id | student |
+----+---------+
| 1  | Doris   |
| 2  | Abbot   |
| 3  | Green   |
| 4  | Emerson |
| 5  | Jeames  |
+----+---------+
Explanation:
Note that if the number of students is odd, there is no need to change the last one's seat.
```

```sql
# Write your MySQL query statement below
-- 自定義新id
select row_number() over() as id, student
from Seat
order by (case when mod(id, 2) = 0 then id - 1 else id + 1 end);
-- first, when id=1, id%2!=0, so id will become id+1=2; when id=2, id%2=0, 
-- so id will become id-1=1, when id=3 ->2, when id=4 ->3, when id=5 ->6.
-- then we got id 2, 1, 4, 3, 6, by using "order by" funtion, 
-- the order of id becomes 1, 2, 3, 4 ,6.
-- ROW_NUMBER() will add a serial number (accumulating from 1) to each column of data queried, 
-- sorting them in order without duplication, finally we get 1, 2, 3, 4, 5 as id.
```