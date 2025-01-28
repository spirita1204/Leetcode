# 2658. Maximum Number of Fish in a Grid  

  Methods: BFS </br> Difficulty: Medium </br> </br>You are given a **0-indexed** 2D matrix `grid` of size `m x n`, where `(r, c)` represents:

- A **land** cell if `grid[r][c] = 0`, or
- A **water** cell containing `grid[r][c]` fish, if `grid[r][c] > 0`.
A fisher can start at any **water** cell `(r, c)` and can do the following operations any number of times:

- Catch all the fish at cell `(r, c)`, or
- Move to any adjacent **water** cell.
Return *the ****maximum**** number of fish the fisher can catch if he chooses his starting cell optimally, or *`0` if no water cell exists.

An **adjacent** cell of the cell `(r, c)`, is one of the cells `(r, c + 1)`, `(r, c - 1)`, `(r + 1, c)` or `(r - 1, c)` if it exists.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2023/03/29/example.png)

```plain text
Input: grid = [[0,2,1,0],[4,0,0,3],[1,0,0,4],[0,3,2,0]]
Output: 7
Explanation: The fisher can start at cell(1,3) and collect 3 fish, then move to cell(2,3) and collect 4 fish.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2023/03/29/example2.png)

```plain text
Input: grid = [[1,0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,1]]
Output: 1
Explanation: The fisher can start at cells (0,0) or (3,3) and collect a single fish.
```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 10`
- `0 <= grid[i][j] <= 10`
```java
class Solution {
    int[] dirs = new int[] { 0, 1, 0, -1, 0 };

    public int findMaxFish(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        boolean[][] vis = new boolean[m][n];
        // 全域最大
        int max = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (vis[i][j] || grid[i][j] == 0)
                    continue;
                max = Math.max(max, bfs(grid, i, j, vis));
            }
        }
        return max;
    }

    private int bfs(int[][] grid, int i, int j, boolean[][] vis) {
        int mMax = 0;
        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[]{i, j});
        vis[i][j] = true;  // 在進入隊列後就標記為已訪問

        while(!q.isEmpty()) {
            int[] e = q.poll();
            mMax += grid[e[0]][e[1]];

            for(int d = 0; d < 4; d++) {
                int x = e[0] + dirs[d];
                int y = e[1] + dirs[d + 1];
                if(x < 0 || x >= grid.length || y < 0 || y >= grid[0].length) // 越界
                    continue;
                if(grid[x][y] == 0)// 陸地
                    continue;
                if(vis[x][y])
                    continue;
                q.offer(new int[]{x, y});
                vis[x][y] = true;  // 標記相鄰節點為已訪問
            }
        }
        return mMax;
    }
}
```



