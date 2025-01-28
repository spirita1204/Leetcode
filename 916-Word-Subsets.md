# 916. Word Subsets

Data structure: Hash Table
Difficulty: Medium

You are given two string arrays `words1` and `words2`.

A string `b` is a **subset** of string `a` if every letter in `b` occurs in `a` including multiplicity.

- For example, `"wrr"` is a subset of `"warrior"` but is not a subset of `"world"`.

A string `a` from `words1` is **universal** if for every string `b` in `words2`, `b` is a subset of `a`.

Return an array of all the **universal** strings in `words1`. You may return the answer in **any order**.

**Example 1:**

```
Input: words1 = ["amazon","apple","facebook","google","leetcode"], words2 = ["e","o"]
Output: ["facebook","google","leetcode"]

```

**Example 2:**

```
Input: words1 = ["amazon","apple","facebook","google","leetcode"], words2 = ["l","e"]
Output: ["apple","google","leetcode"]

```

**Constraints:**

- `1 <= words1.length, words2.length <= 104`
- `1 <= words1[i].length, words2[i].length <= 10`
- `words1[i]` and `words2[i]` consist only of lowercase English letters.
- All the strings of `words1` are **unique**.

```java
class Solution {
    public List<String> wordSubsets(String[] words1, String[] words2) {
        List<String> res = new ArrayList<>();
        int[] hm = new int[26];
        for (int i = 0; i < words2.length; i++) {
            String s = words2[i];
            int[] letterCount = helper(s);
            for (int j = 0; j < 26; j++) {
                hm[j] = Math.max(hm[j], letterCount[j]);
            }
        }
        for (int i = 0; i < words1.length; i++) {
            String s = words1[i];
            boolean isValid = true;
            int[] count = helper(s);
            for (int j = 0; j < 26; j++) {
                if (count[j] < hm[j]) {
                    isValid = false;
                    break;
                }
            }
            if(isValid)
                res.add(s);
        }
        return res;
    }

    private int[] helper(String word) {
        int[] letterCount = new int[26];
        for (char c : word.toCharArray()) {
            letterCount[c - 'a']++;
        }
        return letterCount;
    }
}
```