# 3342. Find Minimum Time to Reach Last Room II  

  Methods: Dijkstra,Shortest Path </br> Data Structure: Heap </br> Difficulty: Medium </br> Similar: 3341 </br> </br>There is a dungeon with `n x m` rooms arranged as a grid.

You are given a 2D array `moveTime` of size `n x m`, where `moveTime[i][j]` represents the **minimum** time in seconds when you can **start moving** to that room. You start from the room `(0, 0)` at time `t = 0` and can move to an **adjacent** room. Moving between **adjacent** rooms takes one second for one move and two seconds for the next, **alternating** between the two.

Return the **minimum** time to reach the room `(n - 1, m - 1)`.

Two rooms are **adjacent** if they share a common wall, either *horizontally* or *vertically*.

---

**Example 1:**

**Input:** moveTime = [[0,4],[4,4]]

**Output:** 7

**Explanation:**

The minimum time required is 7 seconds.

- At time `t == 4`, move from room `(0, 0)` to room `(1, 0)` in one second.
- At time `t == 5`, move from room `(1, 0)` to room `(1, 1)` in two seconds.
---

**Example 2:**

**Input:** moveTime = [[0,0,0,0],[0,0,0,0]]

**Output:** 6

**Explanation:**

The minimum time required is 6 seconds.

- At time `t == 0`, move from room `(0, 0)` to room `(1, 0)` in one second.
- At time `t == 1`, move from room `(1, 0)` to room `(1, 1)` in two seconds.
- At time `t == 3`, move from room `(1, 1)` to room `(1, 2)` in one second.
- At time `t == 4`, move from room `(1, 2)` to room `(1, 3)` in two seconds.
---



**Example 3:**

**Input:** moveTime = [[0,1],[1,2]]

**Output:** 4

**Constraints:**

- `2 <= n == moveTime.length <= 750`
- `2 <= m == moveTime[i].length <= 750`
- `0 <= moveTime[i][j] <= 109`
```java
class Solution {
    public int minTimeToReach(int[][] moveTime) {
        // Dijkstra
        int n = moveTime.length;
        int m = moveTime[0].length;
        int[][] dp = new int[n][m];

        for (int[] row : dp)
            Arrays.fill(row, Integer.MAX_VALUE);
        // 每次從最小走起
        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[0]));

        // (time, x, y, last)
        pq.add(new int[] { 0, 0, 0 });
        moveTime[0][0] = 0;

        int[] dirs = new int[]{0, 1, 0, -1, 0};

        while (!pq.isEmpty()) {
            int[] current = pq.poll();
            int currTime = current[0];
            int currRow = current[1];
            int currCol = current[2];

            if (currTime >= dp[currRow][currCol])// 代表不能走
                continue;
            if (currRow == n - 1 && currCol == m - 1)// 到終點
                return currTime;

            dp[currRow][currCol] = currTime;

            for (int dir = 0; dir < 4; dir++) {
                int nextRow = currRow + dirs[dir];
                int nextCol = currCol + dirs[dir + 1];
                if (nextRow < 0 || nextRow >= n || nextCol < 0 || nextCol >= m)// 越界
                    continue;
                if(dp[nextRow][nextCol] == Integer.MAX_VALUE) {
                    int cost  = (currRow + currCol) % 2 + 1;
                    int nextTime = Math.max(moveTime[nextRow][nextCol], currTime) + cost;
                    
                    pq.add(new int[] { nextTime, nextRow, nextCol });
                }
            }
        }
        return -1;
    }
}
```

