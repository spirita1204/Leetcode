# 2033. Minimum Operations to Make a Uni-Value Grid  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>You are given a 2D integer `grid` of size `m x n` and an integer `x`. In one operation, you can **add** `x` to or **subtract** `x` from any element in the `grid`.

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
        int n = grid.length, m = grid[0].length;
        int N = n * m;
        int[] freq = new int[10001];
        int min = grid[0][0], max = min;

        for (int[] row : grid) {
            for (int val : row) {
                // 判斷 可不可行 mod
                if ((val - grid[0][0]) % x != 0)
                    return -1;
                freq[val]++;
                min = Math.min(min, val);
                max = Math.max(max, val);
            }
        }

        int target = (N + 1) / 2;
        int acc = 0, median = min;
        // 找最佳中位數
        for (int i = min; i <= max; i += x) {
            acc += freq[i];
            if (acc >= target) {
                median = i;
                break;
            }
        }

        int ops = 0;
        for (int i = min; i <= max; i += x)
            ops += Math.abs(i - median) / x * freq[i];

        return ops;
    }
}
```

