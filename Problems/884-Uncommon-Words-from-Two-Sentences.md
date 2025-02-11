# 884. Uncommon Words from Two Sentences

Data structure: Hash Table
Difficulty: Easy

Easy

Topics

Companies

A **sentence** is a string of single-space separated words where each word consists only of lowercase letters.

A word is **uncommon** if it appears exactly once in one of the sentences, and **does not appear** in the other sentence.

Given two **sentences** `s1` and `s2`, return *a list of all the **uncommon words***. You may return the answer in **any order**.

**Example 1:**

**Input:** s1 = "this apple is sweet", s2 = "this apple is sour"

**Output:** ["sweet","sour"]

**Explanation:**

The word `"sweet"` appears only in `s1`, while the word `"sour"` appears only in `s2`.

**Example 2:**

**Input:** s1 = "apple apple", s2 = "banana"

**Output:** ["banana"]

**Constraints:**

- `1 <= s1.length, s2.length <= 200`
- `s1` and `s2` consist of lowercase English letters and spaces.
- `s1` and `s2` do not have leading or trailing spaces.
- All the words in `s1` and `s2` are separated by a single space.

```java
class Solution {
    public String[] uncommonFromSentences(String s1, String s2) {
        String[] s1s = s1.split(" ");
        String[] s2s = s2.split(" ");
        Map<String, Integer> hm = new HashMap<>();
        for(int i = 0; i < s1s.length; i++) {
            String e = s1s[i];
            hm.put(e, hm.getOrDefault(e, 0) + 1);
        }
        for(int i = 0; i < s2s.length; i++) {
            String e = s2s[i];
            if(hm.containsKey(e))
                hm.put(e, 401);// 總長度最多200* 2
            else 
                hm.put(e, 1);
        }
        return hm.entrySet().stream()
                .filter(e -> e.getValue() < 2)// 出現一次
                .map(Map.Entry :: getKey)
                .toArray(String[]::new);
    }
}
```