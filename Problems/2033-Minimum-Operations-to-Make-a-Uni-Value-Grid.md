# 2033. Minimum Operations to Make a Uni-Value Grid  

  Methods: Sort,Math </br> Difficulty: Medium </br> </br>You are given a 2D integer `grid` of size `m x n` and an integer `x`. In one operation, you can **add** `x` to or **subtract** `x` from any element in the `grid`.

A **uni-value grid** is a grid where all the elements of it are equal. 

Return *the ****minimum**** number of operations to make the grid ****uni-value***. If it is not possible, return `-1`.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/09/21/gridtxt.png)

```plain text
Input: grid = [[2,4],[6,8]], x = 2
Output: 4
Explanation: We can make every element equal to 4 by doing the following:
- Add x to 2 once.
- Subtract x from 6 once.
- Subtract x from 8 twice.
A total of 4 operations were used.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/09/21/gridtxt-1.png)

```plain text
Input: grid = [[1,5],[2,3]], x = 1
Output: 5
Explanation: We can make every element equal to 3.
```

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2021/09/21/gridtxt-2.png)

```plain text
Input: grid = [[1,2],[3,4]], x = 2
Output: -1
Explanation: It is impossible to make every element equal.
```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 105`
- `1 <= m * n <= 105`
- `1 <= x, grid[i][j] <= 104`
```java
class Solution {
    public int minOperations(int[][] grid, int x) {
        // sort[2,4,6,8]
        int m = grid.length;
        int n = grid[0].length;
        // trans 2d -> 1d
        int idx = 0;
        int[] mn = new int[m * n];
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                mn[idx++] = grid[i][j];
            }
        }
        // sort
        Arrays.sort(mn);
        int mid = mn[n * m / 2];

        // 1 2 1000, 1 2 998 1000 = 1+996+998
        int res = 0;
        for(int i = 0; i < m * n; i++) {
            if(Math.abs(mn[i] - mid) % x != 0)  
                return -1;
            res += Math.abs(mid - mn[i]) / x;
        }
        return res;
    }
}
```

