# 1351. Count Negative Numbers in a Sorted Matrix

Methods: Binary Search
Difficulty: Easy

**Easy**

3.2K

91

Companies

Given a `m x n` matrix `grid` which is sorted in non-increasing order both row-wise and column-wise, return *the number of **negative** numbers in* `grid`.

**Example 1:**

```
Input: grid = [[4,3,2,-1],[3,2,1,-1],[1,1,-1,-2],[-1,-1,-2,-3]]
Output: 8
Explanation: There are 8 negatives number in the matrix.

```

**Example 2:**

```
Input: grid = [[3,2],[1,0]]
Output: 0

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 100`
- `100 <= grid[i][j] <= 100`

**Follow up:**

Could you find an

```
O(n + m)
```

solution?

```java
class Solution {
    public int countNegatives(int[][] grid) {
        int res = 0;
        for(int i = 0; i < grid.length; i++) {
            // add up negative numbers of each row
            res += negativeEachRow(grid[i]);
        }
        return res;
    }
    public int negativeEachRow(int[] row) {
        int res = 0;
        int l = 0, r = row.length - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            // if midPoint is positive, go to the right side
            // if midPoint is negative, count the right side(because they are all negative) and go to left side.
            if (row[mid] >= 0) {
                l = mid + 1;
            }else if (row[mid] < 0) {
                res += r - mid + 1;
                r = mid - 1;
            }
        }
        return res;
    }
}
```