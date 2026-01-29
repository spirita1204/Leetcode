# 3363. Find the Maximum Number of Fruits Collected  

  Methods: DFS </br> Difficulty: Hard </br> </br>There is a game dungeon comprised of `n x n` rooms arranged in a grid.

You are given a 2D array `fruits` of size `n x n`, where `fruits[i][j]` represents the number of fruits in the room `(i, j)`. Three children will play in the game dungeon, with **initial** positions at the corner rooms `(0, 0)`, `(0, n - 1)`, and `(n - 1, 0)`.

The children will make **exactly** `n - 1` moves according to the following rules to reach the room `(n - 1, n - 1)`:

- The child starting from `(0, 0)` must move from their current room `(i, j)` to one of the rooms `(i + 1, j + 1)`, `(i + 1, j)`, and `(i, j + 1)` if the target room exists.
- The child starting from `(0, n - 1)` must move from their current room `(i, j)` to one of the rooms `(i + 1, j - 1)`, `(i + 1, j)`, and `(i + 1, j + 1)` if the target room exists.
- The child starting from `(n - 1, 0)` must move from their current room `(i, j)` to one of the rooms `(i - 1, j + 1)`, `(i, j + 1)`, and `(i + 1, j + 1)` if the target room exists.
When a child enters a room, they will collect all the fruits there. If two or more children enter the same room, only one child will collect the fruits, and the room will be emptied after they leave.

Return the **maximum** number of fruits the children can collect from the dungeon.

**Example 1:**

**Input:** fruits = [[1,2,3,4],[5,6,8,7],[9,10,11,12],[13,14,15,16]]

**Output:** 100

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2025/08/07/clideo_editor_d0b446db9ba448e1a3fcdd0eecdb58d0-ezgifcom-crop.gif)

In this example:

- The 1 child (green) moves on the path `(0,0) -> (1,1) -> (2,2) -> (3, 3)`.
- The 2 child (red) moves on the path `(0,3) -> (1,2) -> (2,3) -> (3, 3)`.
- The 3 child (blue) moves on the path `(3,0) -> (3,1) -> (3,2) -> (3, 3)`.
In total they collect `1 + 6 + 11 + 16 + 4 + 8 + 12 + 13 + 14 + 15 = 100` fruits.

**Example 2:**

**Input:** fruits = [[1,1],[1,1]]

**Output:** 4

**Explanation:**

In this example:

- The 1 child moves on the path `(0,0) -> (1,1)`.
- The 2 child moves on the path `(0,1) -> (1,1)`.
- The 3 child moves on the path `(1,0) -> (1,1)`.
In total they collect `1 + 1 + 1 + 1 = 4` fruits.

**Constraints:**

- `2 <= n == fruits.length == fruits[i].length <= 1000`
- `0 <= fruits[i][j] <= 1000`
```java
class Solution {
    int n;
    int[][] memo;

    // row = i, col = j
    int dfs3(int row, int col, int[][] fruits) {
        if (row < 0 || col < 0 || row >= n || col >= n) return 0;

        if (memo[row][col] != -1) return memo[row][col];

        int val = fruits[row][col];
        int res = 0;

        if (row == col) {
            res = Math.max(res, dfs3(row + 1, col + 1, fruits));
        } else if (row - 1 == col) {
            res = Math.max(res, Math.max(
                dfs3(row + 1, col + 1, fruits),
                dfs3(row, col + 1, fruits)
            ));
        } else {
            res = Math.max(res, Math.max(
                dfs3(row + 1, col + 1, fruits),
                Math.max(dfs3(row, col + 1, fruits),
                         dfs3(row - 1, col + 1, fruits))
            ));
        }

        return memo[row][col] = val + res;
    }

    int dfs2(int row, int col, int[][] fruits) {
        // 邊界
        if (row < 0 || col < 0 || row >= n || col >= n) return 0;
        // 記憶化
        if (memo[row][col] != -1) return memo[row][col];

        int val = fruits[row][col];
        int res = 0;
        // 用對角線當分隔
        if (row == col) {// 只能往回不然走不回去
            res = Math.max(res, dfs2(row + 1, col + 1, fruits));
        } else if (row == col - 1) {// 可往下 往右下
            res = Math.max(res, Math.max(
                dfs2(row + 1, col + 1, fruits),
                dfs2(row + 1, col, fruits)
            ));
        } else {// 可以往三個方向
            res = Math.max(res, Math.max(
                dfs2(row + 1, col + 1, fruits),
                Math.max(dfs2(row + 1, col, fruits),
                         dfs2(row + 1, col - 1, fruits))
            ));
        }

        return memo[row][col] = val + res;
    }

    public int maxCollectedFruits(int[][] fruits) {
        n = fruits.length;
        int total = 0;

        memo = new int[n][n];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        // child - 1
        // 只能走斜對角
        for (int i = 0; i < n; i++) {
            total += fruits[i][i];
            fruits[i][i] = 0;
        }
        // child - 2
        total += dfs3(n - 1, 0, fruits);
        // child - 3
        total += dfs2(0, n - 1, fruits);

        return total;
    }
}
```

