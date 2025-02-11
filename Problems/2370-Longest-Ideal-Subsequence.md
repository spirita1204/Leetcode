# 2370. Longest Ideal Subsequence

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a string `s` consisting of lowercase letters and an integer `k`. We call a string `t` **ideal** if the following conditions are satisfied:

- `t` is a **subsequence** of the string `s`.
- The absolute difference in the alphabet order of every two **adjacent** letters in `t` is less than or equal to `k`.

Return *the length of the **longest** ideal string*.

A **subsequence** is a string that can be derived from another string by deleting some or no characters without changing the order of the remaining characters.

**Note** that the alphabet order is not cyclic. For example, the absolute difference in the alphabet order of `'a'` and `'z'` is `25`, not `1`.

**Example 1:**

```
Input: s = "acfgbd", k = 2
Output: 4
Explanation: The longest ideal string is "acbd". The length of this string is 4, so 4 is returned.
Note that "acfgbd" is not ideal because 'c' and 'f' have a difference of 3 in alphabet order.
```

**Example 2:**

```
Input: s = "abcd", k = 3
Output: 4
Explanation: The longest ideal string is "abcd". The length of this string is 4, so 4 is returned.

```

**Constraints:**

- `1 <= s.length <= 105`
- `0 <= k <= 25`
- `s` consists of lowercase English letters.

```java
class Solution {
    public int longestIdealString(String s, int k) {
        int res = 0; 
        int n = s.length(); 
        int dp[] = new int[97+25+26];//從a開始到z極可能再往上26空間

        for (int i = 0; i < n; i++) {
            int c = s.charAt(i);// a = 97
            for (int j = c - k; j <= c + k; j++)// 遍歷+-k內元素取最大
                dp[c] = Math.max(dp[c], dp[j]);
            dp[c] = dp[c] + 1;// 可置換範圍內最長 + 1
            res = Math.max(res, dp[c]);
        }
        return res;
    }
}
```