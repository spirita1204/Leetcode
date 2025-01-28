# 1219. Path with Maximum Gold

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Hint

In a gold mine `grid` of size `m x n`, each cell in this mine has an integer representing the amount of gold in that cell, `0` if it is empty.

Return the maximum amount of gold you can collect under the conditions:

- Every time you are located in a cell you will collect all the gold in that cell.
- From your position, you can walk one step to the left, right, up, or down.
- You can't visit the same cell more than once.
- Never visit a cell with `0` gold.
- You can start and stop collecting gold from **any** position in the grid that has some gold.

**Example 1:**

```
Input: grid = [[0,6,0],[5,8,7],[0,9,0]]
Output: 24
Explanation:
[[0,6,0],
 [5,8,7],
 [0,9,0]]
Path to get the maximum gold, 9 -> 8 -> 7.

```

**Example 2:**

```
Input: grid = [[1,0,7],[2,0,6],[3,4,5],[0,3,0],[9,0,20]]
Output: 28
Explanation:
[[1,0,7],
 [2,0,6],
 [3,4,5],
 [0,3,0],
 [9,0,20]]
Path to get the maximum gold, 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7.

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 15`
- `0 <= grid[i][j] <= 100`
- There are at most **25** cells containing gold.

```java
class Solution {
    int[] dirs = { 0, 1, 0, -1, 0 };
    int max = 0;

    public int getMaximumGold(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;

        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if(grid[i][j] != 0)
                    dfs(grid, i, j, row, col, 0);
            }
        }
        return max;
    }

    private void dfs(int[][] grid, int i, int j, int row, int col, int sum) {
        if (i < 0 || i >= row || j < 0 || j >= col || grid[i][j] == 0) {
            max = Math.max(max, sum);
            return;// 碰到邊界
        }
        int origin = grid[i][j];
        grid[i][j] = 0; // mark as visited

        for (int dir = 0; dir < dirs.length - 1; dir++) {// 往四個方向尋找
            int x = i + dirs[dir];
            int y = j + dirs[dir + 1];
            dfs(grid, x, y, row, col, sum + origin);// 相連有多少個
        }
        grid[i][j] = origin; // backtrack
    }
}
```