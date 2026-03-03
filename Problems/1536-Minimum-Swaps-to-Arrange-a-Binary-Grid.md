# 1536. Minimum Swaps to Arrange a Binary Grid  

  Methods: Greedy </br> Difficulty: Medium </br> </br>Given an `n x n` binary `grid`, in one step you can choose two **adjacent rows** of the grid and swap them.

A grid is said to be **valid** if all the cells above the main diagonal are **zeros**.

Return *the minimum number of steps* needed to make the grid valid, or **-1** if the grid cannot be valid.

The main diagonal of a grid is the diagonal that starts at cell `(1, 1)` and ends at cell `(n, n)`.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2020/07/28/fw.jpg)

```plain text
Input: grid = [[0,0,1],[1,1,0],[1,0,0]]
Output: 3
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2020/07/16/e2.jpg)

```plain text
Input: grid = [[0,1,1,0],[0,1,1,0],[0,1,1,0],[0,1,1,0]]
Output: -1
Explanation: All rows are similar, swaps have no effect on the grid.
```

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2020/07/16/e3.jpg)

```plain text
Input: grid = [[1,0,0],[1,1,0],[1,1,1]]
Output: 0    
```

**Constraints:**

- `n == grid.length` `== grid[i].length`
- `1 <= n <= 200`  
- `grid[i][j]` is either `0` or `1`   
```java
class Solution {   
    public int minSwaps(int[][] grid) {
        int n = grid.length;
        int[] zeros = new int[n];
        // 只看「每一列尾巴有幾個 0」
        for (int i = 0; i < n; i++) {
            int count = 0;
            for (int j = n - 1; j >= 0 && grid[i][j] == 0; j--) {
                count++;
            }
            zeros[i] = count;
        }

        int swaps = 0;
        // greedy
        for (int i = 0; i < n; i++) {
            int needed = n - i - 1;// 第 i 列需要
            // 往下找「符合條件的 row」
            int j = i;  
            while (j < n && zeros[j] < needed) j++;

            if (j == n) return -1;
            // 交換(只能 swap 相鄰 所以就是 bubble sort 往上推)
            while (j > i) {
                int temp = zeros[j];
                zeros[j] = zeros[j - 1];
                zeros[j - 1] = temp;
                j--;
                swaps++;
            }
        }

        return swaps;
    }
}
```

