# 827. Making A Large Island  

  Methods: BFS </br> Difficulty: Hard </br> </br>You are given an `n x n` binary matrix `grid`. You are allowed to change **at most one** `0` to be `1`.

Return *the size of the largest ****island**** in* `grid` *after applying this operation*.

An **island** is a 4-directionally connected group of `1`s.

**Example 1:**

```plain text
Input: grid = [[1,0],[0,1]]
Output: 3
Explanation: Change one 0 to 1 and connect two 1s, then we get an island with area = 3.

```

**Example 2:**

```plain text
Input: grid = [[1,1],[1,0]]
Output: 4
Explanation:Change the 0 to 1 and make the island bigger, only one island with area = 4.
```

**Example 3:**

```plain text
Input: grid = [[1,1],[1,1]]
Output: 4
Explanation: Can't change any 0 to 1, only one island with area = 4.

```

**Constraints:**

- `n == grid.length`
- `n == grid[i].length`
- `1 <= n <= 500`
- `grid[i][j]` is either `0` or `1`.
```java
class Solution {
    int[] dirs = new int[]{0, 1, 0, -1, 0};

    public int largestIsland(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        Map<Integer, Integer> islandSize = new HashMap<>();
        int islandId = 2; // 從 2 開始標記不同的島嶼 // 相同島嶼著色
        int maxIsland = 0;
        
        // 1. 遍歷 grid，標記島嶼並記錄其大小
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    int size = bfs(grid, i, j, islandId, m, n);
                    islandSize.put(islandId, size);
                    maxIsland = Math.max(maxIsland, size);
                    islandId++;
                }
            }
        }

        // 2. 遍歷所有 0，嘗試將其變為 1，合併不同的島嶼
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 0) {
                    Set<Integer> seenIslands = new HashSet<>();
                    int newSize = 1; // 先將當前 0 變成 1
                    
                    for (int dir = 0; dir < 4; dir++) {
                        int x = i + dirs[dir];
                        int y = j + dirs[dir + 1];

                        if (x >= 0 && x < m && y >= 0 && y < n && grid[x][y] > 1) {
                            int id = grid[x][y];
                            if (!seenIslands.contains(id)) {
                                newSize += islandSize.get(id);
                                seenIslands.add(id);
                            }
                        }
                    }
                    maxIsland = Math.max(maxIsland, newSize);
                }
            }
        }

        // 3. 如果 grid 全都是 1，直接返回總面積
        return maxIsland == 0 ? m * n : maxIsland;
    }

    private int bfs(int[][] grid, int i, int j, int islandId, int m, int n) {
        int size = 0;
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{i, j});
        grid[i][j] = islandId;// 相同島嶼著色

        while (!queue.isEmpty()) {
            int[] cell = queue.poll();
            size++;

            for (int dir = 0; dir < 4; dir++) {
                int x = cell[0] + dirs[dir];
                int y = cell[1] + dirs[dir + 1];

                if (x >= 0 && x < m && y >= 0 && y < n && grid[x][y] == 1) {
                    grid[x][y] = islandId;
                    queue.offer(new int[]{x, y});
                }
            }
        }
        return size;
    }
}
```



```sql
class Solution {
    int[] dirs = new int[]{0, 1, 0, -1, 0};

    public int largestIsland(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int max = 0;

        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                max = Math.max(max, bfs(grid, i, j, m, n));
            }
        }
        return max;
    }
    private int bfs(int[][] grid, int i, int j, int m, int n) {
        int sum = 0;
        boolean[][] vis = new boolean[m][n];
        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[]{i, j});
        
        while(!q.isEmpty()) {
            int[] e = q.poll();
            
            if(vis[e[0]][e[1]])
                continue;
            vis[e[0]][e[1]] = true;
            sum++;

            for(int dir = 0; dir < 4; dir++) {
                int x = e[0] + dirs[dir];
                int y = e[1] + dirs[dir + 1];
                
                if(x < 0 || x >= m || y < 0 || y >= n || vis[x][y] || grid[x][y] == 0) 
                    continue;
                if(grid[x][y] == 1) {
                    q.offer(new int[]{x, y});
                }
            }
        }
        return sum;
    }
}
```

