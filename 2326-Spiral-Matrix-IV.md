# 2326. Spiral Matrix IV

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given two integers `m` and `n`, which represent the dimensions of a matrix.

You are also given the `head` of a linked list of integers.

Generate an `m x n` matrix that contains the integers in the linked list presented in **spiral** order **(clockwise)**, starting from the **top-left** of the matrix. If there are remaining empty spaces, fill them with `-1`.

Return *the generated matrix*.

**Example 1:**

![https://assets.leetcode.com/uploads/2022/05/09/ex1new.jpg](https://assets.leetcode.com/uploads/2022/05/09/ex1new.jpg)

```
Input: m = 3, n = 5, head = [3,0,2,6,8,1,7,9,4,2,5,5,0]
Output: [[3,0,2,6,8],[5,0,-1,-1,1],[5,2,4,9,7]]
Explanation: The diagram above shows how the values are printed in the matrix.
Note that the remaining spaces in the matrix are filled with -1.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2022/05/11/ex2.jpg](https://assets.leetcode.com/uploads/2022/05/11/ex2.jpg)

```
Input: m = 1, n = 4, head = [0,1,2]
Output: [[0,1,2,-1]]
Explanation: The diagram above shows how the values are printed from left to right in the matrix.
The last space in the matrix is set to -1.
```

**Constraints:**

- `1 <= m, n <= 105`
- `1 <= m * n <= 105`
- The number of nodes in the list is in the range `[1, m * n]`.
- `0 <= Node.val <= 1000`

```java
import java.util.Arrays;

class Solution {
    public int[][] spiralMatrix(int m, int n, ListNode head) {
        int[] dirs = new int[] {0, 1, 0, -1, 0}; // 右 下 左 上
        int[][] res = new int[m][n];
        
        // 初始化矩阵，空位填充 -1
        for (int i = 0; i < m; i++) {
            Arrays.fill(res[i], -1);
        }
        int x = 0, y = 0;
        int minM = 0, minN = 0, maxM = m - 1, maxN = n - 1;
        int dir = 0; // 初始方向为右
        
        while (head != null) {
            // 填充当前点
            res[x][y] = head.val;
            head = head.next;
            // 根据当前方向移动
            int newX = x + dirs[dir];
            int newY = y + dirs[dir + 1];
            // 检查是否越过边界
            if (newX < minM || newX > maxM || newY < minN || newY > maxN || res[newX][newY] != -1) {
                // 如果越界或遇到已填充的格子，改变方向
                dir = (dir + 1) % 4;
                newX = x + dirs[dir];
                newY = y + dirs[dir + 1];
            }
            // 更新坐标
            x = newX;
            y = newY;
        }
        return res;
    }
}

```