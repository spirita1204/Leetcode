# 64. Minimum Path Sum

Methods: DP
Difficulty: Medium

Given a `m x n` `grid` filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

```
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.

```

**Example 2:**

```
Input: grid = [[1,2,3],[4,5,6]]
Output: 12

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 200`
- `0 <= grid[i][j] <= 100`

```java
class Solution {
    public int minPathSum(int[][] grid) {//dp   
        int m = grid.length;
        int n = grid[0].length;
        for(int i = 1; i < n; i++){
            grid[0][i] += grid[0][i - 1];
        }
        for(int i = 1; i < m; i++){
            grid[i][0] += grid[i - 1][0];
        }
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                grid[i][j] += Math.min(grid[i - 1][j],grid[i][j - 1]);
            }
        }
        return grid[m - 1][n - 1];
    }
}
```