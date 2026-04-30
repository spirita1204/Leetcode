# 1559. Detect Cycles in 2D Grid  

  Methods: BFS </br> Difficulty: Medium </br> </br>Given a 2D array of characters `grid` of size `m x n`, you need to find if there exists any cycle consisting of the **same value** in `grid`.

A cycle is a path of **length 4 or more** in the grid that starts and ends at the same cell. From a given cell, you can move to one of the cells adjacent to it - in one of the four directions (up, down, left, or right), if it has the **same value** of the current cell.

Also, you cannot move to the cell that you visited in your last move. For example, the cycle `(1, 1) -> (1, 2) -> (1, 1)` is invalid because from `(1, 2)` we visited `(1, 1)` which was the last visited cell.

Return `true` if any cycle of the same value exists in `grid`, otherwise, return `false`.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2020/07/15/1.png)

```plain text
Input: grid = [["a","a","a","a"],["a","b","b","a"],["a","b","b","a"],["a","a","a","a"]]
Output: true
Explanation:There are two valid cycles shown in different colors in the image below:
```

![Image](https://assets.leetcode.com/uploads/2020/07/15/11.png)

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2020/07/15/22.png)

```plain text
Input: grid = [["c","c","c","a"],["c","d","c","c"],["c","c","e","c"],["f","c","c","c"]]
Output: true
Explanation:There is only one valid cycle highlighted in the image below:
```

![Image](https://assets.leetcode.com/uploads/2020/07/15/2.png)

**Example 3:  **

![Image](https://assets.leetcode.com/uploads/2020/07/15/3.png)

```plain text
Input: grid = [["a","b","b"],["b","z","b"],["b","b","a"]]
Output: false
```

**Constraints:   **

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 500`
- `grid` consists only of lowercase English letters.   
```java
class Solution {    
    public boolean containsCycle(char[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        boolean[][] visited = new boolean[m][n];

        int[] dirs = {0, 1, 0, -1, 0};

        for (int r = 0; r < m; r++) {
            for (int c = 0; c < n; c++) {
                if (visited[r][c]) continue;
   
                Queue<int[]> q = new LinkedList<>();
                q.offer(new int[]{r, c, -1, -1});
                visited[r][c] = true;

                while (!q.isEmpty()) {
                    int[] cur = q.poll();
                    int cr = cur[0], cc = cur[1], pr = cur[2], pc = cur[3];

                    for (int k = 0; k < 4; k++) {
                        int nr = cr + dirs[k];
                        int nc = cc + dirs[k + 1];
                        //  出界
                        if (nr < 0 || nr >= m || nc < 0 || nc >= n) continue;
                        // 搜同字元區域
                        if (grid[nr][nc] != grid[cr][cc]) continue;
                        // 避免走回頭路
                        if (nr == pr && nc == pc) continue;

                        if (visited[nr][nc]) return true;

                        visited[nr][nc] = true;
                        q.offer(new int[]{nr, nc, cr, cc});
                    }
                }
            }
        }

        return false;
    }
}
```

