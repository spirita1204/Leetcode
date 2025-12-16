# 2707. Extra Characters in a String  

  Methods: DP </br> Data Structure: Set </br> Difficulty: Medium </br> </br>Medium

Topics

Companies

Hint

You are given a **0-indexed** string `s` and a dictionary of words `dictionary`. You have to break `s` into one or more **non-overlapping** substrings such that each substring is present in `dictionary`. There may be some **extra characters** in `s` which are not present in any of the substrings.

Return *the ****minimum**** number of extra characters left over if you break up *`s`* optimally.*

**Example 1:**

```plain text
Input: s = "leetscode", dictionary = ["leet","code","leetcode"]
Output: 1
Explanation: We can break s in two substrings: "leet" from index 0 to 3 and "code" from index 5 to 8. There is only 1 unused character (at index 4), so we return 1.


```

**Example 2:**

```plain text
Input: s = "sayhelloworld", dictionary = ["hello","world"]
Output: 3
Explanation: We can break s in two substrings: "hello" from index 3 to 7 and "world" from index 8 to 12. The characters at indices 0, 1, 2 are not used in any substring and thus are considered as extra characters. Hence, we return 3.

```

**Constraints:**

- `1 <= s.length <= 50`
- `1 <= dictionary.length <= 50`
- `1 <= dictionary[i].length <= 50`
- `dictionary[i]` and `s` consists of only lowercase English letters
- `dictionary` contains distinct words
```java
class Solution {
    public int minExtraChar(String s, String[] dictionary) {
        // DP[i] as the min extra character if breaking up s[0:i] optimally.
        Set<String> hs = new HashSet<>();
        for(String d: dictionary)// 方便查找
            hs.add(d);

        int len = s.length();
        int[] dp = new int[len + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;// 空字符串
        // 遍历字符串并尝试匹配词典单词
        for(int i = 1; i <= len; i++) {
            dp[i] = dp[i - 1] + 1;// 假設當前是多餘
            // 如果 s[j:i] 是词典中的一个单词，则更新 dp[i] = min(dp[i], dp[j])
            for(int j = 0; j < i; j++) {
                String substring = s.substring(j, i);
                if(hs.contains(substring)) {
                    dp[i] = Math.min(dp[i], dp[j]);
                }
            }
        }
        return dp[len];
    }
}
```

