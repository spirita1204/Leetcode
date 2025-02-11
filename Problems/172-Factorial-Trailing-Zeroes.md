# 172. Factorial Trailing Zeroes

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Given an integer `n`, return *the number of trailing zeroes in* `n!`.

Note that `n! = n * (n - 1) * (n - 2) * ... * 3 * 2 * 1`.

**Example 1:**

```
Input: n = 3
Output: 0
Explanation: 3! = 6, no trailing zero.

```

**Example 2:**

```
Input: n = 5
Output: 1
Explanation: 5! = 120, one trailing zero.

```

**Example 3:**

```
Input: n = 0
Output: 0

```

**Constraints:**

- `0 <= n <= 104`

**Follow up:** Could you write a solution that works in logarithmic time complexity?

```java
class Solution {
    public int trailingZeroes(int n) {
        /**
         * Because all trailing 0 is from factors 5 * 2.
         * 
         * But sometimes one number may have several 5 factors, for example, 25 have two
         * 5 factors, 125 have three 5 factors. In the n! operation, factors 2 is always
         * ample. So we just count how many 5 factors in all number from 1 to n.
         */
        return n == 0 ? 0 : n / 5 + trailingZeroes(n / 5);
    }
}
```