# 342. Power of Four  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given an integer `n`, return `*true*`* if it is a power of four. Otherwise, return *`*false*`.

An integer `n` is a power of four, if there exists an integer `x` such that `n == 4x`.

**Example 1:**

```plain text
Input: n = 16
Output: true
```

**Example 2:**

```plain text
Input: n = 5
Output: false
```

**Example 3:**

```plain text
Input: n = 1
Output: true
```

**Constraints:**

- `231 <= n <= 231 - 1`
```java
class Solution {
    public boolean isPowerOfFour(int n) {
        if(n <= 0) return false;
        
        while(n > 1) {
            if(n % 4 != 0) return false;
            n = n / 4;
        }
        return true;
    }
}
```

