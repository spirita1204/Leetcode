# 3623. Count Number of Trapezoids I  

  Methods: Combinatorics </br> Difficulty: Medium </br> </br>You are given a 2D integer array `points`, where `points[i] = [xi, yi]` represents the coordinates of the `ith` point on the Cartesian plane.

A **horizontal** **trapezoid** is a convex quadrilateral with **at least one pair** of horizontal sides (i.e. parallel to the x-axis). Two lines are parallel if and only if they have the same slope.

Return the *number of unique ****horizontal***** *****trapezoids*** that can be formed by choosing any four distinct points from `points`.

Since the answer may be very large, return it **modulo** `109 + 7`.

**Example 1:**

**Input:** points = [[1,0],[2,0],[3,0],[2,2],[3,2]]

**Output:** 3

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2025/05/01/desmos-graph-6.png)

![Image](https://assets.leetcode.com/uploads/2025/05/01/desmos-graph-7.png)

![Image](https://assets.leetcode.com/uploads/2025/05/01/desmos-graph-8.png)

There are three distinct ways to pick four points that form a horizontal trapezoid:

- Using points `[1,0]`, `[2,0]`, `[3,2]`, and `[2,2]`.
- Using points `[2,0]`, `[3,0]`, `[3,2]`, and `[2,2]`.
- Using points `[1,0]`, `[3,0]`, `[3,2]`, and `[2,2]`.
**Example 2:**

**Input:** points = [[0,0],[1,0],[0,1],[2,1]]

**Output:** 1

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2025/04/29/desmos-graph-5.png)

There is only one horizontal trapezoid that can be formed.

**Constraints:**

- `4 <= points.length <= 105`
- `–108 <= xi, yi <= 108`
- All points are pairwise distinct.
```java
class Solution {
    public int countTrapezoids(int[][] points) {
        int n = points.length, MOD = 1000000007;
        Arrays.sort(points, Comparator.comparingInt(a -> a[1]));
        long res = 0, total = 0;
        int j = 0;
        for (int i = 0; i < n; i = j){
            j = i + 1;
            while (j < n && points[i][1] == points[j][1]){// y軸相同
                j++;
            }
            long count = j - i;
            long lines = count * (count - 1) / 2;// 幾種組合C(n,2)
            res = (res + total * lines) % MOD;// 用現在這個 y 的線段，搭配之前所有 y 的線段，可以形成幾個梯形
            total = (total + lines) % MOD;
        }
        return (int)res;
    }
}
```



