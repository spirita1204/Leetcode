# 1886. Determine Whether Matrix Can Be Obtained By Rotation  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given two `n x n` binary matrices `mat` and `target`, return `true`* if it is possible to make *`mat`* equal to *`target`* by ****rotating**** *`mat`* in ****90-degree increments****, or *`false`* otherwise.*

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/05/20/grid3.png)

```plain text
Input: mat = [[0,1],[1,0]], target = [[1,0],[0,1]]
Output: true
Explanation:We can rotate mat 90 degrees clockwise to make mat equal target.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/05/20/grid4.png)

```plain text
Input: mat = [[0,1],[1,1]], target = [[1,0],[0,1]]
Output: false
Explanation: It is impossible to make mat equal to target by rotating mat.
```

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2021/05/26/grid4.png)

```plain text
Input: mat = [[0,0,0],[0,1,0],[1,1,1]], target = [[1,1,1],[0,1,0],[0,0,0]]
Output: true
Explanation:We can rotate mat 90 degrees clockwise two times to make mat equal target.   
```

**Constraints:   **

- `n == mat.length == target.length   `
- `n == mat[i].length == target[i].length`
- `1 <= n <= 10`
- `mat[i][j]` and `target[i][j]` are either `0` or `1`.
```java
class Solution {
    public boolean findRotation(int[][] a, int[][] b) {
        int n = a.length;
        int c90 = 0, c180 = 0, c270 = 0, c0 = 0;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (b[i][j] == a[n - j - 1][i])// 旋轉 90° clockwise
                    c90++;
                if (b[i][j] == a[n - i - 1][n - j - 1])// 旋轉 180°
                    c180++;
                if (b[i][j] == a[j][n - i - 1])// 旋轉 270°
                    c270++;
                if (b[i][j] == a[i][j])// 不旋轉
                    c0++;
            }
        }

        if (c90 == n * n || c270 == n * n || c180 == n * n || c0 == n * n)
            return true;
        else
            return false;
    }
}

```

