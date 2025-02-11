# 1292. Maximum Side Length of a Square with Sum Less than or Equal to Threshold

Methods: Prefix Sum
Difficulty: Medium

Medium

Topics

Companies

Hint

Given a `m x n` matrix `mat` and an integer `threshold`, return *the maximum side-length of a square with a sum less than or equal to* `threshold` *or return* `0` *if there is no such square*.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/12/05/e1.png](https://assets.leetcode.com/uploads/2019/12/05/e1.png)

```
Input: mat = [[1,1,3,2,4,3,2],[1,1,3,2,4,3,2],[1,1,3,2,4,3,2]], threshold = 4
Output: 2
Explanation: The maximum side length of square with sum less than 4 is 2 as shown.

```

**Example 2:**

```
Input: mat = [[2,2,2,2,2],[2,2,2,2,2],[2,2,2,2,2],[2,2,2,2,2],[2,2,2,2,2]], threshold = 1
Output: 0

```

**Constraints:**

- `m == mat.length`
- `n == mat[i].length`
- `1 <= m, n <= 300`
- `0 <= mat[i][j] <= 104`
- `0 <= threshold <= 105`

```java
class Solution {
    int[][] prefix;
    public int maxSideLength(int[][] mat, int threshold) {
        int row = mat.length;
        int col = mat[0].length;

        for (int i = 0; i < row; i++) {
            for (int j = 1; j < col; j++) {
                mat[i][j] += mat[i][j - 1];
            }
        }
        for (int i = 1; i < row; i++) {
            for (int j = 0; j < col; j++) {
                mat[i][j] += mat[i - 1][j];
            }
        }
        prefix = mat;

        int max = 0;
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                for(int k = 0; i + k < row && j + k < col; k++) {
                    int sum = sumRegion(i, j, i + k, j + k);
                    if(sum <= threshold) {
                        max = Math.max(max, k + 1);
                    } else
                        continue;
                }
            }
        }
        return max;
    }

    public int sumRegion(int row1, int col1, int row2, int col2) {
        if (row1 == 0) {
            if (col1 == 0) {
                return prefix[row2][col2];
            } else {
                return prefix[row2][col2] - prefix[row2][col1 - 1];
            }
        } else if (col1 == 0) {
            return prefix[row2][col2] - prefix[row1 - 1][col2];
        }
        return prefix[row2][col2] - prefix[row1 - 1][col2] - prefix[row2][col1 - 1] + prefix[row1 - 1][col1 - 1];
    }
}
```

```java
class Solution {
    int[][] prefix;

    public int maxSideLength(int[][] mat, int threshold) {
        int row = mat.length;
        int col = mat[0].length;
        prefix = new int[row + 1][col + 1];   
        
        for (int i = 0; i < row; ++i)
            for (int j = 0; j < col; ++j)
                prefix[i + 1][j + 1] = mat[i][j] + prefix[i][j + 1] + prefix[i + 1][j] - prefix[i][j];

        int max = 0;
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                for (int k = 0; i + k < row && j + k < col; k++) {
                    int sum = sumRegion(i, j, i + k, j + k);
                    if (sum <= threshold) {
                        max = Math.max(max, k + 1);
                    } else
                        continue;
                }
            }
        }
        return max;
    }

    public int sumRegion(int row1, int col1, int row2, int col2) {
        return prefix[row2 + 1][col2 + 1] 
            - prefix[row1][col2 + 1] - prefix[row2 + 1][col1] 
            + prefix[row1][col1];
    }
}
```