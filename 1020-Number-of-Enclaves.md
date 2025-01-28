# 1020. Number of Enclaves

Methods: DFS
Difficulty: Medium

**Medium**

2.9K

59

Companies

You are given an `m x n` binary matrix `grid`, where `0` represents a sea cell and `1` represents a land cell.

A **move** consists of walking from one land cell to another adjacent (**4-directionally**) land cell or walking off the boundary of the `grid`.

Return *the number of land cells in* `grid` *for which we cannot walk off the boundary of the grid in any number of **moves***.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/02/18/enclaves1.jpg](https://assets.leetcode.com/uploads/2021/02/18/enclaves1.jpg)

```
Input: grid = [[0,0,0,0],[1,0,1,0],[0,1,1,0],[0,0,0,0]]
Output: 3
Explanation: There are three 1s that are enclosed by 0s, and one 1 that is not enclosed because its on the boundary.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/02/18/enclaves2.jpg](https://assets.leetcode.com/uploads/2021/02/18/enclaves2.jpg)

```
Input: grid = [[0,1,1,0],[0,0,1,0],[0,0,1,0],[0,0,0,0]]
Output: 0
Explanation: All 1s are either on the boundary or can reach the boundary.

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 500`
- `grid[i][j]` is either `0` or `1`.

```java
class Solution {
    int[] dirs = {0, 1, 0, -1, 0};
    public int numEnclaves(int[][] grid) {
        int res = 0;
        int row = grid.length;
        int col = grid[0].length;

        for(int i = 0; i < row; i++)
            for(int j = 0; j < col; j++){
                if(grid[i][j] == 1) {
                    int get = dfs(grid, i, j, row, col);
                    if(get != -1) res += get;//當輸出為-1代表有越界 不處理
                } 
            }
        return res;
    }
    public int dfs(int[][] grid, int i, int j, int row, int col){
        if(i< 0 || i>= row || j< 0 || j>= col) return -1;//碰到邊界
        int total = 0;
        boolean isboundary = false;
        
        if(grid[i][j] == 0) return 0;//當前不為陸地
        else total++;//當為陸地
        grid[i][j] = 0;

        for(int dir = 0; dir< dirs.length - 1; dir++){//往四個方向尋找
            int x = i + dirs[dir];
            int y = j + dirs[dir+1];
            int amount = dfs(grid, x, y, row, col);//相連有多少個
            
            if(amount == -1) isboundary = true; //碰到邊界
            if(!isboundary) total += amount;
        }
        return (!isboundary) ? total : -1;
    }
}
```