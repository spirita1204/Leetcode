# 28. Find the Index of the First Occurrence in a String

Methods: Basic logic
Difficulty: Easy

Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

**Example 1:**

```
Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.

```

**Example 2:**

```
Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.

```

**Constraints:**

- `1 <= haystack.length, needle.length <= 104`
- `haystack` and `needle` consist of only lowercase English characters.

```java
class Solution {
    public int strStr(String haystack, String needle) {
        for(int i = 0; i < haystack.length(); i++){
            if(haystack.charAt(i) == needle.charAt(0)){
                if(i+needle.length() > haystack.length()) break;
                if(haystack.substring(i,i+needle.length()).equals(needle)) return i;
            }
        }
        return -1;
    }
}
```

2020

```java
class Solution {
  private int[] computeLPS(String str) { // failure function table
    int[] lps = new int[str.length()];
    lps[0] = 0;
    int i = 1; // always walks forward
    int j = 0; // tracks prefix that matches suffix

    while (i < str.length()) {
      if (str.charAt(i) == str.charAt(j)) {
        j++;
        lps[i] = j;
        i++;
      } else { // mismatch
        if (j == 0) { // go onto next character in string
          lps[i] = 0;
          i++;
        } else { // backtrack j to check previous matching prefix
          j = lps[j - 1];
        }
      }
    }
    return lps;
  }

  int strStr(String haystack, String needle) {
      if (haystack == null || needle == null || haystack.length() < needle.length()) {
          return -1;
      } else if (needle.isEmpty()) {
          return 0;
      }

      int[] lps = computeLPS(needle);
      int i = 0;
      int j = 0;

      while (i < haystack.length()) {
          if (needle.charAt(j) == haystack.charAt(i)) {
              i++;
              j++;
              if (j == needle.length()) {
                  return i - j; // match found. Return location of match
              }
          } else {
              if (j == 0) {
                  i++;
              } else {
                  j = lps[j - 1]; // backtrack j to check previous matching prefix
              }
          }
      }

      return -1; // did not find needle
  }
}
```

```java
class Solution {
    public int strStr(String haystack, String needle) {
       return haystack.indexOf(needle);
    }
}
```