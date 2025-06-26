# 2311. Longest Binary Subsequence Less Than or Equal to K  

  Methods: Greedy </br> Difficulty: Medium </br> </br>You are given a binary string `s` and a positive integer `k`.

Return *the length of the ****longest**** subsequence of *`s`* that makes up a ****binary**** number less than or equal to* `k`.  

Note:

- The subsequence can contain **leading zeroes**.
- The empty string is considered to be equal to `0`.
- A **subsequence** is a string that can be derived from another string by deleting some or no characters without changing the order of the remaining characters.
**Example 1:**

```plain text
Input: s = "1001010", k = 5
Output: 5
Explanation: The longest subsequence of s that makes up a binary number less than or equal to 5 is "00010", as this number is equal to 2 in decimal.
Note that "00100" and "00101" are also possible, which are equal to 4 and 5 in decimal, respectively.
The length of this subsequence is 5, so 5 is returned.
```

**Example 2:**

```plain text
Input: s = "00101001", k = 1
Output: 6
Explanation: "000001" is the longest subsequence of s that makes up a binary number less than or equal to 1, as this number is equal to 1 in decimal.
The length of this subsequence is 6, so 6 is returned.
```

**Constraints:**

- `1 <= s.length <= 1000`
- `s[i]` is either `'0'` or `'1'`.
- `1 <= k <= 109`
```java
class Solution {
    public int longestSubsequence(String s, int k) {
        int sum = 0, cnt = 0, len = s.length();
        int bits = (int) (Math.log(k) / Math.log(2)) + 1;// 二進制位數

        for (int i = 0; i < len; i++) {
            char ch = s.charAt(len - 1 - i);// 尾
        
            if (ch == '1') {
                if (i < bits && sum + (1 << i) <= k) {
                    sum += 1 << i;
                    cnt++;
                }
            }
            else 
                cnt++;
        }
        return cnt;
    }
}
```

