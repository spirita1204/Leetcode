# 1653. Minimum Deletions to Make String Balanced

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a string `s` consisting only of characters `'a'` and `'b'`​​​​.

You can delete any number of characters in `s` to make `s` **balanced**. `s` is **balanced** if there is no pair of indices `(i,j)` such that `i < j` and `s[i] = 'b'` and `s[j]= 'a'`.

Return *the **minimum** number of deletions needed to make* `s` ***balanced***.

**Example 1:**

```
Input: s = "aababbab"
Output: 2
Explanation: You can either:
Delete the characters at 0-indexed positions 2 and 6 ("aababbab" -> "aaabbb"), or
Delete the characters at 0-indexed positions 3 and 6 ("aababbab" -> "aabbbb").

```

**Example 2:**

```
Input: s = "bbaaaaabb"
Output: 2
Explanation: The only solution is to delete the first two characters.

```

**Constraints:**

- `1 <= s.length <= 105`
- `s[i]` is `'a'` or `'b'`​​.

```java
class Solution {
    public int minimumDeletions(String s) {
        //dp stores number of chars to remove to make s.substring(0, i) valid
        int len = s.length();
        int[] dp = new int[len + 1];
        int bCnts = 0;// b個數
        for(int i = 0; i < len; i++) {
            char c = s.charAt(i);
            if(c == 'a') {
                // 1. 將當前刪除dp[i] + 1
                // 2. 將b移除
                dp[i + 1] = Math.min(dp[i] + 1, bCnts);
            } else {// b
                dp[i + 1] = dp[i];
                bCnts++;
            }
        }
        return dp[len];
    }
}
```