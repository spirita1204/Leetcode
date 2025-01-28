# 1143. Longest Common Subsequence (經典題)

Methods: DP
Difficulty: Medium

[Longest Common Subsequence (LCS) - GeeksforGeeks](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)

**Medium**

10.8K

131

Companies

Given two strings `text1` and `text2`, return *the length of their longest **common subsequence**.* If there is no **common subsequence**, return `0`.

A **subsequence** of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

- For example, `"ace"` is a subsequence of `"abcde"`.

A **common subsequence** of two strings is a subsequence that is common to both strings.

**Example 1:**

```
Input: text1 = "abcde", text2 = "ace"
Output: 3
Explanation: The longest common subsequence is "ace" and its length is 3.

```

**Example 2:**

```
Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.

```

**Example 3:**

```
Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.

```

**Constraints:**

- `1 <= text1.length, text2.length <= 1000`
- `text1` and `text2` consist of only lowercase English characters.

```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        //DP[i][j] represents the longest common subsequence of text1[0 ... i] & text2[0 ... j].
        int i = text1.length()+ 1;
        int j = text2.length()+ 1;
        int[][] dp = new int[i][j];

        for(int x = 1; x< i; x++){
            for(int y = 1;y < j; y++){
                if(text1.charAt(x-1) == text2.charAt(y-1)){
                    dp[x][y] = dp[x- 1][y- 1] + 1;
                }else{
                    dp[x][y] = Math.max(dp[x-1][y], dp[x][y-1]);
                }
            }
        }
        return dp[i- 1][j- 1];
    }
}
```