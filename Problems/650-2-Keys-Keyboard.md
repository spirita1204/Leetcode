# 650. 2 Keys Keyboard

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Hint

There is only one character `'A'` on the screen of a notepad. You can perform one of two operations on this notepad for each step:

- Copy All: You can copy all the characters present on the screen (a partial copy is not allowed).
- Paste: You can paste the characters which are copied last time.

Given an integer `n`, return *the minimum number of operations to get the character* `'A'` *exactly* `n` *times on the screen*.

**Example 1:**

```
Input: n = 3
Output: 3
Explanation: Initially, we have one character 'A'.
In step 1, we use Copy All operation.
In step 2, we use Paste operation to get 'AA'.
In step 3, we use Paste operation to get 'AAA'.

```

**Example 2:**

```
Input: n = 1
Output: 0

```

**Constraints:**

- `1 <= n <= 1000`

```java
class Solution {
    public int minSteps(int n) {
        // A AA AAAAAA
        // 定義DP[n]: copy+paste到第n位
        // dp[i] = 雙數: dp[i/2]+2 | dp[i/(i/2)]*(i/2),
        // 單數: dp[i] = i(質數) | 3*5(兩奇相乘) dp[i]=dp[i/3]*3...
        if(n == 1) return 0;
        int[] dp = new int[n + 1];
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            dp[i] = i;
            // 找因數
            for (int j = i - 1; j > 1; j--) {
                if (i % j == 0) {// j 從最大往下找
                    dp[i] = Math.min(dp[i / j] + j, dp[i / (i / j)] + (i / j));
                    break;
                }
            }
        }
        return dp[n];
    }
}
```