# 326. Power of Three  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given an integer `n`, return `*true*`* if it is a power of three. Otherwise, return *`*false*`.

An integer `n` is a power of three, if there exists an integer `x` such that `n == 3x`.    

**Example 1:**

```plain text
Input: n = 27
Output: true
Explanation: 27 = 33
```

**Example 2:**

```plain text
Input: n = 0
Output: false
Explanation: There is no x where 3x = 0.
```

**Example 3:**

```plain text
Input: n = -1
Output: false
Explanation: There is no x where 3x = (-1).
```

**Constraints:**

- `231 <= n <= 231 - 1`
**Follow up:**

Could you solve it without loops/recursion?

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        while(n > 0) {
            if(n == 1)
                return true;
            if(n % 3 != 0)
                return false;
            n /= 3;
        }
        return false;
    }
}
```

