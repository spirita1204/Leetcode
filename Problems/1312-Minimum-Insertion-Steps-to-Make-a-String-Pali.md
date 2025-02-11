# 1312. Minimum Insertion Steps to Make a String Palindrome

Methods: DP
Difficulty: Hard

**Hard**

3.8K

49

Companies

Given a string `s`. In one step you can insert any character at any index of the string.

Return *the minimum number of steps* to make `s` palindrome.

A **Palindrome String** is one that reads the same backward as well as forward.

**Example 1:**

```
Input: s = "zzazz"
Output: 0
Explanation: The string "zzazz" is already palindrome we do not need any insertions.

```

**Example 2:**

```
Input: s = "mbadm"
Output: 2
Explanation: String can be "mbdadbm" or "mdbabdm".

```

**Example 3:**

```
Input: s = "leetcode"
Output: 5
Explanation: Inserting 5 characters the string becomes "leetcodocteel".

```

**Constraints:**

- `1 <= s.length <= 500`
- `s` consists of lowercase English letters.

```java
class Solution {
    public int minInsertions(String s) {
        return s.length() - longestPalindromeSubseq(s);
    }
    public int longestPalindromeSubseq(String s) {// 516.Longest Palindromic Subsequence
        int[][] dp = new int[s.length()][s.length()];

        for (int i = s.length() - 1; i >= 0; i--){ 
            dp[i][i] = 1;
            for(int j = i+1; j< s.length(); j++){
                if(s.charAt(i) == s.charAt(j)) dp[i][j] = dp[i+1][j-1] + 2;
                else dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1]);
            }
        }
        return dp[0][s.length() - 1];
    }
}
```