# 91. Decode Ways

Methods: DP
Difficulty: Medium

**Medium**

9.8K

4.2K

Companies

A message containing letters from `A-Z` can be **encoded** into numbers using the following mapping:

```
'A' -> "1"
'B' -> "2"
...
'Z' -> "26"

```

To **decode** an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, `"11106"` can be mapped into:

- `"AAJF"` with the grouping `(1 1 10 6)`
- `"KJF"` with the grouping `(11 10 6)`

Note that the grouping `(1 11 06)` is invalid because `"06"` cannot be mapped into `'F'` since `"6"` is different from `"06"`.

Given a string `s` containing only digits, return *the **number** of ways to **decode** it*.

The test cases are generated so that the answer fits in a **32-bit** integer.

**Example 1:**

```
Input: s = "12"
Output: 2
Explanation: "12" could be decoded as "AB" (1 2) or "L" (12).

```

**Example 2:**

```
Input: s = "226"
Output: 3
Explanation: "226" could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).

```

**Example 3:**

```
Input: s = "06"
Output: 0
Explanation: "06" cannot be mapped to "F" because of the leading zero ("6" is different from "06").

```

**Constraints:**

- `1 <= s.length <= 100`
- `s` contains only digits and may contain leading zero(s).

```java
class Solution {
    public int numDecodings(String s) {
        //dp[i] = dp[i - 1] + dp[i - 2] ...(處理特殊情況)

        if(s.charAt(0) == '0') return 0;

        int[] dp = new int[s.length()+ 1];
        dp[0] = 1;
        dp[1] = 1;

        for(int i = 2; i<= s.length(); i++){//從 index = 1 開始
            int cur = s.charAt(i - 1) - '0';// 當前
            int prevC = s.charAt(i - 2) - '0';// 前一位
            
            if(prevC == 0){
                // 連續2個0 代表錯誤
                if(cur == 0){
                    return 0;
                }
                // 前一位為0 當前為獨立 不能與前一位做交集
                dp[i] = dp[i - 1];
            }else{
                if(cur == 0){// 需與前一位做組合 0不能單獨
                    if(prevC* 10+ cur <= 26){
                        dp[i] = dp[i- 2];
                    }
                }else {// 不需與前一位做組合
                    // 可以和前一位元作組合 介於 A~Z中間
                    if(prevC* 10+ cur <= 26){
                        dp[i] = dp[i- 1] + dp[i -2];
                    }else { 
                        dp[i] = dp[i- 1];
                    }
                }
            }
        }
        return dp[s.length()];
    }
}
```