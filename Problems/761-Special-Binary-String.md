# 761. Special Binary String  

  Methods: Greedy,Recursion </br> Difficulty: Hard </br> </br>**Special binary strings** are binary strings with the following two properties:

- The number of `0`'s is equal to the number of `1`'s.
- Every prefix of the binary string has at least as many `1`'s as `0`'s.
You are given a **special binary** string `s`.

A move consists of choosing two consecutive, non-empty, special substrings of `s`, and swapping them. Two strings are consecutive if the last character of the first string is exactly one index before the first character of the second string.

Return *the lexicographically largest resulting string possible after applying the mentioned operations on the string*.

**Example 1:**

```plain text
Input: s = "11011000"
Output: "11100100"
Explanation: The strings "10" [occuring at s[1]] and "1100" [at s[3]] are swapped.
This is the lexicographically largest string possible after some number of swaps.
```

**Example 2:**

```plain text
Input: s = "10"
Output: "10"
```

**Constraints:**

- `1 <= s.length <= 50`
- `s[i]` is either `'0'` or `'1'`.
- `s` is a special binary string.
```java
class Solution {
    // 括號結構（balance）
    // 分治 recursion
    // 字典序 greedy
    // string manipulation
    public String makeLargestSpecial(String S) {
        // 把 1 當作 (，0 當作 )
        int count = 0, i = 0;
        List<String> res = new ArrayList<String>();
        for (int j = 0; j < S.length(); j++) {
            if (S.charAt(j) == '1')
                count++;
            else
                count--;
            if (count == 0) {
                res.add('1' + makeLargestSpecial(S.substring(i + 1, j)) + '0');
                i = j + 1;
            }
        }
        Collections.sort(res, Collections.reverseOrder());
        return String.join("", res);
    }
    // 11011000
    // 拆： 1 [101100] 0
    // 再拆內部：101100 -> (10)(1100)
    // 排序： 1100 > 10
    // 組回： 1 (1100)(10) 0
    // = 11100100 ✅
}
```

