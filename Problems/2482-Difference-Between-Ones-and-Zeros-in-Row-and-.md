# 2482. Difference Between Ones and Zeros in Row and Column

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a **0-indexed** `m x n` binary matrix `grid`.

A **0-indexed** `m x n` difference matrix `diff` is created with the following procedure:

- Let the number of ones in the `ith` row be `onesRowi`.
- Let the number of ones in the `jth` column be `onesColj`.
- Let the number of zeros in the `ith` row be `zerosRowi`.
- Let the number of zeros in the `jth` column be `zerosColj`.
- `diff[i][j] = onesRowi + onesColj - zerosRowi - zerosColj`

Return *the difference matrix* `diff`.

**Example 1:**

![https://assets.leetcode.com/uploads/2022/11/06/image-20221106171729-5.png](https://assets.leetcode.com/uploads/2022/11/06/image-20221106171729-5.png)

```
Input: grid = [[0,1,1],[1,0,1],[0,0,1]]
Output: [[0,0,4],[0,0,4],[-2,-2,2]]
Explanation:
- diff[0][0] =onesRow0 + onesCol0 - zerosRow0 - zerosCol0 = 2 + 1 - 1 - 2 = 0
- diff[0][1] =onesRow0 + onesCol1 - zerosRow0 - zerosCol1 = 2 + 1 - 1 - 2 = 0
- diff[0][2] =onesRow0 + onesCol2 - zerosRow0 - zerosCol2 = 2 + 3 - 1 - 0 = 4
- diff[1][0] =onesRow1 + onesCol0 - zerosRow1 - zerosCol0 = 2 + 1 - 1 - 2 = 0
- diff[1][1] =onesRow1 + onesCol1 - zerosRow1 - zerosCol1 = 2 + 1 - 1 - 2 = 0
- diff[1][2] =onesRow1 + onesCol2 - zerosRow1 - zerosCol2 = 2 + 3 - 1 - 0 = 4
- diff[2][0] =onesRow2 + onesCol0 - zerosRow2 - zerosCol0 = 1 + 1 - 2 - 2 = -2
- diff[2][1] =onesRow2 + onesCol1 - zerosRow2 - zerosCol1 = 1 + 1 - 2 - 2 = -2
- diff[2][2] =onesRow2 + onesCol2 - zerosRow2 - zerosCol2 = 1 + 3 - 2 - 0 = 2

```

**Example 2:**

![https://assets.leetcode.com/uploads/2022/11/06/image-20221106171747-6.png](https://assets.leetcode.com/uploads/2022/11/06/image-20221106171747-6.png)

```
Input: grid = [[1,1,1],[1,1,1]]
Output: [[5,5,5],[5,5,5]]
Explanation:
- diff[0][0] = onesRow0 + onesCol0 - zerosRow0 - zerosCol0 = 3 + 2 - 0 - 0 = 5
- diff[0][1] = onesRow0 + onesCol1 - zerosRow0 - zerosCol1 = 3 + 2 - 0 - 0 = 5
- diff[0][2] = onesRow0 + onesCol2 - zerosRow0 - zerosCol2 = 3 + 2 - 0 - 0 = 5
- diff[1][0] = onesRow1 + onesCol0 - zerosRow1 - zerosCol0 = 3 + 2 - 0 - 0 = 5
- diff[1][1] = onesRow1 + onesCol1 - zerosRow1 - zerosCol1 = 3 + 2 - 0 - 0 = 5
- diff[1][2] = onesRow1 + onesCol2 - zerosRow1 - zerosCol2 = 3 + 2 - 0 - 0 = 5

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 105`
- `1 <= m * n <= 105`
- `grid[i][j]` is either `0` or `1`.

```java
class Solution {
    public int[][] onesMinusZeros(int[][] grid) {
        int row = grid[0].length;
        int col = grid.length;
        int[] countOf1Row = new int[row];// 用來存每行有幾個1
        int[] countOf1Col = new int[col];// 用來存每列有幾個1

        for(int i = 0; i< col; i++) {// 每列
            for(int j = 0; j< row; j++) {// 每行
                if(grid[i][j] == 1) {
                    countOf1Row[j]++;
                    countOf1Col[i]++;
                }
            }
        }
        for(int i = 0; i< col; i++) {// 每列
            for(int j = 0; j< row; j++) {// 每行
                // countOf1Row[j] + countOf1Col[i] - (row - countOf1Row[j]) - (col - countOf1Col[i]);
                grid[i][j] = 2* (countOf1Row[j] + countOf1Col[i]) - (row + col);
            }
        }
        return grid;
    }
}
```