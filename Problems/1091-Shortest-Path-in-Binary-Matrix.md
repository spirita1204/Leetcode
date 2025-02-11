# 1091. Shortest Path in Binary Matrix

Methods: BFS
Difficulty: Medium

**Medium**

4.6K

181

Companies

Given an `n x n` binary matrix `grid`, return *the length of the shortest **clear path** in the matrix*. If there is no clear path, return `-1`.

A **clear path** in a binary matrix is a path from the **top-left** cell (i.e., `(0, 0)`) to the **bottom-right** cell (i.e., `(n - 1, n - 1)`) such that:

- All the visited cells of the path are `0`.
- All the adjacent cells of the path are **8-directionally** connected (i.e., they are different and they share an edge or a corner).

The **length of a clear path** is the number of visited cells of this path.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/02/18/example1_1.png](https://assets.leetcode.com/uploads/2021/02/18/example1_1.png)

```
Input: grid = [[0,1],[1,0]]
Output: 2

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/02/18/example2_1.png](https://assets.leetcode.com/uploads/2021/02/18/example2_1.png)

```
Input: grid = [[0,0,0],[1,1,0],[1,1,0]]
Output: 4

```

**Example 3:**

```
Input: grid = [[1,0,0],[1,1,0],[1,1,0]]
Output: -1

```

**Constraints:**

- `n == grid.length`
- `n == grid[i].length`
- `1 <= n <= 100`
- `grid[i][j] is 0 or 1`

```java
class Solution {
    public int shortestPathBinaryMatrix(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;
        
        if(grid[0][0] != 0 || grid[row - 1][col - 1] != 0) return -1;

        Queue<int[]> q = new LinkedList<>();
        boolean[][] visited = new boolean[row][col];

        int[][] dirs = {{1,1},{1,0},{-1,-1},{-1,0},{0,-1},{0,1},{-1,1},{1,-1}};
        int shortestPath = 0;
        boolean isEnd = false;

        q.offer(new int[]{0, 0});
        visited[0][0] = true;
        
        while(!q.isEmpty() && !isEnd){//當到尾就不用繼續
            shortestPath++;
            int size = q.size();
            // 遍歷所有周邊
            while(size--> 0){
                int[] node = q.poll();
                // 遍歷所有方向 
                for(int i= 0; i< 8; i++){
                    int x = node[0] + dirs[i][0];
                    int y = node[1] + dirs[i][1];
                   
                    if(x >= 0 && x < row && y >= 0 && y < col && visited[x][y] != true && grid[x][y] == 0){// 當在範圍內
                        q.offer(new int[]{x, y});
                        visited[x][y] = true;
                        // 當到達右下角
                        if(x == row - 1 && y == col - 1){
                            shortestPath++;
                            isEnd = true;
                            break;
                        }
                    }
                }
            }
        }
        if(visited[row - 1][col - 1] != true) return -1;//當沒走到最後
        return shortestPath; 
    }
}
```