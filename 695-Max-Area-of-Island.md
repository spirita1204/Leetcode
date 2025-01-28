# 695. Max Area of Island

Methods: DFS
Difficulty: Medium

**Medium**

8.8K

195

Companies

You are given an `m x n` binary matrix `grid`. An island is a group of `1`'s (representing land) connected **4-directionally** (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The **area** of an island is the number of cells with a value `1` in the island.

Return *the maximum **area** of an island in* `grid`. If there is no island, return `0`.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg](https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg)

```
Input: grid = [[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]
Output: 6
Explanation: The answer is not 11, because the island must be connected 4-directionally.

```

**Example 2:**

```
Input: grid = [[0,0,0,0,0,0,0,0]]
Output: 0

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 50`
- `grid[i][j]` is either `0` or `1`.

```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int max_area = 0;
        int row = grid.length;
        int col = grid[0].length;

        for(int i = 0; i < row; i++)
            for(int j = 0; j < col; j++)
                if(grid[i][j] == 1) max_area = Math.max(max_area, AreaOfIsland(grid, i, j, row, col));
        return max_area;
    }
    public int AreaOfIsland(int[][] grid, int i, int j, int row, int col){// DFS
        if(i >= 0 && i < row && j >= 0 && j < col && grid[i][j] == 1){
            grid[i][j] = 0;//避免重複走
            return 1 + AreaOfIsland(grid, i+1, j, row, col) +
                        AreaOfIsland(grid, i-1, j, row, col)+ 
                        AreaOfIsland(grid, i, j+1, row, col)+ 
                        AreaOfIsland(grid, i, j-1, row, col);
        }
        return 0;
    }
}
```