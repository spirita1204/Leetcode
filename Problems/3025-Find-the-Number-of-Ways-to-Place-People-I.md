# 3025. Find the Number of Ways to Place People I  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>You are given a 2D array `points` of size `n x 2` representing integer coordinates of some points on a 2D plane, where `points[i] = [xi, yi]`.   

Count the number of pairs of points `(A, B)`, where

- `A` is on the **upper left** side of `B`, and
- there are no other points in the rectangle (or line) they make (**including the border**).
Return the count.

---

**Example 1:**

**Input:** points = [[1,1],[2,2],[3,3]]

**Output:** 0

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2024/01/04/example1alicebob.png)

There is no way to choose `A` and `B` so `A` is on the upper left side of `B`.

---

**Example 2:**

**Input:** points = [[6,2],[4,4],[2,6]]

**Output:** 2

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2024/06/25/t2.jpg)

- The left one is the pair `(points[1], points[0])`, where `points[1]` is on the upper left side of `points[0]` and the rectangle is empty.
- The middle one is the pair `(points[2], points[1])`, same as the left one it is a valid pair.
- The right one is the pair `(points[2], points[0])`, where `points[2]` is on the upper left side of `points[0]`, but `points[1]` is inside the rectangle so it's not a valid pair.
---

**Example 3:**

**Input:** points = [[3,1],[1,3],[1,1]]

**Output:** 2

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2024/06/25/t3.jpg)

- The left one is the pair `(points[2], points[0])`, where `points[2]` is on the upper left side of `points[0]` and there are no other points on the line they form. Note that it is a valid state when the two points form a line.
- The middle one is the pair `(points[1], points[2])`, it is a valid pair same as the left one.
- The right one is the pair `(points[1], points[0])`, it is not a valid pair as `points[2]` is on the border of the rectangle.
---

**Constraints:**

- `2 <= n <= 50`
- `points[i].length == 2`
- `0 <= points[i][0], points[i][1] <= 50`
- All `points[i]` are distinct.
---

```java
class Solution {
    public int numberOfPairs(int[][] points) {
        int count = 0;
        int n = points.length;

        for (int i = 0; i < n; i++) {
            int x1 = points[i][0], y1 = points[i][1];
            for (int j = 0; j < n; j++) {
                if (i == j)// 同樣自己
                    continue;
                int x2 = points[j][0], y2 = points[j][1];
                if (x1 > x2 || y1 < y2)// 不在upper left
                    continue;

                boolean flag = true;
                for (int k = 0; k < n; k++) {// 找範圍內無其他
                    if (k == i || k == j)
                        continue;
                    int x = points[k][0], y = points[k][1];

                    if (x >= x1 && x <= x2 && y <= y1 && y >= y2) {
                        flag = false;
                        break;
                    }
                }
                if (flag == true)
                    count++;
            }
        }
        return count;
    }

}
```

