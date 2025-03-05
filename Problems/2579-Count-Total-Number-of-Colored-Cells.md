# 2579. Count Total Number of Colored Cells  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>There exists an infinitely large two-dimensional grid of uncolored unit cells. You are given a positive integer `n`, indicating that you must do the following routine for `n` minutes:

- At the first minute, color **any** arbitrary unit cell blue.
- Every minute thereafter, color blue **every** uncolored cell that touches a blue cell.
Below is a pictorial representation of the state of the grid after minutes 1, 2, and 3.

![Image](https://assets.leetcode.com/uploads/2023/01/10/example-copy-2.png)

Return *the number of ****colored cells**** at the end of *`n` *minutes*.

**Example 1:**

```plain text
Input: n = 1
Output: 1
Explanation: After 1 minute, there is only 1 blue cell, so we return 1.

```

**Example 2:**

```plain text
Input: n = 2
Output: 5
Explanation: After 2 minutes, there are 4 colored cells on the boundary and 1 in the center, so we return 5.

```

**Constraints:**

- `1 <= n <= 105`
```java
class Solution {
    public long coloredCells(int n) {
        // 1. Math 1 1+4 1+4+8 1+4+8+12=25 +16=41

        // 上 下 左 右
        long res = 0;
        while(n-- > 0) 
            res += 4 * n;
        return res + 1;
    }
}
```

