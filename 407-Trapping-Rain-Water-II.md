# 407. Trapping Rain Water II

Methods: BFS
Data structure: Heap
Difficulty: Hard

Given an `m x n` integer matrix `heightMap` representing the height of each unit cell in a 2D elevation map, return *the volume of water it can trap after raining*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/04/08/trap1-3d.jpg](https://assets.leetcode.com/uploads/2021/04/08/trap1-3d.jpg)

```
Input: heightMap = [[1,4,3,1,3,2],[3,2,1,3,2,4],[2,3,3,2,3,1]]
Output: 4
Explanation: After the rain, water is trapped between the blocks.
We have two small ponds 1 and 3 units trapped.
The total volume of water trapped is 4.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/04/08/trap2-3d.jpg](https://assets.leetcode.com/uploads/2021/04/08/trap2-3d.jpg)

```
Input: heightMap = [[3,3,3,3,3],[3,2,2,2,3],[3,2,1,2,3],[3,2,2,2,3],[3,3,3,3,3]]
Output: 10

```

**Constraints:**

- `m == heightMap.length`
- `n == heightMap[i].length`
- `1 <= m, n <= 200`
- `0 <= heightMap[i][j] <= 2 * 104`

```java
class Solution {
    public int trapRainWater(int[][] heightMap) {
        // [1,4,3,1,3,2]
        // [3,2,1,3,2,4]
        // [2,3,3,2,3,1]
        int[] dirs = new int[]{0, 1, 0, -1, 0};
        int m = heightMap.length;
        int n = heightMap[0].length;
        // 按照高度排序由小到大
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]);
        boolean[][] vis = new boolean[m][n];

        // Add first and last column
        for (int i = 0; i < m; i++) {
            vis[i][0] = true;
            vis[i][n - 1] = true;
            pq.offer(new int[]{heightMap[i][0], i, 0});
            pq.offer(new int[]{heightMap[i][n - 1], i, n - 1});
        }

        // Add first and last row
        for (int i = 1; i < n - 1; i++) {
            vis[0][i] = true;
            vis[m - 1][i] = true;
            pq.offer(new int[]{heightMap[0][i], 0, i});
            pq.offer(new int[]{heightMap[m - 1][i], m - 1, i});
        }
        int res = 0;
        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int h = curr[0], r = curr[1], c = curr[2];
            for(int i = 0; i < 4; i++) {
                int x = r + dirs[i];
                int y = c + dirs[i + 1];
                // 出界
                if (x < 0 || x >= m || y < 0 || y >= n) 
                    continue;
                // 訪問過
                if(vis[x][y])
                    continue;
                // 因為p從最小取出 所以假設當前可以trap water 則直接填滿成當前高度
                int trapWater = Math.max(0, h - heightMap[x][y]);
                res += trapWater;
                vis[x][y] = true;
                // 決定是否將當前高度升高
                int compareHeight = Math.max(h, heightMap[x][y]);
                pq.offer(new int[]{compareHeight, x, y});
            }
        }
        return res;
    }
}
```