# 3212. Count Submatrices With Equal Frequency of X and Y

Methods: Prefix Sum
Difficulty: Medium

Medium

Companies

Hint

Given a 2D character matrix `grid`, where `grid[i][j]` is either `'X'`, `'Y'`, or `'.'`, return the number of

submatrices

that contains:

- `grid[0][0]`
- an **equal** frequency of `'X'` and `'Y'`.
- **at least** one `'X'`.

**Example 1:**

**Input:** grid = [["X","Y","."],["Y",".","."]]

**Output:** 3

**Explanation:**

![https://assets.leetcode.com/uploads/2024/06/07/examplems.png](https://assets.leetcode.com/uploads/2024/06/07/examplems.png)

**Example 2:**

**Input:** grid = [["X","X"],["X","Y"]]

**Output:** 0

**Explanation:**

No submatrix has an equal frequency of `'X'` and `'Y'`.

**Example 3:**

**Input:** grid = [[".","."],[".","."]]

**Output:** 0

**Explanation:**

No submatrix has at least one `'X'`.

**Constraints:**

- `1 <= grid.length, grid[i].length <= 1000`
- `grid[i][j]` is either `'X'`, `'Y'`, or `'.'`.

```java
class Solution {
    public int numberOfSubmatrices(char[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;

        // Prefix sums for 'X' and 'Y'
        int[][] prefixX = new int[rows + 1][cols + 1];
        int[][] prefixY = new int[rows + 1][cols + 1];

        // Calculate prefix sums
        for (int i = 1; i <= rows; i++) {
            for (int j = 1; j <= cols; j++) {
                prefixX[i][j] = prefixX[i - 1][j] + prefixX[i][j - 1] - prefixX[i - 1][j - 1] + (grid[i - 1][j - 1] == 'X' ? 1 : 0);
                prefixY[i][j] = prefixY[i - 1][j] + prefixY[i][j - 1] - prefixY[i - 1][j - 1] + (grid[i - 1][j - 1] == 'Y' ? 1 : 0);
            }
        }

        int count = 0;

        // Iterate over all possible bottom-right corners
        for (int i = 1; i <= rows; i++) {
            for (int j = 1; j <= cols; j++) {
                int xCount = prefixX[i][j];
                int yCount = prefixY[i][j];

                if (xCount == yCount && xCount > 0) {
                    count++;
                }
            }
        }

        return count;
    }
}
```