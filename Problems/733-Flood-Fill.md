# 733. Flood Fill

Methods: BFS
Difficulty: Easy

**Easy**

6.8K

683

Companies

An image is represented by an `m x n` integer grid `image` where `image[i][j]` represents the pixel value of the image.

You are also given three integers `sr`, `sc`, and `color`. You should perform a **flood fill** on the image starting from the pixel `image[sr][sc]`.

To perform a **flood fill**, consider the starting pixel, plus any pixels connected **4-directionally** to the starting pixel of the same color as the starting pixel, plus any pixels connected **4-directionally** to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with `color`.

Return *the modified image after performing the flood fill*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/06/01/flood1-grid.jpg](https://assets.leetcode.com/uploads/2021/06/01/flood1-grid.jpg)

```
Input: image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, color = 2
Output: [[2,2,2],[2,2,0],[2,0,1]]
Explanation: From the center of the image with position (sr, sc) = (1, 1) (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected to the starting pixel.

```

**Example 2:**

```
Input: image = [[0,0,0],[0,0,0]], sr = 0, sc = 0, color = 0
Output: [[0,0,0],[0,0,0]]
Explanation: The starting pixel is already colored 0, so no changes are made to the image.

```

**Constraints:**

- `m == image.length`
- `n == image[i].length`
- `1 <= m, n <= 50`
- `0 <= image[i][j], color < 216`
- `0 <= sr < m`
- `0 <= sc < n`

```java
class Solution {
    int[] DIRS = {0, 1, 0, -1, 0};//四個方位
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        if (image[sr][sc] == color) return image; // same color -> no need to replace

        int m = image.length;
        int n = image[0].length;
        int oldColor = image[sr][sc];//紀錄原本顏色
        image[sr][sc] = color;

        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[]{sr, sc});//起點開始氾濫

        while (!q.isEmpty()) {
            int[] top = q.poll();
            for (int i = 0; i < 4; i++) {
                int nr = top[0] + DIRS[i]; //x
                int nc = top[1] + DIRS[i + 1]; //y
                if (nr < 0 || nr == m || nc < 0 || nc == n || image[nr][nc] != oldColor) continue;
                image[nr][nc] = color; // also mean we marked it as visited!
                q.offer(new int[]{nr, nc});
            }
        }
        return image;
    }
}
```