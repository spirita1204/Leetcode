# 2503. Maximum Number of Points From Grid Queries  

  Methods: BFS,Sort </br> Data Structure: Heap </br> Difficulty: Hard </br> </br>You are given an `m x n` integer matrix `grid` and an array `queries` of size `k`. 

Find an array `answer` of size `k` such that for each integer `queries[i]` you start in the **top left** cell of the matrix and repeat the following process:

- If `queries[i]` is **strictly** greater than the value of the current cell that you are in, then you get one point if it is your first time visiting this cell, and you can move to any **adjacent** cell in all `4` directions: up, down, left, and right.
- Otherwise, you do not get any points, and you end this process.
After the process, `answer[i]` is the **maximum** number of points you can get. **Note** that for each query you are allowed to visit the same cell **multiple** times.

Return *the resulting array* `answer`.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2025/03/15/image1.png)

```plain text
Input: grid = [[1,2,3],[2,5,7],[3,5,1]], queries = [5,6,2]
Output: [5,8,1]
Explanation: The diagrams above show which cells we visit to get points for each query.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2022/10/20/yetgriddrawio-2.png)

```plain text
Input: grid = [[5,2,1],[1,1,2]], queries = [3]
Output: [0]
Explanation: We can not get any points because the value of the top left cell is already greater than or equal to 3.
```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `2 <= m, n <= 1000`
- `4 <= m * n <= 105`
- `k == queries.length`
- `1 <= k <= 104`
- `1 <= grid[i][j], queries[i] <= 106`
```java
class Solution {
    public int[] maxPoints(int[][] grid, int[] queries) {
        int rows = grid.length;
        int cols = grid[0].length;
        int[] dir = new int[] { 0, 1, 0, -1, 0 };

        int n = queries.length;
        int[] res = new int[n];
        int[][] vis = new int[rows][cols];
        // heap + bfs + sort
        Queue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[0]));
        List<int[]> sort = new ArrayList<>();

        for (int i = 0; i < n; i++)
            sort.add(new int[] { queries[i], i });
        sort.sort(Comparator.comparingInt(a -> a[0]));

        pq.offer(new int[] { grid[0][0], 0, 0 });
        vis[0][0] = 1;
        int points = 0;

        for (int[] q : sort) {
            int qVal = q[0];
            int qIdx = q[1];

            while (!pq.isEmpty() && pq.peek()[0] < qVal) {
                int[] top = pq.poll();
                int row = top[1];
                int col = top[2];
                points++;

                for (int d = 0; d < 4; d++) {
                    int x = row + dir[d];
                    int y = col + dir[d + 1];
                    if (x >= 0 && x < rows && y >= 0 && y < cols && vis[x][y] == 0) {
                        pq.offer(new int[] { grid[x][y], x, y });
                        vis[x][y] = 1;
                    }
                }
            }
            res[qIdx] = points;
        }
        return res;
    }
}
```

