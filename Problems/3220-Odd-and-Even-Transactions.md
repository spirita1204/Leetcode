# 3220. Odd and Even Transactions  

  Methods: Database </br> Difficulty: Medium </br> </br>Table: `transactions`

```plain text
+------------------+------+
| Column Name      | Type |
+------------------+------+
| transaction_id   | int  |
| amount           | int  |
| transaction_date | date |
+------------------+------+
The transactions_id column uniquely identifies each row in this table.
Each row of this table contains the transaction id, amount and transaction date.

```

Write a solution to find the **sum of amounts** for **odd** and **even** transactions for each day. If there are no odd or even transactions for a specific date, display as `0`.

Return *the result table ordered by* `transaction_date` *in ****ascending**** order*.

The result format is in the following example.

**Example:**

**Input:**

`transactions` table:

```plain text
+----------------+--------+------------------+
| transaction_id | amount | transaction_date |
+----------------+--------+------------------+
| 1              | 150    | 2024-07-01       |
| 2              | 200    | 2024-07-01       |
| 3              | 75     | 2024-07-01       |
| 4              | 300    | 2024-07-02       |
| 5              | 50     | 2024-07-02       |
| 6              | 120    | 2024-07-03       |
+----------------+--------+------------------+

```

**Output:**

```plain text
+------------------+---------+----------+
| transaction_date | odd_sum | even_sum |
+------------------+---------+----------+
| 2024-07-01       | 75      | 350      |
| 2024-07-02       | 0       | 350      |
| 2024-07-03       | 0       | 120      |
+------------------+---------+----------+

```

**Explanation:**

- For transaction dates:
**Note:** The output table is ordered by `transaction_date` in ascending order.

```sql
# Write your MySQL query statement below
select transaction_date,  
    sum(
        case when amount % 2 = 1 
        then amount
        else 0
        end 
    ) as odd_sum,
    sum(
        case when amount % 2 = 0 
        then amount
        else 0
        end 
    ) as even_sum
from transactions
group by transaction_date
order by transaction_date asc
```

