# 3197. Find the Minimum Area to Cover All Ones II  

  Data Structure: Hash Table </br> Difficulty: Hard </br> </br>You are given a 2D **binary** array `grid`. You need to find 3 **non-overlapping** rectangles having **non-zero** areas with horizontal and vertical sides such that all the 1's in `grid` lie inside these rectangles.

Return the **minimum** possible sum of the area of these rectangles.

**Note** that the rectangles are allowed to touch.

---

**Example 1:**

**Input:** grid = [[1,0,1],[1,1,1]]

**Output:** 5

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2024/05/14/example0rect21.png)

- The 1's at `(0, 0)` and `(1, 0)` are covered by a rectangle of area 2.
- The 1's at `(0, 2)` and `(1, 2)` are covered by a rectangle of area 2.
- The 1 at `(1, 1)` is covered by a rectangle of area 1.
---

**Example 2:**

**Input:** grid = [[1,0,1,0],[0,1,0,1]]

**Output:** 5

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2024/05/14/example1rect2.png)

- The 1's at `(0, 0)` and `(0, 2)` are covered by a rectangle of area 3.
- The 1 at `(1, 1)` is covered by a rectangle of area 1.
- The 1 at `(1, 3)` is covered by a rectangle of area 1.
---

**Constraints:**

- `1 <= grid.length, grid[i].length <= 30`
- `grid[i][j]` is either 0 or 1.
- The input is generated such that there are at least three 1's in `grid`.
---

```java
class Solution {
    public int minimumSum(int[][] grid) {
        HashMap<String, Integer> map = new HashMap<>();

        int m = grid.length;
        int n = grid[0].length;

        int ans = getNext(0, 0, m - 1, n - 1, 3, grid, map);

        return ans;
    }
    // 取得 包含所有1的最小矩陣
    private int getOne(int i1, int j1, int i2, int j2, int[][] grid, HashMap<String, Integer> map) {
        int minx = Integer.MAX_VALUE;
        int maxx = Integer.MIN_VALUE;
        int miny = Integer.MAX_VALUE;
        int maxy = Integer.MIN_VALUE;

        for (int i = i1; i <= i2; i++) {
            for (int j = j1; j <= j2; j++) {
                if (grid[i][j] == 1) {
                    minx = Math.min(minx, i);
                    maxx = Math.max(maxx, i);
                    miny = Math.min(miny, j);
                    maxy = Math.max(maxy, j);
                }
            }
        }
        if (minx == Integer.MAX_VALUE) 
            return 0;
        return (maxx - minx + 1) * (maxy - miny + 1);
    }

    private int getNext(int i1, int j1, int i2, int j2, int k, int[][] grid, HashMap<String, Integer> map) {
        String key = i1 + "," + j1 + "," + i2 + "," + j2 + "," + k;
        if (map.containsKey(key)) {
            return map.get(key);
        }

        int output = Integer.MAX_VALUE;

        if (k == 1) {
            output = getOne(i1, j1, i2, j2, grid, map);
        } else if (k == 2) {
            // 如果剩下 2 個矩形可用，它會嘗試用一條水平或垂直的切割線將當前子網格分成兩個子區域
            for (int i = i1; i < i2; i++) {
                output = Math.min(output, getNext(i1, j1, i, j2, 1, grid, map) + getNext(i + 1, j1, i2, j2, 1, grid, map));
            }
            for (int j = j1; j < j2; j++) {
                output = Math.min(output, getNext(i1, j1, i2, j, 1, grid, map) + getNext(i1, j + 1, i2, j2, 1, grid, map));
            }
        } else if (k == 3) {
            // 如果剩下 3 個矩形可用，它使用切割線的方式，但會將一個區域分給一個矩形，而將另一塊區域分給兩個矩形
            for (int i = i1; i < i2; i++) {
                output = Math.min(output, getNext(i1, j1, i, j2, 1, grid, map) + getNext(i + 1, j1, i2, j2, 2, grid, map));
                output = Math.min(output, getNext(i1, j1, i, j2, 2, grid, map) + getNext(i + 1, j1, i2, j2, 1, grid, map));
            }
            for (int j = j1; j < j2; j++) {
                output = Math.min(output, getNext(i1, j1, i2, j, 1, grid, map) + getNext(i1, j + 1, i2, j2, 2, grid, map));
                output = Math.min(output, getNext(i1, j1, i2, j, 2, grid, map) + getNext(i1, j + 1, i2, j2, 1, grid, map));
            }
        }

        map.put(key, output);
        return output;
    }
}
```

