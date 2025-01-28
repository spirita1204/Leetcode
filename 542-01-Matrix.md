# 542. 01 Matrix

Methods: BFS
Difficulty: Medium

**Medium**

6.8K

326

Companies

Given an `m x n` binary matrix `mat`, return *the distance of the nearest* `0` *for each cell*.

The distance between two adjacent cells is `1`.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/04/24/01-1-grid.jpg](https://assets.leetcode.com/uploads/2021/04/24/01-1-grid.jpg)

```
Input: mat = [[0,0,0],[0,1,0],[0,0,0]]
Output: [[0,0,0],[0,1,0],[0,0,0]]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/04/24/01-2-grid.jpg](https://assets.leetcode.com/uploads/2021/04/24/01-2-grid.jpg)

```
Input: mat = [[0,0,0],[0,1,0],[1,1,1]]
Output: [[0,0,0],[0,1,0],[1,2,1]]

```

**Constraints:**

- `m == mat.length`
- `n == mat[i].length`
- `1 <= m, n <= 104`
- `1 <= m * n <= 104`
- `mat[i][j]` is either `0` or `1`.
- There is at least one `0` in `mat`.

```java
class Solution {
    public int[][] updateMatrix(int[][] mat) {
        int row = mat.length;
        int col = mat[0].length;
        int[] dirs = new int[]{0 , 1, 0, -1, 0};
        Queue<int[]> q = new ArrayDeque<>();
        q.offer(new int[]{0, 0});

        for(int i = 0;i< row;i++){
            for(int j = 0;j<col;j++){
                if (mat[i][j] == 0) {
                    q.offer(new int[] {i, j});
                }else{
                    mat[i][j] = Integer.MAX_VALUE;//將1設為最大
                }
            }
        }
        while (!q.isEmpty()) {
            int[] cell = q.poll();
            for (int d = 0; d < 4; d++) {
                int r = cell[0] + dirs[d];
                int c = cell[1] + dirs[d+1];
                if (r < 0 || r >= row || c < 0 || c >= col || 
                    mat[r][c] <= mat[cell[0]][cell[1]]) continue;//已久更近的 路線
                q.add(new int[] {r, c});
                mat[r][c] = mat[cell[0]][cell[1]] + 1;
            }
        }
        return mat;
    }
}
```