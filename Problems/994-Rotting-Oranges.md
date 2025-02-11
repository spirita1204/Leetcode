# 994. Rotting Oranges

Methods: BFS
Difficulty: Medium

**Medium**

10K

338

Companies

You are given an `m x n` `grid` where each cell can have one of three values:

- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return *the minimum number of minutes that must elapse until no cell has a fresh orange*. If *this is impossible, return* `-1`.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/02/16/oranges.png](https://assets.leetcode.com/uploads/2019/02/16/oranges.png)

```
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4

```

**Example 2:**

```
Input: grid = [[2,1,1],[0,1,1],[1,0,1]]
Output: -1
Explanation: The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.

```

**Example 3:**

```
Input: grid = [[0,2]]
Output: 0
Explanation: Since there are already no fresh oranges at minute 0, the answer is just 0.

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 10`
- `grid[i][j]` is `0`, `1`, or `2`.

```java
class Solution {
    public int orangesRotting(int[][] grid) {
        //Bfs
        int row = grid.length;
        int col = grid[0].length;
        int[] dirs = {0, -1, 0, 1, 0};
        int times= 0;//計算幾次
        int needChange = 0;//需要做的次數
        Queue<int[]> q = new ArrayDeque<>();
        boolean[][] visited = new boolean[row][col];

        for(int i = 0;i< row;i++){
            for(int j = 0;j<col;j++){
                if(grid[i][j] == 2) q.offer(new int[]{i, j});//將rotten放入
                if(grid[i][j] != 0) needChange++;
            }
        }

        if(q.size() == 0 && needChange == 0) return 0;//不用作動

        while(!q.isEmpty()){
            int size = q.size();
            times++;
            while(size-- > 0){
                int[] side = q.poll();
                if(visited[side[0]][side[1]]) continue;
                visited[side[0]][side[1]] = true;
                needChange--;
                
                for(int i = 0;i<4;i++){
                    int x = side[0] + dirs[i];
                    int y = side[1] + dirs[i+1];
                    if(x < 0 || x >= row || y < 0 || y >= col || grid[x][y] != 1) continue;
                    q.offer(new int[]{x, y}); 
                    grid[x][y] = 2;//rotten
                }
            }
        }
        return (needChange > 0) ? -1 : times - 1;
    }
}
```