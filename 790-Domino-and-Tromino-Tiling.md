# 790. Domino and Tromino Tiling

Methods: DP
Difficulty: Medium

![Untitled](Untitled%2010.png)

Medium

Topics

Companies

You have two types of tiles: a `2 x 1` domino shape and a tromino shape. You may rotate these shapes.

![https://assets.leetcode.com/uploads/2021/07/15/lc-domino.jpg](https://assets.leetcode.com/uploads/2021/07/15/lc-domino.jpg)

Given an integer n, return *the number of ways to tile an* `2 x n` *board*. Since the answer may be very large, return it **modulo** `109 + 7`.

In a tiling, every square must be covered by a tile. Two tilings are different if and only if there are two 4-directionally adjacent cells on the board such that exactly one of the tilings has both squares occupied by a tile.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/07/15/lc-domino1.jpg](https://assets.leetcode.com/uploads/2021/07/15/lc-domino1.jpg)

```
Input: n = 3
Output: 5
Explanation: The five different ways are show above.

```

**Example 2:**

```
Input: n = 1
Output: 1

```

**Constraints:**

- `1 <= n <= 1000`

```java
class Solution {
    public int numTilings(int n) {
        int mod = 1000000007;
        long[][] dp = new long[n + 1][2];
        dp[0][0] = 1;
        dp[1][0] = 1;

        for (int i = 2; i <= n; i++) {
            dp[i][0] = (dp[i - 1][0] + dp[i - 2][0] + 2 * dp[i - 1][1] % mod) % mod;
            dp[i][1] = (dp[i - 2][0] + dp[i - 1][1]) % mod;
        }
        return (int)dp[n][0];
    }
}
```