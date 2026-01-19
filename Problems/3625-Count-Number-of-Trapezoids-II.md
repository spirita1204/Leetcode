# 3625. Count Number of Trapezoids II  

  Methods: Math </br> Difficulty: Hard </br> </br>You are given a 2D integer array `points` where `points[i] = [xi, yi]` represents the coordinates of the `ith` point on the Cartesian plane.

Return *the number of unique trapezoids* that can be formed by choosing any four distinct points from `points`.

A** trapezoid** is a convex quadrilateral with **at least one pair** of parallel sides. Two lines are parallel if and only if they have the same slope.

**Example 1:**

**Input:** points = [[-3,2],[3,0],[2,3],[3,2],[2,-3]]

**Output:** 2

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2025/04/29/desmos-graph-4.png)

![Image](https://assets.leetcode.com/uploads/2025/04/29/desmos-graph-3.png)

There are two distinct ways to pick four points that form a trapezoid:

- The points `[-3,2], [2,3], [3,2], [2,-3]` form one trapezoid.
- The points `[2,3], [3,2], [3,0], [2,-3]` form another trapezoid.
**Example 2:**

**Input:** points = [[0,0],[1,0],[0,1],[2,1]]

**Output:** 1

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2025/04/29/desmos-graph-5.png)

There is only one trapezoid which can be formed.

**Constraints:   **

- `4 <= points.length <= 500`  
- `–1000 <= xi, yi <= 1000`  
- All points are pairwise distinct.
```java
class Solution {
    public int countTrapezoids(int[][] points) {
        HashMap<Integer, HashMap<Integer, Integer>> t = new HashMap<>();// 同斜率的平行線段（候選梯形）
        HashMap<Integer, HashMap<Integer, Integer>> v = new HashMap<>();// 完全一樣的向量（平行四邊形修正）

        int n = points.length;
        // 枚舉所有「點對 → 線段」
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {

                int dx = points[j][0] - points[i][0];
                int dy = points[j][1] - points[i][1];
                // 保證 (dx, dy) 方向唯一, 避免 (A→B) 和 (B→A) 被當成不同線段
                if (dx < 0 || (dx == 0 && dy < 0)) {
                    dx = -dx;
                    dy = -dy;
                }
                // 斜率
                int g = gcd(dx, Math.abs(dy));
                int sx = dx / g;
                int sy = dy / g;
                // 用「截距」區分不同平行線
                // 同斜率 + 同 des = 同一條線
                // 同斜率 + 不同 des = 不同的平行線
                int des = sx * points[i][1] - sy * points[i][0];
                // sx * y - sy * x = C
                // 對同一條直線上的任何點 (x, y)，右邊的 C 都一樣
                int key1 = (sx << 12) | (sy + 2000);// [sx][sy] 分「平行」
                // 方向,長度,向量完全一樣
                int key2 = (dx << 12) | (dy + 2000);// [dx][dy] 完全一樣的邊(平行四邊形的對邊)

                t.computeIfAbsent(key1, k -> new HashMap<>()).merge(des, 1, (a, b) -> (a + b));
                v.computeIfAbsent(key2, k -> new HashMap<>()).merge(des, 1, (a, b) -> (a + b));
            }
        }
        // 所有「有至少一對平行線段的四點組合」− 所有「兩對邊都平行（平行四邊形）」的組合
        return count(t) - count(v) / 2;
    }

    // Map<方向 key, Map<des, 次數>>
    // 某個方向（斜率 or 向量）
    //  ├─ des = 5   → 有 3 條線段
    //  ├─ des = 10  → 有 2 條線段
    //  └─ des = 20  → 有 4 條線段
    // 同 des → 在同一條直線上->不能形成梯形的一對平行邊
    // 不同 des → 不同平行線->可以當一組平行邊
    private int count(HashMap<Integer, HashMap<Integer, Integer>> map) {
        long ans = 0;

        for (HashMap<Integer, Integer> inner : map.values()) {
            long sum = 0;

            for (int val : inner.values()) sum += val;

            for (int val : inner.values()) {
                sum -= val;
                ans += (long) val * sum;
            }
        }

        return (int) ans;
    }

    private int gcd(int a, int b) {
        while (b != 0) {
            int t = a % b;
            a = b;
            b = t;
        }
        return Math.abs(a);
    }
}
```

