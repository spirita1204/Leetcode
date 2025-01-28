# 72. Edit Distance

Methods: DP
Difficulty: Medium

[https://www.youtube.com/watch?v=MiqoA-yF-0M&t=376s](https://www.youtube.com/watch?v=MiqoA-yF-0M&t=376s)

Given two strings `word1` and `word2`, return *the minimum number of operations required to convert `word1` to `word2`*.

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character

**Example 1:**

```
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation:
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')

```

**Example 2:**

```
Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation:
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```

```java
class Solution {
    public int minDistance(String word1, String word2) {//dp
        /**
        Ai = a1a2a3a4...ai; A的前i字元所構成之子字串
        Bi = b1b2b3b4...bi;
        Z  = r1r2r3r4...ri; 將A轉自B所需最短運算序列 

        insert  : f(i, j - 1) + 1
        delete  : f(i - 1, j) + 1 
        replace : f(i - 1, j - 1) + 1
        equal   : f(i - 1, j - 1)
        取四個最小
         */
        int m = word1.length() + 1;
        int n = word2.length() + 1;
        int[][] dp = new int[m][n];
    
        for(int j = 0; j < n; j++){
            dp[0][j] = j;
        }
        for(int i = 0; i < m; i++){
            dp[i][0] = i;
        }
        /*-------------//既定知道要做的步數 dp[0][0]放隨便一假值=相同
          | 0 | 1 | 2 | 
          -------------
          | 1 |   |   |
          -------------
          | 2 |   |   |
          -------------*/
        for(int i = 1; i < m; i++) {
            for(int j = 1; j < n; j++) {
                if(word1.charAt(i - 1) == word2.charAt(j - 1)){//同樣直接覆蓋
                    dp[i][j] = dp[i-1][j-1];
                }else{//不同 則找insert delete replace中最小
                    dp[i][j] = Math.min(Math.min(dp[i -1][j - 1], dp[i][j - 1]), dp[i -1][j]) + 1;
                }
            }
        }
        return dp[m -1][n - 1];
    }
}
```