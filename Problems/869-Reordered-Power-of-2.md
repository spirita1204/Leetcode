# 869. Reordered Power of 2  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>You are given an integer `n`. We reorder the digits in any order (including the original order) such that the leading digit is not zero.

Return `true` *if and only if we can do this so that the resulting number is a power of two*.

**Example 1:**

```plain text
Input: n = 1
Output: true
```

**Example 2:**

```plain text
Input: n = 10
Output: false
```

**Constraints:**

- `1 <= n <= 109`
```java
class Solution {
    public boolean reorderedPowerOf2(int n) {
        long c = counter(n);
        for (int i = 0; i < 32; i++)
            if (counter(1 << i) == c)// 與2倍數都比較一次
                return true;
        return false;
    }

    public long counter(int n) {// 轉2進制
        long res = 0;
        while(n > 0) {
            res += (int) Math.pow(10, n % 10);
            n /= 10;
        }
        return res;
    }
}
```

