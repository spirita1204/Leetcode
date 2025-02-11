# 567. Permutation in String

Methods: Pointer
Data structure: Hash Table
Difficulty: Medium

**Medium**

9.6K

Given two strings `s1` and `s2`, return `true` *if* `s2` *contains a permutation of* `s1`*, or* `false` *otherwise*.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

**Example 1:**

```
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").

```

**Example 2:**

```
Input: s1 = "ab", s2 = "eidboaoo"
Output: false

```

**Constraints:**

- `1 <= s1.length, s2.length <= 104`
- `s1` and `s2` consist of lowercase English letters.

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int s1Len = s1.length();
        int s2Len = s2.length();
        if(s1Len > s2Len) return false;
        int[] s1Map = new int[26]; 
        int[] s2Map = new int[26];

        for (int i = 0; i < s1Len; i++)//將s1頻率丟到arr中
            s1Map[s1.charAt(i) - 'a']++;

        for (int i = 0; i < s2Len; i++) {
            if (i >= s1Len)
                s2Map[s2.charAt(i - s1Len) - 'a']--;//去掉之前的len之外
            s2Map[s2.charAt(i) - 'a']++;
            if (isPermutation(s1Map, s2Map)) return true;
        }
        return false;
    }
    public boolean isPermutation(int[] s1Map, int[] s2Map) {
        for (int i = 0; i < 26; i++)
            if (s1Map[i] != s2Map[i])
                return false;
        return true;
    }
}
```

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        Map<Character, Integer> hm = new HashMap<>();
        Map<Character, Integer> hm2 = new HashMap<>();

        for(char c: s1.toCharArray()) 
            hm.put(c, hm.getOrDefault(c, 0) + 1);
        int len1 = s1.length();
        int p1 = 0;
        for(int p2 = 0; p2 < s2.length(); p2++) {
            if(p2 - p1 == len1) {
                char c = s2.charAt(p1);
                if(hm2.get(c) == 1)// 代表要刪除
                    hm2.remove(c);
                else
                    hm2.put(c, hm2.get(c) - 1);
                p1++;
            }
            if(p2 - p1 < len1) {
                char c = s2.charAt(p2);
                hm2.put(c, hm2.getOrDefault(c, 0) + 1);
            } 
            if(hm.equals(hm2)) return true;
        } 
        return false;
    }
}
```