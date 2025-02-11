# 59. Spiral Matrix II

Methods: Basic logic
Difficulty: Medium

**Medium**

4.7K

206

Companies

Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n2` in spiral order.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]

```

**Example 2:**

```
Input: n = 1
Output: [[1]]

```

**Constraints:**

- `1 <= n <= 20`

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res = new int[n][n];
        int num = 1;
        int x = 0, y = 0;
        int size = n * n;
        while(num <= size){
            while(y < n && res[x][y] == 0) res[x][y++] = num++;//向右
            y--;//避免越界
            x++;//跳到下一格 不重複走(轉角)
            while(x < n && res[x][y] == 0) res[x++][y] = num++;//向下
            x--;
            y--;
            while(y >= 0 && res[x][y] == 0) res[x][y--] = num++;//向左
            y++;
            x--;
            while(x >= 0 && res[x][y] == 0) res[x--][y] = num++;//向上
            x++;
            y++;
        }
        return res;
    }
}
```