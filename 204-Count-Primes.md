# 204. Count Primes

Methods: Basic logic, Math
Difficulty: Medium

Medium

Topics

Companies

Hint

Given an integer `n`, return *the number of prime numbers that are strictly less than* `n`.

**Example 1:**

```
Input: n = 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.

```

**Example 2:**

```
Input: n = 0
Output: 0

```

**Example 3:**

```
Input: n = 1
Output: 0

```

**Constraints:**

- `0 <= n <= 5 * 106`

```java
class Solution {
    public int countPrimes(int n) {
        // 埃拉托斯特尼篩法. 質數的所有倍數標記成合數
        // https://zh.wikipedia.org/zh-tw/%E5%9F%83%E6%8B%89%E6%89%98%E6%96%AF%E7%89%B9%E5%B0%BC%E7%AD%9B%E6%B3%95
        if(n == 0 || n == 1) 
            return 0;
        boolean[] isPrime = new boolean[n];

        int p = 0;// 計數
        Arrays.fill(isPrime, true);
        isPrime[0] = false;// 1不是質數

        for (int i = 2; i < n; i++) {
            if (isPrime[i - 1]) {
                p++;
                for(long j = (long)i * i; j < n; j += i) {
                    isPrime[(int)j - 1] = false;
                }
            }
        }
        return p;
    }
}
```