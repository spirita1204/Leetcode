# 1380. Lucky Numbers in a Matrix

Methods: Basic logic
Difficulty: Easy

Given an `m x n` matrix of **distinct** numbers, return *all **lucky numbers** in the matrix in **any** order*.

A **lucky number** is an element of the matrix such that it is the minimum element in its row and maximum in its column.

**Example 1:**

```
Input: matrix = [[3,7,8],[9,11,13],[15,16,17]]
Output: [15]
Explanation: 15 is the only lucky number since it is the minimum in its row and the maximum in its column.

```

**Example 2:**

```
Input: matrix = [[1,10,4,2],[9,3,8,7],[15,16,17,12]]
Output: [12]
Explanation: 12 is the only lucky number since it is the minimum in its row and the maximum in its column.

```

**Example 3:**

```
Input: matrix = [[7,8],[1,2]]
Output: [7]
Explanation: 7 is the only lucky number since it is the minimum in its row and the maximum in its column.

```

**Constraints:**

- `m == mat.length`
- `n == mat[i].length`
- `1 <= n, m <= 50`
- `1 <= matrix[i][j] <= 105`.
- All elements in the matrix are distinct.

```java
class Solution {
    public List<Integer> luckyNumbers (int[][] matrix) {  
        // [3, 7, 19] m3  M15 M16 M19 [1, 10,4 ,2 ]  m1  M15 M16 M17 12  
        // [9, 11,13] m9              [9, 3, 8, 7 ]  m3
        // [15,16,17] m15             [15,16,17,12]  m12
        List<Integer> res = new ArrayList<>();
        Set<Integer> min = new HashSet<>();
        int row = matrix.length;
        int col = matrix[0].length;
        // 每行 找出最小
        for(int i = 0; i < row; i++) {
            int minE = matrix[i][0];
            for(int j = 0; j < col; j++) {
                minE = Math.min(minE, matrix[i][j]);
            }
            min.add(minE);
        }
        // 每列 找出最大
        for(int j = 0; j < col; j++) {
            int maxE = matrix[0][j];
            for(int i = 0; i < row; i++) {
                maxE = Math.max(maxE, matrix[i][j]);
            }
            if(min.contains(maxE)) res.add(maxE);
        }
        return res;
    }
}
```