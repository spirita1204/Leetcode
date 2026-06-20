# 1914. Cyclically Rotating a Grid  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>You are given an `m x n` integer matrix `grid`, where `m` and `n` are both **even** integers, and an integer `k`.

The matrix is composed of several layers, which is shown in the below image, where each color is its own layer:

![Image](https://assets.leetcode.com/uploads/2021/06/10/ringofgrid.png)

A cyclic rotation of the matrix is done by cyclically rotating **each layer** in the matrix. To cyclically rotate a layer once, each element in the layer will take the place of the adjacent element in the **counter-clockwise** direction. An example rotation is shown below:

![Image](https://assets.leetcode.com/uploads/2021/06/22/explanation_grid.jpg)

Return *the matrix after applying *`k` *cyclic rotations to it*.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/06/19/rod2.png)

```plain text
Input: grid = [[40,10],[30,20]], k = 1
Output: [[10,20],[40,30]]
Explanation: The figures above represent the grid at every state.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/06/10/ringofgrid5.png)

![Image](https://assets.leetcode.com/uploads/2021/06/10/ringofgrid6.png)

![Image](https://assets.leetcode.com/uploads/2021/06/10/ringofgrid7.png)

```plain text
Input: grid = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]], k = 2   
Output: [[3,4,8,12],[2,11,10,16],[1,7,6,15],[5,9,13,14]]
Explanation: The figures above represent the grid at every state.
```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `2 <= m, n <= 50`
- Both `m` and `n` are **even** integers.   
- `1 <= grid[i][j] <= 5000`
- `1 <= k <= 109`
```java
class Solution {   
    public int[][] rotateGrid(int[][] grid, int k) {
        int T = 0, L = 0;
        int col = grid.length - 1, row = grid[0].length - 1;
        // 從內到外
        while (T < col && L < row) {
            int len = col - T, wid = row - L;
            int perimeter = 2 * len + 2 * wid;
            int r = k % perimeter;

            while (r-- > 0) {// 走r步
                int tmp = grid[T][L];

                for (int i = L; i < row; i++)
                    grid[T][i] = grid[T][i + 1];

                for (int i = T; i < col; i++)
                    grid[i][row] = grid[i + 1][row];

                for (int i = row; i > L; i--)
                    grid[col][i] = grid[col][i - 1];

                for (int i = col; i > T; i--)
                    grid[i][L] = grid[i - 1][L];

                grid[T + 1][L] = tmp;
            }

            T++; L++;
            col--; row--;
        }

        return grid;
    }
}
```



