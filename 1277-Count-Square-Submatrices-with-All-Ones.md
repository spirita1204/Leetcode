# 1277. Count Square Submatrices with All Ones

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Hint

Given a `m * n` matrix of ones and zeros, return how many **square** submatrices have all ones.

**Example 1:**

```
Input: matrix =
[
  [0,1,1,1],
  [1,1,1,1],
  [0,1,1,1]
]
Output: 15
Explanation:
There are10 squares of side 1.
There are4 squares of side 2.
There is1 square of side 3.
Total number of squares = 10 + 4 + 1 =15.

```

**Example 2:**

```
Input: matrix =
[
  [1,0,1],
  [1,1,0],
  [1,1,0]
]
Output: 7
Explanation:
There are6 squares of side 1.
There is1 square of side 2.
Total number of squares = 6 + 1 =7.

```

**Constraints:**

- `1 <= arr.length <= 300`
- `1 <= arr[0].length <= 300`
- `0 <= arr[i][j] <= 1`

```java
class Solution {
    public int countSquares(int[][] matrix) {
        int row = matrix.length;
        int col = matrix[0].length;
        int[][] dp = new int[row][col];
        int res = 0;

        for(int i = 0; i < col; i++) {
            if(matrix[0][i] == 1) {
                res++;
                dp[0][i] = 1;
            }
        }
        for(int i = 1; i < row; i++) {
            if(matrix[i][0] == 1) {
                res++;
                dp[i][0] = 1;
            }
        }
        for(int i = 1; i < row; i++) {
            for(int j = 1; j < col; j++) {
                if(matrix[i][j] == 1) 
                    dp[i][j] = 1 + Math.min(Math.min(dp[i][j-1], dp[i-1][j]), dp[i-1][j-1]);
                res += dp[i][j];
            }
        }
        return res;
    }                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            
}
```