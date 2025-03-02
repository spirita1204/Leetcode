# 1289. Minimum Falling Path Sum II  

  Methods: DP </br> Data Structure: Heap </br> Difficulty: Hard </br> </br>Given an `n x n` integer matrix `grid`, return *the minimum sum of a ****falling path with non-zero shifts***.

A **falling path with non-zero shifts** is a choice of exactly one element from each row of `grid` such that no two elements chosen in adjacent rows are in the same column.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/08/10/falling-grid.jpg)

```plain text
Input: grid = [[1,2,3],[4,5,6],[7,8,9]]
Output: 13
Explanation:
The possible falling paths are:
[1,5,9], [1,5,7], [1,6,7], [1,6,8],
[2,4,8], [2,4,9], [2,6,7], [2,6,8],
[3,4,8], [3,4,9], [3,5,7], [3,5,9]
The falling path with the smallest sum is [1,5,7], so the answer is 13.
```

**Example 2:**

```plain text
Input: grid = [[7]]
Output: 7
```

**Constraints:**

- `n == grid.length == grid[i].length`
- `1 <= n <= 200`
- `99 <= grid[i][j] <= 99`
```java
class Solution {
    public int minFallingPathSum(int[][] grid) {
        int r = grid.length;
        int c = grid[0].length;
        // dp[i][j] = min(前 + now Cost);
        int[][] dp = new int[r][c];
        for(int i = 0; i < c; i++)
            dp[0][i] = grid[0][i];

        for(int i = 1; i < r; i++) {
            Queue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]);// val, idx
            for(int j = 0; j < c; j++) // 紀錄上一行最小值
                pq.offer(new int[]{dp[i - 1][j], j});
            for(int j = 0; j < c; j++) {// 找前一層最小
                int min = Integer.MAX_VALUE;
                int[] e = pq.peek();
                if(e[1] == j) {
                    int[] top = pq.poll();
                    min = pq.peek()[0];
                    pq.offer(top);
                } else {
                    min = pq.peek()[0];
                }
                dp[i][j] = grid[i][j] + min;
            }
        }
        int res = Integer.MAX_VALUE;;
        for(int i = 0; i < c; i++)
            res = Math.min(res, dp[r - 1][i]);

        return res;
    }
}
```

