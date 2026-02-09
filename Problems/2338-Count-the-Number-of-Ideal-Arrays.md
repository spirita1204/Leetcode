# 2338. Count the Number of Ideal Arrays  

  Methods: DP,Math,Combinatorics </br> Difficulty: Hard </br> </br>You are given two integers `n` and `maxValue`, which are used to describe an **ideal** array.

A **0-indexed** integer array `arr` of length `n` is considered **ideal** if the following conditions hold:

- Every `arr[i]` is a value from `1` to `maxValue`, for `0 <= i < n`.
- Every `arr[i]` is divisible by `arr[i - 1]`, for `0 < i < n`.
Return *the number of ****distinct**** ideal arrays of length *`n`. Since the answer may be very large, return it modulo `109 + 7`.

**Example 1:**

```plain text
Input: n = 2, maxValue = 5
Output: 10
Explanation: The following are the possible ideal arrays:
- Arrays starting with the value 1 (5 arrays): [1,1], [1,2], [1,3], [1,4], [1,5]
- Arrays starting with the value 2 (2 arrays): [2,2], [2,4]
- Arrays starting with the value 3 (1 array): [3,3]
- Arrays starting with the value 4 (1 array): [4,4]
- Arrays starting with the value 5 (1 array): [5,5]
There are a total of 5 + 2 + 1 + 1 + 1 = 10 distinct ideal arrays.
```

**Example 2:**

```plain text
Input: n = 5, maxValue = 3
Output: 11
Explanation: The following are the possible ideal arrays:
- Arrays starting with the value 1 (9 arrays):
   - With no other distinct values (1 array): [1,1,1,1,1]
   - With 2nd distinct value 2 (4 arrays): [1,1,1,1,2], [1,1,1,2,2], [1,1,2,2,2], [1,2,2,2,2]
   - With 2nd distinct value 3 (4 arrays): [1,1,1,1,3], [1,1,1,3,3], [1,1,3,3,3], [1,3,3,3,3]
- Arrays starting with the value 2 (1 array): [2,2,2,2,2]
- Arrays starting with the value 3 (1 array): [3,3,3,3,3]
There are a total of 9 + 1 + 1 = 11 distinct ideal arrays.
```

**Constraints:**

- `2 <= n <= 104`
- `1 <= maxValue <= 104`
```java
class Solution {
    long M = 1_000_000_007L;
    long[][] dp = new long[10001][15]; 
    // dp[i][j]: 在前 i 個位置中，放 j 個相同因數的組合數

    public int idealArrays(int n, int maxValue) {
        dp[0][0] = 1;
        // 在第 i 個位置：
        // 放 k 個因數
        // 剩下 j-k 個給前 i-1 個位置
        for (int i = 1; i <= n; i++) {
            dp[i][0] = 1;
            for (int j = 1; j <= 14; j++) {// 最大質因數次方： 2^14 = 16384 > 10000, 所以：最多只會有14次方
                for (int k = 0; k <= j; k++) {
                    dp[i][j] = (dp[i][j] + dp[i - 1][j - k]) % M;
                }
            }
        }
        List<Integer> primes = eratosthenes(maxValue);// 2 ~ maxValue 的所有質數

        long ret = 1; // t = 1 的情況
        // 假設陣列最後一個數字是 t, 有多少長度為 n 的合法陣列, 最後結尾是 t
        for (int t = 2; t <= maxValue; t++) {
            int x = t;
            long ans = 1;

            for (int p : primes) {
                int count = 0;
                while (x > 1 && x % p == 0) {
                    x /= p;
                    count++;
                }
                // 把這個質因數的次方, 分配到 n 個位置的方法數
                ans = ans * dp[n][count] % M;
            }
            ret = (ret + ans) % M;
        }

        return (int) ret;
    }

    private List<Integer> eratosthenes(int n) {
        boolean[] isComposite = new boolean[n + 1];
        List<Integer> primes = new ArrayList<>();

        for (int i = 2; i * i <= n; i++) {
            if (isComposite[i]) continue;
            for (int j = i * 2; j <= n; j += i) {
                isComposite[j] = true;
            }
        }

        for (int i = 2; i <= n; i++) {
            if (!isComposite[i]) {
                primes.add(i);
            }
        }
        return primes;
    }
}

```

