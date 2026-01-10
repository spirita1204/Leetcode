# 1970. Last Day Where You Can Still Cross  

  Methods: Binary Search,BFS </br> Difficulty: Hard </br> </br>There is a **1-based** binary matrix where `0` represents land and `1` represents water. You are given integers `row` and `col` representing the number of rows and columns in the matrix, respectively.

Initially on day `0`, the **entire** matrix is **land**. However, each day a new cell becomes flooded with **water**. You are given a **1-based** 2D array `cells`, where `cells[i] = [ri, ci]` represents that on the `ith` day, the cell on the `rith` row and `cith` column (**1-based** coordinates) will be covered with **water** (i.e., changed to `1`).

You want to find the **last** day that it is possible to walk from the **top** to the **bottom** by only walking on land cells. You can start from **any** cell in the top row and end at **any** cell in the bottom row. You can only travel in the** four** cardinal directions (left, right, up, and down).

Return *the ****last**** day where it is possible to walk from the ****top**** to the ****bottom**** by only walking on land cells*.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/07/27/1.png)

```plain text
Input: row = 2, col = 2, cells = [[1,1],[2,1],[1,2],[2,2]]
Output: 2
Explanation: The above image depicts how the matrix changes each day starting from day 0.
The last day where it is possible to cross from top to bottom is on day 2. 
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/07/27/2.png)

```plain text
Input: row = 2, col = 2, cells = [[1,1],[1,2],[2,1],[2,2]]
Output: 1
Explanation: The above image depicts how the matrix changes each day starting from day 0.
The last day where it is possible to cross from top to bottom is on day 1.
```

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2021/07/27/3.png)

```plain text
Input: row = 3, col = 3, cells = [[1,2],[2,1],[3,3],[2,2],[1,1],[1,3],[2,3],[3,2],[3,1]]
Output: 3
Explanation: The above image depicts how the matrix changes each day starting from day 0.
The last day where it is possible to cross from top to bottom is on day 3.
```

**Constraints:**

- `2 <= row, col <= 2 * 104`
- `4 <= row * col <= 2 * 104`
- `cells.length == row * col`
- `1 <= ri <= row`
- `1 <= ci <= col`
- All the values of `cells` are **unique**.
```java
class Solution {
    int[] DIR = new int[]{0, 1, 0, -1, 0};
    public int latestDayToCross(int row, int col, int[][] cells) {
        // True → False 的單調區間 bs
        int left = 1, right = cells.length, ans = 0;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (canWalk(cells, row, col, mid)) {
                ans = mid; 
                left = mid + 1; 
            } else right = mid - 1; 
        }
        return ans;
    }
    // 建立「第 day 天的地圖」
    private boolean canWalk(int[][] cells, int row, int col, int dayAt) {
        int[][] grid = new int[row][col];
        for (int i = 0; i < dayAt; ++i) 
            grid[cells[i][0]-1][cells[i][1]-1] = 1;
        Queue<int[]> bfs = new LinkedList<>();
        for (int c = 0; c < col; ++c) {
            if (grid[0][c] == 0) { // 最top往下
                bfs.offer(new int[]{0, c});
                grid[0][c] = 1;
            }
        }
        while (!bfs.isEmpty()) {
            int[] curr = bfs.poll();
            int r = curr[0], c  = curr[1];
            if (r == row - 1) return true; // 到終點
            for (int i = 0; i < 4; ++i) {
                int x = r + DIR[i];
                int y = c + DIR[i+1];
                if (x < 0 || x == row || y < 0 || y == col || grid[x][y] == 1) continue;
                grid[x][y] = 1; 
                bfs.offer(new int[]{x, y});
            }
        }
        return false;
    }
}
```

