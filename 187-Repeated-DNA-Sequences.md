# 187. Repeated DNA Sequences

Methods: Pointer
Data structure: Set
Difficulty: Medium

Medium

Topics

Companies

The **DNA sequence** is composed of a series of nucleotides abbreviated as `'A'`, `'C'`, `'G'`, and `'T'`.

- For example, `"ACGAATTCCG"` is a **DNA sequence**.

When studying **DNA**, it is useful to identify repeated sequences within the DNA.

Given a string `s` that represents a **DNA sequence**, return all the **`10`-letter-long** sequences (substrings) that occur more than once in a DNA molecule. You may return the answer in **any order**.

**Example 1:**

```
Input: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
Output: ["AAAAACCCCC","CCCCCAAAAA"]

```

**Example 2:**

```
Input: s = "AAAAAAAAAAAAA"
Output: ["AAAAAAAAAA"]

```

**Constraints:**

- `1 <= s.length <= 105`
- `s[i]` is either `'A'`, `'C'`, `'G'`, or `'T'`.

```java
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        List<String> res = new ArrayList<>();
        if(s.length() <= 10) return res;

        Set<String> hs = new HashSet<>();
        int p1 = 0, p2 = 10;
        while(p2 <= s.length()) {
            if(p2 - p1 == 10) {
                String sub = s.substring(p1, p2);
                if(!hs.contains(sub)) hs.add(sub);
                else 
                    if(!res.contains(sub))
                        res.add(sub);
                p2++;
            } else if(p2 - p1 > 10) 
                p1++;
        }
        return res;
    }
}
```