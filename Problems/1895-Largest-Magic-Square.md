# 1895. Largest Magic Square  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>A `k x k` **magic square** is a `k x k` grid filled with integers such that every row sum, every column sum, and both diagonal sums are **all equal**. The integers in the magic square **do not have to be distinct**. Every `1 x 1` grid is trivially a **magic square**.

Given an `m x n` integer `grid`, return *the ****size**** (i.e., the side length *`k`*) of the ****largest magic square**** that can be found within this grid*.     

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/05/29/magicsquare-grid.jpg)

```plain text
Input: grid = [[7,1,4,5,6],[2,5,1,6,4],[1,5,4,3,2],[1,2,7,3,4]]
Output: 3
Explanation: The largest magic square has a size of 3.
Every row sum, column sum, and diagonal sum of this magic square is equal to 12.
- Row sums: 5+1+6 = 5+4+3 = 2+7+3 = 12
- Column sums: 5+5+2 = 1+4+7 = 6+3+3 = 12
- Diagonal sums: 5+4+3 = 6+4+2 = 12
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/05/29/magicsquare2-grid.jpg)

```plain text
Input: grid = [[5,1,3,1],[9,3,3,1],[1,3,3,8]]
Output: 2
```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 50`
- `1 <= grid[i][j] <= 106`
```java
class Solution {
    public int largestMagicSquare(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int side = Math.min(m, n);

        while (side > 0) {
            for (int i = 0; i < m; i++) {
                for (int j = 0; j < n; j++) {
                    if (i + side <= m && j + side <= n) {
                        if (isValid(grid, m, n, i, j, side))
                            return side;
                    }
                }
            }
            side--;
        }

        return 0;
    }

    private boolean isValid(int[][] grid, int m, int n, int i, int j, int side) {
        int sum = 0;

        // rows
        for (int x = i; x < i + side; x++) {
            int summ = 0;
            for (int y = j; y < j + side; y++) {
                summ += grid[x][y];
            }
            if (x == i)// first
                sum = summ;
            else if (sum != summ)
                return false;
        }

        // columns
        for (int x = j; x < j + side; x++) {
            int summ = 0;
            for (int y = i; y < i + side; y++) {
                summ += grid[y][x];
            }
            if (sum != summ)
                return false;
        }

        // main diagonal
        int summ = 0;
        for (int k = 0; k < side; k++) {
            summ += grid[i + k][j + k];
        }
        if (sum != summ)
            return false;

        // anti-diagonal
        summ = 0;
        for (int k = 0; k < side; k++) {
            summ += grid[i + k][j + side - 1 - k];
        }
        if (sum != summ)
            return false;

        return true;
    }

}
```

