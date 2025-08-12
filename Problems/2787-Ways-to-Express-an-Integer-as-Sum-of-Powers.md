# 2787. Ways to Express an Integer as Sum of Powers  

  Methods: DP </br> Difficulty: Medium </br> </br>Given two **positive** integers `n` and `x`.   

Return *the number of ways *`n`* can be expressed as the sum of the *`xth`* power of ****unique**** positive integers, in other words, the number of sets of unique integers *`[n1, n2, ..., nk]`* where *`n = n1x + n2x + ... + nkx`*.*

Since the result can be very large, return it modulo `109 + 7`.

For example, if `n = 160` and `x = 3`, one way to express `n` is `n = 23 + 33 + 53`.

**Example 1:**

```plain text
Input: n = 10, x = 2
Output: 1
Explanation: We can express n as the following: n = 32 + 12 = 10.
It can be shown that it is the only way to express 10 as the sum of the 2nd power of unique integers
```

**Example 2:**

```plain text
Input: n = 4, x = 1
Output: 2
Explanation: We can express n in the following ways:
- n = 41 = 4.
- n = 31 + 11 = 4.
```

**Constraints:**

- `1 <= n <= 300`
- `1 <= x <= 5`
```java
class Solution {
    public int numberOfWays(int n, int x) {
        // i: + + + + j^x
        // dp[i] += dp[i - j^x] 
        // 要小心重複'
        // dp[5] = dp[4] + 1^x    1+1+2 + 1
        // dp[5] = dp[3] + 2^x    1+1+1 + 2 // 最後拆出x不能超過j
        // dp[i][j] += dp[i][j - 1]  不用j
        // dp[i][j] += dp[i - j^x][j - 1] 用j
        int mod = 1000000007;
        int[][] dp = new int[305][305];
        dp[0][0] = 1;

        for(int i = 0; i <= n; i++) {
            for(int j = 1; j <= n; j++) {
                dp[i][j] += dp[i][j - 1];
                long num = 1;
                for(int k = 0; k < x; k++) // j^x
                    num *= j;
                if(num <= i) {
                    dp[i][j] += dp[i - (int)num][j - 1];
                    dp[i][j] %= mod;
                }
            }
        }
        return dp[n][n];
    }
}
```

