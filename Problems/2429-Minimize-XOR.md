# 2429. Minimize XOR

Methods: Bitewise
Difficulty: Medium

Given two positive integers `num1` and `num2`, find the positive integer `x` such that:

- `x` has the same number of set bits as `num2`, and
- The value `x XOR num1` is **minimal**.

Note that `XOR` is the bitwise XOR operation.

Return *the integer* `x`. The test cases are generated such that `x` is **uniquely determined**.

The number of **set bits** of an integer is the number of `1`'s in its binary representation.

**Example 1:**

```
Input: num1 = 3, num2 = 5
Output: 3
Explanation:
The binary representations of num1 and num2 are 0011 and 0101, respectively.
The integer3 has the same number of set bits as num2, and the value3 XOR 3 = 0 is minimal.

```

**Example 2:**

```
Input: num1 = 1, num2 = 12
Output: 3
Explanation:
The binary representations of num1 and num2 are 0001 and 1100, respectively.
The integer3 has the same number of set bits as num2, and the value3 XOR 1 = 2 is minimal.

```

**Constraints:**

- `1 <= num1, num2 <= 109`

```java
class Solution {
    public int minimizeXor(int num1, int num2) {
        int a = Integer.bitCount(num1);
        int b = Integer.bitCount(num2);
        // 當times1 == times2 時 則=num1
        if (a == b)
            return num1;
        // times1 > times2 時 則從左邊去抵銷1
        // times1 < times2 時 右邊去抵銷
        int target = 0;
        for (int i = 31; i >= 0 && b > 0; --i) {
            if ((num1 & (1 << i)) != 0) {// = 1
                target |= (1 << i);
                --b;
            }
        }
        for (int i = 0; i < 32 && b > 0; ++i) {
            if ((target & (1 << i)) == 0) {// = 0
                target |= (1 << i);
                --b;
            }
        }

        return target;
    }
}
```