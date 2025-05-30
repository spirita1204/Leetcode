# 2131. Longest Palindrome by Concatenating Two Letter Words  

  Methods: BFS </br> Data Structure: Hash Table,Set </br> Difficulty: Medium </br> </br>You are given an array of strings `words`. Each element of `words` consists of **two** lowercase English letters.

Create the **longest possible palindrome** by selecting some elements from `words` and concatenating them in **any order**. Each element can be selected **at most once**. 

Return *the ****length**** of the longest palindrome that you can create*. If it is impossible to create any palindrome, return `0`.

A **palindrome** is a string that reads the same forward and backward.

**Example 1:**

```plain text
Input: words = ["lc","cl","gg"]
Output: 6
Explanation: One longest palindrome is "lc" + "gg" + "cl" = "lcggcl", of length 6.
Note that "clgglc" is another longest palindrome that can be created.
```

**Example 2:**

```plain text
Input: words = ["ab","ty","yt","lc","cl","ab"]
Output: 8
Explanation: One longest palindrome is "ty" + "lc" + "cl" + "yt" = "tylcclyt", of length 8.
Note that "lcyttycl" is another longest palindrome that can be created.
```

**Example 3:**

```plain text
Input: words = ["cc","ll","xx"]
Output: 2
Explanation: One longest palindrome is "cc", of length 2.
Note that "ll" is another longest palindrome that can be created, and so is "xx".
```

**Constraints:**

- `1 <= words.length <= 105`
- `words[i].length == 2`
- `words[i]` consists of lowercase English letters.
```java
class Solution {
    public int longestPalindrome(String[] words) {
        Map<String, Integer> hm = new HashMap<>();

        for(String word: words) 
            hm.put(word, hm.getOrDefault(word, 0) + 1);

        int res = 0;
        Set<String> hs = new HashSet<>();
        int center = 0, same = 0;

        for(String key : hm.keySet()) {
            if(hs.contains(key))
                continue;
            if(key.charAt(0) == key.charAt(1)){
                int cnt = hm.get(key);
                same += cnt / 2;
                center += cnt % 2;
                continue;
            }
            String keyReverse = new StringBuilder(key).reverse().toString();

            if(hm.get(keyReverse) != null) {
                res += Math.min(hm.get(key), hm.get(keyReverse));
                hs.add(key);
            }
        }
        // same                       center
        return (res + same * 2) * 2 + ((center > 0) ? 2: 0);
    }
}
```

