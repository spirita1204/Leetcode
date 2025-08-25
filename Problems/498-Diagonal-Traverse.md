# 498. Diagonal Traverse  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>Given an `m x n` matrix `mat`, return *an array of all the elements of the array in a diagonal order*.

**Example 1:   **

![Image](https://assets.leetcode.com/uploads/2021/04/10/diag1-grid.jpg)

```plain text
Input: mat = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,4,7,5,3,6,8,9]
```

**Example 2:**

```plain text
Input: mat = [[1,2],[3,4]]
Output: [1,2,3,4]
```

**Constraints:**

- `m == mat.length`
- `n == mat[i].length`
- `1 <= m, n <= 104`
- `1 <= m * n <= 104`
- `105 <= mat[i][j] <= 105`
```java
class Solution {
    public int[] findDiagonalOrder(int[][] mat) {
        // 00 01 10 20 11 02 12 21 22
        int r = 0, c = 0;
        int m = mat.length, n = mat[0].length;
        int arr[] = new int[m * n];

        // // //
        // rc c
        // r
        for (int i = 0; i < m * n; i++) {
            arr[i] = mat[r][c];
            if ((r + c) % 2 == 0) { // 上
                if (c == n - 1) // 往左下
                    r++;
                else if (r == 0) // 往右上
                    c++;
                else {// 轉換
                    r--; 
                    c++;
                }
            } else { // 下
                if (r == m - 1) 
                    c++;
                else if (c == 0) 
                    r++;
                else {
                    r++;
                    c--;
                }
            }
        }
        return arr;
    }
}
```

