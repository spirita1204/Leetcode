# 1208. Get Equal Substrings Within Budget

Methods: Pointer
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given two strings `s` and `t` of the same length and an integer `maxCost`.

You want to change `s` to `t`. Changing the `ith` character of `s` to `ith` character of `t` costs `|s[i] - t[i]|` (i.e., the absolute difference between the ASCII values of the characters).

Return *the maximum length of a substring of* `s` *that can be changed to be the same as the corresponding substring of* `t` *with a cost less than or equal to* `maxCost`. If there is no substring from `s` that can be changed to its corresponding substring from `t`, return `0`.

**Example 1:**

```
Input: s = "abcd", t = "bcdf", maxCost = 3
Output: 3
Explanation: "abc" of s can change to "bcd".
That costs 3, so the maximum length is 3.

```

**Example 2:**

```
Input: s = "abcd", t = "cdef", maxCost = 3
Output: 1
Explanation: Each character in s costs 2 to change to character in t,  so the maximum length is 1.

```

**Example 3:**

```
Input: s = "abcd", t = "acde", maxCost = 0
Output: 1
Explanation: You cannot make any change, so the maximum length is 1.

```

**Constraints:**

- `1 <= s.length <= 105`
- `t.length == s.length`
- `0 <= maxCost <= 106`
- `s` and `t` consist of only lowercase English letters.

```java
class Solution {
    public int equalSubstring(String s, String t, int maxCost) {
        int p1 = 0, p2 = 0;
        int maxLen = 0, costs = 0;
        while(p2 < s.length()) {
            char c1 = s.charAt(p2);
            char c2 = t.charAt(p2);
            int cost = Math.abs(c2 - c1);
            costs += cost;

            if(costs > maxCost) {
                while(costs > maxCost) {
                    char c11 = s.charAt(p1);
                    char c12 = t.charAt(p1);
                    int cost1 = Math.abs(c12 - c11);
                    costs -= (cost1);
                    p1++;
                }
            }
            maxLen = Math.max(maxLen, p2 - p1 + 1);
            p2++;
        }
        return maxLen;
    }
}
```