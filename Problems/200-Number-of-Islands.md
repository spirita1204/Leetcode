# 200. Number of Islands

Methods: DFS
Difficulty: Medium

**Medium**

19.5K

434

Companies

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return *the number of islands*.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1

```

**Example 2:**

```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j]` is `'0'` or `'1'`.

```jsx
class Solution {
    int[] dirs = new int[]{0, 1, 0, -1, 0};
    public int numIslands(char[][] grid) {
        int row = grid.length;
        int col = grid[0].length;
        int res = 0;

        for(int i = 0;i< row; i++){
            for(int j = 0;j < col; j++){
                if(grid[i][j] == '1'){
                    islands(i, j, grid, row, col);
                    res++;
                }
            }
        }
        return res;
    }
    public void islands(int i, int j, char[][] grid, int row, int col){
        if(i < 0 || i>= row || j < 0 || j>= col || grid[i][j] == '0') return;
        if(grid[i][j] == '1') grid[i][j] = '0';

        islands(i + 1, j, grid, row, col);
        islands(i - 1, j, grid, row, col);
        islands(i, j + 1, grid, row, col);
        islands(i, j - 1, grid, row, col);
    }
}
```