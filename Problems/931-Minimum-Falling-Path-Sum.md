# 931. Minimum Falling Path Sum

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Given an `n x n` array of integers `matrix`, return *the **minimum sum** of any **falling path** through* `matrix`.

A **falling path** starts at any element in the first row and chooses the element in the next row that is either directly below or diagonally left/right. Specifically, the next element from position `(row, col)` will be `(row + 1, col - 1)`, `(row + 1, col)`, or `(row + 1, col + 1)`.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/11/03/failing1-grid.jpg](https://assets.leetcode.com/uploads/2021/11/03/failing1-grid.jpg)

```
Input: matrix = [[2,1,3],[6,5,4],[7,8,9]]
Output: 13
Explanation: There are two falling paths with a minimum sum as shown.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/11/03/failing2-grid.jpg](https://assets.leetcode.com/uploads/2021/11/03/failing2-grid.jpg)

```
Input: matrix = [[-19,57],[-40,-5]]
Output: -59
Explanation: The falling path with a minimum sum is shown.

```

**Constraints:**

- `n == matrix.length == matrix[i].length`
- `1 <= n <= 100`
- `100 <= matrix[i][j] <= 100`

```java
class Solution {
    public int minFallingPathSum(int[][] matrix) {
        int res = Integer.MAX_VALUE;
        int row = matrix[0].length;
        int col = matrix.length;
        int[][] dp = new int[col][row];//第 i, j代表當前以上最小值

        for(int i = 0; i< row; i++) dp[0][i] = matrix[0][i];

        for(int i = 1; i< col; i++) {
            for(int j = 0; j< row; j++) {
                dp[i][j] = matrix[i][j];
                if(j == 0) {
                    dp[i][j] += Math.min(dp[i - 1][j], dp[i - 1][j + 1]);
                }else if(j == row - 1) {
                    dp[i][j] += Math.min(dp[i - 1][j], dp[i - 1][j - 1]);
                }else {
                    dp[i][j] += Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i - 1][j + 1]));
                }
            }
        }

        for(int i = 0; i< row; i++) {
            res = Math.min(res, dp[col - 1][i]);
        }
        return res;
    }
}
```