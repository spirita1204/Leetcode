# 76. Minimum Window Substring

Methods: Pointer
Data structure: Hash Table
Difficulty: Hard

Hard

Topics

Companies

Hint

Given two strings `s` and `t` of lengths `m` and `n` respectively, return *the **minimum window***

***substring***

*of*

```
s
```

*such that every character in*

```
t
```

*(**including duplicates**) is included in the window*

. If there is no such substring, return

*the empty string*

```
""
```

.

The testcases will be generated such that the answer is **unique**.

**Example 1:**

```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

```

**Example 2:**

```
Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.

```

**Example 3:**

```
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.

```

**Constraints:**

- `m == s.length`
- `n == t.length`
- `1 <= m, n <= 105`
- `s` and `t` consist of uppercase and lowercase English letters.

**Follow up:** Could you find an algorithm that runs in `O(m + n)` time?

```java
class Solution {
    public String minWindow(String s, String t) {
        // 紀錄word 對應可用次數
        Map<Character, Integer> hm = new HashMap<>();
        // 先給每個word 預設值
        for (Character c : t.toCharArray())
            hm.put(c, hm.getOrDefault(c, 0) + 1);

        int p1 = 0, p2 = 0;
        int count = t.length();
        int minWindowStart = 0;
        int minWindowLength = Integer.MAX_VALUE;

        while (p2 < s.length()) {
            char c = s.charAt(p2);
            if (hm.containsKey(c)) {
                hm.put(c, hm.get(c) - 1);// value小於 0 代表當前p1, p2包含多個需要字元
                if(hm.get(c) >= 0) count--;
            }
            while(count == 0) {// t剛好都拿到
                if(p2 - p1 + 1 < minWindowLength) {
                    minWindowLength = p2 - p1 + 1;
                    minWindowStart = p1;
                }
                // 當t剛好都拿到 開始移動左指標
                char leftChar = s.charAt(p1);
                if (hm.containsKey(leftChar)) {
                    hm.put(leftChar, hm.get(leftChar) + 1);
                    if (hm.get(leftChar) > 0) {
                        count++;
                    }
                }
                p1++;
            }
            p2++;
        }
        return minWindowLength == Integer.MAX_VALUE ? "" : s.substring(minWindowStart, minWindowStart + minWindowLength);
    }
}
```

重新試寫

```java
class Solution {
    public String minWindow(String s, String t) {
        Map<Character, Integer> hm = new HashMap<>();
        for (char c : t.toCharArray())
            hm.put(c, hm.getOrDefault(c, 0) + 1);

        int p1 = 0, p2 = 0;
        int count = t.length();
        int start = 0;
        int minLen = Integer.MAX_VALUE;

        while (p2 < s.length()) {
            char c = s.charAt(p2);
            if (hm.containsKey(c)) {
                hm.put(c, hm.get(c) - 1);
                if (hm.get(c) >= 0)
                    count--;
            }
            while (count == 0) {
                if (p2 - p1 + 1 < minLen) {
                    start = p1;
                    minLen = p2 - p1 + 1;
                }
                char left = s.charAt(p1);
                if (hm.containsKey(left)) {
                    hm.put(left, hm.get(left) + 1);
                    if (hm.get(left) > 0)
                        count++;
                }
                p1++;
            }
            p2++;
        }
        return minLen == Integer.MAX_VALUE ? "" : s.substring(start, start + minLen);
    }
}
```