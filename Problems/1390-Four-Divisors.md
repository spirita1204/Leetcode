# 1390. Four Divisors  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>Given an integer array `nums`, return *the sum of divisors of the integers in that array that have exactly four divisors*. If there is no such integer in the array, return `0`.

**Example 1:**

```plain text
Input: nums = [21,4,7]
Output: 32
Explanation:
21 has 4 divisors: 1, 3, 7, 21
4 has 3 divisors: 1, 2, 4
7 has 2 divisors: 1, 7
The answer is the sum of divisors of 21 only.
```

**Example 2:**

```plain text
Input: nums = [21,21]
Output: 64
```

**Example 3:**

```plain text
Input: nums = [1,2,3,4,5]
Output: 0
```

**Constraints:**

- `1 <= nums.length <= 104`
- `1 <= nums[i] <= 105`
```java
class Solution {
    public int sumFourDivisors(int[] nums) {
        int res = 0;

        for (int num : nums) {
            if (sumOne(num) != -1)
                res += sumOne(num);
        }

        return res;
    }

    private int sumOne(int n) {
        // Case 1: p^3   (1, p, p², p³)
        int p = (int) Math.round(Math.cbrt(n));// 立方根
        if ((long) p * p * p == n && isPrime(p)) {
            return 1 + p + p * p + p * p * p;
        }

        // Case 2: p * q   (1, p, q, p×q)
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                int a = i;
                int b = n / i;
                if (a != b && isPrime(a) && isPrime(b)) {
                    return 1 + a + b + n;
                }
                return -1;
            }
        }
        return -1;
    }

    private boolean isPrime(int x) {
        if (x < 2)
            return false;
        for (int i = 2; i * i <= x; i++) {
            if (x % i == 0)
                return false;
        }
        return true;
    }
}
```

