# 3335. Total Characters in String After Transformations I  

  Methods: DP </br> Difficulty: Medium </br> </br>You are given a string `s` and an integer `t`, representing the number of **transformations** to perform. In one **transformation**, every character in `s` is replaced according to the following rules:

- If the character is `'z'`, replace it with the string `"ab"`.
- Otherwise, replace it with the **next** character in the alphabet. For example, `'a'` is replaced with `'b'`, `'b'` is replaced with `'c'`, and so on.
Return the **length** of the resulting string after **exactly** `t` transformations.

Since the answer may be very large, return it **modulo** `109 + 7`.

**Example 1:**

**Input:** s = "abcyy", t = 2

**Output:** 7

**Explanation:**

- **First Transformation (t = 1)**:
- **Second Transformation (t = 2)**:
- **Final Length of the string**: The string is `"cdeabab"`, which has 7 characters.
**Example 2:**

**Input:** s = "azbk", t = 1

**Output:** 5

**Explanation:**

- **First Transformation (t = 1)**:
- **Final Length of the string**: The string is `"babcl"`, which has 5 characters.
**Constraints:**

- `1 <= s.length <= 105`
- `s` consists only of lowercase English letters.
- `1 <= t <= 105`
```javascript
class Solution {
    public int lengthAfterTransformations(String s, int t) {
        // 1.dp[i] = (if i == 'z') dp[i - 1] + 1;
        //          else dp[i] = dp[i - 1];
        // 2.Math
        int mod = 1000000007;
        int[] freq = new int[26];
        long res = 0;
        
        for (char c : s.toCharArray())
            freq[c - 'a']++;

        while (t-- > 0) {
            int[] tmp = new int[26];
            for (int i = 0; i < 25; i++)// a -> y
                tmp[i + 1] = freq[i];
            tmp[0] = (tmp[0] + freq[25]) % mod;// a = z + a
            tmp[1] = (tmp[1] + freq[25]) % mod;// b = z + b
            freq = tmp;
        }
        
        for (int x : freq)
            res = (res + x) % mod;

        return (int) res;
    }
}
```

