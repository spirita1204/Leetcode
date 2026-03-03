# 1680. Concatenation of Consecutive Binary Numbers  

  Methods: Bitwise </br> Difficulty: Medium </br> </br>Given an integer `n`, return *the ****decimal value**** of the binary string formed by concatenating the binary representations of *`1`* to *`n`* in order, ****modulo ***`109 + 7`.

**Example 1:     **

```plain text
Input: n = 1   
Output: 1  
Explanation:"1" in binary corresponds to the decimal value 1.
```

**Example 2:     **

```plain text
Input: n = 3   
Output: 27
Explanation:In binary, 1, 2, and 3 corresponds to "1", "10", and "11".
After concatenating them, we have "11011", which corresponds to the decimal value 27.
```

**Example 3:**

```plain text
Input: n = 12
Output: 505379714
Explanation: The concatenation results in "1101110010111011110001001101010111100".
The decimal value of that is 118505380540.
After modulo 109 + 7, the result is 505379714.
```

**Constraints:**

- `1 <= n <= 105` 
```java
class Solution {
    public int concatenatedBinary(int n) {  
        final int MOD = 1_000_000_007;
        long res = 0;// 目前拼好的結果
        int bits = 0;// 當前數字的「二進位長度」

        for (int i = 1; i <= n; i++) {
            if ((i & (i - 1)) == 0)// i 是不是 2 的次方
                bits++;// 每當到 2^k → binary 位數會增加
            res = ((res << bits) | i) % MOD;// 原本結果「左移 bits 位」，把 i 塞進去（拼接）
        }
        return (int) res;
    }
}
```

   

