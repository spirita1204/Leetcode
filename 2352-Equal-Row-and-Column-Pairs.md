# 2352. Equal Row and Column Pairs

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Hint

Given a **0-indexed** `n x n` integer matrix `grid`, *return the number of pairs* `(ri, cj)` *such that row* `ri` *and column* `cj` *are equal*.

A row and column pair is considered equal if they contain the same elements in the same order (i.e., an equal array).

**Example 1:**

![https://assets.leetcode.com/uploads/2022/06/01/ex1.jpg](https://assets.leetcode.com/uploads/2022/06/01/ex1.jpg)

```
Input: grid = [[3,2,1],[1,7,6],[2,7,7]]
Output: 1
Explanation: There is 1 equal row and column pair:
- (Row 2, Column 1): [2,7,7]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2022/06/01/ex2.jpg](https://assets.leetcode.com/uploads/2022/06/01/ex2.jpg)

```
Input: grid = [[3,1,2,2],[1,4,4,5],[2,4,2,2],[2,4,2,2]]
Output: 3
Explanation: There are 3 equal row and column pairs:
- (Row 0, Column 0): [3,1,2,2]
- (Row 2, Column 2): [2,4,2,2]
- (Row 3, Column 2): [2,4,2,2]

```

**Constraints:**

- `n == grid.length == grid[i].length`
- `1 <= n <= 200`
- `1 <= grid[i][j] <= 105`

```java
class Solution {
    public int equalPairs(int[][] grid) {
        Map<String, Integer> hm = new HashMap<>();
        int row = grid[0].length, col = grid.length;
        int res = 0;

        for (int i = 0; i < col; i++) {
            StringBuilder sb = new StringBuilder();
            for (int j = 0; j < row; j++) {
                sb.append(grid[i][j]);
                sb.append(".");
            }
            String s = sb.toString();
            hm.put(s, hm.getOrDefault(s, 0) + 1);
        }
        for (int i = 0; i < row; i++) {
            StringBuilder sb = new StringBuilder();
            for (int j = 0; j < col; j++) {
                sb.append(grid[j][i]);
                sb.append(".");
            }
            String s = sb.toString();
            if (hm.containsKey(s)) {
                res += hm.get(s);
            }
        }
        return res;
    }
}
```