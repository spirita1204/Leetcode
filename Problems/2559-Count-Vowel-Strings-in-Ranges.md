# 2559. Count Vowel Strings in Ranges

Methods: Prefix Sum
Difficulty: Medium

You are given a **0-indexed** array of strings `words` and a 2D array of integers `queries`.

Each query `queries[i] = [li, ri]` asks us to find the number of strings present in the range `li` to `ri` (both **inclusive**) of `words` that start and end with a vowel.

Return *an array* `ans` *of size* `queries.length`*, where* `ans[i]` *is the answer to the* `i`th *query*.

**Note** that the vowel letters are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`.

**Example 1:**

```
Input: words = ["aba","bcb","ece","aa","e"], queries = [[0,2],[1,4],[1,1]]
Output: [2,3,0]
Explanation: The strings starting and ending with a vowel are "aba", "ece", "aa" and "e".
The answer to the query [0,2] is 2 (strings "aba" and "ece").
to query [1,4] is 3 (strings "ece", "aa", "e").
to query [1,1] is 0.
We return [2,3,0].

```

**Example 2:**

```
Input: words = ["a","e","i"], queries = [[0,2],[0,1],[2,2]]
Output: [3,2,1]
Explanation: Every string satisfies the conditions, so we return [3,2,1].
```

**Constraints:**

- `1 <= words.length <= 105`
- `1 <= words[i].length <= 40`
- `words[i]` consists only of lowercase English letters.
- `sum(words[i].length) <= 3 * 105`
- `1 <= queries.length <= 105`
- `0 <= li <= ri < words.length`

```java
class Solution {
    public int[] vowelStrings(String[] words, int[][] queries) {
        int len = words.length;
        int qLen = queries.length;
        int[] prefix = new int[len + 1];
        prefix[1] = containsVowel(words[0])? 1: 0;
        for(int i = 2; i <= len; i++) {
            if(containsVowel(words[i - 1])) 
                prefix[i] = prefix[i - 1] + 1;
            else 
                prefix[i] = prefix[i - 1];
        }
        int[] res = new int[qLen];
        for(int i = 0; i < qLen; i++) 
            res[i] =  prefix[queries[i][1] + 1] - prefix[queries[i][0]];
            
        return res;
    }
    private boolean containsVowel (String s) {
        char c1 = s.charAt(0);
        char c2 = s.charAt(s.length() - 1);
        if((c1 == 'a' || c1 == 'e' || c1 == 'i' || c1 == 'o' || c1 == 'u') &&
            (c2 == 'a' || c2 == 'e' || c2 == 'i' || c2 == 'o' || c2 == 'u'))
            return true;
        return false;
    }
}
```