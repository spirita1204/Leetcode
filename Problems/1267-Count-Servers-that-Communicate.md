# 1267. Count Servers that Communicate

Methods: Basic logic
Difficulty: Medium

You are given a map of a server center, represented as a `m * n` integer matrix `grid`, where 1 means that on that cell there is a server and 0 means that it is no server. Two servers are said to communicate if they are on the same row or on the same column.

Return the number of servers that communicate with any other server.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/11/14/untitled-diagram-6.jpg](https://assets.leetcode.com/uploads/2019/11/14/untitled-diagram-6.jpg)

```
Input: grid = [[1,0],[0,1]]
Output: 0
Explanation: No servers can communicate with others.
```

**Example 2:**

![https://assets.leetcode.com/uploads/2019/11/13/untitled-diagram-4.jpg](https://assets.leetcode.com/uploads/2019/11/13/untitled-diagram-4.jpg)

```
Input: grid = [[1,0],[1,1]]
Output: 3
Explanation: All three servers can communicate with at least one other server.

```

**Example 3:**

![https://assets.leetcode.com/uploads/2019/11/14/untitled-diagram-1-3.jpg](https://assets.leetcode.com/uploads/2019/11/14/untitled-diagram-1-3.jpg)

```
Input: grid = [[1,1,0,0],[0,0,1,0],[0,0,1,0],[0,0,0,1]]
Output: 4
Explanation: The two servers in the first row can communicate with each other. The two servers in the third column can communicate with each other. The server at right bottom corner can't communicate with any other server.

```

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m <= 250`
- `1 <= n <= 250`
- `grid[i][j] == 0 or 1`

```java
class Solution {
    public int countServers(int[][] grid) {
        int[] Rows = new int[grid.length];
        int[] Col = new int[grid[0].length];
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                Rows[i] += grid[i][j];
                Col[j] += grid[i][j];
            }
        }
        int ans = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 1 && (Rows[i] > 1 || Col[j] > 1)) {
                    ans++;
                }
            }
        }
        return ans;
    }
}
```