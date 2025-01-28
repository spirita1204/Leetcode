# 1572. Matrix Diagonal Sum

Methods: Basic logic
Difficulty: Easy

**Easy**

2.1K

28

Companies

Given a square matrix `mat`, return the sum of the matrix diagonals.

Only include the sum of all the elements on the primary diagonal and all the elements on the secondary diagonal that are not part of the primary diagonal.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/08/14/sample_1911.png](https://assets.leetcode.com/uploads/2020/08/14/sample_1911.png)

```
Input: mat = [[1,2,3],
              [4,5,6],
              [7,8,9]]
Output: 25
Explanation:Diagonals sum: 1 + 5 + 9 + 3 + 7 = 25
Notice that element mat[1][1] = 5 is counted only once.

```

**Example 2:**

```
Input: mat = [[1,1,1,1],
              [1,1,1,1],
              [1,1,1,1],
              [1,1,1,1]]
Output: 8

```

**Example 3:**

```
Input: mat = [[5]]
Output: 5

```

**Constraints:**

- `n == mat.length == mat[i].length`
- `1 <= n <= 100`
- `1 <= mat[i][j] <= 100`

```java
class Solution {
    public int diagonalSum(int[][] mat) {
        /**
        [0, 0]      [0, 2]
              [1, 1]
        [2, 0]      [2, 2]    

        [0, 0]             [0, 3]
              [1, 1] [1, 2]     
              [2, 1] [2, 2]   
        [3, 0]             [3, 3]    
         */
        
        int x = 0, y = 0;
        int row = mat.length, col = mat[0].length;
        int sum = 0;
        int j = 0;

        for(int i = 0; i< row; i++){
            if(j == col - j - 1) sum += mat[i][j];
            else sum = sum + mat[i][j] + mat[i][col - j - 1];
            j++;
        }

        return sum;
    }
}
```