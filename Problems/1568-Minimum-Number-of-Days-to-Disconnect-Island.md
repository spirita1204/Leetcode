# 1568. Minimum Number of Days to Disconnect Island

Methods: BFS
Data structure: Queue
Difficulty: Hard

Hard

Topics

Companies

Hint

You are given an `m x n` binary grid `grid` where `1` represents land and `0` represents water. An **island** is a maximal **4-directionally** (horizontal or vertical) connected group of `1`'s.

The grid is said to be **connected** if we have **exactly one island**, otherwise is said **disconnected**.

In one day, we are allowed to change **any** single land cell `(1)` into a water cell `(0)`.

Return *the minimum number of days to disconnect the grid*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/12/24/land1.jpg](https://assets.leetcode.com/uploads/2021/12/24/land1.jpg)

```
Input: grid = [[0,1,1,0],[0,1,1,0],[0,0,0,0]]

Output: 2
Explanation: We need at least 2 days to get a disconnected grid.
Change land grid[1][1] and grid[0][2] to water and get 2 disconnected island.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/12/24/land2.jpg](https://assets.leetcode.com/uploads/2021/12/24/land2.jpg)

```
Input: grid = [[1,1]]
Output: 2
Explanation: Grid of full water is also disconnected ([[1,1]] -> [[0,0]]), 0 islands.

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 30`
- `grid[i][j]` is either `0` or `1`.

```java
class Solution {
    int[] dirs = new int[]{0, -1, 0, 1, 0};
    int row = 0;
    int col = 0;
    public int minDays(int[][] grid) {
        // 最多4個connect, 答案<= 4 -> 用關鍵點去想 < 3, 只會有三種解 0, 1, 2
        row = grid.length; 
        col = grid[0].length;
        int min = 2;
        if(island(grid) > 1) 
            return 0; 
        for(int i = 0; i < row; i++) {
            for(int j = 0; j < col; j++) {
                if(grid[i][j] != 0) {
                    grid[i][j] = 0; // 變成海洋
                    int cnt = island(grid);
                    if(cnt > 1) 
                        return 1; // 分割一次就能變兩塊的話
                    grid[i][j] = 1; // 恢復原樣
                }
            }
        }
        return 2;
    }
    // 如果有多個島 輸出0
    private int island(int[][] grid) {
        int cnt = 0;
        boolean[][] visited = new boolean[row][col];
        for(int i = 0; i < row; i++) {
            for(int j = 0; j < col; j++) {
                if(visited[i][j]) continue;
                if(grid[i][j] == 0) continue;
                // BFS
                Queue<int[]> pq = new LinkedList<>();
                pq.offer(new int[]{i, j});
                cnt++;
                while(!pq.isEmpty()) {
                    int[] now = pq.poll();
                    int nowX = now[0];
                    int nowY = now[1];
                    for(int dir = 0; dir < 4; dir++) {
                        int x = nowX + dirs[dir];
                        int y = nowY + dirs[dir + 1];
                        if(x < 0 || x >= row || y < 0 || y >= col) continue;
                        if(grid[x][y] != 0 && !visited[x][y]) {
                            pq.offer(new int[]{x, y});
                            visited[x][y] = true;
                        }
                    }
                }
            }
        }
        if(cnt == 0) return 2;// 避免[[0,0,0],[0,1,0],[0,0,0]]情況 刪除1 全部都0
        return cnt;
    }
}
```