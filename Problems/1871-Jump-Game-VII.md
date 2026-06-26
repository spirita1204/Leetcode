# 1871. Jump Game VII  

  Methods: DP,Sliding Window </br> Difficulty: Medium </br> </br>You are given a **0-indexed** binary string `s` and two integers `minJump` and `maxJump`. In the beginning, you are standing at index `0`, which is equal to `'0'`. You can move from index `i` to index `j` if the following conditions are fulfilled:

- `i + minJump <= j <= min(i + maxJump, s.length - 1)`, and
- `s[j] == '0'`.
Return `true`* if you can reach index *`s.length - 1`* in *`s`*, or *`false`* otherwise.*

**Example 1:**

```plain text
Input: s = "011010", minJump = 2, maxJump = 3
Output: true
Explanation:
In the first step, move from index 0 to index 3.
In the second step, move from index 3 to index 5.
```

**Example 2:   **

```plain text
Input: s = "01101110", minJump = 2, maxJump = 3
Output: false     
```

**Constraints:**

- `2 <= s.length <= 105`
- `s[i]` is either `'0'` or `'1'`.  
- `s[0] == '0'`
- `1 <= minJump <= maxJump < s.length`
```java
class Solution {
    public boolean canReach(String s, int minJ, int maxJ) {
        int n = s.length();

        if (s.charAt(n - 1) == '1')
            return false;
        // 能不能到達 i   
        int[] dp = new int[n];
        dp[0] = 1;
        // reach : 目前 Window 裡共有幾個可以到達的位置
        int reach = 0, maxR = maxJ;
        
        for (int i = minJ; i < n; i++) {
            if (i > maxR) return false;

            reach += dp[i - minJ];
            // dp[i-maxJump] ... dp[i-minJump]
            // 看成slide windows
            if (i > maxJ) reach -= dp[i - maxJ - 1];

            if (reach > 0 && s.charAt(i) == '0') {
                dp[i] = 1;
                maxR = i + maxJ;
            }
        }

        return reach > 0;
    }
}
```



