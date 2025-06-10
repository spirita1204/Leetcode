# 3442. Maximum Difference Between Even and Odd Frequency I  

  Data Structure: Hash Table </br> Difficulty: Easy </br> </br>You are given a string `s` consisting of lowercase English letters.

Your task is to find the **maximum** difference `diff = a1 - a2` between the frequency of characters `a1` and `a2` in the string such that:

- `a1` has an **odd frequency** in the string.
- `a2` has an **even frequency** in the string.
Return this **maximum** difference.

---

**Example 1:**

**Input:** s = "aaaaabbc"

**Output:** 3

**Explanation:**

- The character `'a'` has an **odd frequency** of `5` and `'b'` has an **even frequency** of `2`.
- The maximum difference is `5 - 2 = 3`.
---

**Example 2:**

**Input:** s = "abcabcab"

**Output:** 1

**Explanation:**

- The character `'a'` has an **odd frequency** of `3` and `'c'` has an **even frequency** of 2.
- The maximum difference is `3 - 2 = 1`.
---

**Constraints:**

- `3 <= s.length <= 100`
- `s` consists only of lowercase English letters.
- `s` contains at least one character with an odd frequency and one with an even frequency.
```java
class Solution {
    public int maxDifference(String s) {
        int maxOdd = 0, minEven = Integer.MAX_VALUE;
        int[] arr = new int[26];

        for(char c: s.toCharArray()) 
            arr[c - 'a']++;

        for(int i = 0; i < 26; i++) {
            if(arr[i] == 0)
                continue;
            if(arr[i] % 2 == 0) {
                minEven = Math.min(minEven, arr[i]);
            } else {
                maxOdd = Math.max(maxOdd, arr[i]);
            }
        }
        return maxOdd - minEven;
    }
}
```

