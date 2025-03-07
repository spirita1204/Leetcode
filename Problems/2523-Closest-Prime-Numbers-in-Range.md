# 2523. Closest Prime Numbers in Range  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>Given two positive integers `left` and `right`, find the two integers `num1` and `num2` such that:

- `left <= num1 < num2 <= right `.
- Both `num1` and `num2` are .
- `num2 - num1` is the **minimum** amongst all other pairs satisfying the above conditions.
Return the positive integer array `ans = [num1, num2]`. If there are multiple pairs satisfying these conditions, return the one with the **smallest** `num1` value. If no such numbers exist, return `[-1, -1]`*.*

**Example 1:**

```plain text
Input: left = 10, right = 19
Output: [11,13]
Explanation: The prime numbers between 10 and 19 are 11, 13, 17, and 19.
The closest gap between any pair is 2, which can be achieved by [11,13] or [17,19].
Since 11 is smaller than 17, we return the first pair.
```

**Example 2:**

```plain text
Input: left = 4, right = 6
Output: [-1,-1]
Explanation: There exists only one prime number in the given range, so the conditions cannot be satisfied.
```

**Constraints:**

- `1 <= left <= right <= 106`
Hint 1

Use Sieve of Eratosthenes to mark numbers that are primes.

---

Hint 2

Iterate from right to left and find pair with the minimum distance between marked numbers.

```java
class Solution {
    public int[] closestPrimes(int left, int right) {
        // 考慮[23 29] [29 31]
        int prev = -1, first = -1, second = -1;
        List<Integer> list = new ArrayList<>();

        for(int i = left; i <= right; i++) {
            if (isPrime(i)) {
                list.add(i);
            }
        }
        if(list.size() < 2)
            return new int[]{-1, -1}; // 如果沒有找到兩個質數
        
        int min = Integer.MAX_VALUE, res1 = 0, res2 = 0;

        for(int i = 1; i < list.size(); i++) {
            int nowMin = list.get(i) - list.get(i - 1);
            if(nowMin < min) {
                min = nowMin;
                res2 = list.get(i);
                res1 = list.get(i - 1);
            }
        } 
        return new int[]{res1, res2};
    }

    private boolean isPrime(int num) {
        if (num < 2) return false;
        for (int i = 2; i * i <= num; i++) {
            if (num % i == 0) return false;
        }
        return true;
    }
}
```

最優解

