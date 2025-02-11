# 2373. Largest Local Values in a Matrix

Methods: Basic logic
Difficulty: Easy

Easy

Topics

Companies

Hint

You are given an `n x n` integer matrix `grid`.

Generate an integer matrix `maxLocal` of size `(n - 2) x (n - 2)` such that:

- `maxLocal[i][j]` is equal to the **largest** value of the `3 x 3` matrix in `grid` centered around row `i + 1` and column `j + 1`.

In other words, we want to find the largest value in every contiguous `3 x 3` matrix in `grid`.

Return *the generated matrix*.

**Example 1:**

![https://assets.leetcode.com/uploads/2022/06/21/ex1.png](https://assets.leetcode.com/uploads/2022/06/21/ex1.png)

```
Input: grid = [[9,9,8,1],[5,6,2,6],[8,2,6,4],[6,2,2,2]]
Output: [[9,9],[8,6]]
Explanation: The diagram above shows the original matrix and the generated matrix.
Notice that each value in the generated matrix corresponds to the largest value of a contiguous 3 x 3 matrix in grid.
```

**Example 2:**

![https://assets.leetcode.com/uploads/2022/07/02/ex2new2.png](https://assets.leetcode.com/uploads/2022/07/02/ex2new2.png)

```
Input: grid = [[1,1,1,1,1],[1,1,1,1,1],[1,1,2,1,1],[1,1,1,1,1],[1,1,1,1,1]]
Output: [[2,2,2],[2,2,2],[2,2,2]]
Explanation: Notice that the 2 is contained within every contiguous 3 x 3 matrix in grid.

```

**Constraints:**

- `n == grid.length == grid[i].length`
- `3 <= n <= 100`
- `1 <= grid[i][j] <= 100`

```java
class Solution {
    public int[][] largestLocal(int[][] grid) {
        int len = grid.length;
        int[][] res = new int[len - 2][len - 2];

        for(int i = 0; i + 2 < len; i++) {
            for(int j = 0; j + 2 < len; j++) {
                for(int k = i; k < i + 3; k++) {
                    for(int l = j; l < j + 3; l++) {
                        res[i][j] = Math.max(res[i][j], grid[k][l]);
                    }
                }
            }
        }
        return res;
    }
}
```

Python

```python
class Solution:
    def largestLocal(self, grid: List[List[int]]) -> List[List[int]]:
        size = len(grid)
        # because * is copying the address of the object (list).
        # res = [[0]*(size -2)]* (size - 2)
        res = [[0] * (size - 2) for _ in range(size - 2)]
 
        for i in range(size - 2):
            for j in range(size - 2):
                for k in range(i, i + 3):
                    for l in range(j, j + 3):
                        res[i][j] = max(res[i][j], grid[k][l])
        
        return res

        
```

```python
class Solution:
    def largestLocal(self, grid: List[List[int]]) -> List[List[int]]:
        n = len(grid)
        ans = [[0]*(n-2) for _ in range(n-2)]
        for i in range(n-2): 
            for j in range(n-2): 
                ans[i][j] = max(grid[ii][jj] for ii in range(i, i+3) for jj in range(j, j+3))
        return ans 
```