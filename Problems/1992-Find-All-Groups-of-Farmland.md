# 1992. Find All Groups of Farmland

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a **0-indexed** `m x n` binary matrix `land` where a `0` represents a hectare of forested land and a `1` represents a hectare of farmland.

To keep the land organized, there are designated rectangular areas of hectares that consist **entirely** of farmland. These rectangular areas are called **groups**. No two groups are adjacent, meaning farmland in one group is **not** four-directionally adjacent to another farmland in a different group.

`land` can be represented by a coordinate system where the top left corner of `land` is `(0, 0)` and the bottom right corner of `land` is `(m-1, n-1)`. Find the coordinates of the top left and bottom right corner of each **group** of farmland. A **group** of farmland with a top left corner at `(r1, c1)` and a bottom right corner at `(r2, c2)` is represented by the 4-length array `[r1, c1, r2, c2].`

Return *a 2D array containing the 4-length arrays described above for each **group** of farmland in* `land`*. If there are no groups of farmland, return an empty array. You may return the answer in **any order***.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/07/27/screenshot-2021-07-27-at-12-23-15-copy-of-diagram-drawio-diagrams-net.png](https://assets.leetcode.com/uploads/2021/07/27/screenshot-2021-07-27-at-12-23-15-copy-of-diagram-drawio-diagrams-net.png)

```
Input: land = [[1,0,0],[0,1,1],[0,1,1]]
Output: [[0,0,0,0],[1,1,2,2]]
Explanation:
The first group has a top left corner at land[0][0] and a bottom right corner at land[0][0].
The second group has a top left corner at land[1][1] and a bottom right corner at land[2][2].

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/07/27/screenshot-2021-07-27-at-12-30-26-copy-of-diagram-drawio-diagrams-net.png](https://assets.leetcode.com/uploads/2021/07/27/screenshot-2021-07-27-at-12-30-26-copy-of-diagram-drawio-diagrams-net.png)

```
Input: land = [[1,1],[1,1]]
Output: [[0,0,1,1]]
Explanation:
The first group has a top left corner at land[0][0] and a bottom right corner at land[1][1].

```

**Example 3:**

![https://assets.leetcode.com/uploads/2021/07/27/screenshot-2021-07-27-at-12-32-24-copy-of-diagram-drawio-diagrams-net.png](https://assets.leetcode.com/uploads/2021/07/27/screenshot-2021-07-27-at-12-32-24-copy-of-diagram-drawio-diagrams-net.png)

```
Input: land = [[0]]
Output: []
Explanation:
There are no groups of farmland.

```

**Constraints:**

- `m == land.length`
- `n == land[i].length`
- `1 <= m, n <= 300`
- `land` consists of only `0`'s and `1`'s.
- Groups of farmland are **rectangular** in shape.

```java
class Solution {
    public int[][] findFarmland(int[][] land) {
        int row = land.length;
        int col = land[0].length;

        List<List<Integer>> res = new ArrayList<>();

        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                int e = land[i][j];
                if (e == 1) {
                    List<Integer> sub = new ArrayList<>();
                    sub.add(i);
                    sub.add(j);
                    dfs(i, j, land, sub);
                    res.add(sub);
                }
            }
        }
        return res.stream()
                .map(l -> l.stream().mapToInt(Integer::intValue).toArray())
                .toArray(int[][]::new);
    }

    private boolean dfs(int i, int j, int[][] land, List<Integer> sub) {
        if (i < 0 || i >= land.length || j < 0 || j >= land[0].length)
            return false;
        if (land[i][j] == 0)
            return false;

        land[i][j] = 0;

        boolean down = dfs(i + 1, j, land, sub);// 下
        boolean right = dfs(i, j + 1, land, sub);// 右

        if (!down && !right && sub.size() == 2) {// 避免[[1,1],[1,1]]情境重複導致[[0,0,1,1,0,1]]
            sub.add(i);
            sub.add(j);
        }
        return true;
    }
}
```