# 3195. Find the Minimum Area to Cover All Ones I

Methods: Basic logic
Difficulty: Medium

- The input is generated such that there is at least one 1 in `grid`.
- `grid[i][j]` is either 0 or 1.
- `1 <= grid.length, grid[i].length <= 1000`

**Constraints:**

The smallest rectangle has both height and width 1, so its area is `1 * 1 = 1`.

![https://assets.leetcode.com/uploads/2024/05/08/examplerect1.png](https://assets.leetcode.com/uploads/2024/05/08/examplerect1.png)

**Explanation:**

**Output:** 1

**Input:** grid = [[0,0],[1,0]]

**Example 2:**

The smallest rectangle has a height of 2 and a width of 3, so it has an area of `2 * 3 = 6`.

![https://assets.leetcode.com/uploads/2024/05/08/examplerect0.png](https://assets.leetcode.com/uploads/2024/05/08/examplerect0.png)

**Explanation:**

**Output:** 6

**Input:** grid = [[0,1,0],[1,0,1]]

**Example 1:**

Return the **minimum** possible area of the rectangle.

You are given a 2D **binary** array `grid`. Find a rectangle with horizontal and vertical sides with the **smallest** area, such that all the 1's in `grid` lie inside this rectangle.

Hint

Companies

Medium

```java
class Solution {
    public int minimumArea(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;
        
        int minRow = Integer.MAX_VALUE;
        int maxRow = Integer.MIN_VALUE;
        int minCol = Integer.MAX_VALUE;
        int maxCol = Integer.MIN_VALUE;
        
        for (int r = 0; r < row; r++) {
            for (int c = 0; c < col; c++) {
                if (grid[r][c] == 1) {
                    if (r < minRow) minRow = r;
                    if (r > maxRow) maxRow = r;
                    if (c < minCol) minCol = c;
                    if (c > maxCol) maxCol = c;
                }
            }
        }

        int width = maxCol - minCol + 1;
        int height = maxRow - minRow + 1;
        
        return width * height;
    }
}
```