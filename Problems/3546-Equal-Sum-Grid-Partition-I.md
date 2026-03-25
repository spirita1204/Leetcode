# 3546. Equal Sum Grid Partition I  

  Methods: Prefix Sum </br> Difficulty: Medium </br> </br>You are given an `m x n` matrix `grid` of positive integers. Your task is to determine if it is possible to make **either one horizontal or one vertical cut** on the grid such that:

- Each of the two resulting sections formed by the cut is **non-empty**.
- The sum of the elements in both sections is **equal**.
Return `true` if such a partition exists; otherwise return `false`.

**Example 1:**

**Input:** grid = [[1,4],[2,3]]

**Output:** true

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2025/03/30/lc.png)

![Image](https://assets.leetcode.com/uploads/2025/03/30/lc.jpeg)

A horizontal cut between row 0 and row 1 results in two non-empty sections, each with a sum of 5. Thus, the answer is `true`.

**Example 2:**

**Input:** grid = [[1,3],[2,4]]

**Output:** false

**Explanation:**

No horizontal or vertical cut results in two non-empty sections with equal sums. Thus, the answer is `false`.

**Constraints:**

- `1 <= m == grid.length <= 105`
- `1 <= n == grid[i].length <= 105`
- `2 <= m * n <= 105`
- `1 <= grid[i][j] <= 105`
```java
class Solution {
    public boolean canPartitionGrid(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        long total = 0;
        
        for (int[] row : grid)
            for (int x : row)
                total += x;
        
        if ((total & 1) == 1) return false;
        
        long target = total / 2, sum = 0;
        
        for (int i = 0; i < m - 1; i++) {
            for (int j = 0; j < n; j++)
                sum += grid[i][j];
            if (sum == target) return true;
        }
        
        sum = 0;
        
        for (int j = 0; j < n - 1; j++) {
            for (int i = 0; i < m; i++)
                sum += grid[i][j];
            if (sum == target) return true;
        }
        
        return false;
    }
}
```

