# 1039. Minimum Score Triangulation of Polygon  

  Methods: DP </br> Difficulty: Medium </br> </br>You have a convex `n`-sided polygon where each vertex has an integer value. You are given an integer array `values` where `values[i]` is the value of the `ith` vertex in **clockwise order**.

**Polygon** **triangulation** is a process where you divide a polygon into a set of triangles and the vertices of each triangle must also be vertices of the original polygon. Note that no other shapes other than triangles are allowed in the division. This process will result in `n - 2` triangles.

You will **triangulate** the polygon. For each triangle, the *weight* of that triangle is the product of the values at its vertices. The total score of the triangulation is the sum of these *weights* over all `n - 2` triangles.

Return the* minimum possible score *that you can achieve with some* ***triangulation*** *of the polygon.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2025/10/23/ex0-2.png)

**Input:** values = [1,2,3]

**Output:** 6

**Explanation:** The polygon is already triangulated, and the score of the only triangle is 6.

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2025/10/23/ex1-2.png)

**Input:** values = [3,7,4,5]

**Output:** 144

**Explanation:** There are two triangulations, with possible scores: 3*7*5 + 4*5*7 = 245, or 3*4*5 + 3*4*7 = 144.

The minimum score is 144.

**Example 3:**



![Image](https://assets.leetcode.com/uploads/2025/10/23/ex2.png)

**Input:** values = [1,3,1,4,1,5]

**Output:** 13

**Explanation:** The minimum score triangulation is 1*1*3 + 1*1*4 + 1*1*5 + 1*1*1 = 13.

**Constraints:**

- `n == values.length`
- `3 <= n <= 50`
- `1 <= values[i] <= 100`
```java
class Solution {
    public int minScoreTriangulation(int[] values) {
        int n = values.length;
        // dp[i][j] = 頂點區間 [i, j] 的最小分數。
        int[][] dp = new int[n][n];
        // dp[i][j] = min(dp[i][k] + dp[k][j] + values[i]*values[k]*values[j]) 
        // for all i < k < j
        for (int i = n - 1; i >= 0; i--) {          // 從右往左處理起點 i
            for (int j = i + 1; j < n; j++) {       // 終點 j 必須在 i 右邊
                for (int k = i + 1; k < j; k++) {   // 劃分點 k 在 (i, j) 之間
                    dp[i][j] = Math.min(dp[i][j] == 0 ? Integer.MAX_VALUE : dp[i][j],
                        dp[i][k] + dp[k][j] + values[i] * values[k] * values[j]);
                }
            }
        }
        return dp[0][n - 1];
    }
}
```

