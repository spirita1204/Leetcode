# 1162. As Far from Land as Possible

Methods: BFS
Difficulty: Medium

[solution](solution%206198cbb2218a47f8af3f45baed099548.md)

```java
class Solution {
    public int maxDistance(int[][] grid) {//BFS
        Queue<int[]> q = new ArrayDeque<>();
        int max = -1;
        
        for(int i = 0 ; i < grid.length ; i++){//將陸地先放入q
            for(int j = 0 ; j < grid[0].length ; j++){
                if(grid[i][j] == 1){//陸地
                    q.offer(new int[]{i,j});
                }
            }
        }
        int[][] dirs = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};//四個方向
        while(!q.isEmpty()){
            int size = q.size();//定義當前同一波數量
            if(size == grid.length*grid.length) return -1;//當全部都是1或0
            while(size-- > 0){//掃過同一階層
                int[] land = q.poll();
                for(int[] e : dirs){
                    int i = land[0] + e[0];
                    int j = land[1] + e[1];
                    if(i >= 0 && j >= 0 && i < grid.length && j <grid.length && grid[i][j] != 1){//沒超出邊界
                        q.offer(new int[]{i,j});
                        grid[i][j] = 1;
                    }
                    System.out.print("aa");
                }      
            }
            max++;
        }
        return max;
    }
}
```

Given an `n x n` `grid` containing only values `0` and `1`, where `0` represents water and `1` represents land, find a water cell such that its distance to the nearest land cell is maximized, and return the distance. If no land or water exists in the grid, return `-1`.

The distance used in this problem is the Manhattan distance: the distance between two cells `(x0, y0)` and `(x1, y1)` is `|x0 - x1| + |y0 - y1|`.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/05/03/1336_ex1.JPG](https://assets.leetcode.com/uploads/2019/05/03/1336_ex1.JPG)

```
Input: grid = [[1,0,1],[0,0,0],[1,0,1]]
Output: 2
Explanation: The cell (1, 1) is as far as possible from all the land with distance 2.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2019/05/03/1336_ex2.JPG](https://assets.leetcode.com/uploads/2019/05/03/1336_ex2.JPG)

```
Input: grid = [[1,0,0],[0,0,0],[0,0,0]]
Output: 4
Explanation: The cell (2, 2) is as far as possible from all the land with distance 4.

```

**Constraints:**

- `n == grid.length`
- `n == grid[i].length`
- `1 <= n <= 100`
- `grid[i][j]` is `0` or `1`