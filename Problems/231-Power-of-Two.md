# 231. Power of Two  

  Methods: Bitwise </br> Difficulty: Easy </br> </br>Given an integer `n`, return `*true*`* if it is a power of two. Otherwise, return *`*false*`.

An integer `n` is a power of two, if there exists an integer `x` such that `n == 2x`.

**Example 1:**

```plain text
Input: n = 1
Output: true
Explanation:20 = 1

```

**Example 2:**

```plain text
Input: n = 16
Output: true
Explanation:24 = 16

```

**Example 3:**

```plain text
Input: n = 3
Output: false

```

**Constraints:**

- `231 <= n <= 231 - 1`
**Follow up:**

Could you solve it without loops/recursion?

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        return n>0 && Integer.bitCount(n) == 1;
    }
}
```

