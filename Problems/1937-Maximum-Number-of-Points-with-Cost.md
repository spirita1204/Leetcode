# 1937. Maximum Number of Points with Cost

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given an `m x n` integer matrix `points` (**0-indexed**). Starting with `0` points, you want to **maximize** the number of points you can get from the matrix.

To gain points, you must pick one cell in **each row**. Picking the cell at coordinates `(r, c)` will **add** `points[r][c]` to your score.

However, you will lose points if you pick a cell too far from the cell that you picked in the previous row. For every two adjacent rows `r` and `r + 1` (where `0 <= r < m - 1`), picking cells at coordinates `(r, c1)` and `(r + 1, c2)` will **subtract** `abs(c1 - c2)` from your score.

Return *the **maximum** number of points you can achieve*.

`abs(x)` is defined as:

- `x` for `x >= 0`.
- `x` for `x < 0`.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/07/12/screenshot-2021-07-12-at-13-40-26-diagram-drawio-diagrams-net.png](https://assets.leetcode.com/uploads/2021/07/12/screenshot-2021-07-12-at-13-40-26-diagram-drawio-diagrams-net.png)

```
Input: points = [[1,2,3],[1,5,1],[3,1,1]]
Output: 9
Explanation:
The blue cells denote the optimal cells to pick, which have coordinates (0, 2), (1, 1), and (2, 0).
You add 3 + 5 + 3 = 11 to your score.
However, you must subtract abs(2 - 1) + abs(1 - 0) = 2 from your score.
Your final score is 11 - 2 = 9.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/07/12/screenshot-2021-07-12-at-13-42-14-diagram-drawio-diagrams-net.png](https://assets.leetcode.com/uploads/2021/07/12/screenshot-2021-07-12-at-13-42-14-diagram-drawio-diagrams-net.png)

```
Input: points = [[1,5],[2,3],[4,2]]
Output: 11
Explanation:
The blue cells denote the optimal cells to pick, which have coordinates (0, 1), (1, 1), and (2, 0).
You add 5 + 3 + 4 = 12 to your score.
However, you must subtract abs(1 - 1) + abs(1 - 0) = 1 from your score.
Your final score is 12 - 1 = 11.

```

**Constraints:**

- `m == points.length`
- `n == points[r].length`
- `1 <= m, n <= 105`
- `1 <= m * n <= 105`
- `0 <= points[r][c] <= 105`

```java
class Solution {
    public long maxPoints(int[][] points) {
        int row = points.length;
        int col = points[0].length;
        long[] dp = new long[col];
        // 1 2 3
        // 5 7 7
        // 7 9 9
        // Initialize with the first row
        for (int j = 0; j < col; j++) 
            dp[j] = points[0][j];
        for (int i = 1; i < row; i++) {
            long[] curr = new long[col];
            long[] left = new long[col];
            long[] right = new long[col];
            // Left pass
            left[0] = dp[0];
            for (int j = 1; j < col; j++) 
                left[j] = Math.max(left[j - 1] - 1, dp[j]);
            // Right pass
            right[col - 1] = dp[col - 1];
            for (int j = col - 2; j >= 0; j--) 
                right[j] = Math.max(right[j + 1] - 1, dp[j]);
            // Calculate current dp using left and right
            for (int j = 0; j < col; j++) 
                curr[j] = points[i][j] + Math.max(left[j], right[j]);
    
            dp = curr; // Update previous row for next iteration
        }
        // Get the maximum value from the last row
        long max = 0;
        for (long score : dp)
            max = Math.max(max, score);
        
        return max;
    }
}

```