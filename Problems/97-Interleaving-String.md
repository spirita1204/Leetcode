# 97. Interleaving String

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Given strings `s1`, `s2`, and `s3`, find whether `s3` is formed by an **interleaving** of `s1` and `s2`.

An **interleaving** of two strings `s` and `t` is a configuration where `s` and `t` are divided into `n` and `m`

substrings

respectively, such that:

- `s = s1 + s2 + ... + sn`
- `t = t1 + t2 + ... + tm`
- `|n - m| <= 1`
- The **interleaving** is `s1 + t1 + s2 + t2 + s3 + t3 + ...` or `t1 + s1 + t2 + s2 + t3 + s3 + ...`

**Note:** `a + b` is the concatenation of strings `a` and `b`.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/09/02/interleave.jpg](https://assets.leetcode.com/uploads/2020/09/02/interleave.jpg)

```
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true
Explanation: One way to obtain s3 is:
Split s1 into s1 = "aa" + "bc" + "c", and s2 into s2 = "dbbc" + "a".
Interleaving the two splits, we get "aa" + "dbbc" + "bc" + "a" + "c" = "aadbbcbcac".
Since s3 can be obtained by interleaving s1 and s2, we return true.

```

**Example 2:**

```
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
Output: false
Explanation: Notice how it is impossible to interleave s2 with any other string to obtain s3.

```

**Example 3:**

```
Input: s1 = "", s2 = "", s3 = ""
Output: true

```

**Constraints:**

- `0 <= s1.length, s2.length <= 100`
- `0 <= s3.length <= 200`
- `s1`, `s2`, and `s3` consist of lowercase English letters.

**Follow up:** Could you solve it using only `O(s2.length)` additional memory space?

```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        int len1 = s1.length();
        int len2 = s2.length();
        int len3 = s3.length();

        if(len1 + len2 != len3) return false;// 長度不同直接拋
        if(len1 == 0 && len2 == 0 && len3 == 0) return true;

        boolean[][] dp = new boolean[len1 + 1][len2 + 1];
        dp[0][0] = true;
        // 初始化第一列第一行
        for(int i = 1; i <= len2; i++) {
            if(s2.charAt(i - 1) == s3.charAt(i - 1) && dp[0][i - 1]) // 前面需成立不然會s2本身交錯
                dp[0][i] = true;
        }
        for(int i = 1; i <= len1; i++) {
            if(s1.charAt(i - 1) == s3.charAt(i - 1) && dp[i - 1][0]) // 前面需成立不然會s1本身交錯
                dp[i][0] = true;
        }
        // 兩種情況為true
        for(int i = 1; i <= len1; i++) {
            for(int j = 1; j <= len2; j++) {
                // s1當前選擇 == s3當前 且 s1 前一字串組合s3為true
                if(s1.charAt(i - 1) == s3.charAt(i + j - 1) && dp[i - 1][j]) dp[i][j] = true;
                // s2當前選擇 == s3當前 且 s2 前一字串組合s3為true
                if(s2.charAt(j - 1) == s3.charAt(i + j - 1) && dp[i][j - 1]) dp[i][j] = true;
            }
        }
        return dp[len1][len2];
    }
}
```