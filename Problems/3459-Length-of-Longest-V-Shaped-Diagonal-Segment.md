# 3459. Length of Longest V-Shaped Diagonal Segment  

  Methods: DFS,DP </br> Difficulty: Hard </br> </br>You are given a 2D integer matrix `grid` of size `n x m`, where each element is either `0`, `1`, or `2`. 

A **V-shaped diagonal segment** is defined as:

- The segment starts with `1`.
- The subsequent elements follow this infinite sequence: `2, 0, 2, 0, ...`.
- The segment:
Return the **length** of the **longest** **V-shaped diagonal segment**. If no valid segment *exists*, return 0.

**Example 1:**

**Input:** grid = [[2,2,1,2,2],[2,0,2,2,0],[2,0,1,1,0],[1,0,2,2,2],[2,0,0,2,2]]

**Output:** 5

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2024/12/09/matrix_1-2.jpg)

The longest V-shaped diagonal segment has a length of 5 and follows these coordinates: `(0,2) → (1,3) → (2,4)`, takes a **90-degree clockwise turn** at `(2,4)`, and continues as `(3,3) → (4,2)`.

**Example 2:**

**Input:** grid = [[2,2,2,2,2],[2,0,2,2,0],[2,0,1,1,0],[1,0,2,2,2],[2,0,0,2,2]]

**Output:** 4

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2024/12/09/matrix_2.jpg)

The longest V-shaped diagonal segment has a length of 4 and follows these coordinates: `(2,3) → (3,2)`, takes a **90-degree clockwise turn** at `(3,2)`, and continues as `(2,1) → (1,0)`.

**Example 3:**

**Input:** grid = [[1,2,2,2,2],[2,2,2,2,0],[2,0,0,0,0],[0,0,2,2,2],[2,0,0,2,0]]

**Output:** 5

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2024/12/09/matrix_3.jpg)

The longest V-shaped diagonal segment has a length of 5 and follows these coordinates: `(0,0) → (1,1) → (2,2) → (3,3) → (4,4)`.

**Example 4:**

**Input:** grid = [[1]]

**Output:** 1

**Explanation:**

The longest V-shaped diagonal segment has a length of 1 and follows these coordinates: `(0,0)`.

**Constraints:**

- `n == grid.length`
- `m == grid[i].length`
- `1 <= n, m <= 500`
- `grid[i][j]` is either `0`, `1` or `2`.
```java
class Solution {
    // ↘ → ↙ → ↖ → ↗ → ↘
    private static final int[][] DIRS = { { 1, 1 }, { 1, -1 }, { -1, -1 }, { -1, 1 } };

    public int lenOfVDiagonal(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        // Too many dimensions affect efficiency, so compress k and canTurn into one int
        int[][][] memo = new int[m][n][1 << 3];
        int ans = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] != 1) {
                    continue;
                }
                // 剪枝(沿著第 k 個方向，最多能走到邊界的步數上限)
                int[] maxs = { m - i, j + 1, i + 1, n - j }; 
                for (int k = 0; k < 4; k++) { 
                    if (maxs[k] > ans) { 
                        ans = Math.max(ans, dfs(i, j, k, 1, 2, grid, memo) + 1);
                    }
                }
            }
        }
        return ans;
    }
    // k=當前對角方向（0~3） target=下一個格子應該是 2 或 0
    private int dfs(int i, int j, int k, int canTurn, int target, int[][] grid, int[][][] memo) {
        i += DIRS[k][0];
        j += DIRS[k][1];
        // 邊界
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[i].length || grid[i][j] != target) {
            return 0;
        }
        // k代表 4 個方向 需要 2 個 bit 才裝得下
        // canTurn = 0 或 1 只需要 1 個 bit
        int mask = k << 1 | canTurn;
        if (memo[i][j][mask] > 0) {
            return memo[i][j][mask];
        }
        // 先嘗試「不轉彎，繼續直走」
        int res = dfs(i, j, k, canTurn, 2 - target, grid, memo);
        if (canTurn == 1) {// 如果還能轉彎，嘗試「順時針轉一次」
            int[] maxs = { grid.length - i - 1, j, i, grid[i].length - j - 1 }; // 算轉彎後的理論上限（剪枝用）
            k = (k + 1) % 4;// 順時針
            // 剪枝
            if (maxs[k] > res) {
                res = Math.max(res, dfs(i, j, k, 0, 2 - target, grid, memo));
            }
        }
        
        return memo[i][j][mask] = res + 1;
    }
}
```

