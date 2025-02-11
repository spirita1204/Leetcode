# 1941. Check if All Characters Have Equal Number of Occurrences  

  Data Structure: Hash Table </br> Difficulty: Easy </br> </br>Given a string `s`, return `true`* if *`s`* is a ****good**** string, or *`false`* otherwise*.

A string `s` is **good** if **all** the characters that appear in `s` have the **same** number of occurrences (i.e., the same frequency).

**Example 1:**

```plain text
Input: s = "abacbc"
Output: true
Explanation: The characters that appear in s are 'a', 'b', and 'c'. All characters occur 2 times in s.
```

**Example 2:**

```plain text
Input: s = "aaabb"
Output: false
Explanation: The characters that appear in s are 'a' and 'b'.
'a' occurs 3 times while 'b' occurs 2 times, which is not the same number of times.
```

**Constraints:**

- `1 <= s.length <= 1000`
- `s` consists of lowercase English letters.
```java
class Solution {
    public boolean areOccurrencesEqual(String s) {
        int[] hm = new int[26];

        for(int i = 0; i < s.length(); i++) {
            hm[s.charAt(i) - 'a']++;
        }
        int val = 0;
        for(int i = 0; i < 26; i++)
            if(hm[i] != 0) {
                if(val == 0)
                    val = hm[i];
                else 
                    if(val != hm[i])
                        return false;
            }
        return true;
    }
}
```

最優解

```java
class Solution {
    public boolean areOccurrencesEqual(String s) {
        int[] freq = new int[26]; // Array for 'a' to 'z'

        // Count occurrences of each character
        for (char c : s.toCharArray()) {
            freq[c - 'a']++;
        }

        // Find the first non-zero frequency
        int occurrence = 0;
        for (int f : freq) {
            if (f > 0) {
                occurrence = f;
                break;
            }
        }

        // Check if all non-zero frequencies match the first found frequency
        for (int f : freq) {
            if (f > 0 && f != occurrence) {
                return false;
            }
        }

        return true;
    }
}
```

