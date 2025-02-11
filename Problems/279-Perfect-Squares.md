# 279. Perfect Squares

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Given an integer `n`, return *the least number of perfect square numbers that sum to* `n`.

A **perfect square** is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, `1`, `4`, `9`, and `16` are perfect squares while `3` and `11` are not.

**Example 1:**

```
Input: n = 12
Output: 3
Explanation: 12 = 4 + 4 + 4.

```

**Example 2:**

```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.

```

**Constraints:**

- `1 <= n <= 104`

超時!!

### **Time Limit Exceeded502 / 588 testcases passed**

```java
class Solution {
    public int numSquares(int n) {
        int sqrt = (int)Math.sqrt(n);
        int[][] dp = new int[sqrt + 1][n + 1];// 使用前i個perfect square可產生n之最小需數目
        dp[1][1] = 1;
        for(int j = 0; j <= n; j++) dp[0][j] = j;
        for(int i = 1; i <= sqrt; i++) dp[i][1] = 1;

        for(int i = 1; i <= sqrt; i++) {// ex: 1, 2, 3
            for(int j = 2; j <= n; j++) {// ex: 12
                for(int k = 1; k <= j; k++) {
                    if(i * i == j) {// 當是平方
                        dp[i][j] = 1;
                        continue;
                    }
                    if(dp[i][j] == 0) dp[i][j] = Math.min(dp[i - 1][j], dp[i][k] + dp[i][j - k]);
                    else dp[i][j] = Math.min(dp[i][j], Math.min(dp[i - 1][j], dp[i][k] + dp[i][j - k]));
                    //System.out.println("dp[i][j]: "+dp[i][j]+" i: "+i+" j: "+j+" k: "+k);
                }
            }
        }
        return dp[sqrt][n];
    }
}
```

改進

```java
class Solution {
    public int numSquares(int n) {
        // dp[n] indicates that the perfect squares count of the given n
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        for(int i = 1; i <= n; i++) {
            int min = Integer.MAX_VALUE;
            int j = 1;
            while(i - j*j >= 0) {
                min = Math.min(min, dp[i - j*j] + 1);// 最小是當前數字減到每個平方數
                ++j;
            }
            dp[i] = min;
        }		
        return dp[n];
        // dp[0] = 0 
        // dp[1] = dp[0]+1 = 1
        // dp[2] = dp[1]+1 = 2
        // dp[3] = dp[2]+1 = 3
        // dp[4] = Min{ dp[4-1*1]+1, dp[4-2*2]+1 } 
        //     = Min{ dp[3]+1, dp[0]+1 } 
        //     = 1				
        // dp[5] = Min{ dp[5-1*1]+1, dp[5-2*2]+1 } 
        //     = Min{ dp[4]+1, dp[1]+1 } 
        //     = 2
        //                         .
        //                         .
        //                         .
        // dp[13] = Min{ dp[13-1*1]+1, dp[13-2*2]+1, dp[13-3*3]+1 } 
        //     = Min{ dp[12]+1, dp[9]+1, dp[4]+1 } 
        //     = 2
        //                         .
        //                         .
        //                         .
        // dp[n] = Min{ dp[n - i*i] + 1 },  n - i*i >=0 && i >= 1
    }
}
```