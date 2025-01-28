# 712. Minimum ASCII Delete Sum for Two Strings

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Hint

Given two strings `s1` and `s2`, return *the lowest **ASCII** sum of deleted characters to make two strings equal*.

**Example 1:**

```
Input: s1 = "sea", s2 = "eat"
Output: 231
Explanation: Deleting "s" from "sea" adds the ASCII value of "s" (115) to the sum.
Deleting "t" from "eat" adds 116 to the sum.
At the end, both strings are equal, and 115 + 116 = 231 is the minimum sum possible to achieve this.

```

**Example 2:**

```
Input: s1 = "delete", s2 = "leet"
Output: 403
Explanation: Deleting "dee" from "delete" to turn the string into "let",
adds 100[d] + 101[e] + 101[e] to the sum.
Deleting "e" from "leet" adds 101[e] to the sum.
At the end, both strings are equal to "let", and the answer is 100+101+101+101 = 403.
If instead we turned both strings into "lee" or "eet", we would get answers of 433 or 417, which are higher.

```

**Constraints:**

- `1 <= s1.length, s2.length <= 1000`
- `s1` and `s2` consist of lowercase English letters.

---

Hint 1

Let dp(i, j) be the answer for inputs s1[i:] and s2[j:].

```java
class Solution {
    public int minimumDeleteSum(String s1, String s2) {// 類似 1143. Longest Common Subsequence 
        // DP[i][j] represents the lowest ASCII sums of deleted char to ma kake text1[0 ... i] & text2[0 ... j]. equal
        int i = s1.length() + 1;
        int j = s2.length() + 1;
        int[][] dp = new int[i][j];
        
        for(int a = 1; a < i; a++) dp[a][0] = dp[a - 1][0] + (int)s1.charAt(a - 1);
        for(int a = 1; a < j; a++) dp[0][a] = dp[0][a - 1] + (int)s2.charAt(a - 1);
         
        for(int x = 1; x < i; x++){
            for(int y = 1; y < j; y++){
                if(s1.charAt(x - 1) == s2.charAt(y - 1)){
                    dp[x][y] = dp[x- 1][y- 1];
                }else{
                    dp[x][y] = Math.min(dp[x-1][y] + (int)s1.charAt(x - 1), dp[x][y-1] + (int)s2.charAt(y - 1));
                }
            }
        }
        return dp[i- 1][j- 1];
    }
}
```