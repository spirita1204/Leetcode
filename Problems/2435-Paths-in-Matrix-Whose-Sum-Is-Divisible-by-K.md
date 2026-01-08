# 2435. Paths in Matrix Whose Sum Is Divisible by K  

  Methods: Recursion </br> Difficulty: Hard </br> </br>You are given a **0-indexed** `m x n` integer matrix `grid` and an integer `k`. You are currently at position `(0, 0)` and you want to reach position `(m - 1, n - 1)` moving only **down** or **right**.

Return* the number of paths where the sum of the elements on the path is divisible by *`k`. Since the answer may be very large, return it **modulo** `109 + 7`.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2022/08/13/image-20220813183124-1.png)

```plain text
Input: grid = [[5,2,4],[3,0,5],[0,7,2]], k = 3
Output: 2
Explanation: There are two paths where the sum of the elements on the path is divisible by k.
The first path highlighted in red has a sum of 5 + 2 + 4 + 5 + 2 = 18 which is divisible by 3.
The second path highlighted in blue has a sum of 5 + 3 + 0 + 5 + 2 = 15 which is divisible by 3.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2022/08/17/image-20220817112930-3.png)

```plain text
Input: grid = [[0,0]], k = 5
Output: 1
Explanation: The path highlighted in red has a sum of 0 + 0 = 0 which is divisible by 5.
```

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2022/08/12/image-20220812224605-3.png)

```plain text
Input: grid = [[7,3,4,9],[2,3,6,2],[2,3,7,0]], k = 1
Output: 10
Explanation: Every integer is divisible by 1 so the sum of the elements on every possible path is divisible by k.
```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 5 * 104`
- `1 <= m * n <= 5 * 104`
- `0 <= grid[i][j] <= 100`
- `1 <= k <= 50`
```java
class Solution {
    int[][][] dp;
    int mod = 1_000_000_007;

    // 從 (r, c) 出發，
    // 目前走到這格時，路徑總和 mod k = rem
    // 能走到右下角 (rows-1, cols-1) 的路徑數量
    public int numberOfPaths(int[][] grid, int k) {
        int rows = grid.length;
        int cols = grid[0].length;
        dp = new int[rows][cols][k];
        for (int[][] a : dp) {
            for (int[] b : a) {
                Arrays.fill(b, -1);
            }
        }
        return helper(grid, 0, 0, 0, k);
    }

    int helper(int[][] grid, int r, int c, int sum, int k) {
        // 越界直接 0
        if (r < 0 || r == grid.length || c < 0 || c == grid[0].length)
            return 0;

        sum += grid[r][c];
        if (r == grid.length - 1 && c == grid[0].length - 1) // 終點
            return sum % k == 0 ? 1 : 0;

        if (dp[r][c][sum % k] != -1) // memo
            return dp[r][c][sum % k];

        dp[r][c][sum % k] = (helper(grid, r + 1, c, sum, k) + helper(grid, r, c + 1, sum, k)) % mod;
        
        return dp[r][c][sum % k];
    }
}
```

