# 1593. Split a String Into the Max Number of Unique Substrings

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Hint

Given a string `s`, return *the maximum number of unique substrings that the given string can be split into*.

You can split string `s` into any list of **non-empty substrings**, where the concatenation of the substrings forms the original string. However, you must split the substrings such that all of them are **unique**.

A **substring** is a contiguous sequence of characters within a string.

**Example 1:**

```
Input: s = "ababccc"
Output: 5
Explanation: One way to split maximally is ['a', 'b', 'ab', 'c', 'cc']. Splitting like ['a', 'b', 'a', 'b', 'c', 'cc'] is not valid as you have 'a' and 'b' multiple times.

```

**Example 2:**

```
Input: s = "aba"
Output: 2
Explanation: One way to split maximally is ['a', 'ba'].

```

**Example 3:**

```
Input: s = "aa"
Output: 1
Explanation: It is impossible to split the string any further.

```

**Constraints:**

- `1 <= s.length <= 16`
- `s` contains only lower case English letters.

```java
class Solution {
    int max = 0;
    public int maxUniqueSplit(String s) {
        Set<String> hs = new HashSet<>();
        dfs(s, 0, 1, hs);

        return max;
    }

    private void dfs(String s, int i, int j, Set<String> hs) {
        if(i == s.length()) {
            max = Math.max(max, hs.size());
            return;
        }
        for(int last = j; last <= s.length();last++) {
            String e = s.substring(i, last);
            if(!hs.contains(e)) {
                hs.add(e);
                dfs(s, last, last + 1, hs);
                hs.remove(e);
            } else {
                continue;
            }
        }
    }
}
```