# 214. Shortest Palindrome

Methods: Basic logic
Difficulty: Hard

Hard

Topics

Companies

You are given a string `s`. You can convert `s` to a

palindrome

by adding characters in front of it.

Return *the shortest palindrome you can find by performing this transformation*.

**Example 1:**

```
Input: s = "aacecaaa"
Output: "aaacecaaa"

```

**Example 2:**

```
Input: s = "abcd"
Output: "dcbabcd"

```

**Constraints:**

- `0 <= s.length <= 5 * 104`
- `s` consists of lowercase English letters only.

```java
class Solution {
    public String shortestPalindrome(String s) {
        // ex: abac caba -> cabac
        //     abcd dcba -> dcbabcd
        String reverse = new StringBuilder(s).reverse().toString();
        for(int i = 0; i < s.length(); i++) {
            if(s.startsWith(reverse.substring(i))) {// 代表 中間有重疊
                return reverse + s.substring(s.length() - i, s.length());
            }
        }
        return reverse + s;// 沒重疊
    }
}
```