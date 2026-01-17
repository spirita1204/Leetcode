# 3047. Find the Largest Area of Square Inside Two Rectangles  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>There exist `n` rectangles in a 2D plane with edges parallel to the x and y axis. You are given two 2D integer arrays `bottomLeft` and `topRight` where `bottomLeft[i] = [a_i, b_i]` and `topRight[i] = [c_i, d_i]` represent the **bottom-left** and **top-right** coordinates of the `ith` rectangle, respectively.

You need to find the **maximum** area of a **square** that can fit inside the intersecting region of at least two rectangles. Return `0` if such a square does not exist.  

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2024/01/05/example12.png)

**Input:** bottomLeft = [[1,1],[2,2],[3,1]], topRight = [[3,3],[4,4],[6,6]]

**Output:** 1

**Explanation:**

A square with side length 1 can fit inside either the intersecting region of rectangles 0 and 1 or the intersecting region of rectangles 1 and 2. Hence the maximum area is 1. It can be shown that a square with a greater side length can not fit inside any intersecting region of two rectangles.

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2024/07/15/diag.png)

**Input:** bottomLeft = [[1,1],[1,3],[1,5]], topRight = [[5,5],[5,7],[5,9]]

**Output:** 4

**Explanation:**

A square with side length 2 can fit inside either the intersecting region of rectangles 0 and 1 or the intersecting region of rectangles 1 and 2. Hence the maximum area is `2 * 2 = 4`. It can be shown that a square with a greater side length can not fit inside any intersecting region of two rectangles.

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2024/01/04/rectanglesexample2.png)

**Input:** bottomLeft = [[1,1],[2,2],[1,2]], topRight = [[3,3],[4,4],[3,4]]

**Output:** 1

**Explanation:**

A square with side length 1 can fit inside the intersecting region of any two rectangles. Also, no larger square can, so the maximum area is 1. Note that the region can be formed by the intersection of more than 2 rectangles.

**Example 4:**

![Image](https://assets.leetcode.com/uploads/2024/01/04/rectanglesexample3.png)

**Input: **bottomLeft = [[1,1],[3,3],[3,1]], topRight = [[2,2],[4,4],[4,2]]

**Output:** 0

**Explanation:**

No pair of rectangles intersect, hence, the answer is 0.

**Constraints:**

- `n == bottomLeft.length == topRight.length`
- `2 <= n <= 103`
- `bottomLeft[i].length == topRight[i].length == 2`
- `1 <= bottomLeft[i][0], bottomLeft[i][1] <= 107`
- `1 <= topRight[i][0], topRight[i][1] <= 107`
- `bottomLeft[i][0] < topRight[i][0]`
- `bottomLeft[i][1] < topRight[i][1]`
```java
class Solution {
    public long largestSquareArea(int[][] bottomLeft, int[][] topRight) {
        int s = 0;
        int n = bottomLeft.length;

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int minX = Math.max(bottomLeft[i][0], bottomLeft[j][0]);
                int maxX = Math.min(topRight[i][0], topRight[j][0]);
                int minY = Math.max(bottomLeft[i][1], bottomLeft[j][1]);
                int maxY = Math.min(topRight[i][1], topRight[j][1]);
                
                if (minX < maxX && minY < maxY) {
                    int len = Math.min(maxX - minX, maxY - minY);
                    s = Math.max(s, len);
                }
            }   
        }

        return (long) s * s;
    }
}

```

