# 3405. Count the Number of Arrays with K Matching Adjacent Elements  

  Methods: Combinatorics </br> Difficulty: Hard </br> </br>You are given three integers `n`, `m`, `k`. A **good array** `arr` of size `n` is defined as follows:

- Each element in `arr` is in the **inclusive** range `[1, m]`.
- *Exactly* `k` indices `i` (where `1 <= i < n`) satisfy the condition `arr[i - 1] == arr[i]`.
Return the number of **good arrays** that can be formed.

Since the answer may be very large, return it **modulo **`109 + 7`.

---

**Example 1:**

**Input:** n = 3, m = 2, k = 1

**Output:** 4

**Explanation:**

- There are 4 good arrays. They are `[1, 1, 2]`, `[1, 2, 2]`, `[2, 1, 1]` and `[2, 2, 1]`.
- Hence, the answer is 4.
---

**Example 2:**

**Input:** n = 4, m = 2, k = 2

**Output:** 6

**Explanation:**

- The good arrays are `[1, 1, 1, 2]`, `[1, 1, 2, 2]`, `[1, 2, 2, 2]`, `[2, 1, 1, 1]`, `[2, 2, 1, 1]` and `[2, 2, 2, 1]`.
- Hence, the answer is 6.
---

**Example 3:**

**Input:** n = 5, m = 2, k = 0

**Output:** 2

**Explanation:**

- The good arrays are `[1, 2, 1, 2, 1]` and `[2, 1, 2, 1, 2]`. Hence, the answer is 2.
---

**Constraints:**

- `1 <= n <= 105`
- `1 <= m <= 105`
- `0 <= k <= n - 1`
```java
class Solution {
    // 排列組合題 m*(m-1)^(n-k-1)*C_(n-1)_k  
    // C : 從n-1(排除第一)選k個與前面相同
    static final int MOD = 1_000_000_007;

    public int countGoodArrays(int n, int m, int k) {
        long formula = m * binExpo(m - 1, n - (k + 1)) % MOD;
        long updatedFormula = formula * nCr(n - 1, k) % MOD;

        return (int)updatedFormula;
    }
    
    long modInverse(long a, long mod) {
        long res = 1;
        long power = mod - 2;

        while (power > 0) {
            if ((power & 1) == 1)
                res = res * a % mod;
            a = a * a % mod;
            power >>= 1;
        }

        return res;
    }

    int nCr(int n, int r) {// C_(n-1)_k  
        if (r > n) return 0;
        if (r == 0 || r == n) return 1;

        long res = 1;

        for (int i = 1; i <= r; i++) {
            res = res * (n - r + i) % MOD;
            res = res * modInverse(i, MOD) % MOD;
        }

        return (int)res;
    }

    long binExpo(long a, long b) {
        long res = 1;
        while (b > 0) {
            if ((b & 1) == 1)// 奇數
                res = res * a % MOD;
            a = a * a % MOD;
            b >>= 1;
        }
        return res;
    }
}

```

