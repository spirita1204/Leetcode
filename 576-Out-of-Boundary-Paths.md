# 576. Out of Boundary Paths

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Hint

There is an `m x n` grid with a ball. The ball is initially at the position `[startRow, startColumn]`. You are allowed to move the ball to one of the four adjacent cells in the grid (possibly out of the grid crossing the grid boundary). You can apply **at most** `maxMove` moves to the ball.

Given the five integers `m`, `n`, `maxMove`, `startRow`, `startColumn`, return the number of paths to move the ball out of the grid boundary. Since the answer can be very large, return it **modulo** `109 + 7`.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/04/28/out_of_boundary_paths_1.png](https://assets.leetcode.com/uploads/2021/04/28/out_of_boundary_paths_1.png)

```
Input: m = 2, n = 2, maxMove = 2, startRow = 0, startColumn = 0
Output: 6

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/04/28/out_of_boundary_paths_2.png](https://assets.leetcode.com/uploads/2021/04/28/out_of_boundary_paths_2.png)

```
Input: m = 1, n = 3, maxMove = 3, startRow = 0, startColumn = 1
Output: 12

```

**Constraints:**

- `1 <= m, n <= 50`
- `0 <= maxMove <= 50`
- `0 <= startRow < m`
- `0 <= startColumn < n`

```java
class Solution {
    public int findPaths(int m, int n, int maxMove, int startRow, int startColumn) {// 範例2= [3,2,3] [5,8,5] [11,12,11]
        int[][][] dp = new int[maxMove + 1][m][n]; // 定義使用k步數可使位置(i, j) 超過邊界 int[k][i][j]
        int mod = 1_000_000_007;

        for(int k = 1; k <= maxMove; k++) {
            for(int x = 0; x < m; x++) {// x軸
                for(int y = 0; y < n; y++) {// y軸
                    long v1 = (x == 0) ? 1 : dp[k - 1][x - 1][y];
                    long v2 = (x == m - 1) ? 1 : dp[k - 1][x + 1][y];
                    long v3 = (y == 0) ? 1 : dp[k - 1][x][y - 1];
                    long v4 = (y == n - 1) ? 1 : dp[k - 1][x][y + 1];

                    dp[k][x][y] = (int)((v1 + v2 + v3 + v4) % (mod));
                }
            }
        }
        return dp[maxMove][startRow][startColumn];
    }
}
```