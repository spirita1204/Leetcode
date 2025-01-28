# 840. Magic Squares In Grid

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

A `3 x 3` **magic square** is a `3 x 3` grid filled with distinct numbers **from** 1 **to** 9 such that each row, column, and both diagonals all have the same sum.

Given a `row x col` `grid` of integers, how many `3 x 3` contiguous magic square subgrids are there?

Note: while a magic square can only contain numbers from 1 to 9, `grid` may contain numbers up to 15.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/09/11/magic_main.jpg](https://assets.leetcode.com/uploads/2020/09/11/magic_main.jpg)

```
Input: grid = [[4,3,8,4],[9,5,1,9],[2,7,6,2]]
Output: 1
Explanation:
The following subgrid is a 3 x 3 magic square:

while this one is not:

In total, there is only one magic square inside the given grid.

```

![https://assets.leetcode.com/uploads/2020/09/11/magic_valid.jpg](https://assets.leetcode.com/uploads/2020/09/11/magic_valid.jpg)

![https://assets.leetcode.com/uploads/2020/09/11/magic_invalid.jpg](https://assets.leetcode.com/uploads/2020/09/11/magic_invalid.jpg)

**Example 2:**

```
Input: grid = [[8]]
Output: 0

```

**Constraints:**

- `row == grid.length`
- `col == grid[i].length`
- `1 <= row, col <= 10`
- `0 <= grid[i][j] <= 15`

```java
class Solution {
    public int numMagicSquaresInside(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;
        int res = 0;
        for (int i = 0; i <= row -3; i++) {
            for (int j = 0; j <= col - 3; j++) {
                if (grid[i][j] % 2 == 0)
                    if (isMegic(grid, i, j))
                        res++;
            }
        }
        return res;
    }

    private boolean isMegic(int[][] grid, int x, int y) {
        int sum[] = new int[3];
        int sumcol[] = new int[3];
        boolean[] arr = new boolean[10];// 紀錄是否重複
        // 一個3*3一個個看
        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++) {
                // row sum
                sum[i] += grid[x + i][y + j];
                // column sum
                sumcol[j] += grid[x + i][y + j];
                // Must have valus between 1 to 9 and must be unique
                if (grid[x + i][y + j] > 9 || grid[x + i][y + j] == 0 || arr[grid[x + i][y + j]] == true)
                    return false;
                arr[grid[x + i][y + j]] = true;
            }
        // Row sum must be equal to Column sum
        for (int i = 1; i < 3; i++)
            if (sum[i] != sum[i - 1] || sum[i] != sumcol[i] || sumcol[i] != sumcol[i - 1])
                return false;
        // 斜對角
        int dig = grid[x][y] + grid[x + 1][y + 1] + grid[x + 2][y + 2];
        int reverseDig = grid[x][y + 2] + grid[x + 1][y + 1] + grid[x + 2][y];
        // Diagonals sum must be equal and equal to any of the row or sum
        if (dig != reverseDig || dig != sum[0])
            return false;
        return true;
    }
}
```