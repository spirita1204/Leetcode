# 3495. Minimum Operations to Make Array Elements Zero  

  Methods: Math </br> Difficulty: Hard </br> </br>You are given a 2D array `queries`, where `queries[i]` is of the form `[l, r]`. Each `queries[i]` defines an array of integers `nums` consisting of elements ranging from `l` to `r`, both **inclusive**.

In one operation, you can:

- Select two integers `a` and `b` from the array.
- Replace them with `floor(a / 4)` and `floor(b / 4)`.
Your task is to determine the **minimum** number of operations required to reduce all elements of the array to zero for each query. Return the sum of the results for all queries.

**Example 1:**

**Input:** queries = [[1,2],[2,4]]

**Output:** 3

**Explanation:**

For `queries[0]`:

- The initial array is `nums = [1, 2]`.
- In the first operation, select `nums[0]` and `nums[1]`. The array becomes `[0, 0]`.
- The minimum number of operations required is 1.
For `queries[1]`:

- The initial array is `nums = [2, 3, 4]`.
- In the first operation, select `nums[0]` and `nums[2]`. The array becomes `[0, 3, 1]`.
- In the second operation, select `nums[1]` and `nums[2]`. The array becomes `[0, 0, 0]`.
- The minimum number of operations required is 2.
The output is `1 + 2 = 3`.

**Example 2:**

**Input:** queries = [[2,6]]

**Output:** 4   

**Explanation: **

For `queries[0]`:     

- The initial array is `nums = [2, 3, 4, 5, 6]`.
- In the first operation, select `nums[0]` and `nums[3]`. The array becomes `[0, 3, 4, 1, 6]`.
- In the second operation, select `nums[2]` and `nums[4]`. The array becomes `[0, 3, 1, 1, 1]`.
- In the third operation, select `nums[1]` and `nums[2]`. The array becomes `[0, 0, 0, 1, 1]`.
- In the fourth operation, select `nums[3]` and `nums[4]`. The array becomes `[0, 0, 0, 0, 0]`.
- The minimum number of operations required is 4.
The output is 4.

**Constraints:**

- `1 <= queries.length <= 105`
- `queries[i].length == 2`
- `queries[i] == [l, r]`
- `1 <= l < r <= 109`
```java
class Solution {
    public long minOperations(int[][] queries) {
        // 答案 = 所有數字的「需求總次數」÷ 2（向上取整）。
        long ans = 0;
        for (int i = 0; i < queries.length; i++) {
            long start = queries[i][0], end = queries[i][1];
            long ops = 0;
            for (long d = 1, prev = 1; d < 17; d++) {// 最大 r = 1e9 -> 16 次內一定歸零
                // 枚舉： d=要幾次
                // d = 1 → [1, 3]
                // d = 2 → [4, 15]
                // d = 3 → [16, 63]
                long cur = prev * 4;
                // query 區間裡，有多少數字落在「需要 d 次」的區段
                long l = Math.max(start, prev);
                long r = Math.min(end, cur - 1);
                if (r >= l) {
                    ops += (r - l + 1) * d;
                }
                prev = cur;
            }
            // 一次操作 = 同時讓兩個數 /4 一次
            ans += (ops + 1) / 2;
        }
        return ans;
    }
}
```

