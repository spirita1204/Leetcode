# 48. Rotate Image

Methods: Basic logic
Difficulty: Medium

ou are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).

You have to rotate the image [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg](https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg)

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg](https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg)

```
Input: matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]
Output: [[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]

```

**Constraints:**

- `n == matrix.length == matrix[i].length`
- `1 <= n <= 20`
- `1000 <= matrix[i][j] <= 1000`

![Untitled](Untitled%2012.png)

```java
class Solution {
    public void rotate(int[][] matrix) {
        for(int i = 0; i < matrix.length/2; i++){//第幾層圈
            for(int j = 0; j <= matrix.length - 1 - i*2 - 1; j++){//一行 少1
                int temp = matrix[i][i+j];
                matrix[i][i+j] = matrix[matrix.length - 1 - j - i][i];//上
                matrix[matrix.length - 1 - j - i][i] = matrix[matrix.length - 1 - i][matrix.length - 1 - j - i];//左
                matrix[matrix.length - 1 - i][matrix.length - 1 - j - i] = matrix[i + j][matrix.length - 1 - i];//下
                matrix[i + j][matrix.length - 1 - i] = temp;//右
            }
        }
    }
}
```