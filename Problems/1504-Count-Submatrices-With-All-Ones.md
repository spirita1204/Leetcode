# 1504. Count Submatrices With All Ones  

  Methods: DP </br> Difficulty: Medium </br> </br>Given an `m x n` binary matrix `mat`, *return the number of ****submatrices**** that have all ones*.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/10/27/ones1-grid.jpg)

```plain text
Input: mat = [[1,0,1],[1,1,0],[1,1,0]]
Output: 13
Explanation:
There are 6 rectangles of side 1x1.
There are 2 rectangles of side 1x2.
There are 3 rectangles of side 2x1.
There is 1 rectangle of side 2x2.
There is 1 rectangle of side 3x1.  
Total number of rectangles = 6 + 2 + 3 + 1 + 1 = 13.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/10/27/ones2-grid.jpg)

```plain text
Input: mat = [[0,1,1,0],[0,1,1,1],[1,1,1,0]]
Output: 24
Explanation:
There are 8 rectangles of side 1x1.
There are 5 rectangles of side 1x2.
There are 2 rectangles of side 1x3.
There are 4 rectangles of side 2x1.
There are 2 rectangles of side 2x2.
There are 2 rectangles of side 3x1.
There is 1 rectangle of side 3x2.
Total number of rectangles = 8 + 5 + 2 + 4 + 2 + 2 + 1 = 24.
```

**Constraints:**

- `1 <= m, n <= 150`
- `mat[i][j]` is either `0` or `1`.
```java
class Solution {
    public int numSubmat(int[][] mat) {
        int res = 0;
        int row = mat.length;
        int col = mat[0].length;

        for (int i = 1; i < row; i++) {
            for (int j = 0; j < col; j++) {
                mat[i][j] = mat[i][j] == 1 ? mat[i - 1][j] + 1 : 0;
            }
        }
        // 0 1 1 0
        // 0 2 2 1
        // 1 3 3 0
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (mat[i][j] != 0) {
                    int min = mat[i][j];
                    res += min;
                    // 往右邊找可能結果
                    for (int k = j + 1; k < col && mat[i][k] != 0; k++) {
                        min = Math.min(min, mat[i][k]);
                        res += min;
                    }
                }
            }
        }

        return res;
    }
}
```

