# 1930. Unique Length-3 Palindromic Subsequences

Data structure: Hash Table
Difficulty: Medium

Medium

Topics

Companies

Hint

Given a string `s`, return *the number of **unique palindromes of length three** that are a **subsequence** of* `s`.

Note that even if there are multiple ways to obtain the same subsequence, it is still only counted **once**.

A **palindrome** is a string that reads the same forwards and backwards.

A **subsequence** of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

- For example, `"ace"` is a subsequence of `"abcde"`.

**Example 1:**

```
Input: s = "aabca"
Output: 3
Explanation: The 3 palindromic subsequences of length 3 are:
- "aba" (subsequence of "aabca")
- "aaa" (subsequence of "aabca")
- "aca" (subsequence of "aabca")

```

**Example 2:**

```
Input: s = "adc"
Output: 0
Explanation: There are no palindromic subsequences of length 3 in "adc".

```

**Example 3:**

```
Input: s = "bbcbaba"
Output: 4
Explanation: The 4 palindromic subsequences of length 3 are:
- "bbb" (subsequence of "bbcbaba")
- "bcb" (subsequence of "bbcbaba")
- "bab" (subsequence of "bbcbaba")
- "aba" (subsequence of "bbcbaba")

```

**Constraints:**

- `3 <= s.length <= 105`
- `s` consists of only lowercase English letters.

```java
class Solution {
    public int countPalindromicSubsequence(String s) {
    int first[] = new int[26];
    int last[] = new int[26];
    int res = 0;
		// 用字母去想
    Arrays.fill(first, Integer.MAX_VALUE);
    for (int i = 0; i < s.length(); i++) {
        // leftmost
        first[s.charAt(i) - 'a'] = Math.min(first[s.charAt(i) - 'a'], i);
        // rightmost
        last[s.charAt(i) - 'a'] = i;
    }
    for (int i = 0; i < 26; i++)
        // in-between
        if (first[i] < last[i])// 頭尾一定相同
            res += s.substring(first[i] + 1, last[i]).chars().distinct().count();
    return res;
}
}
```