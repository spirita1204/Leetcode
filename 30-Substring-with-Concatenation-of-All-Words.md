# 30. Substring with Concatenation of All Words

Data structure: Hash Table
Difficulty: Hard

Hard

Topics

Companies

You are given a string `s` and an array of strings `words`. All the strings of `words` are of **the same length**.

A **concatenated string** is a string that exactly contains all the strings of any permutation of `words` concatenated.

- For example, if `words = ["ab","cd","ef"]`, then `"abcdef"`, `"abefcd"`, `"cdabef"`, `"cdefab"`, `"efabcd"`, and `"efcdab"` are all concatenated strings. `"acdbef"` is not a concatenated string because it is not the concatenation of any permutation of `words`.

Return an array of *the starting indices* of all the concatenated substrings in `s`. You can return the answer in **any order**.

**Example 1:**

**Input:** s = "barfoothefoobarman", words = ["foo","bar"]

**Output:** [0,9]

**Explanation:**

The substring starting at 0 is `"barfoo"`. It is the concatenation of `["bar","foo"]` which is a permutation of `words`.

The substring starting at 9 is `"foobar"`. It is the concatenation of `["foo","bar"]` which is a permutation of `words`.

**Example 2:**

**Input:** s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]

**Output:** []

**Explanation:**

There is no concatenated substring.

**Example 3:**

**Input:** s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]

**Output:** [6,9,12]

**Explanation:**

The substring starting at 6 is `"foobarthe"`. It is the concatenation of `["foo","bar","the"]`.

The substring starting at 9 is `"barthefoo"`. It is the concatenation of `["bar","the","foo"]`.

The substring starting at 12 is `"thefoobar"`. It is the concatenation of `["the","foo","bar"]`.

**Constraints:**

- `1 <= s.length <= 104`
- `1 <= words.length <= 5000`
- `1 <= words[i].length <= 30`
- `s` and `words[i]` consist of lowercase English letters.

```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        // 紀錄word 對應可用次數
        Map<String, Integer> hm = new HashMap<>();
        // 先給每個word 預設值
        for(String word: words) hm.put(word, hm.getOrDefault(word, 0) + 1);
        // 輸出
        List<Integer> res = new ArrayList<>();

        int sLen = s.length(), wordNum = words.length, word0Len = words[0].length();
        int p1 = 0, p2 = 0; // 左右指標
        
        while(p2 < sLen) {
            if(p2 - p1 + 1 == wordNum * word0Len) {// 長度剛好符合words全部
                String sub = s.substring(p1, p2 + 1);// 剛好符合長度
                HashMap<String, Integer> hm2 = new HashMap<>();
                int p = 0;
                while (p < sub.length()) {
                    String temp = sub.substring(p, p + word0Len);// 對其中一個一個比對
                    hm2.put(temp, hm2.getOrDefault(temp, 0) + 1);
                    p += word0Len;
                }
                if (hm.equals(hm2)){
                    res.add(p1);
                }
                p1++;
            }
            p2++;
        }
        return res;
    }
}
```