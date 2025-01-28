# 583. Delete Operation for Two Strings

Methods: DP
Difficulty: Medium

**Medium**

5K

73

Companies

Given two strings `word1` and `word2`, return *the minimum number of **steps** required to make* `word1` *and* `word2` *the same*.

In one **step**, you can delete exactly one character in either string.

**Example 1:**

```
Input: word1 = "sea", word2 = "eat"
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".

```

**Example 2:**

```
Input: word1 = "leetcode", word2 = "etco"
Output: 4

```

**Constraints:**

- `1 <= word1.length, word2.length <= 500`
- `word1` and `word2` consist of only lowercase English letters.

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int w1Len = word1.length();
        int w2Len = word2.length();

        int[][] dp = new int[w1Len+ 1][w2Len+ 1];// 代表將word1[0~i],word2[0~j]變成相同所需步數

        // if 第i位和第j位相同 dp[i][j] = dp[i-1][j-1]
        // else 第i和j不相同 dp[i][j] = Math.min(dp[i-1][j], dp[i][j-1]) + 1;
        // []  [s] [se] [sea]
        /*-------------//既定知道要做的步數 dp[0][0]放隨便一假值=相同
       [] | 0 | 1 | 2 | 3 |
          -----------------
       [e]| 1 | 2 | 1 | 2 |
          -----------------
      [ea]| 2 | 3 | 2 | 1 |
          -----------------
     [eat]| 3 | 4 | 3 | 2 |
          ---------------*/
        for (int i = 0; i <= w1Len; i++)
            dp[i][0] = i;
        for (int j = 0; j <= w2Len; j++)
            dp[0][j] = j;
        for(int i = 1; i<= w1Len; i++){
            for(int j = 1; j<= w2Len; j++){
                if (word1.charAt(i - 1) == word2.charAt(j - 1))
                    dp[i][j] = dp[i - 1][j - 1];
                else
                    dp[i][j] = Math.min(dp[i-1][j], dp[i][j-1]) + 1;
            }
        }
        return dp[w1Len][w2Len];
    }
}
```