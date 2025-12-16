# 633. Sum of Square Numbers  

  Methods: Pointer </br> Difficulty: Medium </br> </br>**Medium**

2.1K

517

Companies

Given a non-negative integer `c`, decide whether there're two integers `a` and `b` such that `a2 + b2 = c`.

**Example 1:**

```plain text
Input: c = 5
Output: true
Explanation: 1 * 1 + 2 * 2 = 5

```

**Example 2:**

```plain text
Input: c = 3
Output: false

```

**Constraints:**

- `0 <= c <= 231 - 1`
```java
class Solution {
    public boolean judgeSquareSum(int c) {
        long left = 0, right = (long) Math.sqrt(c);
        while (left <= right) {
            long mid = left* left + right* right;
            if(mid == c) return true;
            else if(mid < c) left ++ ;
            else right --;
        }
        return false;
    }
}
```

