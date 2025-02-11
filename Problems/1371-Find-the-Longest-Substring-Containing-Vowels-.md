# 1371. Find the Longest Substring Containing Vowels in Even Counts

Methods: Prefix Sum
Difficulty: Medium

Given the string `s`, return the size of the longest substring containing each vowel an even number of times. That is, 'a', 'e', 'i', 'o', and 'u' must appear an even number of times.

**Example 1:**

```
Input: s = "eleetminicoworoep"
Output: 13
Explanation:The longest substring is "leetminicowor" which contains two each of the vowels:e,i ando and zero of the vowels:a andu.

```

**Example 2:**

```
Input: s = "leetcodeisgreat"
Output: 5
Explanation: The longest substring is "leetc" which contains two e's.

```

**Example 3:**

```
Input: s = "bcbcbc"
Output: 6
Explanation: In this case, the given string "bcbcbc" is the longest because all vowels:a,e,i,o andu appear zero times.

```

**Constraints:**

- `1 <= s.length <= 5 x 10^5`
- `s` contains only lowercase English letters.

Hint 1

Represent the counts (odd or even) of vowels with a bitmask.

---

Hint 2

Precompute the prefix xor for the bitmask of vowels and then get the longest valid substring.

```java
class Solution {
    public int findTheLongestSubstring(String s) {
        int len = s.length();
        // prefix xor
        // a e i o u 字母透過二進位11111表示
        Map<Integer, Integer> hm = new HashMap<>();
        int cnt = 0;// 代表aeiou個數(0雙1單)
        int max = 0;
        for(int i = 0; i < len; i++) {
            int idx = "aeiou".indexOf(s.charAt(i));
            if(idx >= 0) {// contains
                cnt ^= (1 << idx);// 將第idx xor 代表單變雙 雙變單
            }
            // case1 當前及滿足(從0到...)
            if(cnt == 0) max = Math.max(max, i + 1);
            // case2 找出可互補
            if(hm.containsKey(cnt)) max = Math.max(max, i - hm.get(cnt));
            // 避免覆蓋
            if(!hm.containsKey(cnt)) hm.put(cnt, i);
        }
        return max;
    }
}
```