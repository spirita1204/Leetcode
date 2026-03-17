# 1727. Largest Submatrix With Rearrangements  

  Methods: Sort </br> Difficulty: Medium </br> </br>You are given a binary matrix `matrix` of size `m x n`, and you are allowed to rearrange the **columns** of the `matrix` in any order.

Return *the area of the largest submatrix within *`matrix`* where ****every**** element of the submatrix is *`1`* after reordering the columns optimally.*

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2020/12/29/screenshot-2020-12-30-at-40536-pm.png)

```plain text
Input: matrix = [[0,0,1],[1,1,1],[1,0,1]]
Output: 4
Explanation: You can rearrange the columns as shown above.
The largest submatrix of 1s, in bold, has an area of 4.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2020/12/29/screenshot-2020-12-30-at-40852-pm.png)

```plain text
Input: matrix = [[1,0,1,0,1]]
Output: 3
Explanation: You can rearrange the columns as shown above.
The largest submatrix of 1s, in bold, has an area of 3.
```

**Example 3:**

```plain text
Input: matrix = [[1,1,0],[1,0,1]]
Output: 2
Explanation: Notice that you must rearrange entire columns, and there is no way to make a submatrix of 1s larger than an area of 2.
```

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m * n <= 105`
- `matrix[i][j]` is either `0` or `1`.
```java
class Solution {
    public int largestSubmatrix(int[][] matrix) {
        int row = matrix.length;
        int col = matrix[0].length;  

        // Step 1: 累積高度（像 histogram）
        for (int i = 1; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (matrix[i][j] == 1) {
                    matrix[i][j] += matrix[i - 1][j];
                }
            }
        }
        int res = 0;
        // Step 2: 每一列當作 base 計算最大面積
        for (int i = 0; i < row; i++) {
            Arrays.sort(matrix[i]);  // 排序（模擬欄位重排）

            for (int j = 0; j < col; j++) {
                int height = matrix[i][j];
                int width = col - j;
                res = Math.max(res, height * width);
            }
        }
        // 0 0 1    0 0 1
        // 1 1 2 -> 1 1 2
        // 2 0 3    0 2 3 

        return res;        
    }
}
```

