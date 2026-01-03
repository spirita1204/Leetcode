# 1411. Number of Ways to Paint N × 3 Grid  

  Methods: DP </br> Difficulty: Hard </br> </br>You have a `grid` of size `n x 3` and you want to paint each cell of the grid with exactly one of the three colors: **Red**, **Yellow,** or **Green** while making sure that no two adjacent cells have the same color (i.e., no two cells that share vertical or horizontal sides have the same color).

Given `n` the number of rows of the grid, return *the number of ways* you can paint this `grid`. As the answer may grow large, the answer **must be** computed modulo `109 + 7`.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2020/03/26/e1.png)

```plain text
Input: n = 1
Output: 12
Explanation: There are 12 possible way to paint the grid as shown.   
```

**Example 2:**

```plain text
Input: n = 5000
Output: 30228214
```

**Constraints:**

- `n == grid.length`
- `1 <= n <= 5000`
```java
class Solution {
    public int numOfWays(int n) {
        int MOD = (int) (1e9 + 7);
        long color3 = 6;// ABC
        long color2 = 6;// ABA

        for (int i = 2; i <= n; ++i) {
            long tempColor3 = color3;
            color3 = (2 * color3 + 2 * color2) % MOD;// 轉移到 color3
            // ABC → ABC 兩種
            // ABA → ABC 兩種
            //    -> 第 1、3 格不能是 A
            //    -> 第 2 格不能是 B
            color2 = (2 * tempColor3 + 3 * color2) % MOD;// 轉移到 color2
            // ABC → ABA 兩種
            // ABA → ABA 三種 RGR-> GRG,BRB,BGB
        }

        return (int) (color3 + color2) % MOD;
    }
}
```

