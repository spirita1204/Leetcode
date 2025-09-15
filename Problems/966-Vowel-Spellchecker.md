# 966. Vowel Spellchecker  

  Data Structure: Hash Table </br> Difficulty: Medium </br> </br>Given a `wordlist`, we want to implement a spellchecker that converts a query word into a correct word.

For a given `query` word, the spell checker handles two categories of spelling mistakes:

- Capitalization: If the query matches a word in the wordlist (**case-insensitive**), then the query word is returned with the same case as the case in the wordlist.
- Vowel Errors: If after replacing the vowels `('a', 'e', 'i', 'o', 'u')` of the query word with any vowel individually, it matches a word in the wordlist (**case-insensitive**), then the query word is returned with the same case as the match in the wordlist.
In addition, the spell checker operates under the following precedence rules:

- When the query exactly matches a word in the wordlist (**case-sensitive**), you should return the same word back.
- When the query matches a word up to capitlization, you should return the first such match in the wordlist.
- When the query matches a word up to vowel errors, you should return the first such match in the wordlist.
- If the query has no matches in the wordlist, you should return the empty string.
Given some `queries`, return a list of words `answer`, where `answer[i]` is the correct word for `query = queries[i]`.

**Example 1:**

```plain text
Input: wordlist = ["KiTe","kite","hare","Hare"], queries = ["kite","Kite","KiTe","Hare","HARE","Hear","hear","keti","keet","keto"]
Output: ["kite","KiTe","KiTe","Hare","hare","","","KiTe","","KiTe"]
```

**Example 2:**

```plain text
Input: wordlist = ["yellow"], queries = ["YellOw"]
Output: ["yellow"]
```

**Constraints:**

- `1 <= wordlist.length, queries.length <= 5000`
- `1 <= wordlist[i].length, queries[i].length <= 7`
- `wordlist[i]` and `queries[i]` consist only of only English letters.
```java
class Solution {
    public String[] spellchecker(String[] wordlist, String[] queries) {
        Set<String> exact = new HashSet<>(Arrays.asList(wordlist));
        Map<String, String> caseMap = new HashMap<>();
        Map<String, String> vowelMap = new HashMap<>();

        for (String w : wordlist) {
            String lower = w.toLowerCase();
            String devowel = deVowel(lower);
            caseMap.putIfAbsent(lower, w);
            vowelMap.putIfAbsent(devowel, w);
        }
        String[] result = new String[queries.length];
        for (int i = 0; i < queries.length; i++) {
            String q = queries[i];
            if (exact.contains(q)) {// 一樣 直接輸出
                result[i] = q;
            } else {
                String lower = q.toLowerCase();
                String devowel = deVowel(lower);
                if (caseMap.containsKey(lower))
                    result[i] = caseMap.get(lower);
                else if (vowelMap.containsKey(devowel))
                    result[i] = vowelMap.get(devowel);
                else
                    result[i] = "";
            }
        }
        return result;
    }

    private String deVowel(String s) {
        char[] ch = s.toCharArray();
        for (int i = 0; i < ch.length; i++) {
            if (isVowel(ch[i]))
                ch[i] = '*';
        }
        return new String(ch);
    }

    private boolean isVowel(char c) {
        return "aeiou".indexOf(Character.toLowerCase(c)) >= 0;
    }
}
```

