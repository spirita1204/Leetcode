# 3286. Find a Safe Walk Through a Grid  

  Methods: BFS </br> Difficulty: Medium </br> </br>You are given an `m x n` binary matrix `grid` and an integer `health`.

You start on the upper-left corner `(0, 0)` and would like to get to the lower-right corner `(m - 1, n - 1)`.

You can move up, down, left, or right from one cell to another adjacent cell as long as your health *remains* **positive**.

Cells `(i, j)` with `grid[i][j] = 1` are considered **unsafe** and reduce your health by 1.

Return `true` if you can reach the final cell with a health value of 1 or more, and `false` otherwise.

**Example 1:**

**Input:** grid = [[0,1,0,0,0],[0,1,0,1,0],[0,0,0,1,0]], health = 1

**Output:** true

**Explanation:**

The final cell can be reached safely by walking along the gray cells below.

![Image](https://assets.leetcode.com/uploads/2024/08/04/3868_examples_1drawio.png)

**Example 2:**

**Input:** grid = [[0,1,1,0,0,0],[1,0,1,0,0,0],[0,1,1,1,0,1],[0,0,1,0,1,0]], health = 3

**Output:** false

**Explanation:**

A minimum of 4 health points is needed to reach the final cell safely.

![Image](https://assets.leetcode.com/uploads/2024/08/04/3868_examples_2drawio.png)

**Example 3:**

**Input:** grid = [[1,1,1],[1,0,1],[1,1,1]], health = 5

**Output:** true

**Explanation:   **

The final cell can be reached safely by walking along the gray cells below.

![Image](https://assets.leetcode.com/uploads/2024/08/04/3868_examples_3drawio.png)

Any path that does not go through the cell `(1, 1)` is unsafe since your health will drop to 0 when reaching the final cell.

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 50`
- `2 <= m * n`
- `1 <= health <= m + n`
- `grid[i][j]` is either 0 or 1.  
```java
class Solution {
    int[] dx = {1, -1, 0, 0};  
    int[] dy = {0, 0, 1, -1};  

    public boolean findSafeWalk(List<List<Integer>> grid, int health) {
        int n = grid.size();
        int m = grid.get(0).size();

        int[][] maxHealth = new int[n][m];
        for (int i = 0; i < n; i++) {
            Arrays.fill(maxHealth[i], -1);
        }

        int initialH = health - grid.get(0).get(0);
        if (initialH <= 0) return false;

        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[]{initialH, 0, 0});
        maxHealth[0][0] = initialH;

        while (!q.isEmpty()) {
            int[] curr = q.poll();

            int currH = curr[0];
            int r = curr[1];
            int c = curr[2];

            if (r == n - 1 && c == m - 1) {
                return true;
            }

            for (int d = 0; d < 4; d++) {
                int nr = r + dx[d];
                int nc = c + dy[d];

                if (nr < 0 || nc < 0 || nr >= n || nc >= m) continue;

                int remH = currH - grid.get(nr).get(nc);

                if (remH <= 0) continue;
                if (remH <= maxHealth[nr][nc]) continue;

                maxHealth[nr][nc] = remH;
                q.offer(new int[]{remH, nr, nc});
            }
        }

        return false;
    }
}
```



