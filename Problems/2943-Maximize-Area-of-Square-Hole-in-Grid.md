# 2943. Maximize Area of Square Hole in Grid  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>You are given the two integers, `n` and `m` and two integer arrays, `hBars` and `vBars`. The grid has `n + 2` horizontal and `m + 2` vertical bars, creating 1 x 1 unit cells. The bars are indexed starting from `1`.   

You can **remove** some of the bars in `hBars` from horizontal bars and some of the bars in `vBars` from vertical bars. Note that other bars are fixed and cannot be removed.

Return an integer denoting the **maximum area** of a *square-shaped* hole in the grid, after removing some bars (possibly none).

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2023/11/05/screenshot-from-2023-11-05-22-40-25.png)

**Input: **n = 2, m = 1, hBars = [2,3], vBars = [2]

**Output: **4

**Explanation:**

The left image shows the initial grid formed by the bars. The horizontal bars are `[1,2,3,4]`, and the vertical bars are `[1,2,3]`.

One way to get the maximum square-shaped hole is by removing horizontal bar 2 and vertical bar 2.

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2023/11/04/screenshot-from-2023-11-04-17-01-02.png)

**Input: **n = 1, m = 1, hBars = [2], vBars = [2]

**Output: **4

**Explanation:**

To get the maximum square-shaped hole, we remove horizontal bar 2 and vertical bar 2.

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2024/03/12/unsaved-image-2.png)

**Input: **n = 2, m = 3, hBars = [2,3], vBars = [2,4]

**Output: **4

**Explanation:**

One way to get the maximum square-shaped hole is by removing horizontal bar 3, and vertical bar 4.

**Constraints:**

- `1 <= n <= 109`
- `1 <= m <= 109`
- `1 <= hBars.length <= 100`
- `2 <= hBars[i] <= n + 1`
- `1 <= vBars.length <= 100`
- `2 <= vBars[i] <= m + 1`
- All values in `hBars` are distinct.
- All values in `vBars` are distinct.
```java
class Solution {
    public int maximizeSquareHoleArea(int n, int m, int[] hBars, int[] vBars) {
        // 最大正方形邊長
        // = min(連續可移除的水平 bars 數 + 1,
        //     連續可移除的垂直 bars 數 + 1)
        int maxConsecutiveHBars = 1;
        int maxConsecutiveVBars = 1;

        Arrays.sort(hBars);
        Arrays.sort(vBars);

        int hLength = hBars.length;
        int vLength = vBars.length;

        int tempH = 1;
        int tempV = 1;

        for (int i = 1; i < Math.max(hLength, vLength); i++) {
            if (i < hLength && hBars[i] - hBars[i - 1] == 1) {
                tempH++;
            } else if (i < hLength) {// 有擋住 取大的
                maxConsecutiveHBars = Math.max(maxConsecutiveHBars, tempH);
                tempH = 1;
            }

            if (i < vLength && vBars[i] - vBars[i - 1] == 1) {
                tempV++;
            } else if (i < vLength) {// 有擋住 取大的
                maxConsecutiveVBars = Math.max(maxConsecutiveVBars, tempV);
                tempV = 1;
            }
        }
       
        maxConsecutiveHBars = Math.max(maxConsecutiveHBars, tempH);
        maxConsecutiveVBars = Math.max(maxConsecutiveVBars, tempV);
         System.out.println(maxConsecutiveHBars);
          System.out.println(maxConsecutiveVBars);
        int squareLen = Math.min(maxConsecutiveHBars, maxConsecutiveVBars) + 1;

        return squareLen * squareLen;
    }
}
```

