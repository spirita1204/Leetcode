# 861. Score After Flipping Matrix

Methods: Greedy
Difficulty: Medium

Medium

Topics

Companies

You are given an `m x n` binary matrix `grid`.

A **move** consists of choosing any row or column and toggling each value in that row or column (i.e., changing all `0`'s to `1`'s, and all `1`'s to `0`'s).

Every row of the matrix is interpreted as a binary number, and the **score** of the matrix is the sum of these numbers.

Return *the highest possible **score** after making any number of **moves** (including zero moves)*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/07/23/lc-toogle1.jpg](https://assets.leetcode.com/uploads/2021/07/23/lc-toogle1.jpg)

```
Input: grid = [[0,0,1,1],[1,0,1,0],[1,1,0,0]]
Output: 39
Explanation: 0b1111 + 0b1001 + 0b1111 = 15 + 9 + 15 = 39

```

**Example 2:**

```
Input: grid = [[0]]
Output: 1

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 20`
- `grid[i][j]` is either `0` or `1`.

```java
class Solution {
    public int matrixScore(int[][] grid) {
        // 盡量讓 高位多點1 最高為一定是1
        int row = grid.length;
        int col = grid[0].length;
        int res = (1 << (col - 1))* row;// 第一列都是1

        for(int j = 1; j< col; j++) {// 一列一列看
            int cnt = 0;
            for(int i = 0; i < row; i++) {
                cnt += (grid[i][j] == grid[i][0])? 1: 0;// 因為最高為要是1 判斷是否相同 當有反轉->必然為1 統計1個數
            }
            res += Math.max(cnt, row - cnt) * (1 << (col - 1 - j));// 
        }
        return res;
    }
}
```