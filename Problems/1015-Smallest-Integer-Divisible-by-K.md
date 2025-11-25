# 1015. Smallest Integer Divisible by K  

  Methods: Math </br> Difficulty: Medium </br> </br>Given a positive integer `k`, you need to find the **length** of the **smallest** positive integer `n` such that `n` is divisible by `k`, and `n` only contains the digit `1`.

Return *the ****length**** of *`n`. If there is no such `n`, return -1.

**Note:** `n` may not fit in a 64-bit signed integer.

**Example 1:**

```plain text
Input: k = 1
Output: 1
Explanation: The smallest answer is n = 1, which has length 1.
```

**Example 2:**

```plain text
Input: k = 2
Output: -1
Explanation: There is no such positive integer n divisible by 2.
```

**Example 3:**

```plain text
Input: k = 3
Output: 3  
Explanation: The smallest answer is n = 111, which has length 3.
```

**Constraints:**

- `1 <= k <= 105`
```java
class Solution {
    public int smallestRepunitDivByK(int k) {
        /// 111... 任何含 2 或 5 的數，都不可能整除任何 Rₙ。
        if (k % 2 == 0 || k % 5 == 0)
            return -1;
        int r = 0;
        for (int i = 1; i <= k; i++) {
            r = (r * 10 + 1) % k;
            if (r == 0)
                return i;
        }
        return -1;
    }
}
```

