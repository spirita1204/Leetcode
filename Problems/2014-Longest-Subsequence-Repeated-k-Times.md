# 2014. Longest Subsequence Repeated k Times  

  Methods: Basic logic </br> Data Structure: Queue </br> Difficulty: Hard </br> </br>You are given a string `s` of length `n`, and an integer `k`. You are tasked to find the **longest subsequence repeated** `k` times in string `s`.

A **subsequence** is a string that can be derived from another string by deleting some or no characters without changing the order of the remaining characters.

A subsequence `seq` is **repeated** `k` times in the string `s` if `seq * k` is a subsequence of `s`, where `seq * k` represents a string constructed by concatenating `seq` `k` times.

- For example, `"bba"` is repeated `2` times in the string `"bababcba"`, because the string `"bbabba"`, constructed by concatenating `"bba"` `2` times, is a subsequence of the string `"``<u>**b**</u>``a``<u>**bab**</u>``c``<u>**ba**</u>``"`.
Return *the ****longest subsequence repeated**** *`k`* times in string *`s`*. If multiple such subsequences are found, return the ****lexicographically largest**** one. If there is no such subsequence, return an ****empty**** string*.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/08/30/longest-subsequence-repeat-k-times.png)

```plain text
Input: s = "letsleetcode", k = 2
Output: "let"
Explanation: There are two longest subsequences repeated 2 times: "let" and "ete".
"let" is the lexicographically largest one.
```

**Example 2:**

```plain text
Input: s = "bb", k = 2
Output: "b"
Explanation: The longest subsequence repeated 2 times is "b".
```

**Example 3:**

```plain text
Input: s = "ab", k = 2
Output: ""
Explanation: There is no subsequence repeated 2 times. Empty string is returned.
```

**Constraints:**

- `n == s.length`
- `2 <= k <= 2000`
- `2 <= n < min(2001, k * 8)`
- `s` consists of lowercase English letters.
```java
class Solution {
    public String longestSubsequenceRepeatedK(String s, int k) {
        String res = "";
        Queue<String> q = new LinkedList<>();

        q.offer(""); // init
        
        while (!q.isEmpty()) {
            String c = q.poll();
            for (char ch = 'a'; ch <= 'z'; ch++) {
                String n = c + ch;
                if (isK(n, s, k)) {
                    res = n;
                    q.offer(n);
                }
            }
        }

        return res;
    }

    boolean isK(String s, String t, int k) {
        int cnt = 0, i = 0;
        for (char ch : t.toCharArray()) {
            if (ch == s.charAt(i)) {
                if (++i == s.length()) {
                    i = 0;
                    if (++cnt == k)
                        return true;
                }
            }
        }
        return false;
    }
}
```

