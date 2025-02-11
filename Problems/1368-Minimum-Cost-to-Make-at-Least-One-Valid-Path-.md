# 1368. Minimum Cost to Make at Least One Valid Path in a Grid

Methods: BFS
Difficulty: Hard

Given an `m x n` grid. Each cell of the grid has a sign pointing to the next cell you should visit if you are currently in this cell. The sign of `grid[i][j]` can be:

- `1` which means go to the cell to the right. (i.e go from `grid[i][j]` to `grid[i][j + 1]`)
- `2` which means go to the cell to the left. (i.e go from `grid[i][j]` to `grid[i][j - 1]`)
- `3` which means go to the lower cell. (i.e go from `grid[i][j]` to `grid[i + 1][j]`)
- `4` which means go to the upper cell. (i.e go from `grid[i][j]` to `grid[i - 1][j]`)

Notice that there could be some signs on the cells of the grid that point outside the grid.

You will initially start at the upper left cell `(0, 0)`. A valid path in the grid is a path that starts from the upper left cell `(0, 0)` and ends at the bottom-right cell `(m - 1, n - 1)` following the signs on the grid. The valid path does not have to be the shortest.

You can modify the sign on a cell with `cost = 1`. You can modify the sign on a cell **one time only**.

Return *the minimum cost to make the grid have at least one valid path*.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/02/13/grid1.png](https://assets.leetcode.com/uploads/2020/02/13/grid1.png)

```
Input: grid = [[1,1,1,1],[2,2,2,2],[1,1,1,1],[2,2,2,2]]
Output: 3
Explanation: You will start at point (0, 0).
The path to (3, 3) is as follows. (0, 0) --> (0, 1) --> (0, 2) --> (0, 3) change the arrow to down with cost = 1 --> (1, 3) --> (1, 2) --> (1, 1) --> (1, 0) change the arrow to down with cost = 1 --> (2, 0) --> (2, 1) --> (2, 2) --> (2, 3) change the arrow to down with cost = 1 --> (3, 3)
The total cost = 3.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/02/13/grid2.png](https://assets.leetcode.com/uploads/2020/02/13/grid2.png)

```
Input: grid = [[1,1,3],[3,2,2],[1,1,4]]
Output: 0
Explanation: You can follow the path from (0, 0) to (2, 2).

```

**Example 3:**

![https://assets.leetcode.com/uploads/2020/02/13/grid3.png](https://assets.leetcode.com/uploads/2020/02/13/grid3.png)

```
Input: grid = [[1,2],[4,3]]
Output: 1

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 100`
- `1 <= grid[i][j] <= 4`

```java
class Solution {
    // 0 0 0 1 1 有指向別人       4
    // 1 0 0 0 2.別人沒指向他   2    1
    // 0 0 0 1                   3
    // 1 0 0 0

    // 1 1
    // 0 1
    // Direction vectors: right, left, down, up (matching grid values 1,2,3,4)
    private final int[][] dirs = { { 0, 1 }, { 0, -1 }, { 1, 0 }, { -1, 0 } };

    public int minCost(int[][] grid) {
        int numRows = grid.length, numCols = grid[0].length;

        // Track minimum cost to reach each cell
        int[][] minCost = new int[numRows][numCols];
        for (int[] row : minCost) {
            Arrays.fill(row, Integer.MAX_VALUE);
        }
        // Use deque for 0-1 BFS - add zero cost moves to front, cost=1 to back
        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[] { 0, 0 });
        minCost[0][0] = 0;

        while (!q.isEmpty()) {
            int[] curr = q.poll();
            int row = curr[0];
            int col = curr[1];

            // Try all four directions
            for (int dir = 0; dir < 4; dir++) {
                int newRow = row + dirs[dir][0];
                int newCol = col + dirs[dir][1];
                int cost = (grid[row][col] != (dir + 1)) ? 1 : 0;

                // If position is valid and we found a better path
                if (isValid(newRow, newCol, numRows, numCols) &&
                        minCost[row][col] + cost < minCost[newRow][newCol]) {
                    minCost[newRow][newCol] = minCost[row][col] + cost;
                
                    q.offer(new int[] { newRow, newCol });
                }
            }
        }
        return minCost[numRows - 1][numCols - 1];
    }

    // Check if coordinates are within grid bounds
    private boolean isValid(int row, int col, int numRows, int numCols) {
        return row >= 0 && row < numRows && col >= 0 && col < numCols;
    }
}
```