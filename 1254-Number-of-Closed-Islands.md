# 1254. Number of Closed Islands

Methods: DFS
Difficulty: Medium

**Medium**

3.7K

123

Companies

Given a 2D `grid` consists of `0s` (land) and `1s` (water).  An *island* is a maximal 4-directionally connected group of `0s` and a *closed island* is an island **totally** (all left, top, right, bottom) surrounded by `1s.`

Return the number of *closed islands*.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/10/31/sample_3_1610.png](https://assets.leetcode.com/uploads/2019/10/31/sample_3_1610.png)

```
Input: grid = [[1,1,1,1,1,1,1,0],[1,0,0,0,0,1,1,0],[1,0,1,0,1,1,1,0],[1,0,0,0,0,1,0,1],[1,1,1,1,1,1,1,0]]
Output: 2
Explanation:
Islands in gray are closed because they are completely surrounded by water (group of 1s).
```

**Example 2:**

![https://assets.leetcode.com/uploads/2019/10/31/sample_4_1610.png](https://assets.leetcode.com/uploads/2019/10/31/sample_4_1610.png)

```
Input: grid = [[0,0,1,0,0],[0,1,0,1,0],[0,1,1,1,0]]
Output: 1

```

**Example 3:**

```
Input: grid = [[1,1,1,1,1,1,1],
               [1,0,0,0,0,0,1],
               [1,0,1,1,1,0,1],
               [1,0,1,0,1,0,1],
               [1,0,1,1,1,0,1],
               [1,0,0,0,0,0,1],
               [1,1,1,1,1,1,1]]
Output: 2

```

**Constraints:**

- `1 <= grid.length, grid[0].length <= 100`
- `0 <= grid[i][j] <=1`

```java
class Solution {
    int[] dirs = {0, 1, 0, -1, 0};
    public int closedIsland(int[][] grid) {
        int row = grid.length, col = grid[0].length;
        int res = 0;

        for(int i = 0; i < row; i++){
            for(int j = 0; j < col; j++){
                if(grid[i][j] == 0)
                    if(isIslands(grid, i, j, row, col)) res++;
            }
        }
        return res;
    }
    private boolean isIslands(int[][] grid, int i, int j, int row, int col){//DFS
        if(i < 0 || i >= row || j < 0 || j >= col) return false;//越界
        if(grid[i][j] == 1) return true;
        grid[i][j] = 1;
        boolean res = true;
        
        for(int d = 0; d < dirs.length-1; d++){
            res = res & isIslands(grid, i + dirs[d], j + dirs[d+1], row, col);//判斷四個 方向最後結果都會是1
        }
        return res;
    }
    /**
    "&" will evaluate both side even the left part is false
    "&&" will ignore the right part if the left part is false

    res = res && dfs(grid, x + d[0], y + d[1]);
    if res is false, the right dfs will not be evaluated.
    for this question, we need to enter dfs(grid, x + d[0], y + d[1]) no matter what.

    for example:
    111
    101
    100
    111
    think about if we are in the position of 0 at (2,1) - if dfs goes to right 0 (2, 2) first, res will be false
    in the meantime, we still want to dfs go to (1, 1)'s 0 to set it as 1 even res is false

    OR you could switch to:

    for(int[] d : dir){
        if(!dfs(grid, x + d[0], y + d[1])){
            res = false;
        }
    } */
}
```