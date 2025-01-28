# 474. Ones and Zeroes

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

You are given an array of binary strings `strs` and two integers `m` and `n`.

Return *the size of the largest subset of `strs` such that there are **at most*** `m` **`0`*'s and* `n` **`1`*'s in the subset*.

A set `x` is a **subset** of a set `y` if all elements of `x` are also elements of `y`.

**Example 1:**

```
Input: strs = ["10","0001","111001","1","0"], m = 5, n = 3
Output: 4
Explanation: The largest subset with at most 5 0's and 3 1's is {"10", "0001", "1", "0"}, so the answer is 4.
Other valid but smaller subsets include {"0001", "1"} and {"10", "1", "0"}.
{"111001"} is an invalid subset because it contains 4 1's, greater than the maximum of 3.

```

**Example 2:**

```
Input: strs = ["10","0","1"], m = 1, n = 1
Output: 2
Explanation: The largest subset is {"0", "1"}, so the answer is 2.

```

**Constraints:**

- `1 <= strs.length <= 600`
- `1 <= strs[i].length <= 100`
- `strs[i]` consists only of digits `'0'` and `'1'`.
- `1 <= m, n <= 100`

```java
class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        // dp[i][j] 代表使用i個1和j個0可組合最大之subset
        // dp[i][j] = dp[i - 4][j - 2] + 1 假設要包含"111001"
        int[][] dp = new int[m + 1][n + 1]; // 0, 1 個數

        for(String e: strs) {
            int one = countOfOne(e);
            int zero = e.length() - one;
            
            for(int i = m; i >= zero; i--) {// 避免越界 從one 開始 由上往下避免同一數字重複更新
                for(int j = n; j >= one; j--) {
                    dp[i][j] = Math.max(dp[i][j], dp[i - zero][j - one] + 1);
                }
            }
        }
        return dp[m][n];
    }
    private int countOfOne(String a) {
        int res = 0;
        for(int i = 0; i < a.length(); i++) {
            if(a.charAt(i) == '1') res++;
        }
        return res;
    }
}
```