# 1456. Maximum Number of Vowels in a Substring of Given Length

Methods: Pointer
Data structure: Set
Difficulty: Medium

**Medium**

1.8K

67

Companies

Given a string `s` and an integer `k`, return *the maximum number of vowel letters in any substring of* `s` *with length* `k`.

**Vowel letters** in English are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`.

**Example 1:**

```
Input: s = "abciiidef", k = 3
Output: 3
Explanation: The substring "iii" contains 3 vowel letters.

```

**Example 2:**

```
Input: s = "aeiou", k = 2
Output: 2
Explanation: Any substring of length 2 contains 2 vowels.

```

**Example 3:**

```
Input: s = "leetcode", k = 3
Output: 2
Explanation: "lee", "eet" and "ode" contain 2 vowels.

```

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists of lowercase English letters.
- `1 <= k <= s.length`

```java
class Solution {
    public int maxVowels(String s, int k) {
        int p1 = 0, p2 = 0;
        int max = 0, res = 0;
        int sLen = s.length();
        Set<Character> hs = new HashSet<>(Arrays.asList('a', 'e', 'i', 'o', 'u'));

        while(p2 < sLen){
            if(hs.contains(s.charAt(p2))){ // is vowel
                max++;
            }
            if(p2 - p1 + 1 == k){// 當長度達到限制
                res = Math.max(res, max);
                if(hs.contains(s.charAt(p1))){
                    max--;
                    p1++;
                } else p1++;
            }
            p2++;
        }
        return res;
    }
}
```