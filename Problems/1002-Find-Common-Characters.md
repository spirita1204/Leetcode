# 1002. Find Common Characters

Methods: Basic logic
Difficulty: Easy

Easy

Topics

Companies

Given a string array `words`, return *an array of all characters that show up in all strings within the* `words` *(including duplicates)*. You may return the answer in **any order**.

**Example 1:**

```
Input: words = ["bella","label","roller"]
Output: ["e","l","l"]

```

**Example 2:**

```
Input: words = ["cool","lock","cook"]
Output: ["c","o"]

```

**Constraints:**

- `1 <= words.length <= 100`
- `1 <= words[i].length <= 100`
- `words[i]` consists of lowercase English letters.

```java
class Solution {
    public List<String> commonChars(String[] words) {
        int[] minFreq = new int[26];
        List<String> res = new ArrayList<>();
        Arrays.fill(minFreq, Integer.MAX_VALUE);

        for (String word : words) {
            int[] charCount = new int[26];
            for (char c : word.toCharArray()) {
                charCount[c - 'a']++;
            }
            for (int i = 0; i < 26; i++) {
                minFreq[i] = Math.min(minFreq[i], charCount[i]);
            }
        }
        for (int i = 0; i < 26; i++) {
            while (minFreq[i] > 0) {
                res.add(Character.toString((char) (i + 'a')));
                minFreq[i]--;
            }
        }

        return res;
    }
}
```