# 1391. Check if There is a Valid Path in a Grid  

  Methods: DFS </br> Difficulty: Medium </br> </br>You are given an `m x n` `grid`. Each cell of `grid` represents a street. The street of `grid[i][j]` can be:

- `1` which means a street connecting the left cell and the right cell.
- `2` which means a street connecting the upper cell and the lower cell.
- `3` which means a street connecting the left cell and the lower cell.
- `4` which means a street connecting the right cell and the lower cell.
- `5` which means a street connecting the left cell and the upper cell.
- `6` which means a street connecting the right cell and the upper cell.
![Image](https://assets.leetcode.com/uploads/2020/03/05/main.png)

You will initially start at the street of the upper-left cell `(0, 0)`. A valid path in the grid is a path that starts from the upper left cell `(0, 0)` and ends at the bottom-right cell `(m - 1, n - 1)`. **The path should only follow the streets**.

**Notice** that you are **not allowed** to change any street.

Return `true`* if there is a valid path in the grid or *`false`* otherwise*.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2020/03/05/e1.png)

```plain text
Input: grid = [[2,4,3],[6,5,2]]
Output: true
Explanation: As shown you can start at cell (0, 0) and visit all the cells of the grid to reach (m - 1, n - 1).
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2020/03/05/e2.png)

```plain text
Input: grid = [[1,2,1],[1,2,1]]
Output: false
Explanation: As shown you the street at cell (0, 0) is not connected with any street of any other cell and you will get stuck at cell (0, 0)
```

**Example 3:**

```plain text
Input: grid = [[1,1,2]]
Output: false
Explanation: You will get stuck at cell (0, 1) and you cannot reach cell (0, 2).
```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `1 <= grid[i][j] <= 6`
```java
class Solution {
    // TRANS[街道類型][進來方向] = 出去方向
    private static final int[][] TRANS = {
        {-1, 1, -1, 3},
        {0, -1, 2, -1},
        {3, 2, -1, -1},
        {1, -1, -1, 2},
        {-1, 0, 3, -1},
        {-1, -1, 1, 0}
    };
    // 上 右 下 左
    private static final int[][] DIRS = {{-1, 0}, {0, 1}, {1, 0}, {0, -1}};
    // 可以出發的方向 0上 1右 2下 3左 
    private static final int[][] START = {{1, 3}, {0, 2}, {2, 3},
                                          {1, 2}, {0, 3}, {0, 1}};

    public boolean hasValidPath(int[][] grid) {
        int m = grid.length, n = grid[0].length;

        if (m == 1 && n == 1) return true;

        int[] s = START[grid[0][0] - 1];

        return check(grid, s[0]) || check(grid, s[1]);
    }

    private boolean check(int[][] grid, int di) {
        int m = grid.length, n = grid[0].length;

        int r = DIRS[di][0];
        int c = DIRS[di][1];
   
        while (r >= 0 && r < m && c >= 0 && c < n) {
            di = TRANS[grid[r][c] - 1][di];// 出去方向
            // 路斷了 or 走回起點
            if (di == -1 || (r == 0 && c == 0)) return false;
            if (r == m - 1 && c == n - 1) return true;

            r += DIRS[di][0];
            c += DIRS[di][1];
        }
        return false;
    }
}
```

