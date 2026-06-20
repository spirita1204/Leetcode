# 3742. Maximum Path Score in a Grid  

  Methods: DP </br> Difficulty: Medium </br> </br>You are given an `m x n` grid where each cell contains one of the values 0, 1, or 2. You are also given an integer `k`.

You start from the top-left corner `(0, 0)` and want to reach the bottom-right corner `(m - 1, n - 1)` by moving only **right** or **down**.

Each cell contributes a specific score and incurs an associated cost, according to their cell values:

- 0: adds 0 to your score and costs 0.
- 1: adds 1 to your score and costs 1.
- 2: adds 2 to your score and costs 1.
Return the **maximum** score achievable without exceeding a total cost of `k`, or -1 if no valid path exists.

**Note:** If you reach the last cell but the total cost exceeds `k`, the path is invalid.

**Example 1:**

**Input:** grid = [[0, 1],[2, 0]], k = 1

**Output:** 2

**Explanation:**

The optimal path is:

Thus, the maximum possible score is 2.

**Example 2:**

**Input:** grid = [[0, 1],[1, 2]], k = 1

**Output:** -1

**Explanation:   **

There is no path that reaches cell `(1, 1)` without exceeding cost k. Thus, the answer is -1.

**Constraints:**

- `1 <= m, n <= 200`
- `0 <= k <= 103`
- `grid[0][0] == 0`
- `0 <= grid[i][j] <= 2`
```java
class Solution {
    public int maxPathScore(int[][] grid, int k) {
        int m = grid.length, n = grid[0].length;

        int[] scoreAdd = { 0, 1, 2 };
        int[] costAdd = { 0, 1, 1 };

        // dp[i][j][c] = max score at (i, j) with cost c
        int[][][] dp = new int[m][n][k + 1];
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++)
                for (int c = 0; c <= k; c++)
                    dp[i][j][c] = -1;

        dp[0][0][0] = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                for (int costUsed = 0; costUsed <= k; costUsed++) {
                    if (dp[i][j][costUsed] == -1)
                        continue;
                    int curScore = dp[i][j][costUsed];   

                    // Move DOWN
                    if (i + 1 < m) {
                        int nc = costUsed + costAdd[grid[i + 1][j]];
                        if (nc <= k) {
                            int ns = curScore + scoreAdd[grid[i + 1][j]];
                            dp[i + 1][j][nc] = Math.max(dp[i + 1][j][nc], ns);
                        }
                    }

                    // Move RIGHT
                    if (j + 1 < n) {
                        int nc = costUsed + costAdd[grid[i][j + 1]];
                        if (nc <= k) {
                            int ns = curScore + scoreAdd[grid[i][j + 1]];
                            dp[i][j + 1][nc] = Math.max(dp[i][j + 1][nc], ns);
                        }
                    }
                }
            }
        }

        int best = -1;
        for (int c = 0; c <= k; c++) {
            best = Math.max(best, dp[m - 1][n - 1][c]);
        }
        return best;
    }
}
```



