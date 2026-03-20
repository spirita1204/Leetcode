# 3070. Count Submatrices with Top-Left Element and Sum Less Than k  

  Methods: Prefix Sum </br> Difficulty: Medium </br> </br>You are given a **0-indexed** integer matrix `grid` and an integer `k`.

Return *the ****number**** of submatrices that contain the top-left element of the* `grid`, *and have a sum less than or equal to *`k`.    

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2024/01/01/example1.png)

```plain text
Input: grid = [[7,6,3],[6,6,1]], k = 18
Output: 4   
Explanation: There are only 4 submatrices, shown in the image above, that contain the top-left element of grid, and have a sum less than or equal to 18.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2024/01/01/example21.png)

```plain text
Input: grid = [[7,2,9],[1,5,0],[2,6,6]], k = 20
Output: 6   
Explanation: There are only 6 submatrices, shown in the image above, that contain the top-left element of grid, and have a sum less than or equal to 20.
```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= n, m <= 1000`
- `0 <= grid[i][j] <= 1000`
- `1 <= k <= 109`
```java
class Solution {
    public int countSubmatrices(int[][] grid, int k) {
        int m = grid.length, n = grid[0].length;
        int[][] prefix = new int[m][n];

        int count = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {

                prefix[i][j] = grid[i][j];

                if (i > 0) prefix[i][j] += prefix[i - 1][j];
                if (j > 0) prefix[i][j] += prefix[i][j - 1];
                if (i > 0 && j > 0) prefix[i][j] -= prefix[i - 1][j - 1];

                if (prefix[i][j] <= k) {
                    count++;
                }
            }
        }

        return count;
    }
}
```

