# 1922. Count Good Numbers  

  Methods: Recursion,Math </br> Difficulty: Medium </br> </br>A digit string is **good** if the digits **(0-indexed)** at **even** indices are **even** and the digits at **odd** indices are **prime** (`2`, `3`, `5`, or `7`).

- For example, `"2582"` is good because the digits (`2` and `8`) at even positions are even and the digits (`5` and `2`) at odd positions are prime. However, `"3245"` is **not** good because `3` is at an even index but is not even.
Given an integer `n`, return *the ****total**** number of good digit strings of length *`n`. Since the answer may be large, **return it modulo **`109 + 7`.

A **digit string** is a string consisting of digits `0` through `9` that may contain leading zeros.

**Example 1:**

```plain text
Input: n = 1
Output: 5
Explanation: The good numbers of length 1 are "0", "2", "4", "6", "8".
```

**Example 2:**

```plain text
Input: n = 4
Output: 400
```

**Example 3:**

```plain text
Input: n = 50
Output: 564908303
```

**Constraints:**

- `1 <= n <= 1015`
```java
class Solution {
    int mod=(int)1e9+7;
    public int countGoodNumbers(long n) {
        // 5c1
        // 4c1
        long first = (n % 2 == 0) ? (n / 2) : (n / 2) + 1;
        long second = n / 2;
        long mul1 = power(5, first) % mod;
        long mul2 = power(4, second) % mod;
        
        long res = 1;
        res = (res * mul1) % mod;
        if(second != 0)
            return (int)((res * mul2) % mod);
 
        return (int) (res % mod);
    }

    public long power(long x, long y) {
        long temp;
        if (y == 0)
            return 1;
        temp = power(x, y / 2);
        if (y % 2 == 0)
            return (temp * temp) % mod;
        else
            return (x * temp * temp) % mod;
    }
}
```

