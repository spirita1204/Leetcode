# 3567. Minimum Absolute Difference in Sliding Submatrix  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>You are given an `m x n` integer matrix `grid` and an integer `k`.

For every contiguous `k x k` **submatrix** of `grid`, compute the **minimum absolute** difference between any two **distinct** values within that **submatrix**.

Return a 2D array `ans` of size `(m - k + 1) x (n - k + 1)`, where `ans[i][j]` is the minimum absolute difference in the submatrix whose top-left corner is `(i, j)` in `grid`.

**Note**: If all elements in the submatrix have the same value, the answer will be 0.

A submatrix (x1, y1, x2, y2) is a matrix that is formed by choosing all cells matrix[x][y]

where x1 <= x <= x2 and y1 <= y <= y2.

**Example 1:**

**Input:** grid = [[1,8],[3,-2]], k = 2

**Output:** [[2]]

**Explanation:**

- There is only one possible `k x k` submatrix: `[[1, 8], [3, -2]]`.
- Distinct values in the submatrix are `[1, 8, 3, -2]`.
- The minimum absolute difference in the submatrix is `|1 - 3| = 2`. Thus, the answer is `[[2]]`.
**Example 2:**

**Input:** grid = [[3,-1]], k = 1

**Output:** [[0,0]]

**Explanation:**

- Both `k x k` submatrix has only one distinct element.
- Thus, the answer is `[[0, 0]]`.
**Example 3:**

**Input:** grid = [[1,-2,3],[2,3,5]], k = 2

**Output:** [[1,2]]

**Explanation:**

- There are two possible `k × k` submatrix:
- Thus, the answer is `[[1, 2]]`.
**Constraints:**

- `1 <= m == grid.length <= 30`
- `1 <= n == grid[i].length <= 30`
- `105 <= grid[i][j] <= 105`
- `1 <= k <= min(m, n)`
```java
class Solution {
    public int[][] minAbsDiff(int[][] grid, int k) {
        int m = grid.length, n = grid[0].length;
        int[][] res = new int[m - k + 1][n - k + 1];

        for (int i = 0; i + k <= m; i++) {
            for (int j = 0; j + k <= n; j++) {
                Set<Integer> hs = new TreeSet<>();

                for (int o = i; o < i + k; o++) {
                    for (int l = j; l < j + k; l++) {
                        hs.add(grid[o][l]);
                    }
                }
                int minDiff = findMinDifference(hs);
                res[i][j] = minDiff;
            }
        }
        // 1 -2  3
        // 2  5  5
        return res;
    }

    public int findMinDifference(Set<Integer> set) {
        if (set == null || set.size() < 2) {
            return 0;
        }
        int minDiff = Integer.MAX_VALUE;
        
        List<Integer> sortedList = new ArrayList<>(set);
        Collections.sort(sortedList);

        for (int i = 1; i < sortedList.size(); i++) {
            int diff = sortedList.get(i) - sortedList.get(i - 1);
            minDiff = Math.min(minDiff, Math.abs(diff));
        }

        return minDiff;
    }
}
```

