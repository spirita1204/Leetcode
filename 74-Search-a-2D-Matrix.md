# 74. Search a 2D Matrix

Methods: Binary Search
Difficulty: Medium

You are given an `m x n` integer matrix `matrix` with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` *if* `target` *is in* `matrix` *or* `false` *otherwise*.

You must write a solution in `O(log(m * n))` time complexity.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/10/05/mat.jpg](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false

```

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 100`
- `104 <= matrix[i][j], target <= 104`

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int colRes = colSearch(matrix, target);
        if(colRes < matrix.length && matrix[colRes][0] == target) return true;
        if(colRes < matrix.length && target < matrix[0][0]) return false;//當[[1],[3]] t = 0情況
        int rowRes = rowSearch(matrix, target, colRes-1);
        return (rowRes < matrix[0].length && matrix[colRes-1][rowRes] == target) ? true : false;
    }
    public int rowSearch(int[][] matrix, int target, int colRes){//先找到哪行
        int left = 0;
        int right = matrix[0].length - 1;
        while(left <= right){
            System.out.println(right);
            int mid = (left + right)/2;
            if(matrix[colRes][mid] > target){
                right = mid - 1;
            }else if(matrix[colRes][mid] < target){
                left = mid + 1;
            }else{
                return mid;
            }
        }
        return left;
    }
    public int colSearch(int[][] matrix, int target){//{再套列
        int left = 0;
        int right = matrix.length - 1;
        while(left <= right){
            int mid = (left + right)/2;
            if(matrix[mid][0] > target){
                right = mid - 1;
            }else if(matrix[mid][0] < target){
                left = mid + 1;
            }else{
                return mid;
            }
        }
        return left;        
    }
}
```