# 205. Isomorphic Strings

Data structure: Hash Table
Difficulty: Easy

Solved

Easy

Given two strings `s` and `t`, *determine if they are isomorphic*.

Two strings `s` and `t` are isomorphic if the characters in `s` can be replaced to get `t`.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

**Example 1:**

```
Input: s = "egg", t = "add"
Output: true

```

**Example 2:**

```
Input: s = "foo", t = "bar"
Output: false

```

**Example 3:**

```
Input: s = "paper", t = "title"
Output: true

```

**Constraints:**

- `1 <= s.length <= 5 * 104`
- `t.length == s.length`
- `s` and `t` consist of any valid ascii character.

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        Map<Character, Character> hm = new HashMap<>();
        Map<Character, Character> hm2 = new HashMap<>();

        for(int i = 0; i< s.length(); i++) {
            char a = s.charAt(i);
            char b = t.charAt(i);

            Character getE = hm.putIfAbsent(a, b);
            Character getE2 = hm2.putIfAbsent(b, a);
            
            if(getE != null && b != getE)  return false;
            if(getE2 != null && a != getE2) return false;
        }
        return true;
    }
}
```