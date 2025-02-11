# 1790. Check if One String Swap Can Make Strings Equal  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>You are given two strings `s1` and `s2` of equal length. A **string swap** is an operation where you choose two indices in a string (not necessarily different) and swap the characters at these indices.

Return `true` *if it is possible to make both strings equal by performing ****at most one string swap ****on ****exactly one**** of the strings. *Otherwise, return `false`.

**Example 1:**

```plain text
Input: s1 = "bank", s2 = "kanb"
Output: true
Explanation: For example, swap the first character with the last character of s2 to make "bank".

```

**Example 2:**

```plain text
Input: s1 = "attack", s2 = "defend"
Output: false
Explanation: It is impossible to make them equal with one string swap.

```

**Example 3:**

```plain text
Input: s1 = "kelb", s2 = "kelb"
Output: true
Explanation: The two strings are already equal, so no string swap operation is required.

```

**Constraints:**

- `1 <= s1.length, s2.length <= 100`
- `s1.length == s2.length`
- `s1` and `s2` consist of only lowercase English letters.
```java
class Solution {
    public boolean areAlmostEqual(String s1, String s2) {
        int i = -1, j = -1;
        int diff = 0;
        for(int k = 0; k < s1.length(); k++) {
            if(s1.charAt(k) != s2.charAt(k)) {
                diff++;
                if(i == -1) i = k;
                else if(j == -1) j = k;
            }
        }
        if(diff == 0)
            return true;
        if(diff == 2 && s1.charAt(i)==s2.charAt(j) && s1.charAt(j)==s2.charAt(i))
            return true;
        return false;
    }
}
```

