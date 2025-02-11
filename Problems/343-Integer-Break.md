# 343. Integer Break

Methods: DP
Difficulty: Medium

**Medium**

3.6K

364

Companies

Given an integer `n`, break it into the sum of `k` **positive integers**, where `k >= 2`, and maximize the product of those integers.

Return *the maximum product you can get*.

**Example 1:**

```
Input: n = 2
Output: 1
Explanation: 2 = 1 + 1, 1 × 1 = 1.

```

**Example 2:**

```
Input: n = 10
Output: 36
Explanation: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36.

```

**Constraints:**

- `2 <= n <= 58`

```java
class Solution {
    public int integerBreak(int n) {
        // 可將n切成兩等分 最大化乘積
        // dp[i] 代表 到第i前可形成最大乘積
        int[] dp = new int[n + 1];
        dp[1] = 1;

        for(int i = 2;i <= n; i++){
            for(int j = 1; j< i; j++){// 便利所有組合 ex: 4 = 1+3, 2+2, 3+1..
                dp[i] = Math.max(dp[i], 
                    //當前最大 = 可拆成左邊dp最大或本身最大 * 右邊dp最大或本身最大
                    Math.max(dp[j], j)* Math.max(dp[i- j], i- j));
            }
        }
        return dp[n];
    }
}
```