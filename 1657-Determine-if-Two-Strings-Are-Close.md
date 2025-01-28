# 1657. Determine if Two Strings Are Close

Data structure: Hash Table
Difficulty: Medium

Medium

Topics

Companies

Hint

Two strings are considered **close** if you can attain one from the other using the following operations:

- Operation 1: Swap any two **existing** characters.
    - For example, `abcde -> aecdb`
- Operation 2: Transform **every** occurrence of one **existing** character into another **existing** character, and do the same with the other character.
    - For example, `aacabb -> bbcbaa` (all `a`'s turn into `b`'s, and all `b`'s turn into `a`'s)

You can use the operations on either string as many times as necessary.

Given two strings, `word1` and `word2`, return `true` *if* `word1` *and* `word2` *are **close**, and* `false` *otherwise.*

**Example 1:**

```
Input: word1 = "abc", word2 = "bca"
Output: true
Explanation: You can attain word2 from word1 in 2 operations.
Apply Operation 1: "abc" -> "acb"
Apply Operation 1: "acb" -> "bca"

```

**Example 2:**

```
Input: word1 = "a", word2 = "aa"
Output: false
Explanation:It is impossible to attain word2 from word1, or vice versa, in any number of operations.

```

**Example 3:**

```
Input: word1 = "cabbba", word2 = "abbccc"
Output: true
Explanation: You can attain word2 from word1 in 3 operations.
Apply Operation 1: "cabbba" -> "caabbb"
Apply Operation 2: "caabbb" -> "baaccc"
Apply Operation 2: "baaccc" -> "abbccc"

```

**Constraints:**

- `1 <= word1.length, word2.length <= 105`
- `word1` and `word2` contain only lowercase English letters.

```java
class Solution {
    public boolean closeStrings(String word1, String word2) {
        // STEP 1
        if (word1.length() != word2.length()) return false;
        // STEP 2
        Map<Character, Integer> hm1 = new HashMap<>();
        Map<Character, Integer> hm2 = new HashMap<>();

        for (int i = 0; i < word1.length(); i++) {
            char c = word1.charAt(i); 
            hm1.put(c, hm1.getOrDefault(c, 0) + 1);
        }
        for (int i = 0; i < word2.length(); i++) {
            char c = word2.charAt(i); 
            hm2.put(c, hm2.getOrDefault(c, 0) + 1);
        }
        // 判斷是否字母皆相同
        Set<Character> s1 = hm1.keySet();
        Set<Character> s2 = hm2.keySet();
        if(!s1.equals(s2)) return false;
         
        List<Integer> list1 = hm1.values().stream().collect(Collectors.toList());
        List<Integer> list2 = hm2.values().stream().collect(Collectors.toList());

        Collections.sort(list1);
        Collections.sort(list2);
        
        for(int i = 0; i < list1.size(); i++) {
            int e1 = list1.get(i);
            int e2 = list2.get(i);
            if(e1 != e2) return false; 
        }
        return true;
    }
}
```