# 1400. Construct K Palindrome Strings

Data structure: Hash Table
Difficulty: Medium

Given a string `s` and an integer `k`, return `true` *if you can use all the characters in* `s` *to construct* `k` *palindrome strings or* `false` *otherwise*.

**Example 1:**

```
Input: s = "annabelle", k = 2
Output: true
Explanation: You can construct two palindromes using all characters in s.
Some possible constructions "anna" + "elble", "anbna" + "elle", "anellena" + "b"

```

**Example 2:**

```
Input: s = "leetcode", k = 3
Output: false
Explanation: It is impossible to construct 3 palindromes using all the characters of s.

```

**Example 3:**

```
Input: s = "true", k = 4
Output: true
Explanation: The only possible solution is to put each character in a separate string.

```

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists of lowercase English letters.
- `1 <= k <= 105`

```java
class Solution {
    public boolean canConstruct(String s, int k) {
        // a 2 二給誰都可 看一夠不夠分
        // n 2
        // b 1
        // e 2 
        // l 2
        // --- 
        // s='aaaa' k='3'
        // aa a a 
        int len = s.length();
        if(len == k)
            return true;
        if(len < k)
            return false;
        int[] hm = new int[26];
        for(int i = 0; i < len; i++) 
            hm[s.charAt(i) - 'a']++;
        int odd = 0;
        for(int i = 0; i < 26; i++)
            if(hm[i] % 2 != 0)
                odd++;
        if(odd <= k)
            return true;

        return false;
    }
}
```