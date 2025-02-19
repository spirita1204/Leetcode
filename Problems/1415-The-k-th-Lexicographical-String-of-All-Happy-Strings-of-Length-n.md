# 1415. The k-th Lexicographical String of All Happy Strings of Length n  

  Methods: DFS,Greedy </br> Difficulty: Medium </br> </br>A **happy string** is a string that:

- consists only of letters of the set `['a', 'b', 'c']`.
- `s[i] != s[i + 1]` for all values of `i` from `1` to `s.length - 1` (string is 1-indexed).
For example, strings **"abc", "ac", "b"** and **"abcbabcbcb"** are all happy strings and strings **"aa", "baa"** and **"ababbc"** are not happy strings.

Given two integers `n` and `k`, consider a list of all happy strings of length `n` sorted in lexicographical order.

Return *the kth string* of this list or return an **empty string** if there are less than `k` happy strings of length `n`.

**Example 1:**

```plain text
Input: n = 1, k = 3
Output: "c"
Explanation: The list ["a", "b", "c"] contains all happy strings of length 1. The third string is "c".
```

**Example 2:**

```plain text
Input: n = 1, k = 4
Output: ""
Explanation: There are only 3 happy strings of length 1.
```

**Example 3:**

```plain text
Input: n = 3, k = 9
Output: "cab"
Explanation: There are 12 different happy string of length 3 ["aba", "abc", "aca", "acb", "bab", "bac", "bca", "bcb", "cab", "cac", "cba", "cbc"]. You will find the 9th string = "cab"
```

**Constraints:**

- `1 <= n <= 10`
- `1 <= k <= 100`
```java
class Solution {
    private String res = "";
    private char[] chars = new char[] { 'a', 'b', 'c' };
    private int k;

    public String getHappyString(int n, int k) {
        res = "";
        this.k = k;
        dfs(0, n, new StringBuilder());
        return res;
    }

    private void dfs(int len, int n, StringBuilder sb) {
        if (len == n) {// 剛好長度
            if (--k == 0) 
                res = sb.toString();
            return;
        }
        for (char c : chars) {
            if (len == 0 || sb.charAt(len - 1) != c) {// 判斷最後一位不要重複
                sb.append(c);
                dfs(len + 1, n, sb);
                sb.deleteCharAt(sb.length() - 1);
            }
        }
    }
}
```

