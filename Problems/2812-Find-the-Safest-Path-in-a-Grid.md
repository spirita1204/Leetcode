# 2812. Find the Safest Path in a Grid

Methods: BFS, Binary Search
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a **0-indexed** 2D matrix `grid` of size `n x n`, where `(r, c)` represents:

- A cell containing a thief if `grid[r][c] = 1`
- An empty cell if `grid[r][c] = 0`

You are initially positioned at cell `(0, 0)`. In one move, you can move to any adjacent cell in the grid, including cells containing thieves.

The **safeness factor** of a path on the grid is defined as the **minimum** manhattan distance from any cell in the path to any thief in the grid.

Return *the **maximum safeness factor** of all paths leading to cell* `(n - 1, n - 1)`*.*

An **adjacent** cell of cell `(r, c)`, is one of the cells `(r, c + 1)`, `(r, c - 1)`, `(r + 1, c)` and `(r - 1, c)` if it exists.

The **Manhattan distance** between two cells `(a, b)` and `(x, y)` is equal to `|a - x| + |b - y|`, where `|val|` denotes the absolute value of val.

**Example 1:**

![https://assets.leetcode.com/uploads/2023/07/02/example1.png](https://assets.leetcode.com/uploads/2023/07/02/example1.png)

```
Input: grid = [[1,0,0],[0,0,0],[0,0,1]]
Output: 0
Explanation: All paths from (0, 0) to (n - 1, n - 1) go through the thieves in cells (0, 0) and (n - 1, n - 1).

```

**Example 2:**

![https://assets.leetcode.com/uploads/2023/07/02/example2.png](https://assets.leetcode.com/uploads/2023/07/02/example2.png)

```
Input: grid = [[0,0,1],[0,0,0],[0,0,0]]
Output: 2
Explanation: The path depicted in the picture above has a safeness factor of 2 since:
- The closest cell of the path to the thief at cell (0, 2) is cell (0, 0). The distance between them is | 0 - 0 | + | 0 - 2 | = 2.
It can be shown that there are no other paths with a higher safeness factor.

```

**Example 3:**

![https://assets.leetcode.com/uploads/2023/07/02/example3.png](https://assets.leetcode.com/uploads/2023/07/02/example3.png)

```
Input: grid = [[0,0,0,1],[0,0,0,0],[0,0,0,0],[1,0,0,0]]
Output: 2
Explanation: The path depicted in the picture above has a safeness factor of 2 since:
- The closest cell of the path to the thief at cell (0, 3) is cell (1, 2). The distance between them is | 0 - 1 | + | 3 - 2 | = 2.
- The closest cell of the path to the thief at cell (3, 0) is cell (3, 2). The distance between them is | 3 - 3 | + | 0 - 2 | = 2.
It can be shown that there are no other paths with a higher safeness factor.

```

**Constraints:**

- `1 <= grid.length == n <= 400`
- `grid[i].length == n`
- `grid[i][j]` is either `0` or `1`.
- There is at least one thief in the `grid`.

```java
class Solution {
    int[] dirs = {0, 1, 0, -1, 0};
    public int maximumSafenessFactor(List<List<Integer>> grid) {
        // score[i][j] = 到最近盜賊距離 + 1 -> 避免跟原本盜賊搞混
        // 透過BS猜一個Safe Distance 讓路徑都grid[i][j]都 大於 及代表有路徑
        int n = grid.size();
        int[][] score = new int[n][n];
        for (int[] row : score)
            Arrays.fill(row, Integer.MAX_VALUE);// 因為要找最小 初始不得為0

        // 先給定每格score
        bfs(grid, score, n);
        // 透過bs猜d
        int left = 0, right = n;// 兩點最遠距離
        while(left <= right) {
            int mid = left + (right-left) / 2;
            // 猜的d 有路線從左上到右下
            if(isSafeDistance(score, mid)) left = mid + 1;
            else right = mid - 1;
        }
        return (left == 0)? 0: left - 1;
    }

    private void bfs(List<List<Integer>> grid, int[][] score, int n) {
        Queue<int[]> q = new LinkedList<>();
        // 先將thieves取出 再對每個thieves做BFS
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                if(grid.get(i).get(j) == 1) {
                    score[i][j] = 1;
                    q.offer(new int[]{i, j});
                }
            }
        }
        // 填充每個grid[i][j] 的score 
        while(!q.isEmpty()) {
            int[] e = q.poll();
            int i = e[0];
            int j = e[1];

            for(int d = 0; d < dirs.length - 1; d++) {
                int x = i + dirs[d];
                int y = j + dirs[d + 1];
                // 如果當前值已在其他thief更新並更小 即不處理
                if(x >= 0 && x < n && y >= 0 && y < n && score[x][y] > score[i][j] + 1) {// 邊界內 
                    // Manhattan distance + 1
                    score[x][y] = score[i][j] + 1;
                    q.offer(new int[]{x, y});
                }
            }
        }
    }

    private boolean isSafeDistance(int[][] score, int mid) {
        int n = score.length;
        Queue<int[]> q = new LinkedList<>();
        boolean[][] visited = new boolean[n][n];
        // 起點即不滿足
        if(score[0][0] <= mid) return false;
        // 從左上開始
        q.offer(new int[]{0, 0});
        visited[0][0] = true;

        while(!q.isEmpty()) {
            int[] e = q.poll();
            int i = e[0];
            int j = e[1];

            for(int d = 0; d < dirs.length - 1; d++) {
                int x = i + dirs[d];
                int y = j + dirs[d + 1];
                // 訪問過就跳過
                // 當前score <= mid 跳過
                if(x >= 0 && x < n && y >= 0 && y < n && !visited[x][y] && score[x][y] > mid) {// 邊界內 
                    // 當前mid可以跑到終點
                    if(x == n - 1 && y == n -1) return true;
                    visited[x][y] = true;
                    q.offer(new int[]{x, y});
                }
            }
        }
        return false;
    }
}
```