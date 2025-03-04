# 1780. Check if Number is a Sum of Powers of Three  

  Methods: Math </br> Difficulty: Medium </br> </br>Given an integer `n`, return `true` *if it is possible to represent *`n`* as the sum of distinct powers of three.* Otherwise, return `false`.

An integer `y` is a power of three if there exists an integer `x` such that `y == 3x`.

**Example 1:  **

```plain text
Input: n = 12
Output: true
Explanation: 12 = 31 + 32
```

**Example 2:**

```plain text
Input: n = 91
Output: true
Explanation: 91 = 30 + 32 + 34
```

**Example 3:**

```plain text
Input: n = 21
Output: false
```

**Constraints:**

- `1 <= n <= 107`
```java
class Solution {
    public boolean checkPowersOfThree(int n) {
        // 1 3 9 27 81
        // 1*3^0 1*3^1 1*3^2...
        while(n > 0) {
            if(n % 3 == 2)
                return false;
            n /= 3;
        }
        return true;
    }
}
```

