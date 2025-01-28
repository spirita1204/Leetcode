# 50. Pow(x, n)

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates `x` raised to the power `n` (i.e., `xn`).

**Example 1:**

```
Input: x = 2.00000, n = 10
Output: 1024.00000

```

**Example 2:**

```
Input: x = 2.10000, n = 3
Output: 9.26100

```

**Example 3:**

```
Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25

```

**Constraints:**

- `100.0 < x < 100.0`
- `231 <= n <= 2311`
- `n` is an integer.
- Either `x` is not zero or `n > 0`.
- `104 <= xn <= 104`

```java
class Solution {
    public double myPow(double x, int n) {
        if(n < 0){
            n = -n;
            x = 1 / x;
        }
        // n = -2147483648 -n = -2147483648
        double pow = 1;
        
        while(n != 0){
            if((n & 1) != 0){// 最後一位比較 n是奇數
                pow *= x;
            } 
            x *= x;
            n >>>= 1;
            // >> 保留正負號向右位移
            // >>> 無正負號向右位移
        }
        return pow;
    }
}
```