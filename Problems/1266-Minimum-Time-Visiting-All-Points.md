# 1266. Minimum Time Visiting All Points  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>On a 2D plane, there are `n` points with integer coordinates `points[i] = [xi, yi]`. Return *the ****minimum time**** in seconds to visit all the points in the order given by *`points`.

You can move according to these rules:

- In `1` second, you can either:
- You have to visit the points in the same order as they appear in the array.
- You are allowed to pass through points that appear later in the order, but these do not count as visits.
**Example 1:**

![Image](https://assets.leetcode.com/uploads/2019/11/14/1626_example_1.PNG)

```plain text
Input: points = [[1,1],[3,4],[-1,0]]
Output: 7
Explanation:One optimal path is [1,1] -> [2,2] -> [3,3] -> [3,4]-> [2,3] -> [1,2] -> [0,1] -> [-1,0]
Time from [1,1] to [3,4] = 3 seconds
Time from [3,4] to [-1,0] = 4 seconds
Total time = 7 seconds
```

**Example 2:**

```plain text
Input: points = [[3,2],[-2,2]]
Output: 5
```

**Constraints:**

- `points.length == n`
- `1 <= n <= 100`
- `points[i].length == 2`
- `1000 <= points[i][0], points[i][1] <= 1000`
```java
class Solution {
    public int minTimeToVisitAllPoints(int[][] points) {
        int sum = 0;
        for(int i = 1; i < points.length; i++) {
            int x1 = points[i - 1][0];
            int y1 = points[i - 1][1];
            int x2 = points[i][0];
            int y2 = points[i][1];
            sum += sum(x1, x2, y1, y2);
        }
        return sum;
    }

    private int sum(int x1, int x2, int y1, int y2) {
        int diag = Math.min(Math.abs(x1 - x2), Math.abs(y1 - y2));

        return (diag == Math.abs(x1 - x2))? Math.abs(y1 - y2) : Math.abs(x1 -x2);
    }
}
```

