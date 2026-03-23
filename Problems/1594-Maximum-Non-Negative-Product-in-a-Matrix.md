# 1594. Maximum Non Negative Product in a Matrix  

  Methods: DP </br> Difficulty: Medium </br> </br>You are given a `m x n` matrix `grid`. Initially, you are located at the top-left corner `(0, 0)`, and in each step, you can only **move right or down** in the matrix.

Among all possible paths starting from the top-left corner `(0, 0)` and ending in the bottom-right corner `(m - 1, n - 1)`, find the path with the **maximum non-negative product**. The product of a path is the product of all integers in the grid cells visited along the path.

Return the *maximum non-negative product ****modulo**** *`109 + 7`. *If the maximum product is ****negative****, return *`-1`.

Notice that the modulo is performed after getting the maximum product.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/12/23/product1.jpg)

```plain text
Input: grid = [[-1,-2,-3],[-2,-3,-3],[-3,-3,-2]]
Output: -1
Explanation: It is not possible to get non-negative product in the path from (0, 0) to (2, 2), so return -1.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/12/23/product2.jpg)

```plain text
Input: grid = [[1,-2,1],[1,-2,1],[3,-4,1]]
Output: 8
Explanation: Maximum non-negative product is shown (1 * 1 * -2 * -4 * 1 = 8).  
```

**Example 3:  **

![Image](https://assets.leetcode.com/uploads/2021/12/23/product3.jpg)

```plain text
Input: grid = [[1,3],[0,-4]]
Output: 0
Explanation: Maximum non-negative product is shown (1 * 0 * -4 = 0).
```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 15   `
- `4 <= grid[i][j] <= 4`
```java
class Solution {
    public int maxProductPath(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        long MOD = 1000000007;
        // 負數會翻轉最大 / 最小關係
        long[][] mx = new long[m][n];// 到 (i,j) 的最大 product
        long[][] mn = new long[m][n];// 到 (i,j) 的最小 product

        mx[0][0] = mn[0][0] = grid[0][0];

        // first row
        for (int j = 1; j < n; j++) {
            mx[0][j] = mn[0][j] = mx[0][j - 1] * grid[0][j];
        }

        // first column
        for (int i = 1; i < m; i++) {
            mx[i][0] = mn[i][0] = mx[i - 1][0] * grid[i][0];
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                long x = grid[i][j];

                long a = mx[i - 1][j] * x;// 上最大 × 自己
                long b = mn[i - 1][j] * x;// 上最小 × 自己
                long c = mx[i][j - 1] * x;// 左最大 × 自己
                long d = mn[i][j - 1] * x;// 左最小 × 自己

                mx[i][j] = Math.max(Math.max(a, b), Math.max(c, d));
                mn[i][j] = Math.min(Math.min(a, b), Math.min(c, d));
            }
        }
        long ans = mx[m - 1][n - 1];
        if (ans < 0) 
            return -1;

        return (int)(ans % MOD);
    }
}
```

