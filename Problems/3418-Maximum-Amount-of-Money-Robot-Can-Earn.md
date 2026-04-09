# 3418. Maximum Amount of Money Robot Can Earn  

  Methods: DP </br> Difficulty: Medium </br> </br>You are given an `m x n` grid. A robot starts at the top-left corner of the grid `(0, 0)` and wants to reach the bottom-right corner `(m - 1, n - 1)`. The robot can move either right or down at any point in time.   

The grid contains a value `coins[i][j]` in each cell:

- If `coins[i][j] >= 0`, the robot gains that many coins.
- If `coins[i][j] < 0`, the robot encounters a robber, and the robber steals the **absolute** value of `coins[i][j]` coins.
The robot has a special ability to **neutralize robbers** in at most **2 cells** on its path, preventing them from stealing coins in those cells.

**Note:** The robot's total coins can be negative.

Return the **maximum** profit the robot can gain on the route.

**Example 1:**

**Input:** coins = [[0,1,-1],[1,-2,3],[2,-3,4]]

**Output:** 8

**Explanation:**

An optimal path for maximum coins is:

1. Start at `(0, 0)` with `0` coins (total coins = `0`).
1. Move to `(0, 1)`, gaining `1` coin (total coins = `0 + 1 = 1`).
1. Move to `(1, 1)`, where there's a robber stealing `2` coins. The robot uses one neutralization here, avoiding the robbery (total coins = `1`).
1. Move to `(1, 2)`, gaining `3` coins (total coins = `1 + 3 = 4`).
1. Move to `(2, 2)`, gaining `4` coins (total coins = `4 + 4 = 8`).
**Example 2:**

**Input:** coins = [[10,10,10],[10,10,10]]

**Output:** 40

**Explanation:**

An optimal path for maximum coins is:

1. Start at `(0, 0)` with `10` coins (total coins = `10`).
1. Move to `(0, 1)`, gaining `10` coins (total coins = `10 + 10 = 20`).
1. Move to `(0, 2)`, gaining another `10` coins (total coins = `20 + 10 = 30`).
1. Move to `(1, 2)`, gaining the final `10` coins (total coins = `30 + 10 = 40`).
**Constraints:**

- `m == coins.length`
- `n == coins[i].length`
- `1 <= m, n <= 500`
- `1000 <= coins[i][j] <= 1000`
```javascript
class Solution {
    public int maximumAmount(int[][] coins) {
        int n = coins.length;
        int m = coins[0].length;
        // 到達 (i, j) 時的最大收益，且最多可以使用 k 次抵消劫匪的能力。
        int[][][] dp = new int[n][m][3];

        for (int[][] row : dp) {
            for (int[] col : row) {
                Arrays.fill(col, (int)-1e9);
            }
        }

        dp[0][0][1] = 0;
        dp[0][0][2] = 0;  
        dp[0][0][0] = coins[0][0];

        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                for (int k = 0; k < 3; k++) {
                    if (i > 0) // 是否可以從上方移動過來
                        dp[i][j][k] = Math.max(dp[i][j][k], dp[i - 1][j][k] + coins[i][j]);
                    if (i > 0 && k > 0) // 是否可以從上方移動過來，並且是否還剩餘抵消劫匪的能力
                        dp[i][j][k] = Math.max(dp[i][j][k], dp[i - 1][j][k - 1]);
                    if (j > 0) // 是否可以從左方移動過來
                        dp[i][j][k] = Math.max(dp[i][j][k], dp[i][j - 1][k] + coins[i][j]);
                    if (j > 0 && k > 0) // 是否可以從左方移動過來，並且是否還剩餘抵消劫匪的能力
                        dp[i][j][k] = Math.max(dp[i][j][k], dp[i][j - 1][k - 1]);
                }

        return Math.max(dp[n - 1][m - 1][0], Math.max(dp[n - 1][m - 1][1], dp[n - 1][m - 1][2]));
    }
}
```

